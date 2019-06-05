==========================
OTIS-related entities
==========================

Online triage and intake system (OTIS) entities are:

* oas_intake_settings
* ilao_oas_financial_category
* ilao_oas_income_standard
* oas_triage_user
* oas_referral_history

(oas was the precurser to OTIS and stood for online access system)


OAS Intake Settings Entity
===========================

This is the documentation for the oas_intake_settings module. This module provides a framework for data related to online intake.

Dependencies
--------------
This module requires:

* entity
* entity_reference
* ilao_oas_financial_category
* oas_triage_user

Base Tables
-------------

* oas_intake_settings_type stores the intake settings types.  This was created mostly because it was in the model code Gwen used.  It contains only 1 record for the actual oas_intake_settings entity type.
  
  * id (not null; serial; primary key)
  * type (machine readable name; varchar, not null)
  * label (human readable name; varchar; not null)
  * weight (int, not null)
  * data (serialized array)
  
* oas_intake_settings
  
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
-----------
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
-----------
The oas_intake_settings module creates the oas_callback_hours taxonomy.


ILAO OAS Financial Category
=============================

This documentation covers the ilao_oas_financial_category module which provides a framework for types of financial information that may be collected via online intake.

Dependencies
-------------
This module requires:

* entity
* entityreference

Base Tables
---------------

* ilao_oas_financial_category_type: Stores the type of financial category
  
  +--------------------+--------------------------------------+-------------------------------+
  | Name                | Description                         | Type                          |
  +=====================+=====================================+===============================+
  | id                  | id of the category type             | Serial; primary key; not null |
  +---------------------+-------------------------------------+-------------------------------+
  | type                | machine name of the category type   | varchar; 255                  |
  +---------------------+-------------------------------------+-------------------------------+
  | label               | human-readable name of the type     | varchar; 255                  |
  +---------------------+-------------------------------------+-------------------------------+
  | weight              | weight of the type                  | int                           |
  +---------------------+-------------------------------------+-------------------------------+
  | data                | serialized array of data            | text                          |
  +---------------------+-------------------------------------+-------------------------------+
  
* ilao_oas_financial_category: Stores the category of financial information within a category type. 
  
  +--------------------+--------------------------------------+-------------------------------+
  | Name                | Description                         | Type                          |
  +=====================+=====================================+===============================+
  | ilao_oas_financial  | id of the category                  | Serial; primary key; not null |
  | _category_id        |                                     |                               |
  +---------------------+-------------------------------------+-------------------------------+
  | type                | financial category type of category | varchar; 255                  |
  +---------------------+-------------------------------------+-------------------------------+
  | language            | language of the category            | varchar; 32                   |
  +---------------------+-------------------------------------+-------------------------------+
  | name                | name of the category                | varchar; 255                  |
  +---------------------+-------------------------------------+-------------------------------+
  | created             | Unix timestamp when entity created  | int                           |
  +---------------------+-------------------------------------+-------------------------------+
  | changed             | Unix timestamp of last update       | int                           |
  +---------------------+-------------------------------------+-------------------------------+
  | weight              | weight of the type                  | int                           |
  +---------------------+-------------------------------------+-------------------------------+
  | data                | serialized array of data            | blob                          |
  +---------------------+-------------------------------------+-------------------------------+
  | help_text           | help text to show user              | text                          |
  +---------------------+-------------------------------------+-------------------------------+
  | subcategory         | grouping for related categories     | varchar; 128                  |
  +---------------------+-------------------------------------+-------------------------------+
  
Default categories
-------------------
As part of the intall process, the following are created:

* income, asset, and expense category types
* categories within the income category type
* categories within the asset category type
* categories within the expense category type

These default items are based off of original configuration of OTIS financial data.


ILAO OAS Income Standard
=========================

This documentation covers the ilao_oas_income_standard module which provides a framework for storing income standards to be used on a website.

Administration
---------------
Income standards are managed through admin/structure/ilao_oas_income_standards.  Each income standard consists of:

* a name
* a dollar amount for a household of size 1 through 8 members
* a dollar amount per household member above 8 people

Base Table
------------

The base table is ilao_oas_income_standard and consists of:

+-----------------------+-------------------------------------+-------------------------------+
| Name                  | Description                         | Type                          |
+=======================+=====================================+===============================+
| id                    | Id for the income standard entity   | serial, primary key, not null |
+-----------------------+-------------------------------------+-------------------------------+
| type                  | Not used                            | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| language              | Language of the entity              | varchar; 32                   |
+-----------------------+-------------------------------------+-------------------------------+
| name                  | Name of the income standard         | varchar; 255                  |
+-----------------------+-------------------------------------+-------------------------------+
| created               | Unix timestamp of when the income   | int                           |
|                       | standard was created                |                               |
+-----------------------+-------------------------------------+-------------------------------+
| changed               | Unix timestamp of when the income   | int                           |
|                       | standard was last changed           |                               |
+-----------------------+-------------------------------------+-------------------------------+
| data                  | Serialized area of additional data  | blob                          |
+-----------------------+-------------------------------------+-------------------------------+
| amount_1              | Income standard for household of 1  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_2              | Income standard for household of 2  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_3              | Income standard for household of 3  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_4              | Income standard for household of 4  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_5              | Income standard for household of 5  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_6              | Income standard for household of 6  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_7              | Income standard for household of 7  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| amount_8              | Income standard for household of 8  | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| additional_family     | Amount for each household member    | int                           |
| _members              | for household larger than 8 members |                               |
+-----------------------+-------------------------------------+-------------------------------+      


OAS Triage User
=================

This documentation covers the oas_triage_user module which provides an entity to store information about a specific OTIS triage and intake instance.

Dependencies
-------------
None

Base Tables
---------------

oas_triage_user_type
^^^^^^^^^^^^^^^^^^^^^^
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
^^^^^^^^^^^^^^^^^

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
--------
The install hook(s) add a number of fields and field instances upon installation:

+----------------------------+----------------------------------------------------------+
| Field                      | Description                                              |
+============================+==========================================================+
| oas_referrals              | Installed in install hook; deleted in update hook        |
+----------------------------+----------------------------------------------------------+
| oas_triage_help_type       | Type of help the user is seeking (list_text, unlimited)  |
+----------------------------+----------------------------------------------------------+
| field_triage_problem       | User problem (term reference; uses legal issues taxonomy;|
|                            | cardinality is 1                                         |
+----------------------------+----------------------------------------------------------+
| field_limited_populations  | Populations the user belongs to (term reference; uses    |
|                            | intake populations taxonomy                              |
+----------------------------+----------------------------------------------------------+
| field_triage_search        | Text field of user's problem (text, cardinality of 1     |
+----------------------------+----------------------------------------------------------+
| field_triage_problem       | Term reference for user problem (term reference; uses    |
|                            | legal issues taxonomy; cardinality unlimited             |
+----------------------------+----------------------------------------------------------+
| field_triage_referrals     | Exists in install script but deleted in intake settings  |
| _given                     | update hook                                              |
+----------------------------+----------------------------------------------------------+
| field_triage_callback_times| Stores user callback times; text field; unlimited        |
+----------------------------+----------------------------------------------------------+
| field_opt_in_sms           | Field to get opt in consent for SMS; boolean             |
+----------------------------+----------------------------------------------------------+
| field_mobile_phone         | Text field for mobile phone number                       |
+----------------------------+----------------------------------------------------------+

 




Taxonomies
------------
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




  










  


