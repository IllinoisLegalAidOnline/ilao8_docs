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
| get-intake-id          | POST     | Gets the intake settings ID associated with       |
|                        |          | a triage user.  See also intake settings API      |
+------------------------+----------+---------------------------------------------------+
| set-intake-id          | GET      | Sets the intake settings ID associated with       |
|                        |          | a triage user.  See also intake settings API      |
+------------------------+----------+---------------------------------------------------+
| get-referral-source    | GET      | Gets the referral source for a triage user        |
+------------------------+----------+---------------------------------------------------+
| set-referral-source    | POST     | Sets the referral source for a triage user        |
+------------------------+----------+---------------------------------------------------+
| get-lsc-code           | GET      | Gets the LSC code associated with the triage user |
+------------------------+----------+---------------------------------------------------+
| get-lsc-subcode        | GET      | Gets the LSC subcode associated with the triage   |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| set-lsc-code           | POST     | Sets the LSC code associated with the triage user |
+------------------------+----------+---------------------------------------------------+
| set-lsc-subcode        | POST     | Sets the LSC subcode associated with the triage   |
|                        |          | user                                              |
+------------------------+----------+---------------------------------------------------+
| get-triage-county      | GET      | Gets the county associated with the triage user   |
+------------------------+----------+---------------------------------------------------+
| set-triage-county      | POST     | Sets the county associated with the triage user   |
+------------------------+----------+---------------------------------------------------+
| get-triage-state       | GET      | Gets the state associated with the triage user    |
+------------------------+----------+---------------------------------------------------+
| set-triage-state       | POST     | Sets the state associated with the triage user    |
+------------------------+----------+---------------------------------------------------+
| get-last-screen-viewed | GET      | Gets the last screen viewed by the triage user    |
+------------------------+----------+---------------------------------------------------+
| set-last-screen-viewed | POST     | Sets the last screen viewed by the triage user    |
+------------------------+----------+---------------------------------------------------+
| get-triage-user-ip     | GET      | Gets the IP address of the triage user            |
+------------------------+----------+---------------------------------------------------+
| set-triage-user-ip     | POST     | Sets the IP address of the triage user            |
+------------------------+----------+---------------------------------------------------+
| get-intake-notes       | GET      | Gets the intake notes for the triage user         |
+------------------------+----------+---------------------------------------------------+
| set-intake-notes       | POST     | Sets the intake notes for the triage user         |
+------------------------+----------+---------------------------------------------------+
| get-triage-gender      | GET      | Gets the gender for the triage user               |
+------------------------+----------+---------------------------------------------------+
| set-triage-gender      | POST     | Sets the gender for the triage user               |
+------------------------+----------+---------------------------------------------------+
| get-triage-race        | GET      | Gets the race for the triage user                 |
+------------------------+----------+---------------------------------------------------+
| set-triage-race        | POST     | Sets the race for the triage user                 |
+------------------------+----------+---------------------------------------------------+
| get-triage-ethnicity   | GET      | Gets the ethnicity for the triage user            |
+------------------------+----------+---------------------------------------------------+
| set-triage-ethnicity   | POST     | Sets the ethnicity for the triage user            |
+------------------------+----------+---------------------------------------------------+
| get-triage-marital     | GET      | Gets the marital status for the triage user       |
| -status                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-triage-marital     | POST     | Sets the marital status for the triage user       |
| -status                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-triage-citizenship | GET      | Gets the citizenship for the triage user          |
+------------------------+----------+---------------------------------------------------+
| set-triage-citizenship | POST     | Sets the citizenship for the triage user          |
+------------------------+----------+---------------------------------------------------+
| get-triage-immigrant   | GET      | Gets the immigrant status for the triage user     |
| -status                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-triage-immigrant   | GET      | Gets the immigrant status for the triage user     |
| -status                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-triage-user-age    | GET      | Gets the triage user's age                        |
+------------------------+----------+---------------------------------------------------+
| set-triage-user-age    | POST     | Sets the triage user's age                        |
+------------------------+----------+---------------------------------------------------+
| get-triage-language    | GET      | Gets the triage user's primary language           |
+------------------------+----------+---------------------------------------------------+
| set-triage-language    | POST     | Sets the triage user's primary language           |
+------------------------+----------+---------------------------------------------------+
| get-triage-country     | GET      | Gets the triage user's country of origin          |
+------------------------+----------+---------------------------------------------------+
| set-triage-country     | POST     | Sets the triage user's country of origin          |
+------------------------+----------+---------------------------------------------------+
| get-financial-status   | GET      | Gets the triage user's income status (over-income,|
|                        |          | over asset, etc)                                  |
+------------------------+----------+---------------------------------------------------+
| set-financial-status   | POST     | Sets the triage user's income status (over-income,|
|                        |          | over asset, etc)                                  |
+------------------------+----------+---------------------------------------------------+
| get-transfer-status    | GET      | Gets the etransfer status of a triage user entity |
+------------------------+----------+---------------------------------------------------+
| set-transfer-status    | POST     | Sets the etransfer status of a triage user entity |
+------------------------+----------+---------------------------------------------------+
| get-transfer-failure   | GET      | Gets the transfer failure reason of an application|
| -reason                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-transfer-failure   | POST     | Sets the transfer failure reason of an application|
| -reason                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-etransfer-data     | GET      | Gets the serialized data of an application        |
+------------------------+----------+---------------------------------------------------+
| set-etransfer-data     | POST     | Sets the serialized data of an application        |
+------------------------+----------+---------------------------------------------------+
| get-triage-populations | GET      | Gets any populations the user has identified as   |
+------------------------+----------+---------------------------------------------------+
| set-triage-populations | POST     | Sets any populations the user has identified as   |
+------------------------+----------+---------------------------------------------------+
| get-triage-populations | GET      | Gets any populations the user has identified as   |
+------------------------+----------+---------------------------------------------------+
| get-triage-problem     | GET      | Gets the text of the user's entered legal problem |
+------------------------+----------+---------------------------------------------------+
| set-triage-problem     | POST     | Sets the text of the user's entered legal problem |
+------------------------+----------+---------------------------------------------------+
| get-triage-problem-tree| GET      | Gets the legal issue tree of the user's entered   |
|                        |          | legal problem                                     |
+------------------------+----------+---------------------------------------------------+
| set-triage-problem-tree| SET      | Sets the legal issue tree of the user's entered   |
|                        |          | legal problem                                     |
+------------------------+----------+---------------------------------------------------+



