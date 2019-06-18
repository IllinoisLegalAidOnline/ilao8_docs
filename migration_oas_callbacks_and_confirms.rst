===============================
Exit screens and Callbacks
===============================

Exit screen functionality is largely within tihe oas_triage_user.exits.inc file.

There are six exit screens:

* Callback select form
* Callback confirmation page
* Please call us confirmation page
* Failure page
* Bypass intake page
* Referrals page

.. note::
   The bypass intake page is only ever called when processing triage rules and the user hits a bypass end point.  See the triage rules section for details on this exit screen.
   The referrals is only generated if a user is directed to referrals.  See the referrals page for more details.
   
Template files
================
Each page (not the select form) has a template file provided in the module that can be themed per the usual Drupal theme layer.  The 4 template files are:

* oas--bypass.tpl.php
* oas--please-call.tpl.php
* oas--referrals.tpl.php
* oas--we-call-you.tpl.php

.. todo:: in an ideal world, the template files would have been themed in ILAO's theme folder rather than in the module.   
   
Please call page
=================

The please call page is displayed when:

* the callback type is "client calls   
* the user selects "none of these times work for me" on the callback select form
* the callback type is "we call client" but there are no callback slots available.

and the etransfer was successful (see the oas_triage_user_please_call function)

If the etransfer_status was already set when this page is built, the user will see a message that their application was already submitted and it will not resubmit it.

The page is built by the oas_triage_user_build_please_call_page function.

oas_triage_user_build_please_call_page
---------------------------------------
Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^^^
Requires: the intake settings ID of the intake settings used to generate the application
Returns: a render array 

Process
^^^^^^^^

In building the page the function:
* invokes the oas_triage_user_save_exit to save the last screen viewed as Please call and set the intake status to eTransferred.
* Loads the organization name
* Sets the page title
* Builds out the content array for the template file:

  * Call label (hand-coded in the module)
  * Contact label
  * Call message from the intake settings (requires token_replace to replace OAS tokens with values
  * Steps (loads the steps from the oas_triage_user_get_steps function
  * Adds the steps image


oas_triage_user_save_exit
--------------------------
Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^
Requires: 

* exit type; string to populate last screen viewed
* transfer type; string to populate the intake status.

Returns:  null

Process
^^^^^^^^^

Updates the triage user entity to:

* set the last screen viewed to the exit type parameter
* set the intake status to the transfer type parameter
* set the intake changed timestamp to the current timestamp
* saves the changes to the database

oas_triage_user_get_steps
---------------------------
Generates the steps array to be included in the render array for the page.

Parameters
^^^^^^^^^^
Requires:

* the organization name
* the contact type string ("please_call", etc)

Returns a render array element that includes:

* the #theme type of item_list
* an empty tite
* the class
* the array of items in the list

Callback Selection Form
=========================
The callback selection form is displayed when:

* the callback type is "we call client"
* there are callback times available to display

oas_triage_user_callback_form builds the form.
_oas_triage_user_get_callback_options builds the list of callback option times.

Getting callback times
------------------------
The private _oas_triage_user_get_callback_options function generates the list of callback times.
Located in oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^^
Accepts an intake_settings entity
Returns an array of callback options for use in a checkbox form element.

Process
^^^^^^^^^

* Determines the start date available for next callback slot.  This is either:

  * 2 days from the current day
  * 3 days from the current day if it is a Saturday
  
* Builds an array of days from the start date going to the next 15 days.
* For each day in the array:

  * Gets the field name where the callback slots are stored.  This is determined by taking the lower case of the day of the week and appending it to oas_callback_hours.
  * Invokes oas_triage_user_is_holiday to determine if the day is a holiday
  * If there are callback hours and it is not a holiday, builds the time slot options for that day by:
  
    * Loading the taxonomy term that represents the hour slot
    * Checking to see if the time slot is full
    * If the time slot is not full, creates an option element for the checkbox element
    
.. note::
   Is the time slot full?  Programs currently can limit the number of callbacks that can be scheduled in a slot at either the intake setting or service level.  Service level is most common.  This requires then that we check the total number of callbacks for given slot to determine if the max has been reached. If the max has been reached, the time slot is not available for booking.      
  
.. todo::
   Consider reducing the number of days where callbacks are offered
   Consider allowing programs to set their own additional holidays.
   Consider refactoring to break this down further.

Displaying the form
--------------------
oas_triage_user_callback_form defines the form.
Located in: oas_triage_user.exits.inc

Process
^^^^^^^^^^

* Invokes the oas_triage_user_save_exit function to update the triage user information.
* Determines the maximum number of options the user can pick.  By default, that number is 3 but the program may have defined a different number in their service.  
* Builds the form with elements for:

  * Callback times, as a list of checkboxes
  * A single checkbox to indicate that none of the times work for them
  * A hidden value of for the maximum slots
  
Processing the form
-------------------- 
oas_triage_user_callback_form_submit validates and submits the form.

Process
^^^^^^^^^
* If the user has picked more time slots than allowed, an error is displayed and the user must reduce the number of selections before proceeding.
* If the user has indicated that none of the times work for them, they are redirected to the get-legal-help/please-call confirmation
* Otherwise:

  * The system invokes oas_triage_user_save_callback_times to save the selected callback times
  * Redirects the user to the get-legal-help/callback-confirm page.
  
oas_triage_user_save_callback_times
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in: oas_triage_user.exits.inc

* Updates the field_triage_callback_times associated with the triage user with an array of callback times.

* Invokes oas_triage_user_save to save the triage user with updated information.  

  

   
Callback Confirmation Page
===========================
The callback confirmation page is displayed when:

* the callback type is "we call client"   
* the user selects at least one callback time

See also:  `Contact form submission in <migration_oas_intake_ui.html>`_

and the etransfer was successful (see the oas_triage_user_please_call function)

If the etransfer_status was already set when this page is built, the user will see a message that their application was already submitted and it will not resubmit it.   
   
   
Bypass Intake Page
===================

The bypass intake page appears when the end point in the triage rules is set to bypass. The function oas_triage_user_bypass builds the bypass page and the oas--bypass.tpl.php file displays the page.

oas_triage_user_bypass
-----------------------
Located in oas_triage_user.exits.inc

Process
^^^^^^^^

* Loads the intake settings associated with the triage
* Loads the organization's name
* Build the content render array:

  * call_header is empty
  * If the program has defined a bypass message to display, sets the call_msg to that message, replacing any tokens for OAS:name with the organization name and the OAS:phone with the callback number.
  * If the program has not defined a bypass message, provides a generic message that uses the default organization name and callback number.
  
Saving the triage exit to the triage object
============================================
oas_triage-user_save_exit
Located in: oas_triage_user.exits.inc

Parameters
-----------
Requires an exit type and a transfer type as strings

+--------------------------+----------------------+----------------------+
| Page                     | Exit type            | Transfer type        |
+==========================+======================+======================+
| callback-form            | Callback form        | Started              |
+--------------------------+----------------------+----------------------+
| callback-confirm         | Callback confirm     | eTransferred         |            
+--------------------------+----------------------+----------------------+
| please-call              | Please call          | Not eTransferred     |
+--------------------------+----------------------+----------------------+


For a user accessing the callback form, the exit type is Callback form and transfer type is started.

Process
--------
Updates the triage user entity to:

* set the last screen viewed to the exit type
* set the intake status to the transfer type
* set the intake changed to the current timestamp
* saves the triage user entity by invoking oas_triage_user_save


.. todo::
   Unclear if bypass sets an exit type.
  
  
     

