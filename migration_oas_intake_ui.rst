===================================
OTIS Intake UI and Pre-Transfer
===================================

When a user reaches intake, after completing a program's triage rules successfully, they complete a series of forms to collect additional information.

Application form
============================
Location: oas_triage_user.application_form.inc

The main get-legal-help/intake form is a multi-page form and what pages display to a user depends on the intake settings. An error is thrown if there is  no session variable for the triage id.

The form consists of:
* The first page that collects name, date of birth, and demographics.  These are defined in the oas_triage_user_application_form.
* A page to collect household size
* Pages to collect financial information


The oas_triage_user_application_form_validate manages form validation and invokes specific validation on each page's submission.

The contact form and callback selection form are separate forms.

Invokes and Requires
----------------------
Invokes hook_form 
Requires:

* ilao_triage
* Session variable containing the current intake settings id

First page of the form
------------------------
The first page of the form is defined in the oas_triage_user_application_form form.


Form Elements
^^^^^^^^^^^^^^^^^
Note that the select taxonomy require oas_triage_user_load_intake_taxonomy to load the options.  For fields marked "only displays if enabled," these only display if the intake settings are configured to collect the field.  When collected, the help text is pulled from the intake settings.

The Select country requires the locale module to load Drupal's country list.
+------------------------------+----------------------------+----------------------------+
| Form variable                | Type                       | Notes                      |
+==============================+============================+============================+
| settings_id                  | hidden                     | the session intake settting|
+------------------------------+----------------------------+----------------------------+
| about_you                    | field set                  | Just a label               |
+------------------------------+----------------------------+----------------------------+
| first_name                   | text field                 | User's first name          |
+------------------------------+----------------------------+----------------------------+
| middle_name                  | text field                 | User's middle name         |
+------------------------------+----------------------------+----------------------------+
| last_name                    | text field                 | User's last name           |
+------------------------------+----------------------------+----------------------------+
| maiden_name                  | text field                 | User's maiden name         |
+------------------------------+----------------------------+----------------------------+
| nickname                     | text field                 | User's nickname(s)         |
+------------------------------+----------------------------+----------------------------+
| date_of_birth                | date or text field         | If date module exists,     |
|                              |                            | separate month, day, year  |
|                              |                            | elements; goes back 110 yrs|
+------------------------------+----------------------------+----------------------------+
| race                         | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+| ethnicity                    | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| gender                       | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| marital_status               | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| country                      | select country             | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| language                     | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| immigration                  | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| citizenship                  | select taxonomy            | Only displays if enabled   |
+------------------------------+----------------------------+----------------------------+
| current_client               | checkbox                   | Is user current client for |
|                              |                            | same problem?              |
+------------------------------+----------------------------+----------------------------+
| applied                      | checkbox                   | Has user applied for same  |
|                              |                            | problem?                   |
+------------------------------+----------------------------+----------------------------+
| current_client_different     | checkbox                   | Is user current client w/  |
|                              |                            | a different problem?       |
+------------------------------+----------------------------+----------------------------+
| never_client                 | checkbox                   | Has user never been a      |
|                              |                            | client of organization z   |
+------------------------------+----------------------------+----------------------------+
| prisoner                     | checkbox                   | Is user in jail or prison? |
|                              |                            | Only asked if needed       |
+------------------------------+----------------------------+----------------------------+


Validation
^^^^^^^^^^^^^^
The global validation function:

* Invokes the page 1 submit function (oas_triage_user_submit_page1)
* Updates the current page in the form state array
* Stores the first page's data in the form state array
* Drupal's own validation handles the required field validation.

Submit handler
^^^^^^^^^^^^^^^^

Displays an error message if 

* the user has indicated that they are a current client
* the user has indicated that they have already applied
* the user has indicated that they are in jail or prison and the intake settings does not allow prisoners to apply online
* the user is younger than the minimum age to apply online.  

If an error message is displayed, the user is not allowed to proceed to the second page.

The _oas_triage_user_get_user_age private function takes the user's date of birth to calculate their age.

Invokes oas_triage_user_save_demographics to save demographic data.

Saving entity data from page 1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The oas_triage_user_save_demographics function loads the current triage entity and updates:

* the last screen viewed to "Intake start"
* the intake status to "Started"
* the intake_changed time to the current timestamp
* the user's age
* the user's various demographic properties, if collected:

  * gender
  * race
  * ethnicity
  * marital_status
  * citizenship_status
  * immigration_status
  * primary language
  * country of origin

Household size page
---------------------

Form Elements
^^^^^^^^^^^^^^^^^

+------------------------------+----------------------------+----------------------------+
| Form variable                | Type                       | Notes                      |
+==============================+============================+============================+
| description                  | markup                     | From intake settings, the  |
|                              |                            | program's definition of who|
|                              |                            | is in the household        |
+------------------------------+----------------------------+----------------------------+
| household_size               | markup                     | Heading label              |
+------------------------------+----------------------------+----------------------------+
| adults                       | integer                    | Number of adults; required |
+------------------------------+----------------------------+----------------------------+
| children                     | integer                    | Number of kids; required   |
+------------------------------+----------------------------+----------------------------+

Validation
^^^^^^^^^^^^
This page has a custom validate function, oas_triage_user_validate_household.

Validation requires that:

* Number of adults is a positive integer or empty
* Number of children is a positive integer or empty
* Total number of adults and children is at least 1

Submission
^^^^^^^^^^^^
This page has a custom submit function, oas_triage_user_submit_household.

Upon submission, the triage user entity is updated:

* to set the number of household_adults
* to set the number of household_children
* sets the intake_changed property to the current timestamp
* changes the last screen viewed to "Intake household"

Financial Pages
------------------
The financial form pages depend on the financial settings in the relevant intake_settings entity.  Programs may collect:

* income
* assets
* expenses
* expenses only if the user appears to be over-income
* nothing at all

If intake settings are configured to not collect any financial information, the user's application is then processed.

The oas_triage_user_get_next_screen function determines which form page to show:
* From household size, show income if income needs collected
* From household size, process if no income, assets, or expenses need collected
* From income page, show assets if assets need collected
* From income page, show expenses if assets are not collected but expenses are
* From income page, show expenses if assets are not collected, expenses are only collected if the user is over-income and the user appears to be over-income
* From income page, go to done if no assets or expenses need collected
* From asset page, show expenses if expenses are generally collected
* From asset page, show expenses if  expenses are only collected if the user is over-income and the user appears to be over-income
* From asset page, go to done if no expenses need collected
* From expense page, go to done

..warning::
  It appears that if income is not collected, assets and expenses can not be collected either.

..note ::
  There was agreement in the evaluation meeting to remove some of the financial pages across programs.
  
Building the form
^^^^^^^^^^^^^^^^^^^
The form is built in the oas_triage_user_ask_financial function
Located: oas_triage_user.application_form.inc

Parameters:

* $form => the form
* $terms => the financial taxonomy terms to collect
* $category => a string (expense types, assets, income sources)
* $suffix => a label to append to the end of the help description (per month, total, etc)
* $progress => the progress percentage to display in the progress form

Form elements:

With this information, the ask_financial function builds a form that:

* adds a description header, with the number of household members
* loops through each taxonomy term and loads the related ilao_oas_financial_category entity
* builds field groups for each unique subcategory of financial categories
* adds each financial category item as a field within the correct field group
* each term is:

  * required
  * named a variation of the taxonomy term name that is lowercase and spaces replaced with underscores.  For example Checking account becomes named checking_account.
  * prefixed with a $
  * any suffix is added
  * help text from the entity is added
  * a textfield
  * required to be an integer
  * defaults to 0

Form validation:

* The _oas_triage_user_validate_financial validates each item to ensure it is a positive integer or 0

Saving Financial Data
^^^^^^^^^^^^^^^^^^^^^^
Each type category of financial data has its own save function.

Income:  oas_triage_user_save_income, which:

* Loads the triage user entity
* Sets the last screen viewed to "Income questions"
* Adds up all the income amounts and stores it in the total income property
* Updates the intake changed timestamp to the current timestamp
* Saves the triage user entity

Assets:  oas_triage_user_save_assets, which:

* Loads the triage user entity
* Sets the last screen viewed to "Assets questions"
* Adds up all the income amounts and stores it in the total assets property
* Updates the intake changed timestamp to the current timestamp
* Saves the triage user entity

Expenses:  oas_triage_user_save_expenses, which:

* Loads the triage user entity
* Sets the last screen viewed to "Expense questions"
* Adds up all the expense amounts and stores it in the total expenses property
* Updates the intake changed timestamp to the current timestamp
* Saves the triage user entity

Calculating Financial Eligibility
===================================

Income eligibility
--------------------
The oas_triage_user_calculate_income_eligibility calculates income eligiblity.  Income eligibility is generally determined by looking at the total income minus countable expenses against a maximum percentage of an income standard based on household size.

Parameters
^^^^^^^^^^^^
Requires:  intake settings entity, count expenses boolean (Default is true)
Returns: boolean value "is user income eligible?"

Process
^^^^^^^^^
Returns true if income is not collected.  For all other cases:

* Invokes oas_triage_user_check_for_exemption to see if income is waived for the user
* Calculates the total household size
* Adds up all the entered income fields and multiplies by 12 to get annual income
* If expenses can be offset against income:

  * Adds up all collected expenses
  * Multiplies expenses by 12

* If expenses are not available to offset income, set total expenses to 0  
* Sets the total income for eligibility to income - assets with a minimum income of 0
* Loads the ilao_income_standard used in the intake settings as the income standard to apply
* Calculates the correct annual amount by:

  * For households with 8 or fewer members, taking that amount from the income standards entity
  * For households with more than 8 members, taking the amount for 8 members and adding the additional member amount * the number of additional members
  * Determines the maximum allowed income based on the percentage allowed in the intake settings
  * Returns true if the user is not over income and eligible for services
  * Returns false if the user is over income and not eligible

Asset eligibility
-------------------

The oas_triage_user_calculate_asset_eligibility calculates asset eligiblity.  Asset eligiblity is generally calculated by adding up all countable assets and comparing that against a maximum asset dollar limit.  Some programs exclude a dollar amount for personal property in adding up assets.

Parameters
^^^^^^^^^^^^
Requires:  intake settings entity,
Returns: boolean value "is user asset eligible?"


Process
^^^^^^^^^

* Adds up all the asset items
* If personal property is collected and there is a dollar exemption for personal property, the total assets are reduced (but not by more than the amount of personal property) by the exemption amount.  For example: 

  * if total assets are $5000, personal property is $2000 and the personal property exemption is $8500, total assets of $3000 would be counted.
  * if total assets are $10000, personal property is $9000 and the personal property exemption is $8500, total assets of $1500 would be counted.
  
* Pulls the maximum allowed assets tied to the intake settings
* If the total countable assets are less than the maximum allowed, returns TRUE (user is asset eligible)
* If the total countable assets are equal to or more than the maximum allowed, returns FALSE (user is not asset eligible)

Final processing
-------------------
The application submit function then:
* Updates the overincome property in the triage user entity to 3 if the user is over asset, 2 if the user is over-income  If a user is both over income and over asset, the status is set to 3.

If a user is financially ineligible, they are redirected to referrals.  If they are eligible, they are taken to the contact form.

  
 
  

Contact form
==============