Triage Listing API
---------------------
Each of the triage listing API methods listed below will return the list of options from the OTIS taxonomy system and return them in JSON format.  

* get-intake-statuses
* get-triage-statuses
* get-last-screens
* get-gender-list
* get-race-list
* get-ethnicity-list
* get-marital-status-list
* get-citizenship-list
* get-immigrant-status-list
* get-income-status

Financial entities API
========================
The financial entities include:

* income standards
* income, asset, and expense categories

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-income-standards   | GET      | Gets the list of income standard entities         |
+------------------------+----------+---------------------------------------------------+
| get-income-standard    | GET      | Gets an entire specified income standard          |
+------------------------+----------+---------------------------------------------------+
| get-income-standard    | GET      | Get the income standard amount for a specified    |
| -household             |          | household size                                    |
+------------------------+----------+---------------------------------------------------+
| get-income-standard    | GET      | Get the income standard amount to add for each    |   
| -additional-member     |          | family member over 8                              |                       
+------------------------+----------+---------------------------------------------------+
| get-income             | GET      | Returns the list of subcategories under income    |
| -subcategories         |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-income-items       | GET      | Returns the list of income items in a subcategory |
+------------------------+----------+---------------------------------------------------+
| get-expense            | GET      | Returns the list of subcategories under expense   |
| -subcategories         |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-expense-items      | GET      | Returns the list of expense items in a subcategory|
+------------------------+----------+---------------------------------------------------+
| get-asset              | GET      | Returns the list of subcategories under asset     |
| -subcategories         |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-asset -items       | GET      | Returns the list of asset items in a subcategory  |
+------------------------+----------+---------------------------------------------------+




Notifications & Reminders API
==============================

