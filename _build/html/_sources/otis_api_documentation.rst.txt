===================================
Drupal 8 OTIS API Implementation
===================================

Triage User API
=====================
References to "triage user" refer to an instance of a triage user entity.  An individual may have multiple triage user entities associated with them if they apply more than once. 

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| create-triage-user     | POST     | Creates an initial triage user entity             |
+------------------------+----------+---------------------------------------------------+
| save-triage-user       | POST     | Saves a triage user entity to the database        |
+------------------------+----------+---------------------------------------------------+
| load-triage-user       | GET      | Loads a specific triage user entity by ID         |
+------------------------+----------+---------------------------------------------------+
| load-triage-users      | GET      | Loads multiple triage user entities by an array   |
|                        |          | of IDs                                            |
+------------------------+----------+---------------------------------------------------+
| get-triage-user-       | GET      | Gets the list of properties of the triage user    |
| properties             |          | entity                                            |
+------------------------+----------+---------------------------------------------------+
| get-created-date       | GET      | Gets the created date of a specific triage user   |
+------------------------+----------+---------------------------------------------------+
| set-created-date       | POST     | Sets the created date of a specific triage user   |
+------------------------+----------+---------------------------------------------------+
| get-changed-date       | GET      | Gets the changed date of a specific triage user   |
+------------------------+----------+---------------------------------------------------+
| set-changed-date       | POST     | Sets the changed date of a specific triage user   |
+------------------------+----------+---------------------------------------------------+
| get-intake-created-date| GET      | Gets the intake created date of a specific triage |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| set-intake-created-date| POST     | Sets the intake created date of a specific triage |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| get-intake-created-date| GET      | Gets the intake created date of a specific triage |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| get-user-id            | GET      | Gets the user id associated with a triage user    |
+------------------------+----------+---------------------------------------------------+
| set-user-id            | POST     | Sets the user id associated with a triage user    |
+------------------------+----------+---------------------------------------------------+
| get-household-size     | GET      | Gets the total household size for a triage user   |
+------------------------+----------+---------------------------------------------------+
| set-household-size     | POST     | Sets the total household size for a triage user   |
+------------------------+----------+---------------------------------------------------+
| get-household-adults   | GET      | Gets the number of adults in a household for a    |
|                        |          | triage user                                       |
+------------------------+----------+---------------------------------------------------+         
| set-household-adults   | POST     | Sets the number of adults in a household for a    |
|                        |          | triage user                                       |
+------------------------+----------+---------------------------------------------------+ 
| get-household-children | GET      | Gets the number of children in a household for a  |
|                        |          | triage user                                       |
+------------------------+----------+---------------------------------------------------+     
| set-household-children | POST     | Sets the number of children in a household for a  |
|                        |          | triage user                                       |
+------------------------+----------+---------------------------------------------------+     
| get-total-income       | GET      | Gets the total income of a triage user            |
+------------------------+----------+---------------------------------------------------+ 
| set-total-income       | POST     | Sets the total income of a triage user            |
+------------------------+----------+---------------------------------------------------+
| get-total-expenses     | GET      | Gets the total exepnses of a triage user          |
+------------------------+----------+---------------------------------------------------+ 
| set-total-expenses     | POST     | Sets the total expenses of a triage user          |
+------------------------+----------+---------------------------------------------------+
| get-total-assets       | GET      | Gets the total assets of a triage user            |
+------------------------+----------+---------------------------------------------------+ 
| set-total-assets       | POST     | Sets the total assets of a triage user            |
+------------------------+----------+---------------------------------------------------+
| get-zip-code           | GET      | Gets the stored zip code of a triage user         |
+------------------------+----------+---------------------------------------------------+ 
| set-zip-code           | POST     | Sets the zip code of a triage user                |
+------------------------+----------+---------------------------------------------------+
| get-triage-status      | GET      | Gets the current triage status of the triage user |
+------------------------+----------+---------------------------------------------------+
| set-triage-status      | POST     | Sets the current triage status of the triage user |
+------------------------+----------+---------------------------------------------------+
| get-intake-status      | GET      | Gets the current intake status of the triage user |
+------------------------+----------+---------------------------------------------------+
| set-intake-status      | POST     | Sets the current intake status of the triage user |
+------------------------+----------+---------------------------------------------------+
| get-intake-id          | SET      | Gets the intake settings ID associated with       |
|                        |          | a triage user.  See also intake settings API      |
+------------------------+----------+---------------------------------------------------+
| set-intake-id          | GET      | Sets the intake settings ID associated with       |
|                        |          | a triage user.  See also intake settings API      |
+------------------------+----------+---------------------------------------------------+
| get-referral-source    | GET      | Gets the referral source for a triage user        |
+------------------------+----------+---------------------------------------------------+
| set-referral-source    | SET      | Sets the referral source for a triage user        |
+------------------------+----------+---------------------------------------------------+
| get-lsc-code           | GET      | Gets the LSC code associated with the triage user |
+------------------------+----------+---------------------------------------------------+
| get-lsc-subcode        | GET      | Gets the LSC subcode associated with the triage   |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| set-lsc-code           | SET      | Sets the LSC code associated with the triage user |
+------------------------+----------+---------------------------------------------------+
| set-lsc-subcode        | SET      | Sets the LSC subcode associated with the triage   |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| get-triage-county      | GET      | Gets the county associated with the triage user   |
+------------------------+----------+---------------------------------------------------+
| set-triage-county      | SET      | Sets the county associated with the triage user   |
+------------------------+----------+---------------------------------------------------+
| get-triage-state       | GET      | Gets the state associated with the triage user    |
+------------------------+----------+---------------------------------------------------+
| set-triage-state       | SET      | Sets the state associated with the triage user    |
+------------------------+----------+---------------------------------------------------+

