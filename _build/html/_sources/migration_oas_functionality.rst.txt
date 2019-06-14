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

Functions to determine whether intake is available
----------------------------------------------------
oas_triage_user_is_intake_available
    
   

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