Contact API
--------------
The manages notifications and reminders settings.  By design, this should work across entities (triage users, Drupal users, for example) by requiring parameters for:

* entity type
* entity id

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-sms-opt-in-status  | GET      | Gets the opt in status.                           |
+------------------------+----------+---------------------------------------------------+
| set-sms-opt-in-status  | POST     | Sets the opt in status.                           |
+------------------------+----------+---------------------------------------------------+
| get-mobile-phone       | GET      | Gets the phone associated with the entity         |
+------------------------+----------+---------------------------------------------------+
| set-mobile-phone       | POST     | Gets the phone associated with the entity         |
+------------------------+----------+---------------------------------------------------+

Reminder API
----------------
The reminder API sends, logs, and provides report data:

* Confirmation messages upon completing an online application
* Appointment reminders

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| build-confirmation-msg | POST     | Builds the confirmation message                   |
+------------------------+----------+---------------------------------------------------+
| build-app-reminder     | POST     | Builds an appointment reminder                    |
+------------------------+----------+---------------------------------------------------+
| send-SMS-message       | POST     | Sends an SMS message of confirmation or           |
|                        |          | reminder type                                     |
+------------------------+----------+---------------------------------------------------+
| send-mail-message      | POST     | Sends an email message of confimation or          |
|                        |          | reminder type                                     |
+------------------------+----------+---------------------------------------------------+
| save-SMS-message       | POST     | Saves an sms message record                       |
+------------------------+----------+---------------------------------------------------+
| save-mail-message      | POST     | Saves a record of sent mail                       |
+------------------------+----------+---------------------------------------------------+
| get-messages           | GET      | Gets messages; allows for parameters for date,    |
|                        |          | type, format                                      |
+------------------------+----------+---------------------------------------------------+







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
| get-legal-issue-text   | GET      | Accepts text and translates it to one or more     |
|                        |          | legal issues                                      |
+------------------------+----------+---------------------------------------------------+
| get-legal-issues-tree  | GET      | Loads the legal issues tree for a specific term   |
+------------------------+----------+---------------------------------------------------+
| get-legal-issue-parents| GET      | Returns the parent terms of a specific term       |
+------------------------+----------+---------------------------------------------------+
| get-legal-issue        | GET      | Returns the child terms of a specific term        |
| -children              |          |                                                   |
+------------------------+----------+---------------------------------------------------+


Online Intake API
======================

