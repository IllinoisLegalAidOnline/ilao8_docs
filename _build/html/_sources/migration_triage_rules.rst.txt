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


Webform Components & Conditionals
===================================


Webform Processing
====================
