===================================
OAS Intake Settings 
===================================

This is the documentation for the oas_intake_settings module and related information. Combined, these provide a framework for data related to online intake.

.. note::
   There is also an ilao_oas_intake_settings module in the Drupal 7 codebase.  This module is not in fact enabled.

OAS Intake Settings Module
============================

Dependencies
-------------
This module requires:

* entity
* entity_reference
* ilao_oas_financial_category
* oas_triage_user

Base Tables
------------

oas_intake_settings_type
^^^^^^^^^^^^^^^^^^^^^^^^^

Stores the intake settings types.  This was created mostly because it was in the model code Gwen used.  It contains only 1 record for the actual oas_intake_settings entity type.
  
  * id (not null; serial; primary key)
  * type (machine readable name; varchar, not null)
  * label (human readable name; varchar; not null)
  * weight (int, not null)
  * data (serialized array)
  
oas_intake_settings
^^^^^^^^^^^^^^^^^^^^^
  
+---------------------+----------------------------------------+------------------+
| Name                | Description                            | Type             |
+=====================+========================================+==================+
| intake_settings_id  | ID of the intake settings              | Serial; primary  |
|                     |                                        | key; not null    |
+---------------------+----------------------------------------+------------------+
| type                | type from                              | varchar; 255;    |
|                     | oas_intake_settings_type               | not null         |
+---------------------+----------------------------------------+------------------+     
| created             | unix timestamp of when entity created  | int              |
+---------------------+----------------------------------------+------------------+
| changed             | unix timestamp of when last changed    | int              |
+---------------------+----------------------------------------+------------------+
| uid                 | User id of the author                  | int              |
+---------------------+----------------------------------------+------------------+
| data                | serialized array of additional dat     | blob             |
+---------------------+----------------------------------------+------------------+
| name                | name/label of the entity               | varchar; 255     |
|                     |                                        | not null         |
+---------------------+----------------------------------------+------------------+
| entity_id           | entity associated with the settings;   | int; not null    |
|                     | location_services tied to the settings |                  |
+---------------------+----------------------------------------+------------------+
| entity_type         | entity type of the associated entity   | varchar; 255;    |
|                     | in our use case, always is node        | not null         |
+---------------------+----------------------------------------+------------------+
| current_count       | Current number of completed intakes    | int; not null    |
+---------------------+----------------------------------------+------------------+
| enabled             | 0 or 1; whether settings are active    | int; not null    |
+---------------------+----------------------------------------+------------------+
| collect_mar         | 0 or 1; whether to collect marital     | int              |
| ital__status        | status                                 |                  |
+---------------------+----------------------------------------+------------------+ 
| collect_immigration | 0 or 1; whether to collect immigration | int              |
+---------------------+----------------------------------------+------------------+           
| collect_citizenship | 0 or 1; whether to collect citizenship | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_country     | 0 or 1; whether to collect country     | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_language    | 0 or 1; whether to collect language    | int              |
+---------------------+----------------------------------------+------------------+           
| collect_race        | 0 or 1; collect user's race            | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_ethnicity   | 0 or 1; collect user's ethnicity       | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_income      | 0 or 1; whether to collect income      | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_assets      | 0 or 1; whether to collect assets      | int              |
+---------------------+----------------------------------------+------------------+ 
| collect_expenses    | 0 or 1; whether to collect expenses    | int              |
+---------------------+----------------------------------------+------------------+ 
| apply_income_limit  | 0 or 1; whether to apply an income     | int              |
|                     | limit                                  |                  |
+---------------------+----------------------------------------+------------------+ 
| apply_asset_limit   | 0 or 1; whether to apply an asset limit| int              |
+---------------------+----------------------------------------+------------------+ 
| collect_expenses    | 0 or 1; whether to collect expenses    | int              |
| _over_income        | only if user is over-income w/o expense|                  |
+---------------------+----------------------------------------+------------------+ 
| allow_prisoners     | 0 or 1; whether to allow prisoners to  | int              |
|                     | apply online                           |                  |
+---------------------+----------------------------------------+------------------+
| maximum_allowed     | maximum allowed income, as a percentage| int              |
| _income             | of an income standard entity           |                  |
+---------------------+----------------------------------------+------------------+
| maximum_allowed     | maximum allowed assets, as a dollar    | int              |
| _assets             | amount                                 |                  |
+---------------------+----------------------------------------+------------------+
| personal_exemption  | dollar amount to exclude from assets   | int              |
| _amount             | when calculating asset eligibility     |                  |
+---------------------+----------------------------------------+------------------+
| intake_limit        | maximum number of etransfers to allow  | int              |
+---------------------+----------------------------------------+------------------+
| reset_limit         | how often to reset intake count; 1, 7, | int              |
| _frequency          | or 30 days.  0 for unlimited           |                  |
+---------------------+----------------------------------------+------------------+
| maximum_callbacks   | Maximum callbacks to allow in a time   | int; deprecate   |
| _per_slot           | slot.                                  |                  |
+---------------------+----------------------------------------+------------------+
| minimum_minor_age   | Minimum age to apply; minimum is 13;   | int; default = 18|
+---------------------+----------------------------------------+------------------+
| minimum_senior_age  | Minimum age to qualify as a senior     | int; default = 60|
+---------------------+----------------------------------------+------------------+
| callback_number     | Callback telephone number              | varchar; 128     |
+---------------------+----------------------------------------+------------------+
| callback_type       | Type of callback to allow              | varchar; 128     |
+---------------------+----------------------------------------+------------------+
| cms_vendor          | CMS vendor to etransfer to             | varchar; 255     |
+---------------------+----------------------------------------+------------------+
  
