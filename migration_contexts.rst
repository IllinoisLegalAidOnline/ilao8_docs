=================
Contexts
=================

In Drupal 7, ILAO has used the Context module to control some layout and other functionality. We also have added a number of custom contexts in the ilao_context module.

Custom contexts
=================


ilao_contexts_zipcode
----------------------
Sets a context based on the user's zip code

ilao_contexts_legal_bundle_menu
---------------------------------
Seta a context based on whether a bundle menu should be displayed

ilao_contexts_paragraphs_type
------------------------------
Sets a context based on the paragraphs bundles in a specific node


ilao_contexts_oas_help_type
----------------------------
Sets a context based on the type of help a user has selected

ilao_contexts_advocate_type
-----------------------------
Sets a context based on the OG member roles a user has

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

* business hours, when the current time is between 9am and 5pm Mon-Fri
* outside of business hours, when the current time is between 5pm and 9am Mon - Fri
* weekend, when the current day is Saturday or Sunday

.. note::
   This context was created to control fundraising pop ups and should be evaluated to determine if it in fact needs to be migrated. 
