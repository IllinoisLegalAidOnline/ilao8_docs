==============================
Legal content migration
==============================

.. toctree::
   :maxdepth: 1
   :caption: See also:

   legal_content_paragraphs
   legal_content_workflow

Content types:

* legal_content

Relies on
============

Currently relies on:

* Contributed modules:

  * token_custom allows us to create custom snippets within legal content
  * workbench
  * workbench_moderation
  * workbench_access
  * paragraphs
  * voting_api
  * fivestar
  * google_analytics_reports (GA)
  
* Custom modules:

  * ckeditor_rsm supports our ability to localize legal content snippets
  * ilao_access controls access to restricted content
  * ilao_legal_articles provides the core custom functionality for the content type
  * ilao_workbench provides custom settings for workbench moderation
  
* Taxonomies
  
  * Legal_issues
  * Content_keywords
  * content_section
  * region
   
It is unclear if we actually use:

* workbench_moderation_buttons
* workbench_moderation_profile
* workbench_scheduler or scheduler_workbench (I think we use one of these but I'm not sure how successful it is)
  

Fields
========
See also the `content migration spreadsheet. <https://docs.google.com/spreadsheets/d/18yC6qCk5gi3naY5f0xxT8Ye_aProaJIekmezI0copFI/edit#gid=1991457894>`_

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_annual_updates         | Term reference to annual      | Migrate             |
|                              | updates taxonomy              |                     |
+------------------------------+-------------------------------+---------------------+
| field_content_access         | Select (legal aid members or  | Migrate             |
|                              | pro bono members)to restrict  |                     |
|                              | by role                       |                     |
+------------------------------+-------------------------------+---------------------+
| field_content_description    | Description field for website;| Migrate             |
|                              | limited to 200 characters     |                     |
+------------------------------+-------------------------------+---------------------+
| field_content_level          | Select (basic or advanced)    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_content_type           | Paragraphs field              | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_issues           | Taxonomy term for legal issues| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_position         | Select: plaintiff, defendant, | Migrate             |
|                              | or neutral                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_pageviews              | Number of pageviews in last   | Migrate             |
|                              | 60 days; from GA              |                     |
+------------------------------+-------------------------------+---------------------+
| field_popularviews           | Number of pageviews in last 2 | Migrate             |
|                              | days; from GA                 |                     |
+------------------------------+-------------------------------+---------------------+
| field_rating                 | Stores our ratings data       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_share                  | Add this field                | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image for use in social media | Replace w/ media    |
+------------------------------+-------------------------------+---------------------+
| field_last_substantive_update| Date of last substantive edit | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_meta_description       | Description for metatags;     | Migrate             |
|                              | limited to 300 characters     |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_category       | Single term reference to top  | Migrate             |
|                              | legal issue category          |                     |
+------------------------------+-------------------------------+---------------------+
| field_primary_content_type   | Content format; determined by | Migrate             |
|                              | paragraphs included           |                     |
+------------------------------+-------------------------------+---------------------+
| field_substantive_update     | Boolean; indicates whether an | Migrate             |
|                              | edit is substantive or not    |                     |
+------------------------------+-------------------------------+---------------------+
| title_field                  | Standard Drupal translatable  | Migrate             |
|                              | title field                   |                     |
+------------------------------+-------------------------------+---------------------+
| body                         | Replaced with paragraphs      | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_translation_outdated   | Boolean to indicate if new    | Delete; duplicative |
|                              | translation required          | of core function    |
+------------------------------+-------------------------------+---------------------+
| field_promote_as_best_for    | search terms to return this   | Migrate             |
|                              | as number 1 search result     |                     |
+------------------------------+-------------------------------+---------------------+
| field_request_translation    | On English content, yes/no    | Migrate             |
|                              | as to whether it should also  |                     |
|                              | be translated                 |                     |
+------------------------------+-------------------------------+---------------------+
| field_exclude_from           | Indicates that the content    | Delete              |
| _sms_content_s               | should not be available in SMS|                     |
+------------------------------+-------------------------------+---------------------+
| field_major_revision         |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_keyword   | Content_keywords term ref.    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_section   | Content_section term reference| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_jurisdiction_type      | Select list of national,      | Migrate             |
|                              | statewide or parts of Illinois|                     |
+------------------------------+-------------------------------+---------------------+
| field_cities                 | Term reference to region at   | Migrate             |
|                              | city level                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_counties               | Term reference to region at   | Migrate             |
|                              | county level                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_zipcodes               | Term reference to region at   | Migrate             |
|                              | zip code level                |                     |
+------------------------------+-------------------------------+---------------------+
| field_include_exclude_by_type| Select list; what level(cities| Migrate             |
|                              | counties or zip codes) to tag |                     |
|                              | content to                    |                     |
+------------------------------+-------------------------------+---------------------+
| field_include_exclude        | Whether to include or exclude | Migrate             |
|                              | the region(s) from the content|                     |
+------------------------------+-------------------------------+---------------------+
| field_recommendation         | Reference to related content  | Migrate             |
+------------------------------+-------------------------------+---------------------+


.. note:: 
   Jurisdictions are managed on an include or exclude basis when the content is set to parts of Illinois.  For example, if a node applies only to Cook county, I might include counties = Cook and if a node applies to all but Cook county, I might exclude counties = Cook.  
   
Paragraphs
============
Our content_block field uses paragraphs to build the actual legal content.  These are the paragraph bundles associated with legal content:

See Legal content paragraphs for migration information.

* Text
* Automated documents
* Video
* Process step
* Static form
* File (non-form)
* Link (non-form)
* IICLE content
* Legal bundle
* Teach Me
* Decision tree
* Portal layout timeline
* A2J author  
   
Scheduler Issues
=================
We have 2 modules in our file system, workbench_scheduler and scheduler_workbench.  I don't know which we need but we do want to be able to schedule nodes for publication.   

Workbench Moderation
=====================



Legal content functionality to deprecate
=========================================

* Sharing content by SMS; this is not used widely and the current architecture is problematic.
* Recommended for you block; migrating the field but need to evaluate the utility vs other ways to do this in D8
