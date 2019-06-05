===================================
ILAO OAS Financial Category
===================================


This documentation covers the ilao_oas_financial_category module which provides a framework for types of financial information that may be collected via online intake.

Dependencies
===============
This module requires:

* entity
* entityreference

Base Tables
===============

ilao_oas_financial_category_type
---------------------------------

Stores the type of financial category
  
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

ilao_oas_financial_category
-----------------------------

Stores the category of financial information within a category type. 
  
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
====================
As part of the intall process, the following are created:

* income, asset, and expense category types
* categories within the income category type
* categories within the asset category type
* categories within the expense category type

These default items are based off of original configuration of OTIS financial data.


