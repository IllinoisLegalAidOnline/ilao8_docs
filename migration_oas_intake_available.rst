===================================
Intake Availability Functions
===================================


Most of the code to determine if intake is available is found in the oas_triage_user.intake_available.inc file in the OAS Triage User module.

oas_triage_user_is_intake_available
=======================================

Located in: oas_triage_user.intake_available.inc
Parameters
--------------
Requires: Triage user entity for the specific user
Returns:
* Null if user is overincome and not in a specific population
* Null if user is overincome and in a specific population but income is not waived
* A query results set of intake setting ids

Depends on
-------------

* ilao_geolocation module to get the user's region information from a zip code
* oas_triage_user_get_child_problem to get the user's legal issue
* oas_triage_user_set_up_intake_object


Process
-----------

.. note::
   Intake has not reached its limit if it is has a limit of 0 (unlimited) or if the current count is less than the maximum set.  Scheduled tasks clear the current count as deteremined by the reset frequency. 

If the user indicated that they are over-income on the initial Get Legal Help form:

* Checks to see if the user has indicated that tehy are a member of a special population
* If the user is not a member of a special population, intake is not available
* Runs a database query to check:

  * For an intake settings that matches the user's zip code, city, county, or state OR for intake settings that are statewide.  This data is stored in 4 different tables.
  * For intake settings that are unlimited in capacity OR that have not yet reached capacity
  * Is income exempt for the specific population OR does not apply an income limit at all
  * The legal issue is in the intake settings
  * The intake status is open

If the user indicated that they are not over-income on the initial Get Legal Help form:

* First checks to see what intake setting are available based on:

  * matches the user's zip code, city, county, or state OR for intake settings that are statewide.  This data is stored in 4 different tables.
  * For intake settings that are unlimited in capacity OR that have not yet reached capacity
  * Is income exempt for the specific population OR does not apply an income limit at all
  * The legal issue is in the intake settings
  * The intake status is open
  
If there is exactly one intake settings:

* Checks to see if the user meets any population requirements via oas_triage_user_intake_specific_population
* Checks to see if the it is a general service


oas_triage_user_intake_specific_population
============================================
Located in: oas_triage_user.intake_available.inc

Filters a list of intake settings to a set that matches the user's specific population.  This function fires only when the user has selected a special population.

Parameters
----------
Requires: 

* array of populations the user belongs to
* an array of initial applicable intake settings

Returns: a query result set or null.

Process
---------

* Loads the triage user entity from the session variables
* Loads the user's problem
* Checks to see if there are available triage rules using oas_triage_user_get_triage_rules
* If there are no triage rules, then there can be no intake available
* If there are matching triage rules, it runs a query to return an ordered set of intake settings that:

  * match the user's population
  * are in the set of intake settings passed into the function
  * are ordered by maximum allowed income descending, service volume, current count
    
    
oas_triage_user_intake_general
================================

Located in: oas_triage_user.intake_available.inc

Filters a list of potential intake settings matches to return a maximum of one result that has triage rules and meets the best available criteria.

Parameters
------------
Parameters: an array of initial applicable intake settings
Returns: a query result set or null.

Process
------------

* Loads the triage user entity from the session variables
* Loads the user's problem
* Checks to see if there are available triage rules using oas_triage_user_get_triage_rules
* If there are no triage rules, then there can be no intake available
* If there are matching triage rules, it runs a query to return an ordered set of intake settings that:

  * are in the set of intake settings passed into the function
  * are ordered by maximum allowed income descending, service volume, current count  

* Passes the resulting query to oas_triage_user_least_updated_intake_organization to return exactly one result.  
  
.. note::
   Intake settings can be applied to multiple legal issues.  Triage rules can as well.  In order for a user to be guided to online intake, there must be a legal issues match ON BOTH.  
   

   
oas_triage_user_least_updated_intake_organization
===================================================

Located in: oas_triage_user.intake_available.inc
Invoked by: oas_triage_user_intake_general

Parameters
------------

Requires:
* Query result set of intake settings id
* Original set of intake settings id

Returns the intake settings id that:
* If there is only 1 filtered results, returns that
* If there are 2 or more results, returns the best match that:
  
  * the user has not already been triaged through and diverted
  * is free
  * if multiple free services exist, the one that has gone the longest without an intake
  * if no free service is available, then the paid service 
  * if multiple paid services exist, the one that has gone the longest without an intake

Relies on _oas_triage_user_return_organization to return a matching organization.

oas_triage_user_get_triage_rules
=================================
Located in: oas_triage_user.intake_available.inc
Determines if there are triage rules that align with the intake settings on service and legal issue.

Parameters
-------------
Requires:

* $intake_options => array of intake settings ID
* $problem => legal issue

Returns a query set of triage rules

Process
--------

* the legal issue matches the passed in $problem
* the triage rules node is tied to a service that matches the service(s) that match any of the intake settings id passed in

oas_triage_user_set_up_intake_object
======================================

Located in: oas_triage_user.intake_available.inc

Sets the $_SESSION['oas_intake']['intake_settings_id'] session variable to the selected intake settings id.

Parameters
------------
Requires: integer; intake_settings_id
Returns; null


    