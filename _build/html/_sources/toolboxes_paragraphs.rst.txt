===================================
Toolbox-related paragraphs bundles
===================================


Tickler settings
=================
Used in the field_tickler_settings field in the toolbox tool step content type.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_number_of_days_to      | Text; number of days to invoke| Migrate             |
| _trigger                     | a tickler                     |                     |
+------------------------------+-------------------------------+---------------------+
| field_tickler_type           | Select; end_last or end_this  | Migrate             |
|                              | what date to start calc from  |                     |
+------------------------------+-------------------------------+---------------------+
| field_sms_message_to_send    | Long text; 160 character max  | Migrate             |
|                              | message to send to SMS users  |                     |
+------------------------------+-------------------------------+---------------------+
| field_email_subject          | Text; subject for email users | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_email_body             | Long text; body for mail users| Migrate             |
+------------------------------+-------------------------------+---------------------+

Webform
=========
Machine name: webform. Used in the field_step_type field.  

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_heading                | Text;heading for webform block| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_portal_icons           | List; icon to include on block| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Body to display with webform  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_webform                | Block reference to webform    | Migrate             |
+------------------------------+-------------------------------+---------------------+

Fill out forms (single)
========================

Machine name: fill_out_forms_single. Used in the field_step_type field to pull in a single form from ILAO's website.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_callout                |Paragraphs; limited to callout | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_internal_forms         |Paragraphs; limited to internal| Migrate             |
|                              |forms                          |                     |
+------------------------------+-------------------------------+---------------------+

Fill out forms (multiple)
==========================

Machine name: fill_out_forms_multiple. Used in the field_step_type to pull together a list of forms.
 
+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_callout                |Paragraphs; limited to callout | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_required_forms_label   | Text; label for grouping of   | Migrate             |
|                              | required forms                |                     |
+------------------------------+-------------------------------+---------------------+
| field_optional_forms_label   | Text; label for grouping of   | Migrate             |
|                              | optional forms                |                     |
+------------------------------+-------------------------------+---------------------+ 
| field_internal_forms         |Paragraphs; limited to internal| Migrate             |
|                              |forms                          |                     |
+------------------------------+-------------------------------+---------------------+ 
| field_external_forms         |Paragraphs; limited to external| Migrate             |
|                              | forms                         |                     |
+------------------------------+-------------------------------+---------------------+

Callout
===========

Machine name: callout
Nested within multiple paragraph bundles.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_title                  | Text; Header for callout block| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body of callout    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_portal_icons           | List; icon to display         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_position               | List; top or bottom; where to | Migrate             |
|                              | show callout on page          |                     |
+------------------------------+-------------------------------+---------------------+

Internal forms
===============

Machine name: internal_forms

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_form                   | Entity reference to legal     | Migrate             |
|                              | content that are forms        |                     |
+------------------------------+-------------------------------+---------------------+
| field_form_type              | List; form is required or not | Migrate             |
+------------------------------+-------------------------------+---------------------+

External forms
=================

Machine name: external_forms

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_link                   | Link to an external form      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; description of form| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_form_type              | List; form is required or not | Migrate             |
+------------------------------+-------------------------------+---------------------+

Process step
===============

Machine name: process_step

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_title                  | Text; Step title              | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body of step       | Migrate             |
+------------------------------+-------------------------------+---------------------+


.. note::
   Also used in legal content.
   
Short answer component
=======================

Machine name: short_answer_component

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_component_label        | Text; Header for  block       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_component_description  | Paragraphs; limited to        | Migrate             |
|                              | component description         |                     |
+------------------------------+-------------------------------+---------------------+

Component description
=======================

Machine name: component_description

Used in short answer component to build out individual items.


+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body               | Migrate             |
+------------------------------+-------------------------------+---------------------+ 

Key terms
============

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_term                   | Text; term name               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; definition         | Migrate             |
+------------------------------+-------------------------------+---------------------+ 
  


Paragraph bundles to delete
==============================

* informational_step