.. note::
  
   Maximum callbacks per slot should be deprecated in favor the maximum callbacks per slot in the service content type.
  
     
Fields
-------
The OAS intake settings entity type ships with a set of predefined fields:


+----------------------------+----------------------------------------------------------+
| Field                      | Description                                              |
+============================+==========================================================+
| oas_household_definition   | Text area; provides an editable household definition     |
+----------------------------+----------------------------------------------------------+
| oas_msg_already_applied    | Text area; editable message for users who have already   |
|                            | applied                                                  |
+----------------------------+----------------------------------------------------------+
| oas_msg_current_client     | Text area; editable message for current clients of an    |
|                            | program                                                  |
+----------------------------+----------------------------------------------------------+
| oas_msg_we_call_you        | Text area; editable message shown to users who are told  |
|                            | that the program will call them.                         |
+----------------------------+----------------------------------------------------------+
| oas_msg_please_call        | Text area; editable message shown to users who are told  |
|                            | to call the program                                      |
+----------------------------+----------------------------------------------------------+
| oas_msg_disclaimer         | Text area; editable program disclaimer                   |
+----------------------------+----------------------------------------------------------+
| oas_help_marital_status    | Text area; editable help text for marital status         |
+----------------------------+----------------------------------------------------------+
| oas_help_immigration_status| Text area; editable help text for immigration status     |
+----------------------------+----------------------------------------------------------+
| oas_help_citizenship_status| Text area; editable help text for citizenship status     |
+----------------------------+----------------------------------------------------------+
| oas_help_country_of_origin | Text area; editable help text for collecting country     |
+----------------------------+----------------------------------------------------------+
| oas_help_language          | Text area; editable help text for user's language        |
+----------------------------+----------------------------------------------------------+
| oas_help_race              | Text area; editable help text for user's race            |
+----------------------------+----------------------------------------------------------+
| oas_help_gender            | Text area; editable help text for user's gender          |
+----------------------------+----------------------------------------------------------+
| oas_help_ethnicity         | Text area; editable help text for user's ethnicity       |
+----------------------------+----------------------------------------------------------+
| oas_income_exempt          | Term reference (intake populations); unlimited           |
|                            | Used to waive income for special populations             |                                  
+----------------------------+----------------------------------------------------------+
| oas_income_standard        | Entity reference (ilao_oas_income_standard); limited to 1|
|                            | Used to apply a specific income standard                 |
+----------------------------+----------------------------------------------------------+
| oas_income_categories      | Entity reference (ilao_oas_financial_category; income    |
|                            | types bundle); unlimited                                 |
|                            | Used to indicate what income types to collect            |
+----------------------------+----------------------------------------------------------+
| oas_asset_categories       | Entity reference (ilao_oas_financial_category; asset     |
|                            | types bundle); unlimited                                 |
|                            | Used to indicate what asset types to collect             |
+----------------------------+----------------------------------------------------------+
| oas_expense_categories     | Entity reference (ilao_oas_financial_category; expense   |
|                            | types bundle); unlimited                                 |
|                            | Used to indicate what exepense types to collect          |
+----------------------------+----------------------------------------------------------+