Triage Listing API
---------------------

* get-intake-statuses
* get-triage-statuses
* get-last-screens

Financial entity API
========================

Referral History API
======================
The referral API will provide referral history information between systems.

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-recent-history     | GET      | Returns referral ids of referral instances for    |
|                        |          | a user in last 30 days;                           |
+------------------------+----------+---------------------------------------------------+
| get-referrals          | GET      | Loads a set of referrals based on a referral id   |
+------------------------+----------+---------------------------------------------------+
| get-referral           | GET      | Loads a specific referral                         |
+------------------------+----------+---------------------------------------------------+
| get-referral-service   | GET      | Loads a specific referral history service         |
+------------------------+----------+---------------------------------------------------+
| get-all-history        | GET      | Returns the entire referral history for a given   |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| get-referral-type      | GET      | Returns whether the referral was a cold referral  |
|                        |          | or an OTIS application                            |
+------------------------+----------+---------------------------------------------------+
| get-referral-status    | GET      | Checks the status of an OTIS application based on |
|                        |          | a predefined closed date                          |
+------------------------+----------+---------------------------------------------------+
| create-referral-history| POST     | Creates a referral history entity                 |
+------------------------+----------+---------------------------------------------------+
| update-referral-history| POST     | Updates a referral history entity                 |
+------------------------+----------+---------------------------------------------------+

Organization API
==================

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-organization-name- | GET      | Loads the name of the parent organization         |
| service-id             |          | by service id.                                    |
+------------------------+----------+---------------------------------------------------+
| get-organization-id-   | GET      | Loads the node id of the parent organization      |
| service-id             |          | by service id.                                    |
+------------------------+----------+---------------------------------------------------+

Location API
==============

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| detect-zipcode         | GET      | Invokes 3rd party detection to determine user zip |
+------------------------+----------+---------------------------------------------------+
| get-zipcode-from-user  | GET      | Loads the zip code for a specific Drupal user ID  |
+------------------------+----------+---------------------------------------------------+
| get-region-from-zip    | GET      | Loads region data for a specific zip code         |
+------------------------+----------+---------------------------------------------------+
| get-city-from-zip      | GET      | Loads city for a specific zip code from taxonomy  |
+------------------------+----------+---------------------------------------------------+
| get-county-from-zip    | GET      | Loads county for a specific zip code from taxonomy|
+------------------------+----------+---------------------------------------------------+
| get-state-from-zip     | GET      | Loads state for a specific zip code from taxonomy |
+------------------------+----------+---------------------------------------------------+
| get-county-fips        | GET      | Loads the county FIPS for a specific county       |
+------------------------+----------+---------------------------------------------------+

Legal Issues API
=================

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-node-legal-issue   | GET      | Returns legal issues based on a node ID           |
+------------------------+----------+---------------------------------------------------+


Intake available API
======================

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| is-intake-available    | GET      | Determines if online intake is available          |
+------------------------+----------+---------------------------------------------------+










