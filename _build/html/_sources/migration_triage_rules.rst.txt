===========================
Triage Rules
===========================

Triage rules are a standard Drupal content type that has been integrated with Webform and adds some custom functionality to process.  Triage rules are essentially black boxes where ILAO's platform has no understanding of the logic within them.  

Content Type
================

The content type has a handful of fields.  

+--------------------------+---------------------+---------------------------------------+
| Field                    | Type                | Description                           |
+==========================+=====================+=======================================+
| Title                    | text field          | Title for the triage rule             |
+--------------------------+---------------------+---------------------------------------+
| Service(s)               | entity reference    | Services associated with the triage   |
| (field_service)          |                     | rules; unlimited cardinality          |
+--------------------------+---------------------+---------------------------------------+
| Legal issue(s)           | term reference      | Legal issues tagged to the triage     |
| (field_legal_issues)     |                     | rules; unlimited cardinality          |
+--------------------------+---------------------+---------------------------------------+
| Groups audience          | Entity reference    | The organization associated with the  |
| (og_group_ref)           | Hidden              | service(s); controls permission       |
+--------------------------+---------------------+---------------------------------------+

It also has the webform module attached to allow webforms to be created and attached to the content.     

.. note::
   The ilao_triage module provides some special handling for the node:
   
   * The og_group_ref is hidden in the ilao_triage_form_triage_rules_node_form_alter.
   * The ilao_triage_node_after_build function hides some additional settings from users.
   * ilao_triage_node_presave sets the organic group to the organization of the first service selected.  This then controls access to edit the triage rules.
          


Webform Components & Conditionals
===================================

The ilao_triage module makes changes to the default webform module for the triage rule form to simplify it for OTIS administrators.

Form alteration
-----------------
Form alteration is located in ilao_triage.module in the ilao_triage_form_alter function.

For triage rules, the available types of form elements is different than for generic webforms.  The allowed form elements are:

* Date
* Hidden; the hidden type allows a triage rules author to save data that is passed in the notes field of an eTransfer OR set an endpoint
* Message; this is a markup element that displays to a user completing a set of program triage rules
* Number; a text field that requires a numerical value
* Radio; a single select option
* Text input; a text field that has no validation
* Yes/No; a radio single select option built using a custom webform component.  The yes/no component is defined in ilao_triage/components/yesno.inc.

Custom validation
-------------------
The ilao_triage_conditional_validate function provides a custom validation check to ensure that if there is a form element named 'end point', that it validates as one of the defined OTIS end points:

* intake (takes user to intake application)
* divert (gives the user referrals) 
* bypass (gives user the bypass screen; no intake or referrals are provided)
* pro bono (takes users to intake application but adds a note for pro bono placement)
* self help line (takes users to intake application but adds a note to direct to self help line)


Webform Processing
====================

The ilao_triage_module processes the submitted triage rules webform.  This logic is in the ilao_triage_submit function.

Process
-----------
For each submitted form element, it adds appropriate values to a notes object that is then inserted into an etransfer packet:

* For yes/no elements, it adds the name of the form element and then Yes or No based on the user's answer.
* For radio elements, adds the submitted answer.  For example for the radio question "What's your issue?" with options for "I had a cut in my food stamps, I received a letter that my food stamps are being terminated" and the user selects "I had a cut in my food stamps," the notes object would include the text I had a cut in my food stamps
* For hidden elements, other than those named end point or endpoint, the name of the form element and the hidden value are added to the notes. 
* For any other type, the name of the form element and then submitted value are added to the notes.

Endpoint processing
---------------------
A hidden field with a name of endpoint or end point is treated as the form element that controls routing of the triage rules through OTIS.

In all cases, the triage user entity is updated with the following:

* the last screen viewed is set to "Program triage"
* the intake_created timestamp is set to the current timestamp
* the changed timestamp is set to the current timestamp
* the intake_status is set to the correct status (see specific endpoints below)
* the triage_status is set to "Program triage_completed"
* if county and state information has not yet been stored, the county and state are saved based on the zip code entered.


.. note::
   The saving of triage user data checks first that the oas_triage_user module is enabled and a triage_id is stored in a session variable.  For a user coming through the normal workflow, these will always be true.  If this check fails, an error is thrown directing the user to the main Get Legal Help page.
   
Endpoint: intake, pro bono or self help line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
When the end point is intake, pro bono, or self help line:

* the user is redirected to the get-legal-help/intake page
* the intake status is updated to "Offered"

Endpoints of pro bono or self help line work just as any other form of intake except that:

* if the end point is pro bono, a note " Route to pro bono" is added to the case notes.
* if the end point is self help line, a note of " Route to self-represented litigant help line" is added to the case notes.

Endpoint: bypass
^^^^^^^^^^^^^^^^^
Bypass is designed to tell the user not to apply online but to call the program directly and should be used for high priority cases.  When the end point is set to bypass:

* the user is redirected to the get-legal-help/bypass page
* the intake status is updated to "Bypass intake"

Endpoint: divert
^^^^^^^^^^^^^^^^^^  
Diversion happens when a user answers triage rules in such a way that the program is not going to take their case.  When that happens:

* if program triage rules exist for a different program, the user is directed to their triage rules.
* if no other program triage rules exist for a different program, the user is given other referrals and directed to the /get-legal-help/referrals page.

In either case:

* the intake status is set to Diverted
* a record is entered in the oas_referral_history to log the diversion:

  * the service ID is stored in the database
  * the reject reason is set to "intake diversion"
  * the reject date is set to the current timestamp.
  
We did not start logging this information until 1/24/2018.  

.. warning::
   Our intention was to capture all instances where a user was offered a second chance intake.  This was probably not the best approach as it logs every intake diversion and not just those that resulted in a secondary intake.  





