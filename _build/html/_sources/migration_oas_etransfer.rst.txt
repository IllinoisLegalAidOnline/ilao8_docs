==============================
OTIS eTransfer Processing
==============================

OTIS currently only supports eTransferring to the statewide instance of Legal Server. 

.. note::
   As of June 15, 2019, ILAO uses a `POST/XML-based eTransfer method <https://iloi.legalserver.org/modules/matter/intake_xml.php>`_.  Legal Server has also implemented a REST-based API that we have not yet migrated over to.

Building the client array
===========================
The function oas_triage_user_etransfer builds an array of data needed for the eTransfer and sets default values as needed. This data array includes:

* first name mapped to firstName
* middle name mapped to middleName
* last name mapped to lastName
* nickname mapped to aliasFirst
* maiden name mapped to aliasLast
* street address line 1 mapped to address1
* street address line 2 mapped to address2
* city mapped to city
* state is hard coded to 'IL'
* zip as zip
* county from oas_triage_user_get_county (returns FIPS county)
* phone number as phoneHome (current eTransfer does not support different phone types)
* date of birth as dateOfBirth
* email as email
* martial status 
* race 
* ethnicity
* gender
* language
* veteran; true or false based on user's selected populations
* disabled; true or false based on user's selected populations
* organization name as eTransferOrganization.  See oas_triage_user_get_legal_server_org
* legal issue as LSC problem code.  See oas_triage_user_get_problemcode()
* notes.  See oas_triage_user_notes()
* number of adults in household mapped as numberOfAdults
* number of children in household mapped as numberofChildren
* citizenship status mapped as citizenshipStatus
* callback type (We call client or client calls) as callbackType
* callback time slot(s) mapped as callbackDayTime.  See oas_triage_user_set_callback_times
* collected assets (see oas_triage_user_process_assets)
* intake settings id as intake_settings_id
* an external id as externalId.  This is the string ILAOWeb- with the triage_id appended.


.. note::
   Demographic data (marital status, race, ethnicity, gender, language) all require a mapping on our end to acceptable Legal Server data.  See the oas_triage_user_get_demographic_mapping function.

.. todo::
   * There may be a bug in getting/setting the disabled and veteran values.
   * Hard coding of state is bad practice; is problem for out-of-state NIJC users.
   * Get demographic mapping does not account for potential duplication across taxonomies
   
oas_triage_user_get_demographic_mapping
----------------------------------------
Located in oas_triage_user.exits.inc
Parameters
^^^^^^^^^^^^^

* Requires a term name
* Returns either:

  * the value from field_legal_server_mapping that associated with the term name
  * null, if no match is found


oas_triage_user_get_population
--------------------------------
Located in oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^

* Requires a term ID that reflects a population
* Returns a Boolean (true if the user matches on the population; false otherwise)

oas_triage_user_get_county
---------------------------
Located in oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^

* Requires a zip code
* Returns the county FIPS value associated with the zip code taxonomy term and stored in field_countyfips

oas_triage_user_get_legal_server_org
-------------------------------------

Located in oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^^

* Requires the intake settings entity associated with the triage user
* Returns the value of the variable created in the oas_legal_server module for the organization associated with the intake settings.

.. note::
   The OAS Legal Server module stores a variable for each organization in OTIS in the format of oas_legal_server_org_[nid] where [nid] is the organization's node ID.

oas_triage_user_get_problemcode
---------------------------------
Located in: oas_triage_user.exits.inc

Returns the problem code related to the user's legal issue, from the legal server problem code mappings taxonomy, which maps ILAO's legal issue taxonomy to Legal Server's problem code table.

.. note::
   Relies on the `Legal Server Problem Code Mappings <https://www.illinoislegalaid.org/admin/structure/taxonomy/legal_server_problem_code_mappings>`_ taxonomy where each term name is the Legal Server problem code and a field maps ILAO's legal issues to that term.  For example, the 01 Bankruptcy/ Debter Relief maps to ILAO's bankruptcy legal issues.  The term names MUST match exactly how they exist in Legal Server.  

oas_triage_user_notes
-------------------------
Located in: oas_triage_user.exits.inc

Returns an updated notes string that includes:

* any notes generated from the triage rules
* the callback type, as a string using oas_triage_user_set_callback_type
* the callback times
* the user's immigrant status, if collected since this does not map in Legal Server
* the user's country of origin, since this is not mapped in Legal Server

oas_triage_user_set_callback_times
------------------------------------

Creates a string that represents the callback hours.


