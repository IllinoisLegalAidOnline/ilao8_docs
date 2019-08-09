============================
Portal content
============================

The portal main page was developed to create a custom landing page for a collection of issues.  

.. toctree::
   :maxdepth: 1
   :caption: See also:

   portal_content_paragraphs

Content type:  portal_main_page


Fields
========
See also the `content migration spreadsheet. <https://docs.google.com/spreadsheets/d/18yC6qCk5gi3naY5f0xxT8Ye_aProaJIekmezI0copFI/edit#gid=1991457894>`_

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_subdomain              | Text field; Path for portal;  | Migrate             |
|                              | pages are tied together via   |                     |
|                              | the domain                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_page_type              | Select; one of main_page, sub-| Migrate             |
|                              | page or toolbox_selector_page |                     |
+------------------------------+-------------------------------+---------------------+
| title_field                  | Title field                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_meta_description       | Long text; description for SEO| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image for social media        | Migrate to media    |
+------------------------------+-------------------------------+---------------------+
| field_hero_image             | Image for page's hero banner  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_hero_title             | Text; Title to overlay on     | Migrate             |
|                              | hero image                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_hero_subtitle          | Text; subtitle to overlay     | Migrate             |
|                              | on hero image                 |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_category       | Term reference to legal issues| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_portal_paragraphs      | Paragraphs; items to include  | Migrate             |
|                              | on page                       |                     |
+------------------------------+-------------------------------+---------------------+
| field_rating                 | Five star rating field        | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_share                  | AddThis                       | Deprecate/replace   |
+------------------------------+-------------------------------+---------------------+
| field_substantive_update     | Boolean/when checked, update  | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_last_substantive_update| Date                          | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_transation_outdated    |                               | Do not migrate      |
+------------------------------+-------------------------------+---------------------+
| field_legal_issues           | Term reference to legal issue | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_promote_as_best_for    | Text; Best bet reference      | Migrate             |
+------------------------------+-------------------------------+---------------------+      

.. note::
   The hero image already uses the media module but the image field does not.
   

Open issues
==============

* Should we even have portal content?  Can we accommodate the same type of pages within the legal content type?  
* Workflow should be identical to legal content
