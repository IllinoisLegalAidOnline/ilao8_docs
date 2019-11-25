============================
Reporting Migration
============================

.. note::
   There are views that are used to create blocks and pages within the system.  This page covers the views that we use for reporting.
   
Legal information reports
===========================

Find content
--------------
Find content is the basic content report, with some modifications that is part of the Administrative views module (which we should deprecate in Drupal 8)

Fields include:

* NID
* Title
* Content type
* Primary content type
* Author
* Published
* Last updated

Filters include:

* Title
* Content type
* Published (any, yes, no)
* Vocabulary
* Has taxonomy terms (with depth)
* Image (has image/no image)
* Primary content type


Find legal content
--------------------
Find legal content is specialized version of the content report designed to show legal content only.  Excluded from this report is any other legal content like portal main pages, toolboxes, tool steps, tools, which make it less than ideal as a full view of our legal content.

Fields include:

* Node ID
* Title
* Primary content type
* Primary legal category
* Created date
* Author
* Last updated
* Last reviewed
* Published

Filters include:

* Node ID
* Title (contains)
* Description (contains)
* Body (contains)
* Primary legal category
* Published (defaults to Yes)
* Content type (multiple select)
* Translation exists (English, Spanish, Polish)
* Advanced filters

  * Content level
  * Legal position
  * Restrict to legal aid and/or pro bono
  * Jurisdiction
  * Annual updates
  * Translation outdated
  * Created date (between)
  * Last reviewed date (between)


Find file content
------------------

Localized content
-------------------

Requested forms
----------------

Images for legal content
-------------------------

Toolbox tool usage report
--------------------------

Toolbox tool step usage report
--------------------------------

Learn more articles by guide
-----------------------------

Take action articles by guide
-------------------------------


Comments with Ratings
----------------------

Content ratings
------------------

OTIS/Get Legal Help reports
============================
The OTIS/Get Legal Help reports are custom reports we created to keep track of online intake information.

Get Legal Help Report
-----------------------
This is the main report for tracking usage of the Get Legal Help feature.

Found at https://www.illinoislegalaid.org/admin/intake/reporting/get-legal-help-summary

Fields include:

* Triage ID
* Created
* Zip code
* Over-income (yes or no)
* Household size
* Legal problem
* Help type sought
* Triage status

Filters include:

* Help type (lawyer, forms, information)
* Start date
* End date
* Legal issues

Exportable as a CSV

Should include:
* filter for zip code
* column for county
* filter for zip code

Referral History
-------------------
Found at admin/reporting/get-legal-help/referrals

Fields include:

* Referral ID
* Title of the service the user was referred to
* County of the user
* Over-income status
* Referral date
* Problem history

Includes filter for:

* Referral date (between)
* County
* Legal issue

Should include:

* Organization
* A way to export the data
* Explanation of over income statuses
* Triage User ID


May need to review:

* Whether the problem field is correct or not

Referral Count Report
-----------------------
Includes:

* Number of referrals made to a service
* Title of the service

Has filters for:

* Referral date (between)
* County
* Legal issue

Should include:

* Organization name
* A way to export the data

eTransfers report
-------------------
The eTransfers report shows all instances of Get Legal Help where the user got past the basic Get Legal Help pages and into the OTIS funnel.  

Has fields for:

* Triage ID
* Intake organization name
* Location
* Service
* Date of intake
* Intake status
* Zip code
* County
* Gender
* Race
* Ethnicity
* Marital status
* Legal problem

Has filters for:

* Start and end dates
* Organization name
* Service
* Legal issue
* Intake status
* Source (to account for ILAO's modal, program widget, etc).

Should have:
* Filter for zip code
* Filter for county

Organization Report
^^^^^^^^^^^^^^^^^^^^^
There are also organization specific intake reports that mirror the etransfer report at admin/organizations/reporting/intake-report that can also be exported


SMS OAS Survey report
----------------------
We have one SMS-based survey created that ties into Webform to follow up with users who complete an online intake application.  This view displays the data associated with that survey along with OTIS information.

Fields include:

* triage user ID
* intake date
* survey submission date
* zip code
* legal issue
* service
* location
* organization
* survey responses

Filters include:

* survey date (beginning/ending range)
* organization name
* callback type
* legal issue



User reports
=============

The people reports are based off of the administrative views module, which should probably not be used in Drupal 8.

All of these reports are exportable as CSV.

People
--------
The people report should include:

* Last name
* First name
* Email
* Roles
* Active (as yes/no)
* Create date
* Last access date
* Member type
* Participates in user tests (yes/no)
* Operations to edit or cancel account

Filters should include:

* First name (contains)
* Last name (contains)
* Email (contains)
* Has roles (any, yes/no)
* Roles (multi-select)
* Active
* Member type
* Participate in user test (all, yes, no)
* Joined between dates

Never validated accounts
--------------------------
This report shows all users who registered on the website but then did not activate their account.  These users are automatically deleted after [x] days.

It is a mirror of the people report but limited to users who:

* have a last access date of less than Jan 1, 2015
* have an empty internal organization value

User demographics report
--------------------------
Similar to the people table, this report lets us export user demographic data and includes fields for:

* email
* first name
* last name
* role(s)
* member type
* year born
* gender
* zip code
* language preferences
* last login
* date joined

Filters:

* roles
* date joined between
* gender
* language preference
* zip code (with options for filter type)
* year born (with options for filter type)

Needs:
* Participate in user test (all, yes, no) filter

Board, staff, YPB users
------------------------
We use this report to filter users with an "internal organization" role so that we can control who shows up on the board, staff, and YPB pages in the About Us section.

The report should include:

* User name
* Last name
* First name
* Company/Organization 
* Biography
* Internal organization
* Internal title
* Roles
* Edit link

The report should be filtered on:

* Active users
* Has one or more internal roles (this should be exposed)

Login Report
----------------
This report shows the number of times a user has logged into the website.

The report should include:

* user ID
* email
* first name
* last name
* roles
* member type
* first log in
* last log in
* total number of logins
* frequency of logins

Additional reports
===================

SMS Reports
-------------
These are all of a status of "TBD"

* List of campaigns
* Campaign keywords
* Campaign summary report
* Campaign interactions report
* Legal content sharing report
   