Intake settings
-----------------

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-intake-settings    | GET      | Gets the intake settings entity based on ID       |
+------------------------+----------+---------------------------------------------------+
| save-intake-settings   | POST     | Saves an intake settings entity                   |
+------------------------+----------+---------------------------------------------------+
| get-is-created         | GET      | Gets the created date for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| get-is-changed         | GET      | Gets the last updated date for an intake settings |
+------------------------+----------+---------------------------------------------------+
| set-is-created         | POST     | Sets the created date for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| set-is-changed         | POST     | Sets the last updated date for an intake settings |
+------------------------+----------+---------------------------------------------------+
| get-is-author          | GET      | Gets the author user id of an intake settings     |
+------------------------+----------+---------------------------------------------------+
| set-is-author          | POST     | Sets the author user id of an intake settings     |
+------------------------+----------+---------------------------------------------------+
| get-is-current-count   | GET      | Gets the current count for an intake settings     |
+------------------------+----------+---------------------------------------------------+
| increment-is-current-  | POST     | Increments the current count of an intake setting |
| -count                 |          | by one                                            |
+------------------------+----------+---------------------------------------------------+
| reset-is-current-count | POST     | Resets intake current count to zero               |
+------------------------+----------+---------------------------------------------------+
| get-is-status          | GET      | Gets the current status (open/closed) for an      |
|                        |          | intake settings                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-status          | POST     | Sets the current status for an intake settings    |
+------------------------+----------+---------------------------------------------------+
| get-collect-marital-   | GET      | Gets whether we collect marital status            |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-collect-marital-   | POST     | Updates whether we collect marital status         |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-collect-immigration| GET      | Gets whether we collect immigration               |
+------------------------+----------+---------------------------------------------------+
| set-collect-immigration| POST     | Sets whether we collect immigration               |
+------------------------+----------+---------------------------------------------------+
| get-collect-citizenship| GET      | Gets whether we collect citizenship               |
+------------------------+----------+---------------------------------------------------+
| set-collect-citizenship| POST     | Sets whether we collect citizenship               |
+------------------------+----------+---------------------------------------------------+
| get-collect-country    | GET      | Gets whether we collect country of origin         |
+------------------------+----------+---------------------------------------------------+
| set-collect-country    | POST     | Sets whether we collect country of origin         |
+------------------------+----------+---------------------------------------------------+
| get-collect-language   | GET      | Gets whether we collect language spoken at home   |
+------------------------+----------+---------------------------------------------------+
| set-collect-language   | POST     | Sets whether we collect language spoken at home   |
+------------------------+----------+---------------------------------------------------+
| get-collect-race       | GET      | Gets whether we collect race                      |
+------------------------+----------+---------------------------------------------------+
| set-collect-race       | POST     | Sets whether we collect race                      |
+------------------------+----------+---------------------------------------------------+
| get-collect-ethnicity  | GET      | Gets whether we collect ethnicity                 |
+------------------------+----------+---------------------------------------------------+
| set-collect-ethnicity  | POST     | Sets whether we collect ethnicity                 |
+------------------------+----------+---------------------------------------------------+
| get-collect-income     | GET      | Gets whether we collect income information        |
+------------------------+----------+---------------------------------------------------+
| set-collect-income     | POST     | Sets whether we collect income information        |
+------------------------+----------+---------------------------------------------------+
| get-is-income-types    | GET      | Gets types of income we collect                   |
+------------------------+----------+---------------------------------------------------+
| set-is-income-types    | POST     | Sets types of income we collect                   |
+------------------------+----------+---------------------------------------------------+
| get-is-asset-types     | GET      | Gets types of assets we collect                   |
+------------------------+----------+---------------------------------------------------+
| set-is-asset-types     | POST     | Sets types of assets we collect                   |
+------------------------+----------+---------------------------------------------------+
| get-is-expense-types   | GET      | Gets types of expenses we collect                 |
+------------------------+----------+---------------------------------------------------+
| set-is-expense-types   | POST     | Sets types of expenses we collect                 |
+------------------------+----------+---------------------------------------------------+
| get-is-apply-income-   | GET      | Gets whether we apply an income limit             |
| limit                  |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-apply-income-   | POST     | Sets whether we apply an income limit             |
| limit                  |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-is-apply-asset-    | GET      | Gets whether we apply an asset limit              |
| limit                  |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-apply-asset-    | POST     | Sets whether we apply an asset limit              |
| limit                  |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-is-max-income-     | GET      | Gets maximum income percentage                    |
| allowed                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-max-income-     | POST     | Sets maximum income percentage                    |
| allowed                |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-is-income-standard | GET      | Gets income standard to apply                     |
+------------------------+----------+---------------------------------------------------+
| set-is-income-standard | POST     | Sets income standard to apply                     |
+------------------------+----------+---------------------------------------------------+
| get-is-max-allowed-    | GET      | Gets the maximum assets allowed                   |
| assets                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-max-allowed-    | POST     | Sets the maximum assets allowed                   |
| assets                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-is-personal-       | GET      | Gets the amount of any personal exemption         |
| exemption              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-personal-       | POST     | Sets the amount of any personal exemption         |
| exemption              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-intake-limit       | GET      | Gets the intake limit                             |
+------------------------+----------+---------------------------------------------------+
| set-intake-limit       | POST     | Sets the intake limit                             |
+------------------------+----------+---------------------------------------------------+
| get-intake-reset-      | GET      | Gets the intake reset frequency                   |
| frequency              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-intake-reset-      | POST     | Sets the intake reset frequency                   |
| frequency              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-minimum-age        | GET      | Gets the minimum age to apply                     |
+------------------------+----------+---------------------------------------------------+
| set-minimum-age        | POST     | Gets the minimum age to apply                     |
+------------------------+----------+---------------------------------------------------+
| get-senior-age         | GET      | Gets the minimum age to be considered a senior    |
+------------------------+----------+---------------------------------------------------+
| set-senior-age         | POST     | Sets the minimum age to be considered a senior    |
+------------------------+----------+---------------------------------------------------+
| get-callback-number    | GET      | Get intake callback number                        |
+------------------------+----------+---------------------------------------------------+
| set-callback-number    | POST     | Set intake callback number                        |
+------------------------+----------+---------------------------------------------------+
| get-callback-type      | GET      | Get default callback type                         |
+------------------------+----------+---------------------------------------------------+
| set-callback-type      | POST     | Set default callback type                         |
+------------------------+----------+---------------------------------------------------+
| get-is-household-      | GET      | Gets the household definition for the settings    |
| definition             |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-household-      | POST     | Sets the household definition for the settings    |
| definition             |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-already     | GET      | Gets the message for when a user has already      |
| applied                |          | applied                                           |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-already     | POST     | Sets the message for when a user has already      |
| applied                |          | applied                                           |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-current     | GET      | Gets the message for when a user is already a     |
| client                 |          | client with this problem                          |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-current     | POST     | Sets the message for when a user has already      |
| client                 |          | applied                                           |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-we-call-you | GET      | Gets message for when user is told program calls  |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-we-call-you | POST     | Sets message for when user is told program calls  |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-please-call | GET      | Gets message for when user is told to call        |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-please-call | POST     | Sets message for when user is told to call        |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-bypass      | GET      | Gets message for when user is to bypass intake    |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-bypass      | POST     | Sets message for when user is to bypass intake    |
+------------------------+----------+---------------------------------------------------+
| get-is-msg-disclaimer  | GET      | Gets program disclaimer message                   |
+------------------------+----------+---------------------------------------------------+
| set-is-msg-disclaimer  | POST     | Sets program discmailer message                   |
+------------------------+----------+---------------------------------------------------+
| get-help-marital-status| GET      | Gets the help text for asking for marital status  |
+------------------------+----------+---------------------------------------------------+
| set-help-marital-status| POST     | Sets the help text for asking for marital status  |
+------------------------+----------+---------------------------------------------------+
| get-help-immigration-  | GET      | Gets the help text for asking immigration status  |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-help-immigration-  | POST     | Sets the help text for asking immigration status  |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-help-citizenship-  | GET      | Gets the help text for asking citizenship status  |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-help-citizenship-  | POST     | Sets the help text for asking citizenship status  |
| status                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-help-language      | GET      | Gets the help text for asking language            |
+------------------------+----------+---------------------------------------------------+
| set-help-language      | POST     | Sets the help text for asking language            |
+------------------------+----------+---------------------------------------------------+
| get-help-race          | GET      | Gets the help text for asking race                |
+------------------------+----------+---------------------------------------------------+
| set-help-race          | POST     | Sets the help text for asking race                |
+------------------------+----------+---------------------------------------------------+
| get-help-gender        | GET      | Gets the help text for asking gender              |
+------------------------+----------+---------------------------------------------------+
| set-help-gender        | POST     | Sets the help text for asking gender              |
+------------------------+----------+---------------------------------------------------+
| get-help-ethnicity     | GET      | Gets the help text for asking ethnicity           |
+------------------------+----------+---------------------------------------------------+
| set-help-ethnicity     | POST     | Sets the help text for asking ethnicity           |
+------------------------+----------+---------------------------------------------------+
| get-waived-populations | GET      | Gets populations for whom income is waived        |
+------------------------+----------+---------------------------------------------------+
| set-waived-populations | POST     | Sets populations for whom income is waived        |
+------------------------+----------+---------------------------------------------------+
| get-is-legal-issues    | GET      | Gets the legal issues for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| set-is-legal-issues    | POST     | Sets the legal issues for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| get-is-service-area    | GET      | Gets the service area for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| set-is-service-area    | POST     | Sets the service area for an intake settings      |
+------------------------+----------+---------------------------------------------------+
| get-is-callback-hours- | GET      | Gets the callback hours for a specific day        |
| by-day                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| set-is-callback-hours- | POST     | Sets the callback hours for a specific day        |
| by-day                 |          |                                                   |
+------------------------+----------+---------------------------------------------------+




