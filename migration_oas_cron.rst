============================
OTIS Scheduled Tasks
============================


.. note::
   We have invoked scheduled tasks using the Drupal hook_cron and also the hook_cronapi methods.  The hook_cronapi method is more useful when connecting to third party cron, like Elysian cron.
   
Process queued eTransfers
===========================
Located in: oas_triage_user.module
Requires: nothing
Invokes:  hook_cron
Relies on: oas_triage_user_process_etransfer
Purpose: Runs the scheduled task to retry failed eTransfers.
Executes: This task is scheduled to run hourly.

Related: oas_triage_user_cron_queue_info in the same module, tells the Drupal queue about our scheduled task.

oas_triage_user_process_etransfer
------------------------------------
This is a fairly complex piece of code that goes through the queue of unprocessed etransfers and attempts to resend them.  


Located in: oas_triage_user.module

Invoked by: Cron 
Purpose: processes an etransfer that is in the queue (has had a prior failure).

Parameters:  
  Accepts: a triage_id that ties to the oas_triage_user table
  Returns: a boolean (succeeded or failure)

It relies on:

* variables set in the legal server configuration for end point and maximum retries
* the serialized data stored in the user's triage record
* the oas_triage_user_email_notify function to send the user a confirmation message
* the ilao_triage_sms_reminders module to send an SMS confirmation if the user has SMS
* oas_triage_save_user to save the user's information and update their record


.. note::
   The SMS reminder is not a dependency; the code checks that the module is enabled and if it is not, SMS is ignored.



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


Remove OAS Triage User Test Data
==================================
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: oas_triage_user_remove_test_data
Purpose: Removes test data from our production database.  Test data includes any instance where the user's last name is test or tester. 
Executes:  This task is scheduled to run daily.

Update intake status for incompletes
======================================
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: oas_triage_user_set_intake_status
Purpose: Updates the intake status for users who started but did not complete intake.  
Executes:  This task is scheduled to run daily.

Notify Site architects if etransfers stop completely
======================================================
Located in: oas_triage_user.module
Invokes: hook_cronAPI
Relies on: 

* oas_triage_user_send_email_regarding_etransfer_issue
* rules module
* custom rule component (rules_potential_problem_with_etransfers)

Purpose:  Sends an email notification to site architect when no etransfers have been processed in 2 days.

.. todo:: 
   this component needs to be updated to send to OTIS manager not site architect.


