=================================
OTIS Global Items
=================================

Custom Menu Routes
====================

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
   
Important notes
==================

Locations
-----------

Location is tricky because we allow for tagging of service area at different levels: a range of zip codes OR a range of cities OR a range of counties or as a statewide service area.  NIJC also serves states outside of Illinois that needs to be accounted for.  Each of these elements are in different fields (and different database tables):
   
   * field_data_field_zipcodes for zip code
   * field_data_field_cities for cities
   * field_data_field_counties for counties
   * field_data_field_statewide with a value of 1 for statewide entities
   * field_extended_service_area for states served by NIJC outside of Illinois  
   
Overlap
---------
Triage rules can be tied to 1 or more service and 1 or more legal issues.
Intake settings can be tied to 1 service and 1 or more legal issues.  

If there is more than 1 intake setting that matches on legal issue for a user:

* If one is tied to a matching special population, that one is returned
* If there is still more than 1 match, the first one created will be returned

If there is more than 1 set of triage rules that matches on service and legal issue, the first created will be returned.

..  warning::
   Programs need to be careful not to overlap triage rules or intake settings with each other.  When that happens, the first match is returned.  For example, if a program has 2 sets of intake settings tagged to the same service and the same 5 legal issues, the first one created will always be returned. The same happens with triage rules.     
    
Common Functions
=================

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

oas_triage_user_save
-----------------------
Located in: 
Requires:  a triage user entity
Saves the triage user entity to the database.

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