Taxonomies
--------------
The oas_intake_settings module creates the oas_callback_hours taxonomy.


Tokens
========
The oas_intake_settings.token.inc file defines specific tokens for use in OTIS.  All tokens are prefixed with OAS, for example: [OAS:name].

When used in text that is then run through the token module, the token string is replaced with actual data.

+----------------------------+----------------------------------------------------------+
| Token                      | Description                                              |
+============================+==========================================================+
| OAS:name] or [OAS:Name]    | Returns the organization name of the service the user has|
|                            | applied to.                                              |
+----------------------------+----------------------------------------------------------+
| [OAS:call-back-number],    | Returns the call back number from the intake settings    |
| [OAS:phone], [OAS:Phone]   |                                                          |
+----------------------------+----------------------------------------------------------+
| [OAS:minimum-age]          | Returns the minimum age to apply online through OTIS     |
+----------------------------+----------------------------------------------------------+
| [OAS:senior-age]           | Returns the minimum age to be considered a senior        |
+----------------------------+----------------------------------------------------------+
| [OAS:maximum-assets]       | Returns the dollar amount of the maximum allowed assets  |
+----------------------------+----------------------------------------------------------+
| [OAS:personal-property     | Returns the amount of the personal property exemption    |
| -exemption]                | when calculating asset eligibility                       |
+----------------------------+----------------------------------------------------------+
| [OAS:maximum-income        | Returns the maximum income percentage allowed when       |
| -percent]                  | calculating income eligibility                           |
+----------------------------+----------------------------------------------------------+
| [OAS:income-standard]      | Returns the lower-cased name of the income standard to   |
|                            | apply                                                    |
+----------------------------+----------------------------------------------------------+
| [OAS:triage-id]            | Returns the triage id of the current user                |
+----------------------------+----------------------------------------------------------+

Views Integration
==================


The OAS intake settings entity integrates with Views.  Views can be used to generate reports.

