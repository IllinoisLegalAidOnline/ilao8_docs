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

First page of the form
------------------------
The first page of the form is defined in the oas_triage_user_application_form form.

Invokes and Requires
^^^^^^^^^^^^^^^^^^^^^^
Invokes hook_form 
Requires:

* ilao_triage
* Session variable containing the current intake settings id

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


Validation and Submission
^^^^^^^^^^^^^^^^^^^^^^^^^^

Contact form
==============