Intake Application Integration
-------------------------------

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-is-intake-available| GET      | Determines if online intake is available          |
+------------------------+----------+---------------------------------------------------+
| get-user-callback-type | GET      | Loads the callback type for a specific intake     |
+------------------------+----------+---------------------------------------------------+
| set-user-callback-type | POST     | Sets the callback type for a specific intake      |
+------------------------+----------+---------------------------------------------------+
| get-client-first-name  | GET      | Gets the client's first name                      |
+------------------------+----------+---------------------------------------------------+
| set-client-first-name  | POST     | Sets the client's first name                      |
+------------------------+----------+---------------------------------------------------+
| get-client-middle-name | GET      | Gets the client's middle name                     |
+------------------------+----------+---------------------------------------------------+
| set-client-middle-name | POST     | Sets the client's middle name                     |
+------------------------+----------+---------------------------------------------------+
| get-client-last-name   | GET      | Gets the client's last name                       |
+------------------------+----------+---------------------------------------------------+
| set-client-last-name   | POST     | Sets the client's last name                       |
+------------------------+----------+---------------------------------------------------+
| get-client-maiden-name | GET      | Gets the client's maiden name                     |
+------------------------+----------+---------------------------------------------------+
| set-client-maiden-name | POST     | Sets the client's maiden name                     |
+------------------------+----------+---------------------------------------------------+
| get-client-nickname    | GET      | Gets the client's nickname                        |
+------------------------+----------+---------------------------------------------------+
| set-client-nickname    | POST     | Sets the client's nickname                        |
+------------------------+----------+---------------------------------------------------+
| get-client-dob         | GET      | Gets the client's date of birth                   |
+------------------------+----------+---------------------------------------------------+
| set-client-dob         | POST     | Sets the client's date of birth                   |
+------------------------+----------+---------------------------------------------------+
| calculate-client-age   | POST     | Returns an integer based on a date of birth       |
+------------------------+----------+---------------------------------------------------+
| calculate-minor-age    | POST     | Returns a boolean for user is too young to apply  |
|                        |          | online based on program rules                     |               
+------------------------+----------+---------------------------------------------------+
| calculate-senior-age   | POST     | Returns a boolean indicator of whether the user is|
|                        |          | or is not a senior based on program rules         |
+------------------------+----------+---------------------------------------------------+
| get-is-current-client  | GET      | Gets whether the user is a current client of      |
|                        |          | partner org for the specific problem              |
+------------------------+----------+---------------------------------------------------+
| set-is-current-client  | POST     | Sets boolean based on whether user is a current   |
|                        |          | client of partner org for the specific problem    |
+------------------------+----------+---------------------------------------------------+ 
| get-is-current-client  | GET      | Gets whether the user is a current client of      |
| -different             |          | partner org for a different problem               |
+------------------------+----------+---------------------------------------------------+
| set-is-current-client  | POST     | Sets boolean based on whether user is a current   |
| -different             |          | client of partner org for a different problem     |
+------------------------+----------+---------------------------------------------------+ 
| get-is-new-client      | GET      | Gets whether the user has never been a client of  |
| -different             |          | partner org                                       |
+------------------------+----------+---------------------------------------------------+
| set-is-current-client  | POST     | Sets boolean based on whether user has never      |
| -different             |          | been a client of partner org                      |
+------------------------+----------+---------------------------------------------------+ 
| get-client-prisoner    | GET      | Gets whether the user has indicated that they are |
|                        |          | in jail or prison                                 |
+------------------------+----------+---------------------------------------------------+ 
| set-client-prisoner    | POST     | Sets whether the user has indicated that they are |
|                        |          | in jail or prison                                 |
+------------------------+----------+---------------------------------------------------+ 
| get-veteran-status     | GET      | Gets the user's veteran status                    |
+------------------------+----------+---------------------------------------------------+
| set-veteran-status     | POST     | Sets the user's veteran status                    |
+------------------------+----------+---------------------------------------------------+
| get-homeless-status    | GET      | Gets the user's homeless status                   |
+------------------------+----------+---------------------------------------------------+
| set-homeless-status    | POST     | Sets the user's homeless status                   |
+------------------------+----------+---------------------------------------------------+
| get-client-phone       | GET      | Gets the client phone number                      |
+------------------------+----------+---------------------------------------------------+ 
| get-client-phone-type  | GET      | Gets the client phone type                        |
+------------------------+----------+---------------------------------------------------+ 
| get-client-email       | GET      | Gets the client email address                     |
+------------------------+----------+---------------------------------------------------+ 
| get-client-street-1    | GET      | Get the clients street address, line 1            |
+------------------------+----------+---------------------------------------------------+ 
| get-client-street-2    | GET      | Get the clients street address, line 2            |
+------------------------+----------+---------------------------------------------------+ 
| get-client-city        | GET      | Get client's entered city                         |
+------------------------+----------+---------------------------------------------------+
| get-client-state       | GET      | Get client's entered state                        |
+------------------------+----------+---------------------------------------------------+
| get-client-zipcode     | GET      | Gets client's entered zip code                    |
+------------------------+----------+---------------------------------------------------+
| set-client-phone       | POST     | Sets the client phone number                      |
+------------------------+----------+---------------------------------------------------+ 
| set-client-phone-type  | POST     | Sets the client phone type                        |
+------------------------+----------+---------------------------------------------------+ 
| set-client-email       | POST     | Sets the client email address                     |
+------------------------+----------+---------------------------------------------------+ 
| set-client-street-1    | POST     | Set the clients street address, line 1            |
+------------------------+----------+---------------------------------------------------+ 
| set-client-street-2    | POST     | Set the clients street address, line 2            |
+------------------------+----------+---------------------------------------------------+ 
| set-client-city        | POST     | Set client's entered city                         |
+------------------------+----------+---------------------------------------------------+
| set-client-state       | POST     | Set client's entered state                        |
+------------------------+----------+---------------------------------------------------+
| set-client-zipcode     | POST     | Sets client's entered zip code                    |
+------------------------+----------+---------------------------------------------------+
| calculate-total-income | POST     | Given collected income, returns total income      |
+------------------------+----------+---------------------------------------------------+
| calculate-total-assets | POST     | Given collected assets, returns total assets      |
+------------------------+----------+---------------------------------------------------+
| calculate-countable    | POST     | Given asset information, calculates countable     |
| -assets                |          | assets after excluding any exemptions             |
+------------------------+----------+---------------------------------------------------+
| calculate-countable    | POST     | Given income information, calculates countable    |
| -income                |          | income after deducting expenses                   |
+------------------------+----------+---------------------------------------------------+
| calculate-total        | POST     | Given collected expenses, returns total expenses  |
| -expenses              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| load-callback-times    | GET      | Loads available callback times for a day or days  |
+------------------------+----------+---------------------------------------------------+





