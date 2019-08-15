================================
Toolbox related fields
================================


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

