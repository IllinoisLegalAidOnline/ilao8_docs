=================
Contexts
=================

In Drupal 7, ILAO has used the Context module to control some layout and other functionality. We also have added a number of custom contexts in the ilao_context module.

Custom contexts
=================


ilao_contexts_zipcode
----------------------
Sets a context based on the user's zip code

Returns on of:

* "US" if the zip code is a US zip code but not Illinois
* "Illinois" if the zip code is in Illinois
* "Not in US" if the zip code is not a US zip code

Relies on the ilao_geolocation module.

Executes on node view

ilao_contexts_legal_bundle_menu
---------------------------------
Sets a context based on whether a bundle menu should be displayed

Returns one of:

* Bundle overview, when the node being viewed is a Guide
* Learn more, when the node being viewed is in a single Guide as a Learn more article
* Take action, when the node being viewed is in a single Guide as a take action article
* Multiple (Appears in multiple legal bundles), when the node being viewed is in more than one Guide
* None, when the node being viewed is not associated with a Guide

Executes on node view

ilao_contexts_paragraphs_type
------------------------------
Sets a context based on the paragraphs bundles in a specific node

Returns one of:

* Automated documents
* Decision tree
* Video
* Static form
* Link
* File
* Article
* IICLE
* Process
* Legal bundle

based on the paragraphs included in the node and is applied only to legal content. If a node has multiple paragraph bundles, it is set based on the following hierarchy:

* Autodocs 
* Legal bundle if not an autodocs
* Process step if not an autodoc or bundle
* Video if not a process step or autodoc
* All others only if nothing else has been set



.. note::
   This could probably be replaced with a check for primary content format but may break if the taxonomy is changed.
   
.. warning::
   This is behind.  Is missing some content formats.   

ilao_contexts_oas_help_type
----------------------------
Sets a context based on the type of help a user (information, forms, or lawyer) has selected. It is designed to handle all permutations of options.

Returns one of:

* Information only (user only checked help finding information)
* Forms only (user only checked court forms)
* Information and forms (user checked all but lawyer)
* Lawyer, information and form (user checked all 3 options)
* Lawyer, forms (user checked lawyer, court forms but not information)
* Lawyer, content (user checked lawyer, information but not court forms)
* Lawyer (user checked lawyer only)

Fires on page reaction when the user is on one of the following:

* get-legal-help/referrals
* get-legal-help/callback-confirm
* get-legal-help/please-call
 
.. note::
   Should this context be available for get-legal-help/bypass?


ilao_contexts_advocate_type
-----------------------------
Sets a context based on the OG member roles a user has.

Returns one of:

* 'non member'
* 'staff'
* 'organization manager'
* 'OAS manager'

The logic works as follows: for a specific user ID, it loads the organization the uer is a member of and then the roles.  By default, the user is set to staff.  If they are an OAS manager, the status is set to OAS manager (regardless of any other roles); If they are an organization manager (but not an OAS manager), the context returns organization manager.

For ILAO staff and interns, the context returns non-member since we do not need this context.


Executes on page reaction when the page path is one of:

* node/edit
* node/add/location-services
* node/add/location
* user/

ilao_context_oas_modal
------------------------
Seta a context based on whether we should show the OAS modal


ilao_contexts_check_empty_variable
------------------------------------
Set this context to check if variable exists and is not empty.

ilao_contexts_check_region_specific_markup
---------------------------------------------
Set this context to check if node contains region specific Markup

ilao_contexts_business_hours
------------------------------
Set this context to when current time in business hours.

Returns one of:

* Weekday business hours, when the current time is between 9am and 5pm Mon-Fri
* Outside business hours, when the current time is between 5pm and 9am Mon - Fri
* Weekend hours, when the current day is Saturday or Sunday

.. note::
   This context was created to control fundraising pop ups and should be evaluated to determine if it in fact needs to be migrated. 
   
Executes on page reaction (all pages)    