oas_triage_user_set_callback_type
-------------------------------------

Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^
Accepts a callback type string
Returns a Legal server acceptable callback type string



oas_triage_user_process_assets
--------------------------------
Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^
Accepts a triage user entity
Returns an array of collected assets formatted as:

.. code-block:: php  
 
   assetType => name
   assetAmount => $ amount of asset.

    Relies on oas_triage_user_get_financial_category to set the name based on Legal Server mappings.


oas_triage_user_process_income
---------------------------------
Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^^^
Accepts a triage user entity
Returns an array of collected income formatted as:

.. code-block:: php

   incomeType => name
   incomeFrequencey => 12 (since we collect monthly only)
   incomeAmount => dollar amount of income

Relies on oas_triage_user_get_financial_category to set the name based on Legal Server mappings.

oas_triage_user_process_expenses
-----------------------------------
Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^^
Accepts a triage user entity
Returns an array of collected expenses formatted as:

.. code-block:: php

  expenseType => name
  expenseFrequencey => 12 (since we collect monthly only)
  expenseAmount => dollar amount of income

Relies on oas_triage_user_get_financial_category to set the name based on Legal Server mappings.

oas_triage_user_get_financial_category
-----------------------------------------

Located in: oas_triage_user.exits.inc

Parameters
^^^^^^^^^^^^
Accepts:  $type and $class where class is the financial category type and type is the term name in the oas_financial_category types

Returns:  the term name from the legal_server_financial_mappings taxonomy where the term associated with the type passed in matches on the field_data_field_maps_to_financial.

.. note::
   The legal_server_financial_mappings taxonomy maps Legal Server financial categories to those provided by OTIS.  The legal_server_financial_mappings must be an exact match to Legal Server.
   
Submitting the eTransfer
=========================
Once the array of data is built, the system:

* Make a serialized copy of the array as part of the triage user entity
* Sets the etransfer status to Etransfer_Queued in the triage user entity
* Saves the triage user entity to the database
* Checks to see that the oas_legal_server is installed
* eTransfers the application
* Updates the intake settings to increment the current count by 1
* Displays the confirmation message to the user.


The actual eTransfer process is handled in the oas_legal_server module.  This was done to eventually allow us to leverage additional endpoints for transferring OTIS data.

Getting Legal Server's configuration
--------------------------------------

The oas_legal_server module includes a number of settings, stored as variables, that include:

* whether the site should be running OTIS in demo mode
* whether the site should be running OTIS in suspended mode
* the live transfer endpoint url
* the demo transfer endpoint url
* the maximum number of retries in case of failure
* the Legal server name of each organization
* a failure contact point

.. warning::
   If running in suspended mode, the etransfer will not be submitted.  If running in demo mode, the eTransfer will be sent to a demo server. These should NEVER be enabled on production.

Building the Legal Server transfer
-----------------------------------
The client array generated must be further transformed into XML to be sent to Legal Server.  That work is handled in the oas_legal_server module in the oas_legal_server_build_eTransfer function.

Parameters
^^^^^^^^^^^^
Accepts: a client data array
Returns: XML that complies with Legal Server's schema

Process
^^^^^^^^^^
The module:
* Replaces any & with the word and to ensure that the text passed is XML-friendly
* Wraps the data from the client data array into a <matter> XML tag
* Converts the client data array into XML
* Adds the matter_xml_version element

Sending the XML transfer
--------------------------
Once the XML packet is created, the oas_legal_server relies on CURL to send the eTransfer and waits for a response from Legal Server.

Success
^^^^^^^^^^
If Legal Server responds with a success message, the oas_legal_server module does nothing.  The oas_triage_user module takes back over and:

* sets the etransfer status to "Success"
* sets the intake status to eTransferred
* Sends out confirmation messages
* Displays the confirmation screen to the user.

Failure
^^^^^^^^
Failures happen in 2 ways:
* A server failure.  That usually resolves itself with a retry.
* A data validation failure.  That usually requires a manual resubmission

When Legal Server responds with a failure:
* the eTransfer status gets set to Failure
* the intake status gets set to not eTransferred
* the user is given an application delayed message
* the failure contact is notified
* the system will retry every hour until success up to the maximum number of retries.

.. note::
   If the failure is due to a data validation, the failure contact email will include a copy of the bad data.  Gwen's usual approach for this is to open the `XML endpoint <https://iloi.legalserver.org/modules/matter/intake_xml.php>`_ and build the XML by hand using the sample data, fixing any errors and then using Drush to update the oas_triage_user database.  This is not ideal.
   