+-----------------------+-------------------------+-------------------------------------+
| Property              | Views label             | Description                         |
+=======================+=========================+=====================================+
| intake_settings_id    | ID                      | Unique id of the intake setting     |
+-----------------------+-------------------------+-------------------------------------+
| name                  | name                    | Name of the intake settings         |
+-----------------------+-------------------------+-------------------------------------+
| created               | created                 | Date the intake settings were       |
|                       |                         | created                             |
+-----------------------+-------------------------+-------------------------------------+
| changed               | changed                 | Date settings were last updated     |
+-----------------------+-------------------------+-------------------------------------+
| uid                   | user                    | Author of the settings; ties back to|
|                       |                         | the users table                     |
+-----------------------+-------------------------+-------------------------------------+
| entity_id             | service                 | Location services node associated w/|
|                       |                         | the settings; ties to node table    |
+-----------------------+-------------------------+-------------------------------------+
| current_count         | Current count           | Current number of intakes since last|
|                       |                         | reset (based on reset frequency)    |
+-----------------------+-------------------------+-------------------------------------+
| enabled               | Intake open             | Yes or no;is intake currently open? |
+-----------------------+-------------------------+-------------------------------------+
| collect_marital_status| Collect marital status  | Yes or no; do we collect this info? |
+-----------------------+-------------------------+-------------------------------------+
| collect_immigration   | Collect immigrant status| Yes or no; do we collect this info? |
+-----------------------+-------------------------+-------------------------------------+
| collect_citizenship   | Collect citizenship     | Yes or no; do we collect citizenship|
|                       | status                  | status from users                   |
+-----------------------+-------------------------+-------------------------------------+
| collect_country       | Collect country of      | Yes or no; do we collect the user's |
|                       | origin                  | country of origin                   |
+-----------------------+-------------------------+-------------------------------------+
| collect_language      | Collect language spoken | Yes or no; do we collect the user's |
|                       | at home                 | primary language                    |
+-----------------------+-------------------------+-------------------------------------+
| collect_gender        | Collect gender          | Yes or no; do we collect this info? |
+-----------------------+-------------------------+-------------------------------------+
| collect_race          | Collect race            | Yes or no; do we collect this info? |
+-----------------------+-------------------------+-------------------------------------+
| collect_ethnicity     | Collect ethnicity       | Yes or no; do we collect this info? |
+-----------------------+-------------------------+-------------------------------------+
| collect_assets        | Collect assets          | Yes or no; do we collect asset info?|
+-----------------------+-------------------------+-------------------------------------+
| collect_income        | Collect income          | Yes or no; do we collect income?    |
+-----------------------+-------------------------+-------------------------------------+
| collect_expenses      | Collect expenses        | Yes or no; do we collect expenses?  |
+-----------------------+-------------------------+-------------------------------------+
| apply_income_limit    | Test for income         | Yes or no; do we apply an income    |
|                       | eligibility             | limit                               |
+-----------------------+-------------------------+-------------------------------------+
| apply_asset_limit     | Test for asset          | Yes or no; do we apply an asset     |
|                       | eligibility             | limit                               |
+-----------------------+-------------------------+-------------------------------------+
| collect_expenses_over | Collect expenses when   | Yes or no; do we collect expenses   |
| _income               | user is overincome      | only when user is overincome        |
+-----------------------+-------------------------+-------------------------------------+
| allow_prisoners       | Can prisoners apply     | Yes or no; whether people in prison |
|                       | online                  | or jail apply online                |
+-----------------------+-------------------------+-------------------------------------+
| maximum_allowed_income| Maximum allowed income  | Integer; percentage of income       |
|                       |                         | standard as maximum                 |
+-----------------------+-------------------------+-------------------------------------+
| personal_exemption    | Amount of personal prop-| Integer; dollar amount to exclude   |
| _amount               | erty to exempt          | from asset test                     |
+-----------------------+-------------------------+-------------------------------------+
| intake_limit          | Maximum number of       | Integer; if 0, intakes are unlimited|
|                       | intakes allowed         |                                     |
+-----------------------+-------------------------+-------------------------------------+
| maximum_callbacks_per | Maximum number of call- | Integer; should be deprecated       |
| _slot                 | backs to allow per slot |                                     |
+-----------------------+-------------------------+-------------------------------------+
| minimum_minor_age     | Minimum age for a minor | Integer                             |
+-----------------------+-------------------------+-------------------------------------+
| minimum_senior_age    | Minimum age to be con-  | Integer                             |
|                       | sidered a senior        |                                     |
+-----------------------+-------------------------+-------------------------------------+
| callback_number       | Callback number         | Text; telephone number              |
+-----------------------+-------------------------+-------------------------------------+
| callback_type         | Callback type           | Text: we call you, client calls     |
+-----------------------+-------------------------+-------------------------------------+
| reset_limit_frequency | How often do intake     | Number: 0, 1, 7, 30; 0 is never     |
|                       | limits get reset        | 1,7,30 days between resets          |
+-----------------------+-------------------------+-------------------------------------+
| cms_vendor            | CMS vendor              | Text; what CMS vendor do we send to |
+-----------------------+-------------------------+-------------------------------------+


ILAO-specific functionality
============================
We've added a lot of additional fields and functionality to the standard intake settings entity.  This is encapsulated in:
* the ilao_f_oas_intake_settings feature
* the ilao_intake_settings module

Intake settings fields
------------------------

