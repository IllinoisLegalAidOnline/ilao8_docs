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
   
Callback Confirmation Page
===========================
The callback confirmation page is displayed when:

* the callback type is "we call client"   
* the user selects at least one callback time

and the etransfer was successful (see the oas_triage_user_please_call function)

If the etransfer_status was already set when this page is built, the user will see a message that their application was already submitted and it will not resubmit it.   
   

