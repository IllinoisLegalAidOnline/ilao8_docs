==============================
OAS Referral History
==============================


This documentation covers the oas_referral_history module which provides an entity to store referrals provided to users.


Dependencies
=============
Officially, none.  Unofficially, this module expects the oas_triage_user and location_services content type to exist to work correctly.

Base Tables
==============

The oas_referral_history is the base table for the OASReferral entity.

+-----------------------+-------------------------------------+-------------------------------+
| Name                  | Description                         | Type                          |
+=======================+=====================================+===============================+
| referral_id           | Id for the referral entity; each    | serial, primary key, not null |
|                       | set of referrals made is 1 entity   |                               |
+-----------------------+-------------------------------------+-------------------------------+
| created               | Unix timestamp for when referrals   | int                           |
|                       | made                                |                               |
+-----------------------+-------------------------------------+-------------------------------+
| changed               | Unix timestamp for when referrals   | int                           |
|                       | last updated                        |                               |
+-----------------------+-------------------------------------+-------------------------------+
| data                  | Serialized array of extra info      | blob                          |
+-----------------------+-------------------------------------+-------------------------------+
| triage_id             | Reference to the triage_id of the   | int                           |
|                       | user receiving the referrals        |                               |
+-----------------------+-------------------------------------+-------------------------------+
| services_id           | Location services node ID of the    | int                           |
|                       | service the user referred to        |                               |
+-----------------------+-------------------------------------+-------------------------------+
| reject_reason_id      | ID for the reject reason (not used) | int                           |
+-----------------------+-------------------------------------+-------------------------------+
| reject_reason         | Text of the reject reason; used now | varchar; 255                  |
|                       | for intake diversions               |                               |
+-----------------------+-------------------------------------+-------------------------------+
| reject_date           | Unix timestamp for reject date      | int                           |
+-----------------------+-------------------------------------+-------------------------------+

                          
Functionality
===============

The module provides standard entity-related functions, such as the ability to create, update, delete, and load referral history entities.

The module also supports custom code that allows a user to view their referral history.


Views Integration
===================

The following properties have been exposed to Views:

* referral_id as ID
* triage_Id as Triage User; ties back to the related oas_triage_user entity.
* services_id as Referral; ties back to the related node
* created as Referral date; date of the referral.


  

