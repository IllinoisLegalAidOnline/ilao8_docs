===================================
Get Legal Help Form to Next Step
===================================

Functions
============

oas_triage_user_route_to_initial_results
-----------------------------------------
This is the initial function called when the user submits the Get Legal Help form.


.. warning::  

   The code in this function needs refactored.
   
Located in: oas_triage_user.


Parameters
^^^^^^^^^^^^

* form
* form_state (results of the user's Get legal help form)
* triage_user entity

Invokes
^^^^^^^^^

* oas_triage_user_get_legal_issues
* oas_triage_user_get_top_parents
* oas_triage_user_get_legal_issue

Process
^^^^^^^^

* Unsets any existing triage id (acts as a reset)
* Determines based on the user's search term:

  * We have an exact term match
  
    * Updates the user's problem in the system
    * Redirects the user to the right resources using the oas_triage_user_determine_resources function.
    
  * We have more than one matching term
  
    * Sets the triage status to Legal issue
    * Directs the user to the triage-questions page
  * We have no matching terms
  
    * Sets the triage status to top of triage tree
    * Sets the start terms to the top level terms
    * Redirects the user to triage-start

* Redirects the user to the legal-information/not-illinois page if they are out of the service area (see the oas_triage_user_in_service_area function)

oas_triage_user_get_legal_issues
---------------------------------

oas_triage_user_get_top_parents
----------------------------------
Returns an array of legal isssues in the legal issues taxonomy that do not have a parent term.

Array is structured as the term id => translated name

oas_triage_user_get_legal_issue
-----------------------------------
Determines the user's legal issue from a search term.  

Located in: oas_triage_user.evaluate_triage.inc

Parameters
^^^^^^^^^^^
Parameter:  String of a search term
Returns either:

* 0 if no legal issue can be determined
* the term id for the matching term if exactly 1 is found
* the array of matching terms if more than 1 match is found

Relies on
^^^^^^^^^^^
* taxonomy
* i18n 
* legal_issues_autosuggest view

Process
^^^^^^^^^^

* Checks first to see if the search term is an exact match for a legal issue taxonomy term.  
* Checks to see if there is a localized match to the search term
* If no result, uses the legal_issue_autosuggest to look for an exact match

  * If the search term is a single keyword, rewrites it to include plural formats
  * If the search term is not single keyword, uses the combined phrase
  * Then it loops through the results and:
    
     * if it is the lowest level term, adds the term object into an array
     * if that array is then empty (meaning none of the results were low-level terms)
      
       * adds any term that has a child and a parent (this avoids adding the top level terms
       * loops through the resulting array to remove child terms if the parent term is included
       
  * if there is just one result, the term id is returned
  * if there is more than one result, the array is returned.  The array includes the term id as the key and the term name as the value.      
    
oas_triage_user_in_service_area
---------------------------------- 
Located in: oas_triage_user.evaluate_triage.inc

Determines if the user is in our service area

Parameters
^^^^^^^^^^^^
Accepts:  triage_user entity
Returns: Boolean

Process
^^^^^^^^^^
* Users in Illinois are always in the service area
* Users outside of Illinois are out of the service area unless:

  * User is looking for help in immigration (see oas_triage_user_is_immigration)
  * User is looking for a lawyer
  * User is in NIJC's extended service area (see oas_triage_user_check_nijc)

oas_triage_user_is_immigration
--------------------------------
Located in: oas_triage_user.evaluate_triage.inc

Determines if the user's issue is immigration-related.

Parameters
^^^^^^^^^^^
Parameters: integer representing the term id of the user's problem
Returns: Boolean  

oas_triage_user_check_nijc
-----------------------------
Located in: oas_triage_user.evaluate_triage.inc

Determines if a user is in NIJC's extended service area as NIJC allows intakes through our platfor outside of Illinois.


Parameters
^^^^^^^^^^^^^^
Parameters: integer representing the term ID of the user's state
Returns:  Boolean

.. warning:: 
   NIJC's organization node ID is hard coded into this function.
   
   
   
oas_triage_user_determine_resources
---------------------------------------
Located in: oas_triage_user.evaluate_triage.inc

Updated the form_state to set an appropriate redirect to the next page.

Parameters
^^^^^^^^^^^^^^^
Accepts:

* triage user entity
* form_state array

Returns: form_state
 
Process
^^^^^^^^^^

* If no help type exists, sets the help type to lawyer.
* If the help types include a lawyer:

  * Determines if intake is available (see oas_triage_user_is_intake_available)
  * If intake is possible:
  
    * Checks to see if there are program triage rules
    * If there are program triage rules:
    
      * Sets the triage status to Program triage
      * Sets the redirect to the triage rules node
    * If there are no triage rules:
    
      * Sets the triage status to Referrals
      * Redirects to referrals page
      
 * If intake is not possible:
 
   * Sets the triage status to Referrals
   * Redirects to referrals page
   
* If the user is not looking for a lawyer:
  
  * Sets the triage status to referrals
  * Redirects to the referrals page   
          

.. warning::
   There is a reference to referrals when the user overincome value is 10; this is never invoked.

oas_triage_user_get_search_terms
----------------------------------
Located in: oas_triage_user.evaluate_triage.inc
Parameters: An array of terms
Returns: An array of term reference options for use in a form, formatted as tid => name


Forms
==========

Get Legal Help main form
---------------------------
Function: oas_triage_user_edit_form
Found in: oas_triage_user.ui.inc


On menu access, creates a triage user entity.  The default form:

* Loads the user if the user is logged in
* Loads the user's zip code if it is defined in their account or in a session variable
* Adds a heading markup element to describe Get Legal Help
* Adds a zip code text field
* Adds a household size field
* Adds an overincome field (yes or no that asks the user if their income is more than a maximum amount
* Adds an ajax callback that takes the household size and calculates the maximum income amount. 
* Attaches any additional fields created in the user interface.  In ILAO's instance that includes
  
  * What type of help do you want? Check all that apply. (oas_triage_help_type)
  * What is your problem about? (field_triage_search, text field)
  * I would like to get confirmation, reminders, and additional information via text message (field_opt_in_sms); this field is currently set to no access
  * My problem is about: (field_triage_problem; term reference); set to no access
  * Do any of the following describe you? Check all that apply. (field_limited_populations; term reference)
  * Mobile phone (field_mobile_phone; text); set to no access
  * Problem history (field_triage_problem_history, term reference); set to no access
  * Callback times selected (field_triage_callback_times; text)

Calculating Maximum Income
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The oas_triage_user_get_maximum_income function in the oas_triage_user.ui.inc file controls the maximum intake value that appears on the main Get Legal Help form. 

It defaults to $10,000 unless ILAO's custom ilao_oas_income_standard module is installed (this is installed on ILAO's website).  With that module installed, the function:

* Loads the federal poverty level income standard
* Grabs the amount that matches the user's household size; this amount is annual income
* Calculates the monthly maximum by multiplying the annual income by 350%, dividing by 12 and adding $500. 
* Calculates the amount to display by taking the maximum amount and dividing it by 1000, dropping any fractions and then adding $1000.
* Applies a number format to the amount

.. note::
   If the annual income is $12500 per year, the system will take that amount multiply it by 3.5 and divide by 12 ($3645.83) and then adding $500 ($4145.83).  It will then divide that by 1000 (4.14583) and drop any fraction (4) and then multipling by 1000 for an amount of $4000
  

Known Alters
^^^^^^^^^^^^^^
The Get legal help form can be altered by any other module.  Our ILAO-specific intake settings module does this.  

Function: ilao_intake_settings_form_oas_triage_user_edit_form_alter
Location: ilao_intake_settings.module
  
Alterations:

* Sets the callback times text field to no access
* Adds a fieldset for legal
* Adds a checkbox field for a disclaimer
* Adds a checkbox field for terms and conditions
* Adds translation support for help type options   

Validation
^^^^^^^^^^^^^
Function: oas_triage_user_edit_form_validate
Located in: oas_triage_user.ui.inc

Validates that if the help type includes lawyer that the household size and income fields are both required.

Form submit
^^^^^^^^^^^^
Function: oas_triage_user_edit_form_submit
Located in: oas_triage_user.ui.inc

Process:

* Stores the household size in a session variable
* Updates the tirage user entity to:

  * Sets the created time to the current time for a new entity 
  * Set the changed time to the current time
  * Store the user ID
  * Store the IP address
  * Set the last screen viewed to "get-legal-help"
  
* If the ilao_geolocation module is enabled (it currently is), the submit form also updates the triage entity to:

  * Set the county to the county associated with the submitted zip code
  * Set the state to the state associated with the submitted zip code 
  
* Invokes the oas_triage_user_route_to_initial_results function to launch the next step  
  


Triage form
-------------
Function: oas_triage_user_ilao_triage_form
Found in: oas_triage_user.evaluate_triage.inc

If necessary, will set the session variable triage_id based on url path and then loads the triage entity.

Form consists of up to 4 radio elements that represent the maximum depth of the legal issues taxonomy.  For example, when the taxonomy tree structure looks like this:

* Level 1

  * Level 2
  
    * Level 3
    * Level 3
      
      * Level 4
      * Level 4
      * Level 4
    * Level 2
  
    * Level 3
    * Level 3
      
      * Level 4
      * Level 4
      * Level 4    
* Level 1
* Level 1

If the user's search matches on Level 1, all the Level 2s will appear and then upon selecting a Level 2, all the Level 3s will display under that Level 2 and then upon selecting a Level 3, all the Level 4s will display.  

If the user starts at a lower level term or there are no child terms, the submit form displays.

Form Submit
^^^^^^^^^^^^
Function: oas_triage_user_ilao_triage_form_submit
Located in: oas_triage_user.evaluate_triage.inc

Upon submitting the form:

* The user's legal problem history is updated in the field_triage_problem_history record.  This field maintains the entire hierarchy of their selections.
* Updates the triage user entity
* Invokes the oas_triage_user_determine_resources function to determine how to route the user

oas_triage_user_legal_issue_build_tree
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Found in: oas_triage_user.evaluate_triage.inc
Parameter: integer; taxonomy term id from legal issues
Returns an array of select options that are at the level immediately below the hierarchy level as the term parameter

Triage start form
--------------------
Function: oas_triage_user_ilao_triage_start_form
Found in: oas_triage_user.evaluate_triage.inc

If necessary, will set the session variable triage_id based on url path and then loads the triage entity.

This is a dynamic form that is used on the get-legal-help/triage-start page.
It consists of a single checkbox field that displays either:

* The top categories from our legal issues taxonomy (from oas_triage_user_get_top_parents)
* The list of terms from based on the user's search (using oas_triage_user_get_search_terms)  

Form submit
^^^^^^^^^^^^^
Function: oas_triage_user_ilao_triage_start_submit
Located in: oas_triage_user.evaluate_triage.inc
If the user has selected a lowest level legal issue:

* update the user's problem in their triage entity
* use the oas_triage_user_determine_resources function to proceed.

If the user has not selected a lowest level legal issue:

* update the user's problem in their triage entity
* Redirects to the /triage-questions form




