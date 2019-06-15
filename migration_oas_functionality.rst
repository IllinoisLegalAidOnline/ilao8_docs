=================================
OTIS Functionality Documentation
=================================

Custom menu routes
=====================
We have defined a series of menu routes that provide the user interface for the system.

In oas_triage_user.module:

 * /get-legal-help:  Displays the main page of Get Legal Help.  Calls the form found in oas_triage_user.ui.inc.
 * /get-legal-help/triage-questions: Displays a picker for the user to narrow their legal issue when they select or enter a term that exactly matches on the legal issues taxonomy at anything above the lowest level. Relies on the oas_triage_user.evaluate_triage.inc and within that, the oas_triage_user_ilao_triage_form.
 * /get-legal-help/triage-start: Displays a picker for the user to identify their legal issue when they enter a term that is not an exact match to the legal issues taxonomy.  If no match is found, the user is given the top 8 substantive areas to pick from. Relies on the oas_triage_user.evaluate_triage.inc file and within that, the oas_triage_user_ilao_triage_start_form.
 * get-legal-help/referrals: Displays the user's referrals and relies on the oas_triage_user.referrals.inc file and oas--referrals.tpl.php template file.
 * get-legal-help/referral-history: Displays the user's past referrals based on a specific triage ID and relies on the oas_triage_user.referrals.inc file.
 * get-legal-help/intake: Displays the intake forms. The intake form is actually a multi-page form.  Relies on the oas_triage_user.application_form.inc file to generate the oas_triage_user_application_form.
 * get-legal-help/bypass: Displays the bypass intake page to users who reach a bypass intake exit point in online intake.  Relies on the oas_triage_user.exits.inc file and the oas--bypass.tpl.php template file.
 * get-legal-help/address-form: Displays the address form for users who successfully get through online intake.  Relies on the oas_triage_user_client_address_form in the oas_triage_user.address_form.inc file.
 * get-legal-help/please-call: Displays the please call us confirmation form.  Relies on the  the oas_triage_user.exits.inc file and the oas--please-call.tpl.php template file.
 * get-legal-help/callback-form: Displays the form for a user to pick one or more call back times.  Relies on the oas_triage_user_callback_form form in the oas_triage_user.exits.inc file.
 * get-legal-help/callback-confirm: Displays the please call us confirmation form.  Relies on the oas_triage_user.exits.inc file and the oas--we-call-you.tpl.php template file.


.. note::
   Depending on the legal issue selected a user would get routed from triage-start to triage-questions if further narrowing is required and from the triage-questions page to either referrals or program triage rules.
   
   
Functions
=============

oas_triage_user_get_organization_name($id)
--------------------------------------------
Located in: oas_triage_user.module
Requires: an integer representing the node ID of a location_service ($id)
Returns: a string that represents the name of the organization associated with the location

oas_triage_user_get_organization_nid ($id)
--------------------------------------------
Located in: oas_triage_user.module
Requires: an integer representing the node ID of a location_service ($id)
Returns: an integer that represents the node ID of the organization associated with the location

oas_triage_user_process_etransfer
----------------------------------
Located in: oas_triage_user.module
Requires: an integer representing the triage ID to process
Returns: a Boolean
Invoked by: Cron (see Scheduled tasks)
Purpose: processes an etransfer that is in the queue (has had a prior failure).

Process
^^^^^^^^

* Loads the triage user entity
* Checks the legal server configuration to see if it has already hit the limit (defaults to 3 tries otherwise)
* Returns a failure if the maximum retries has been reached
* Unserializes the user's data from the etransfer_data property
* Attempts to build the transfer (dependency: oas_legal_server_etransfer)
* Updates the triage user entity based on success or failure
* On success:

  * Sends the email confirmation message 
  * Sends an sms confirmation is available and user has opted in
  * Updates the triage user's intake status to etransferred, etransfer status to success
  
* On failure:

  * Updates the triage user's intake status to not eTransferred
  * Updates the triage user's etransfer status to failure if the maximum retries has not been met
  * Updates the triage user's etransfer status to abandoned if the maximum retries has been met
  * Updates the triage user's etransfer reason to the received failure reason.
  
  
Dependencies
^^^^^^^^^^^^^
Modules

* oas_legal_server to capture and return maximum number of retries
* ilao_triage_sms_reminders to send SMS confirmation 

Functions:

* oas_legal_server_eTransfer to build and send the etransfer
* oas_triage_user_email_notify to send email notification
* ilao_triage_sms_reminders_send_confirmation to send SMS notification
* oas_triage_user_phone_notify to send related legal content via SMS 
* oas_triage_user_save to update the triage user entity.
  

.. todo:: should be refactored.

oas_triage_user_email_notify
--------------------------------  
Parameters:

* an integer representing the intake settings ID associated with the triage
* the array of callback times
* the user's email

