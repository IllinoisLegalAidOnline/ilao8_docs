==================
ADRM Content
==================

Content types:

* adrm

Relies on
============

Currently relies on:

* Contributed modules:

  * token_custom allows us to create custom snippets within legal content
  * book
  * paragraphs
  * voting_api
  * fivestar
  * google_analytics_reports (GA)
  * workbench_moderation
  
* Custom modules:

  * ckeditor_rsm supports our ability to localize legal content snippets
  * ilao_access controls access to restricted content
  * ilao_ardm provides the core custom functionality for the content type
  
* Taxonomies
  
  * Legal_issues
  * Content_keywords
  * content_section
  * annual updates
  * content format
  
Fields
========
See also the `content migration spreadsheet. <https://docs.google.com/spreadsheets/d/18yC6qCk5gi3naY5f0xxT8Ye_aProaJIekmezI0copFI/edit#gid=1991457894>`_

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Title                         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_annual_updates         | Term reference to annual      | Migrate             |
|                              | updates taxonomy              |                     |
+------------------------------+-------------------------------+---------------------+
| field_meta_description       | Long text; SEO description    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_content_description    | Long text; site description   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_content_type           | Paragraphs; limited to link   | Migrate             |
|                              | (non-form), video, text, file |                     |
|                              | (non-form)                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_legal_position         | List (integer), 0 neutral, 1  | Migrate             |
|                              | plaintiff, 2 defendant        |                     |
+------------------------------+-------------------------------+---------------------+
| field_content_level          | List (text) basic or advanced | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_issues           | Term reference to legal issues| Migrate             |
|                              | Unlimited cardinality         |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_category       | Term reference to top level   | Migrate             |
|                              | legal category; limited to 1  |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_content_type   | Term reference                | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image                         | Migrate to media    |
+------------------------------+-------------------------------+---------------------+
| field_content_access         | List(1 legal aid; 2 pro bono) | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_pageviews              | Integer; from Google analytics| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_popularviews           | Integer; from Google analytics| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_rating                 | Fivestar rating               | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_share                  | AddThis                       | Replace             |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_keyword   | Content_keywords term ref.    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_section   | Content_section term reference| Migrate             |
+------------------------------+-------------------------------+---------------------+

Workbench Moderation
=====================

Notes
========

Field primary content type currently is never set for ADRM content; these are by definition attorney manuals.

Content access does not appear to have actually been implemented on the ADRM content type.
























