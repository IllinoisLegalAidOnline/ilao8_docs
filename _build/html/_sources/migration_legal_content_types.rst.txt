==============================
Legal content migration
==============================

.. toctree::
   :maxdepth: 1
   :caption: See also:

   legal_content_paragraphs
   legal_content_workflow
   legal_content_comments

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
  * annual updates
  * content format
   
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

See :ref:`legal_content_paragraphs` for migration information.

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

See :ref:`legal_content_workflows`

Functionality Notes
=====================

Primary content format
-----------------------

The field_primary_content_type field should not be editable but should be determined when content is created or updated based on the following algorithm.  Once it hits a value in this chart, it stops (so for example, if a node contains a automated_documents block and an iicle_content block, it will be IICLE content because that is what it hits first).

+-----------------------------------+---------------------------------------------+
| If the field_content_type contains| Then the field_primary_content_type is set  |
| this bundle                       | to this taxonomy term id from content format|
+===================================+=============================================+
| iicle_content                     | 523396 (IICLE)                              |
+-----------------------------------+---------------------------------------------+
| automated_documents               | 41 (Easy Form)                              |
+-----------------------------------+---------------------------------------------+
| decision_tree                     | 523631 (Decision Tree)                      |
+-----------------------------------+---------------------------------------------+
| teachme                           | 523401 (Teach Me)                           |
+-----------------------------------+---------------------------------------------+
| legal_bundle                      | 523406 (Guide)                              |
+-----------------------------------+---------------------------------------------+
| process_step                      | 501551 (How-To)                             |
+-----------------------------------+---------------------------------------------+
| portal_layout_timeline            | 501551 (How-To)                             |
+-----------------------------------+---------------------------------------------+
| static_form (link)                | 501221 (Form link)                          |
+-----------------------------------+---------------------------------------------+
| static_form (file)                | 501216 (From download)                      |
+-----------------------------------+---------------------------------------------+
| link_not_form``_``                | 21 (Link)                                   |
+-----------------------------------+---------------------------------------------+
| file_not_form``_``                | 22 (File download)                          |
+-----------------------------------+---------------------------------------------+
| video_content                     | 13 (Video)                                  |
+-----------------------------------+---------------------------------------------+
| a2j_author                        | 523631 (Decision Tree)                      |
+-----------------------------------+---------------------------------------------+
| anything else                     | 16 (Text article)                           |
+-----------------------------------+---------------------------------------------+


.. note::
   Do we really care if forms are links or downloads?                  

Custom breadcrumbs
---------------------

.. warning::
   This will need to be re-evaluated based on the new design.
   
We set custom breadcrumbs based on how the user accessed the node:

* If the user came in from our primary navigation, we use the category they selected
* If the user came in from a portal page, we use the portal page name in the breadcrumb
* If the user came in directly or from search or any other path besides a portal page or primary nav, we use the primary category field value

Custom code: ilao_legal_articles_set_breadcrumb called from ilao_legal_articles_node_view_alter

   
   
Archive MCLE Credit
---------------------

When a node contains a video and the video has MCLE credit assigned to it, the email contact form is used to send an email to a contact to request MCLE credit when:

* The user is logged in
* The node has a video block
* The cut off date for MCLE credit has not been reached

Custom code
^^^^^^^^^^^^^

Custom functionality to alter the request can be found in:

* ilao_legal_articles_form_email_mail_page_form_alter
* ilao_legal_articles_form_email_mail_page_redirect_handler
* ilao_legal_articles_form_email_mail_page_validate
* ilao_legal_articles_form_email_mail_page_submit


Custom access
---------------


Annual updates
------------------

The annual update field tracks when a content needs to be reviewed based on a date (for example, food stamp content needs to updated in October when new financial values are released by USDA).


Lift integration
-------------------
   


Legal content functionality to deprecate
=========================================

* Sharing content by SMS; this is not used widely and the current architecture is problematic.
* Recommended for you block; migrating the field but need to evaluate the utility vs other ways to do this in D8
* Code related to lingotek in the ilao_legal_articles should not be migrated; we will not be using Lingotek in Drupal 8.


Known Issues & Notes for Drupal 8
==================================

These are known issues and open questions to discuss with the content team:

* Current platform is overkill.
* Major / minor revision system => this has been disabled for months.  It should be completely deprecated in Drupal 8
* Ticket integration (ilao_workbench_check_for_open_ticket) should be discontinued.
* Notification of updates to users is dependent on what we do for account access moving forward.
* Popular today configuration may be depreciable if we do not continue that functionality moving forward.


     
          

