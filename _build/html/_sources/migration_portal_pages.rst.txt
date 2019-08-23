============================
Portal content
============================

The portal main page was developed to create a custom landing page for a collection of issues.  

.. toctree::
   :maxdepth: 1
   :caption: See also:

   portal_content_paragraphs

Content type:  portal_main_page

.. note::
   See also our `end-user documentation <https://ilaodocs.readthedocs.io/en/latest/portal_admin.html>`_.

Relies on
============

Currently relies on:

* Contributed modules:

  * token_custom allows us to create custom snippets within legal content
  * paragraphs
  * voting_api
  * fivestar
  * block_reference
  * webform
  * webform_conditionals
  
* Custom modules:

  * ilao_portal_pages
  * ilao_legal_articles (the send_notification_preferences function only)
  * ilao_webform

* Taxonomies:

  * legal_issues

.. note::
   There are functions in the ilao_portal_pages module related to the toolbox content type that are not documented here but are documented in the Toolbox content. See `toolbox documentation <migration_toolboxes.html>`_  

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
   
Functionality
================

The ilao_portal_pages module provides a set of functions related to the add/edit content form:

Add/Edit Form alter
----------------------
Alters the form to include information about

* updating the revision date, which should be replaced to match legal content
* asking about translation outdated, which should be replaced with core translation pieces
* validates for best bet
* adds an After build to hide language, which should be evaluated for necessity in Drupal 8

Webform alter
---------------
Has a special webform alter for webform with NID 99541 to set a custom submission function (ilao_portal_pages_submit).  This provides custom node redirection for that specific webform.

.. note::
   Is this still necessary after the custom webform tool that lets us specify node redirects?
   
Node Presave
--------------
The node presave function:

* Forces the last substantive update date to the current date for new content
* Updates the last substantive update date when the user indicates it is an update
* Invokes the notifications function in ilao_legal_articles to send notification to users.


Node view changes
------------------
There is some custom code for NID 99176 to force Spanish users back to the English content page.  

.. note::
   This doesn't support Polish and should be reevaluated rather than migrated.
   
Webform redirects
------------------
The ilao_webform module:

* Checks to see if the webform is not a triage rules node
* Checks an endpoint hidden field and redirects to:

  * a specific node if the value is numeric
  * an internal url if it is not numeric
  
.. note:;
   For example, an endpoint of node/1 would direct back to the home page while an endpoint of get-legal-help would direct to /get-legal-help     


Open issues
==============

* Should we even have portal content?  Can we accommodate the same type of pages within the legal content type?  
* Workflow should be identical to legal content but currently there is no workflow management


