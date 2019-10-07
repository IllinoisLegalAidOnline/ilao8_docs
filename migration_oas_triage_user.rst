==============================
OAS Triage User
==============================


This documentation covers the oas_triage_user module which provides an entity to store information about a specific OTIS triage and intake instance.

In addition, it provides most of the actual intake and triage functionality

Dependencies
==============
None

Base Tables
=============

oas_triage_user_type
---------------------
Base table for triage user types.  There is in fact only the one type.

+-----------------------+-------------------------------------+-------------------------------+
| Name                  | Description                         | Type                          |
+=======================+=====================================+===============================+
| id                    | Id for the triage user type         | serial, primary key, not null |
+-----------------------+-------------------------------------+-------------------------------+
| type                  | Machine name of the triage user type| varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| label                 | Human-readable name of the type     | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| weight                | Weight of the type                  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| data                  | Serialized array of extra info      | text                          |
+-----------------------+-------------------------------------+-------------------------------+

oas_triage_user 
--------------------

+-----------------------+-------------------------------------+-------------------------------+
| Name                  | Description                         | Type                          |
+=======================+=====================================+===============================+
| triage_id             | Id for the triage user instance     | serial, primary key, not null |
+-----------------------+-------------------------------------+-------------------------------+
| type                  | Triage type (oas_triage_user_type)  | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| created               | Unix timestamp of when the entity   | int                           |
|                       | was created                         |                               |
+-----------------------+-------------------------------------+-------------------------------+
| changed               | Unix timestamp of when the entity   | int                           |
|                       | was last updated                    |                               |
+-----------------------+-------------------------------------+-------------------------------+
| intake_created        | Unix timestamp of when intake was   | int                           |
|                       | started                             |                               |
+-----------------------+-------------------------------------+-------------------------------+
| intake_changed        | Unix timestamp of when intake was   | int                           |
|                       | last updated (ie the user completes |                               |
|                       | a step in the intake process)       |                               |
+-----------------------+-------------------------------------+-------------------------------+
| data                  | Serialized array of extra data      | blob                          |
+-----------------------+-------------------------------------+-------------------------------+
| uid                   | User ID of the person using Get     | int                           |
|                       | Legal Help; 0 for anonymous users   |                               |                        
+-----------------------+-------------------------------------+-------------------------------+
| household size        | Total household size                | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| household_adults      | Number of adults in household; only | int                           |
|                       | collected in intake                 |                               |
+-----------------------+-------------------------------------+-------------------------------+
| household_children    | Number of children in household;    | int                           |
|                       | only collected in intake            |                               |
+-----------------------+-------------------------------------+-------------------------------+
| total_income          | Total monthly income for household; | float                         |
|                       | only collected with intake          |                               |
+-----------------------+-------------------------------------+-------------------------------+
| total_expenses        | Total monthly household expenses;   | float                         |
|                       | only collected with intake          |                               |
+-----------------------+-------------------------------------+-------------------------------+
| total_assets          | Total assets for household;         | float                         |
|                       | only collected with intake          |                               |
+-----------------------+-------------------------------------+-------------------------------+
| zip_code              | User's zip code                     | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| triage_status         | Current triage status               | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| intake_status         | Current intake status               | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| intake_organization   | Intake settings id associated with  | int                           |
|                       | an intake application.              |                               |
+-----------------------+-------------------------------------+-------------------------------+
| lsc_code              | LSC problem code (not active)       | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| lsc_subcode           | LSC subproblem code (not active)    | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| referral_source       | Tracks how the user got to OTIS     | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| county                | User's county                       | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| state                 | User's state                        | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| ip_address            | User IP address (for ILAO, our load | varchar; 255                  |
|                       | balancer IP masks the actual user IP|                               |
+-----------------------+-------------------------------------+-------------------------------+
| last_screen_viewed    | Last screen the user viewed         | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| intake_notes          | Intake notes sent with application  | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| gender                | Gender of the user; collected only  | varchar; 255                  |
|                       | in intakes where it is required     |                               |
+-----------------------+-------------------------------------+-------------------------------+
| race                  | Race of the user; collected only    | varchar; 255                  |
|                       | in intakes where it is required     |                               |
+-----------------------+-------------------------------------+-------------------------------+
| ethnicity             | Ethnicity of the user; collected    | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| marital_status        | Marital status of user; collected   | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| citizenship           | Citizenship of the user; collected  | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| immigrant_status      | Immigrant status of user; collected | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| age                   | User's age; intake only             | int                           |                
+-----------------------+-------------------------------------+-------------------------------+
| primary_language      | Language spoken at home; collected  | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| country_of_origin     | User's country of origin; collected | varchar; 255                  |
|                       | only in intakes where it's required |                               |
+-----------------------+-------------------------------------+-------------------------------+
| overincome            | Whether user is overincome or not   | int; see key                  |
+-----------------------+-------------------------------------+-------------------------------+
| etransfer_status      | E-transfer status                   | text                          |
+-----------------------+-------------------------------------+-------------------------------+
| etransfer_failure     | E-transfer failure reason           | text                          |
| _reason               |                                     |                               |
+-----------------------+-------------------------------------+-------------------------------+
| etransfer_data        | Serialized array of etransfer data; | blob                          |
|                       | scrubbed after 7 days               |                               |
+-----------------------+-------------------------------------+-------------------------------+
| daily_reminder_sent   | Logs a 1 when a daily reminder of   | int                           |
|                       | an appointment is sent              |                               |
+-----------------------+-------------------------------------+-------------------------------+
| hourly_reminder_sent  | Logs a 1 when the hour-before an    | int                           |
|                       | appointment reminder is sent        |                               |
+-----------------------+-------------------------------------+-------------------------------+

Fields
=========
The install hook(s) add a number of fields and field instances upon installation:

+----------------------------+----------------------------------------------------------+
| Field                      | Description                                              |
+============================+==========================================================+
| oas_referrals              | Do not migrate; Installed in install hook; deleted in    | 
|                            | update hook                                              |
+----------------------------+----------------------------------------------------------+
| oas_triage_help_type       | Type of help the user is seeking (list_text, unlimited)  |
+----------------------------+----------------------------------------------------------+
| field_triage_problem       | User problem (term reference; uses legal issues taxonomy;|
|                            | cardinality is 1)                                        |
+----------------------------+----------------------------------------------------------+
| field_limited_populations  | Populations the user belongs to (term reference; uses    |
|                            | intake populations taxonomy                              |
+----------------------------+----------------------------------------------------------+
| field_triage_search        | Text field of user's problem (text, cardinality of 1     |
+----------------------------+----------------------------------------------------------+
| field_triage_problem       | Term reference for user problem (term reference; uses    |
|                            | legal issues taxonomy; cardinality unlimited)            |
+----------------------------+----------------------------------------------------------+
| field_triage_referrals     | Do not migrate; Exists in install script but deleted in  |
| _given                     | intake settings update hook                              |
+----------------------------+----------------------------------------------------------+
| field_triage_callback_times| Stores user callback times; text field; unlimited        |
+----------------------------+----------------------------------------------------------+
| field_opt_in_sms           | Field to get opt in consent for SMS; boolean             |
+----------------------------+----------------------------------------------------------+
| field_mobile_phone         | Text field for mobile phone number                       |
+----------------------------+----------------------------------------------------------+

.. warning::
   field_triage_referrals_given and oas_referrals should be removed from the Drupal 8 module.
   Also the field_triage_problem stores the term reference SELECTED by the user without capturing a full hierarchy while field_triage_search stores the actual text or taxonomy term depending on what was entered. 

 
Taxonomies
============
The module automatically creates a number of default taxonomies upon installation.

+----------------------------+----------------------------------------------------------+
| Taxonomy                   | Description                                              |
+============================+==========================================================+
| oas_gender                 | Provides default gender terms for OTIS                   |
+----------------------------+----------------------------------------------------------+
| oas_ethnicity              | Provides default ethnicity terms for OTIS                |
+----------------------------+----------------------------------------------------------+
| oas_race                   | Provides default race terms for OTIS                     |
+----------------------------+----------------------------------------------------------+
| oas_languages              | Provides default list of languages for OTIS              |
+----------------------------+----------------------------------------------------------+
| oas_citizenship_status     | Provides default list of citizenship statuses for OTIS;  |
|                            | this field is used primarily by the LSC-funded orgs      |
+----------------------------+----------------------------------------------------------+
| oas_immigration_status     | Provides default list of immigrant statuses for OTIS;    |
|                            | this field is used primarily by NIJC                     |
+----------------------------+----------------------------------------------------------+
| oas_marital_status         | Provides default marital statuses for OTIS               |
+----------------------------+----------------------------------------------------------+