+----------------------------+----------------------------------------------------------+
| Field                      | Description                                              |
+============================+==========================================================+
| field_service_single       | Entity reference to the related service; cardinality of 1|   
|                            | This is stored as the entity id attached to the intake   |
|                            | settings entity                                          | 
+----------------------------+----------------------------------------------------------+
| field_same_legal_issues    | Boolean; whether to inherit the legal issues from the    |
|                            | selected service                                         |
+----------------------------+----------------------------------------------------------+
| field_legal_issues         | Term reference (to legal issues taxonomy); used to limit |
|                            | what legal issues the intake settings apply              |
+----------------------------+----------------------------------------------------------+
| field_same_service_area_as | Boolean; whether to inherit the service area from the    |
| _locat                     | attached service entity                                  |
+----------------------------+----------------------------------------------------------+
| field_statewide            | Boolean; intake settings is statewide                    |
+----------------------------+----------------------------------------------------------+
| field_include_exclude_by   | List (Text); what geographic region type the settings are|
| _type                      | limited to (city, county, zip code)                      |
+----------------------------+----------------------------------------------------------+
| field_counties             | Entity reference to counties from the region taxonomy    |
|                            | Select list of unlimited cardinality                     |
+----------------------------+----------------------------------------------------------+
| field_cities               | Entity reference to cities from the region taxonomy      |
|                            | Select list of unlimited cardinality                     |
+----------------------------+----------------------------------------------------------+
| field_zipcodes             | Entity reference to zip codes from the region taxonomy   |
|                            | Select list of unlimited cardinality                     |
+----------------------------+----------------------------------------------------------+
| field_extended_service_area| Whether this service offers an extended service area     |
| _yn                        | Boolean                                                  |
+----------------------------+----------------------------------------------------------+
| field_extended_service_area| Entity reference to region taxonomy of additional states |
|                            | This is used exclusively for NIJC                        |
+----------------------------+----------------------------------------------------------+
| oas_income_categories      | Entity reference to finance categories of type income    |
|                            | that should be collected from the user.                  |
+----------------------------+----------------------------------------------------------+
| oas_income_standard        | Entity reference to income categories                    |
+----------------------------+----------------------------------------------------------+
| oas_income_exempt          | Term reference to intake populations that should have any|
|                            | ncome limits waived                                      |  
+----------------------------+----------------------------------------------------------+
| oas_asset_categories       | Entity references to finance categories of type assets   |
|                            | that should be collected from the user.                  |
+----------------------------+----------------------------------------------------------+
| oas_expense_categories     | Entity references to finance categories of type expense  |
|                            | that should be collected from the user.                  |
+----------------------------+----------------------------------------------------------+
| oas_msg_we_call_you        | Long text; message to display to users when the callback |
|                            | type is "we call you"                                    |
+----------------------------+----------------------------------------------------------+
| oas_msg_please_call        | Long text; message to display to users when the callback |
|                            | type is "client calls"                                   |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours_sunday  | Term reference to OAS callback hours; used to indicate   |
|                            | available hours for callbacks on Sundays                 |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours_monday  | Term reference to OAS callback hours; used to indicate   |
|                            | available hours for callbacks on Mondays                 |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours_tuesday | Term reference to OAS callback hours; used to indicate   |
|                            | available hours for callbacks on Tuesdays                |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours         | Term reference to OAS callback hours; used to indicate   |
| _wednesday                 | available hours for callbacks on Wednesdays              |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours         | Term reference to OAS callback hours; used to indicate   |
| _thursday                  | available hours for callbacks on Thursdays               |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours_friday  | Term reference to OAS callback hours; used to indicate   |
|                            | available hours for callbacks on Fridays                 |
+----------------------------+----------------------------------------------------------+
| oas_callback_hours_saturday| Term reference to OAS callback hours; used to indicate   |
|                            | available hours for callbacks on Saturdays               |
+----------------------------+----------------------------------------------------------+
| field_bypass_intake_message| Long text; message to display when intake is bypassed    |
+----------------------------+----------------------------------------------------------+
| oas_msg_disclaimer         | Long text; program disclaimer to display to user starting|
|                            | an online intake application                             |
+----------------------------+----------------------------------------------------------+
| oas_household_definition   | Long text; the program's definition of a household       |
+----------------------------+----------------------------------------------------------+
| oas_msg_current_client     | Long text; message to display to a user who is already a |
|                            | current client for the same problem                      |
+----------------------------+----------------------------------------------------------+
| oas_msg_already_applied    | Long text; message to display to a user who has already  |
|                            | applied for this same problem                            |
+----------------------------+----------------------------------------------------------+
| oas_help_citizenship_status| Long text; help text to display to users when collecting |
|                            | citizenship status                                       |
+----------------------------+----------------------------------------------------------+
| oas_help_country_of_origin | Long text; help text to display to users when collecting |
|                            | a user's country of origin                               |
+----------------------------+----------------------------------------------------------+
| oas_help_marital_status    | Long text; help text to display to users when collecting |
|                            | marital status                                           |
+----------------------------+----------------------------------------------------------+
| oas_help_gender            | Long text; help text to display to users when collecting |
|                            | user's gender                                            |
+----------------------------+----------------------------------------------------------+
| oas_help_immigration_status| Long text; help text to display to users when collecting |
|                            | their immigrant status                                   |
+----------------------------+----------------------------------------------------------+
| oas_help_language          | Long text; help text to display to users when collecting |
|                            | the user's primary language                              |
+----------------------------+----------------------------------------------------------+