Process:

* Loads the intake settings for the intake
* Builds the email
* If the triage id exists in a session variable:

  * Loads the user's legal problem
  * Finds related content
  * Updates the email body to include those resources
  
* Invokes drupal_mail to send

Relies on:
* oas_triage_user_build_confirmation_body
* oas_triage_user_get_child_problem
* block 7 of the related legal content view


.. warning::
   This code needs to be reviewed. It appears to only include legal content if the session variable for triage ID exists.  Would be better to instead load the triage user ID as the parameter and build off of that data rather than rely on session when we may need to handle late etransfers.
   
oas_triage_user_phone_notify
------------------------------
Purpsose:  sends an SMS of related legal content to a user via SMS if they have completed intake.

Parameters:
* triage user entity

Relies on:

* oas_triage_user_get_child_problem
* block 7 of the related legal content view
* ilao_sms module

  * ilao_sms_check_mode (checks to determine if we are running SMS in demo mode)
  * ilao_sms_get_demo_phone (gets the demo number from configuration)
  
* twilio module (twilio_send to send the text)
* ilao_triage_sms module (ilao_triage_sms_save_message to send the actual sms text)
* shurly module (shurly_shorten to generate a shortened URL)
    
oas_triage_user_build_confirmation_body
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Builds the body of a successful intake email.

Parameters:

* intake settings entity
* call back times array

Relies on:

* oas_intake_settings.token.inc

Functions to determine user's problem
----------------------------------------
oas_triage_user_route_to_initial_results
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. warning::  

   The code in this function needs refactored.
   
Located in: oas_triage_user.
Parameters:

* form
* form_state (results of the user's Get legal help form)
* triage_user entity

Relies on:

* oas_triage_user_get_legal_issues
* oas_triage_user_get_top_parents
* oas_triage_user_get_legal_issue

Process

* Unsets any existing triage id (acts as a reset)
* Determines based on the user's search term:

  * We have an exact term match
  
    * Updates the user's problem in the system
    * Redirects the user to the right resources using the oas_triage_user_determine_resources function.
    
  * We have more than one matching term
  
    * Sets the triage status to Legal issue
    * Directs the user to the triage-questions page
  * We have no matching terms
  
    * Sets the triage status to top of triage tree
    * Sets the start terms to the top level terms
    * Redirects the user to triage-start

* Redirects the user to the legal-information/not-illinois page if they are out of the service area (see the oas_triage_user_in_service_area function)

oas_triage_user_get_legal_issues
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

oas_triage_user_get_top_parents
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Returns an array of legal isssues in the legal issues taxonomy that do not have a parent term.

Array is structured as the term id => translated name

oas_triage_user_get_legal_issue
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Parameter:  String of a search term
Returns either:

* 0 if no legal issue can be determined
* the term id for the matching term if exactly 1 is found
* the array of matching terms if more than 1 match is found

Relies on:
* taxonomy
* i18n 
* legal_issues_autosuggest view

Process:

* Checks first to see if the search term is an exact match for a legal issue taxonomy term.  
* Checks to see if there is a localized match to the search term
* If no result, uses the legal_issue_autosuggest to look for an exact match

  * If the search term is a single keyword, rewrites it to include plural formats
  * If the search term is not single keyword, uses the combined phrase
  * Then it loops through the results and:
    
     * if it is the lowest level term, adds the term object into an array
     * if that array is then empty (meaning none of the results were low-level terms)
      
       * adds any term that has a child and a parent (this avoids adding the top level terms
       * loops through the resulting array to remove child terms if the parent term is included
       
  * if there is just one result, the term id is returned
  * if there is more than one result, the array is returned.  The array includes the term id as the key and the term name as the value.      
    
oas_triage_user_in_service_area
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^    
Located in: oas_triage_user.evaluate_triage.inc
Parameters: triage_user entity
Returns: Boolean
Purpose: Determines if the user is in our service area:

* Users in Illinois are always in the service area
* Users outside of Illinois are out of the service area unless:

  * User is looking for help in immigration (see oas_triage_user_is_immigration)
  * User is looking for a lawyer
  * User is in NIJC's extended service area (see oas_triage_user_check_nijc

oas_triage_user_is_immigration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in: oas_triage_user.evaluate_triage.inc
Parameters: integer representing the term id of the user's problem
Returns: Boolean  
Purpose: Determine if the user's legal issue is related to an immigration problem in our taxonomy

oas_triage_user_check_nijc
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in: oas_triage_user.evaluate_triage.inc
Parameters: integer representing the term ID of the user's state
Returns:  Boolean
Purpose:  Determines if a user is in NIJC's extended service area as NIJC allows intakes through our platfor outside of Illinois.

.. warning:: 
   NIJC's organization node ID is hard coded into this function.
   
   
oas_triage_user_determine_resources
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in: oas_triage_user.evaluate_triage.inc
Parameters: 

* triage user entity
* form_state array

Returns: form_state
Purpose:  Updated the form_state to set an appropriate redirect to the next page.
Process:

* If no help type exists, sets the help type to lawyer.
* If the help types include a lawyer:

  * Determines if intake is available (see oas_triage_user_is_intake_available)
  * If intake is possible:
  
    * Checks to see if there are program triage rules
    * If there are program triage rules:
    
      * Sets the triage status to Program triage
      * Sets the redirect to the triage rules node
    * If there are no triage rules:
    
      * Sets the triage status to Referrals
      * Redirects to referrals page
      
 * If intake is not possible:
 
   * Sets the triage status to Referrals
   * Redirects to referrals page
   
* If the user is not looking for a lawyer:
  
  * Sets the triage status to referrals
  * Redirects to the referrals page   
          

.. warning::
   There is a refernce to referrals when the user overincome value is 10; this is never invoked.

oas_triage_user_get_search_terms
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in: oas_triage_user.evaluate_triage.inc
Parameters: An array of terms
Returns: An array of term reference options for use in a form, formatted as tid => name

Functions to determine whether intake is available
----------------------------------------------------
oas_triage_user_is_intake_available
    
Forms
==========

Get Legal Help main form
---------------------------
Function: oas_triage_user_edit_form
Found in: oas_triage_user.ui.inc


On menu access, creates a triage user entity.  The default form:

* Loads the user if the user is logged in
* Loads the user's zip code if it is defined in their account or in a session variable
* Adds a heading markup element to describe Get Legal Help
* Adds a zip code text field
* Adds a household size field
* Adds an overincome field (yes or no that asks the user if their income is more than a maximum amount
* Adds an ajax callback that takes the household size and calculates the maximum income amount. 
* Attaches any additional fields created in the user interface.  In ILAO's instance that includes
  
  * What type of help do you want? Check all that apply. (oas_triage_help_type)
  * What is your problem about? (field_triage_search, text field)
  * I would like to get confirmation, reminders, and additional information via text message (field_opt_in_sms); this field is currently set to no access
  * My problem is about: (field_triage_problem; term reference); set to no access
  * Do any of the following describe you? Check all that apply. (field_limited_populations; term reference)
  * Mobile phone (field_mobile_phone; text); set to no access
  * Problem history (field_triage_problem_history, term reference); set to no access
  * Callback times selected (field_triage_callback_times; text)

Calculating Maximum Income
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The oas_triage_user_get_maximum_income function in the oas_triage_user.ui.inc file controls the maximum intake value that appears on the main Get Legal Help form. 

It defaults to $10,000 unless ILAO's custom ilao_oas_income_standard module is installed (this is installed on ILAO's website).  With that module installed, the function:

* Loads the federal poverty level income standard
* Grabs the amount that matches the user's household size; this amount is annual income
* Calculates the monthly maximum by multiplying the annual income by 350%, dividing by 12 and adding $500. 
* Calculates the amount to display by taking the maximum amount and dividing it by 1000, dropping any fractions and then adding $1000.
* Applies a number format to the amount

.. note::
   If the annual income is $12500 per year, the system will take that amount multiply it by 3.5 and divide by 12 ($3645.83) and then adding $500 ($4145.83).  It will then divide that by 1000 (4.14583) and drop any fraction (4) and then multipling by 1000 for an amount of $4000
  

Known Alters
^^^^^^^^^^^^^^
The Get legal help form can be altered by any other module.  Our ILAO-specific intake settings module does this.  

Function: ilao_intake_settings_form_oas_triage_user_edit_form_alter
Location: ilao_intake_settings.module
  
Alterations:

* Sets the callback times text field to no access
* Adds a fieldset for legal
* Adds a checkbox field for a disclaimer
* Adds a checkbox field for terms and conditions
* Adds translation support for help type options   

Validation
^^^^^^^^^^^^^
Function: oas_triage_user_edit_form_validate
Located in: oas_triage_user.ui.inc

Validates that if the help type includes lawyer that the household size and income fields are both required.

Form submit
^^^^^^^^^^^^
Function: oas_triage_user_edit_form_submit
Located in: oas_triage_user.ui.inc

Process:

* Stores the household size in a session variable
* Updates the tirage user entity to:

  * Sets the created time to the current time for a new entity 
  * Set the changed time to the current time
  * Store the user ID
  * Store the IP address
  * Set the last screen viewed to "get-legal-help"
  
* If the ilao_geolocation module is enabled (it currently is), the submit form also updates the triage entity to:

  * Set the county to the county associated with the submitted zip code
  * Set the state to the state associated with the submitted zip code 
  
* Invokes the oas_triage_user_route_to_initial_results function to launch the next step  
  


Triage form
-------------
Function: oas_triage_user_ilao_triage_form
Found in: oas_triage_user.evaluate_triage.inc

If necessary, will set the session variable triage_id based on url path and then loads the triage entity.

Form consists of up to 4 radio elements that represent the maximum depth of the legal issues taxonomy.  For example, when the taxonomy tree structure looks like this:

* Level 1

  * Level 2
  
    * Level 3
    * Level 3
      
      * Level 4
      * Level 4
      * Level 4
    * Level 2
  
    * Level 3
    * Level 3
      
      * Level 4
      * Level 4
      * Level 4    
* Level 1
* Level 1

If the user's search matches on Level 1, all the Level 2s will appear and then upon selecting a Level 2, all the Level 3s will display under that Level 2 and then upon selecting a Level 3, all the Level 4s will display.  

If the user starts at a lower level term or there are no child terms, the submit form displays.

Form Submit
^^^^^^^^^^^^
Function: oas_triage_user_ilao_triage_form_submit
Located in: oas_triage_user.evaluate_triage.inc

Upon submitting the form:

* The user's legal problem history is updated in the field_triage_problem_history record.  This field maintains the entire hierarchy of their selections.
* Updates the triage user entity
* Invokes the oas_triage_user_determine_resources function to determine how to route the user

oas_triage_user_legal_issue_build_tree
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Found in: oas_triage_user.evaluate_triage.inc
Parameter: integer; taxonomy term id from legal issues
Returns an array of select options that are at the level immediately below the hierarchy level as the term parameter

Triage start form
--------------------
Function: oas_triage_user_ilao_triage_start_form
Found in: oas_triage_user.evaluate_triage.inc

If necessary, will set the session variable triage_id based on url path and then loads the triage entity.

This is a dynamic form that is used on the get-legal-help/triage-start page.
It consists of a single checkbox field that displays either:

* The top categories from our legal issues taxonomy (from oas_triage_user_get_top_parents)
* The list of terms from based on the user's search (using oas_triage_user_get_search_terms)  

Form submit
^^^^^^^^^^^^^
Function: oas_triage_user_ilao_triage_start_submit
Located in: oas_triage_user.evaluate_triage.inc
If the user has selected a lowest level legal issue:

* update the user's problem in their triage entity
* use the oas_triage_user_determine_resources function to proceed.

If the user has not selected a lowest level legal issue:

* update the user's problem in their triage entity
* Redirects to the /triage-questions form





Scheduled tasks
================

.. note::
   We have invoked scheduled tasks using the Drupal hook_cron and also the hook_cronapi methods.  The hook_cronapi method is more useful when connecting to third party cron, like Elysian cron.
   
Process queued eTransfers
--------------------------
Located in: oas_triage_user.module
Requires: nothing
Invokes:  hook_cron
Relies on: oas_triage_user_process_etransfer
Purpose: Runs the scheduled task to retry failed eTransfers.
Executes: This task is scheduled to run hourly.

Related: oas_triage_user_cron_queue_info in the same module, tells the Drupal queue about our scheduled task.

oas_triage_user_process_etransfer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This is a fairly complex piece of code that goes through the queue of unprocessed etransfers and attempts to resend them.  

Parameters:  
  Accepts: a triage_id that ties to the oas_triage_user table
  Returns: a boolean (succeeded or failure)

It relies on:

* variables set in the legal server configuration for end point and maximum retries
* the serialized data stored in the user's triage record
* the oas_triage_user_email_notify function to send the user a confirmation message
* the ilao_triage_sms_reminders module to send an SMS confirmation if the user has SMS
* oas_triage_save_user to save the user's information and update their record

  * on success, the user's intake status is set to eTransferred and their eTransfer status updated to success
  * on failure, the user's etransfer status is set to Abandoned and the failure reason stored, if the maximum number of tries has been reached.
  * on failure, the user's etransfer status is set to Failure and the failure reason stored, if the maximum number of tries has not yet been reached.

.. note::
   The SMS reminder is not a dependency; the code checks that the module is enabled and if it is not, SMS is ignored.


Remove OAS Triage User Test Data
----------------------------------
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: oas_triage_user_remove_test_data
Purpose: Removes test data from our production database.  Test data includes any instance where the user's last name is test or tester. 
Executes:  This task is scheduled to run daily.

Update intake status for incompletes
-------------------------------------
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: oas_triage_user_set_intake_status
Purpose: Updates the intake status for users who started but did not complete intake.  
Executes:  This task is scheduled to run daily.

Notify Site architects if etransfers stop completely
-----------------------------------------------------
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: 

* oas_triage_user_send_email_regarding_etransfer_issue
* rules module
* custom rule component (rules_potential_problem_with_etransfers)

Purpose:  Sends an email notification to site architect when no etransfers have been processed in 2 days.

.. todo:: 
   this component needs to be updated to send to OTIS manager not site architect.
