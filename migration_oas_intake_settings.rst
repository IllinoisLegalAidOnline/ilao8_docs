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

Functionality
---------------


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