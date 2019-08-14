==================================
Toolboxes and related structures
==================================

.. _migration_toolboxes:

Content types and custom entities
===================================

The toolboxes platform relies on 4 content types:
* portal_main_page
* toolboxes
* toolbox_tool
* toolbox_tool_step

See also `End user toolbox documentation <https://ilaodocs.readthedocs.io/en/latest/toolboxes_admin.html>`_

Relies on
============

Currently relies on:

* Contributed modules:

  * token_custom allows us to create custom snippets within legal content
  * paragraphs
  * voting_api
  * fivestar
  * block_reference
  
* Custom modules:

  * ilao_portal_pages

* Taxonomies:

  * legal_issues


Toolbox Fields
===============
+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; Title for the toolbox   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_portal                 | Entity reference to portal    | Migrate             |
|                              | page toolbox belongs to       |                     |
+------------------------------+-------------------------------+---------------------+
| field_content_description    | Long text; description for    | Migrate             |
|                              | site display                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_meta_description       | Long text; description for    | Migrate             |
|                              | social media                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_purpose_description    | Long text; description for    | Migrate             |
|                              | "My issues" pages             |                     |
+------------------------------+-------------------------------+---------------------+
| field_selector_form_label    | Text; label for toolbox       | Migrate             |
|                              | selector form                 |                     |
+------------------------------+-------------------------------+---------------------+
| field_overall_level_of_effort| List; easy, medium or hard    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_encourage_user_legal   | Boolean                       | TBD                 |
| help                         |                               |                     |
+------------------------------+-------------------------------+---------------------+
| field_fast_fact_block        | Long text; block for page     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_page_components        | Paragraphs; limited to portal | Migrate             |
|                              | layout webform, portal layout |                     |
|                              | sidebar, portal layout split  |                     |
|                              | column                        |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_category       | Term reference to top legal   | Migrate             |
|                              | issues                        |                     |
+------------------------------+-------------------------------+---------------------+
| field_legal_issues           | Term reference to legal issues| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_promote_as_best_for    | Text; used for search         | Migrate             |
+------------------------------+-------------------------------+---------------------+

Toolbox Tool Fields
=====================
+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; Title for the toolbox   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_toolbox                | Entity reference to toolbox   | Migrate             |
|                              | nodes                         |                     |
+------------------------------+-------------------------------+---------------------+
| field_selector_form_label    | Text; label for tool picker   | Migrate             |
|                              | form                          |                     |
+------------------------------+-------------------------------+---------------------+
| field_overall_level_of_effort| List; easy, medium, or hard   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_purpose_description    | Long text; description for    | Migrate             |
|                              | "My issues" pages             |                     |
+------------------------------+-------------------------------+---------------------+
| field_overview               | Overview for the tool         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_pick_up_where_I_left   | Long text; for pick up block  | TBD                 |
| _off                         |                               |                     |
+------------------------------+-------------------------------+---------------------+
| field_before_you_get_started | Long text; before you get     | Migrate             |
|                              | started text                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_component   | Boolean; include learn more   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_component   | List; build manually or use   | Migrate             |
| _type                        | existing guide                |                     |
+------------------------------+-------------------------------+---------------------+
| field_guide                  | Entity reference to legal     | Migrate             |
|                              | content of type "Guide"       |                     |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_content     | Entity reference to legal     | Migrate             |
|                              | content, blogs to include     |                     |
+------------------------------+-------------------------------+---------------------+
| field_share                  | AddThis                       | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_steps                  | Entity reference to toolbox   | Migrate             |
|                              | tool steps in the tool        |                     |
+------------------------------+-------------------------------+---------------------+
| field_exclude_from_sms_cont  |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_primary_category       | Term reference to top legal   | TBD                 |
|                              | issue                         |                     |
+------------------------------+-------------------------------+---------------------+


Toolbox Tool Step Fields
=========================

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; Title for the toolbox   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_tool                   | Entity reference to tool node | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_purpose_description    | Long text; used on My issues  | Migrate             | 
+------------------------------+-------------------------------+---------------------+
| field_step_always_required   | Boolean; does a user always   | Migrate             |
|                              | have to complete the step     |                     |
+------------------------------+-------------------------------+---------------------+
| field_explain_step_not       | Long text; description of when| Migrate             |
| _required                    | step is not required          |                     |
+------------------------------+-------------------------------+---------------------+
| field_include_e_filing_block |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_last_step              | Boolean;is this last step in  | Migrate             |
|                              | tool                          |                     |
+------------------------------+-------------------------------+---------------------+
| field_step_type              | Paragraphs; main content for  | Migrate             |
|                              | step. Limited to webform, fill|                     |
|                              | out forms (single/multiple),  |                     |
|                              | process step                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_tool_step_component    | Paragraphs; side content     | Migrate              |
|                              | Limited to callout, key terms,|                     |
|                              | Short answer component        |                     |
+------------------------------+-------------------------------+---------------------+
| field_share                  | AddThis                       | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_tickler_settings       | Paragraphs; limited to tickler| Migrate             |
|                              | settings bundle               |                     |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_component   | Boolean; include learn more   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_component   | List; build manually or use   | Migrate             |
| _type                        | existing guide                |                     |
+------------------------------+-------------------------------+---------------------+
| field_guide                  | Entity reference to legal     | Migrate             |
|                              | content of type "Guide"       |                     |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_content     | Entity reference to legal     | Migrate             |
|                              | content, blogs to include     |                     |
+------------------------------+-------------------------------+---------------------+
| field_exclude_from_sms...    |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_include_fee_waiver     |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


Toolbox Paragraph Bundles
==========================

Tickler settings
-----------------
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
---------
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
-------------------------

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
--------------------------

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
---------

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
---------------

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
----------------
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
---------------
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
------------------------
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
----------------------
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
------------

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_term                   | Text; term name               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; definition         | Migrate             |
+------------------------------+-------------------------------+---------------------+ 
  


Paragraph bundles to delete
--------------------------------

* informational_step








Open issues
============

* Toolboxes currently must be tied to a portal


