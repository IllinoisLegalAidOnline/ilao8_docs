==============================
OTIS Automated Notifications
==============================

Two sets of notifications exist in OTIS:

* Initial confirmation, by email and, optionally, SMS
* Reminders of callback appointments

Initial Confirmations
======================
Located in: oas_triage_user.module file in the oas_triage_user_process_etransfer function.

When an etransfer is successful:

* Invokes oas_triage_user_email_notify to send an email confirmation
* Checks to see if the ilao_triage_sms_reminders module is enabled and if so:

  * Sends a confirmation text via ilao_triage_sms_reminders_send_confirmation
  * Sends a content follow up via oas_triage_user_phone_notify
  
Email notifications
--------------------------------  
Function:  oas_triage_user_email_notify
Located in: oas_triage_user.module

Parameters
^^^^^^^^^^^^

* an integer representing the intake settings ID associated with the triage
* the array of callback times
* the user's email

Process
^^^^^^^^^

* Loads the intake settings for the intake
* Builds the email
* If the triage id exists in a session variable:

  * Loads the user's legal problem
  * Finds related content
  * Updates the email body to include those resources
  
* Invokes drupal_mail to send

Relies on
^^^^^^^^^^^^^
* oas_triage_user_build_confirmation_body
* oas_triage_user_get_child_problem
* block 7 of the related legal content view


.. warning::
   This code needs to be reviewed. It appears to only include legal content if the session variable for triage ID exists.  Would be better to instead load the triage user ID as the parameter and build off of that data rather than rely on session when we may need to handle late etransfers.
   
SMS Confirmation  Notification
--------------------------------

Function: ilao_triage_sms_reminders_send_confirmation
Located in: ilao_traige_sms_reminders.module

Parameters
^^^^^^^^^^^^
Requires:

* Triage user entity
* Intake settings ID
* Callback hours string (which may be null)

Returns: nothing

Process
^^^^^^^^^
The function:

Verifies that the user has opte-in to SMS as part of their online intake application.  If the user has opted in:

* Calls oas_triage_user_build_confirmation_body to build the message
* Converts the resulting message to plain text since SMS does not support HTML
* Loads the user's phone number (or demo phone number if running in demo mode)
* Verifies that a phone number exists and then:

  * Sends the confirmation message via Twilio
  * Checks to see if callback hours exists and if so:
  
    * Calls ilao_triage_sms_reminders_build_cancel_reminder to build a cancel message
    * Sends the cancel message via Twilio
    
  * Logs the message via ilao_triage_sms_save_message
  
ilao_triage_sms_reminders_build_cancel_reminder
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Parameters:

* Accepts a triage user entity
* Returns a string

Process:

* Loads the intake_settings for the intake organization
* Builds the message (If you need to change or cancel your appointment...)
* Relies on the oas_intake_settings tokens to replace OAS:name and OAS:call-back-number tokens.


ilao_triage_sms_save_message
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^   

Parameters:
Accepts the telephone number, message, and a message type.  For sms reminders, the type is "OAS confirmation"

Returns: null

Process:

* Creates a message array
* Invokes the ilao_sms_surveys_create function to create a message object
* Saves the message object

.. code-block:: php

   $message['created'] = REQUEST_TIME;
   $message['changed'] = REQUEST_TIME;
   $message['from_number'] = variable_get('twilio_number');
   $message['to_number'] = $to_number;
   $message['message_type'] = $type;
   $message['message'] = $body;

ilao_sms_surveys_create to create an entity and save it.  

 

.. todo:: 

   * Depends on the ilao_sms_surveys module but does not include that as a module dependency or check for it in the code.
   * Should probably be saving messages to the ilao_sms_message table.
  


SMS Related Content Notification
---------------------------------
oas_triage_user_phone_notify

Purpose:  sends an SMS of related legal content to a user via SMS if they have completed intake.

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