.. note:: 
   get-is-intake-available is an extensive API call that will require specific data to make an evaluation including the user's zip code, legal issue(s), and any population they may be a member of.  


Legal Server eTransfer APIs
==============================

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| generate-ls-xml-data   | POST     | Generates XML data from a triage user entity      |
+------------------------+----------+---------------------------------------------------+
| get-ls-organization    | POST     | Given an intake settings, return the correct Legal|
|                        |          | Server organization name                          |
+------------------------+----------+---------------------------------------------------+
| get-ls-problem-code    | POST     | Given a triage user, get the Legal Server problem |
|                        |          | code from mappings                                |
+------------------------+----------+---------------------------------------------------+
| get-ls-external-id     | POST     | Given a triage user, generate a unique ID for     |
|                        |          | Legal Server                                      |
+------------------------+----------+---------------------------------------------------+
| send-to-legal-server   | POST     | Sends an eTransfer to Legal Server                |
+------------------------+----------+---------------------------------------------------+
| get-legal-server       | GET      | Gets the Legal Server endpoint for eTransfer      |
| -endpoint              |          |                                                   |
+------------------------+----------+---------------------------------------------------+
| get-transfer-status    | GET      | Loads the triage user transfer status             |
+------------------------+----------+---------------------------------------------------+
| set-transfer-status    | POST     | Updates the triage user transfer status           |
+------------------------+----------+---------------------------------------------------+





