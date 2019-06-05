==================================
ILAO OAS Income Standard
==================================

This documentation covers the ilao_oas_income_standard module which provides a framework for storing income standards to be used on a website.

Administration
===============
Income standards are managed through admin/structure/ilao_oas_income_standards.  Each income standard consists of:

* a name
* a dollar amount for a household of size 1 through 8 members
* a dollar amount per household member above 8 people

Base Table
============

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

