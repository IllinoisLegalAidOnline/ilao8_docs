===========================
Portal related paragraphs
===========================

The following paragraphs bundles are associated with the portal content type:

* Toolbox selector form
* Portal layout webform
* Portal layout grid
* Portal story
* Portal CTA
* Portal CTA image
* Portal layout summary
* Portal layout timeline
* Portal layout sidebar
* Portal layout split column
* Portal layout structured content
* Portal text
* Portal message

.. note::
   The portal layout types are generally just holders for other paragraphs and look the same but have different layouts associated with them.  

Fields
========
See also the `content migration spreadsheet. <https://docs.google.com/spreadsheets/d/18yC6qCk5gi3naY5f0xxT8Ye_aProaJIekmezI0copFI/edit#gid=1991457894>`_



.. note::
   In some bundles, the title_field provided by the title module is being used.  Should this be used or a different translatable field?
   

Toolbox selector form
=======================

The toolbox selector form is used to generate a toolbox selector form that pulls together all the toolbox portal pages in a particular portal subdomain.

.. note::
   The toolbox selector form is only supposed to be used to tie toolboxes together.  It needs to be evaluated.  It is stored only in a portal page of type "toolbox selector page" 
   


+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+ 
| field_form_label             | Text; Title for the form      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_label_for_other_option | Text; label to display for    | Migrate             |
|                              | when no toolbox applies       |                     |
+------------------------------+-------------------------------+---------------------+
| field_description_for_other  | Long text; help text to show  | Migrate             |
|                              | for other                     |                     |
+------------------------------+-------------------------------+---------------------+
| field_node_for_other_option  | Entity reference to node to   | Migrate             |
|                              | refer "other" users to        |                     |
+------------------------------+-------------------------------+---------------------+

Portal layout webform
=======================

Relies on:

* block_reference module
* webform
             
+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_layout_paragraph       | Paragraphs; holds a single    | Migrate             |
|                              | portal text bundle to display |                     |
|                              | next to a webform             |                     |
+------------------------------+-------------------------------+---------------------+
| field_webform                | Block reference to the webform| Migrate             |
+------------------------------+-------------------------------+---------------------+

Portal layout grid
===================

This is a 4 section grid. 

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Title of the bundle           | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_portal_grid_columns    | Paragraphs; hold grid items   | Migrate             |
|                              | allows only portal story items|                     |
+------------------------------+-------------------------------+---------------------+


Portal Story
==============

The is a single cell in the portal layout grid.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; heading for the cell    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image; displays in cell       | Migrate/Media       |
+------------------------------+-------------------------------+---------------------+
| field_quote                  | Text                          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_summary                | Long text and summary         | Migrate (long text) |
+------------------------------+-------------------------------+---------------------+
| field_url                    | URL; used for a clickable     | Migrate             |
|                              | button                        |                     |
+------------------------------+-------------------------------+---------------------+

Portal CTA
============
Portal Call to Action layout consists of an icon, a title, a body, and a clickable button.


+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_icons           | List; class of icon to display| Migrate             |
+------------------------------+-------------------------------+---------------------+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_url                    | Link; url and title of button | Migrate             |
+------------------------------+-------------------------------+---------------------+

Portal CTA Image
=================

Portal Call to Action Image layout consists of an icon, an image, a title, a body, and a clickable button.


+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_icons           | List; class of icon to display| Migrate             |
+------------------------------+-------------------------------+---------------------+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_url                    | Link; url and title of button | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image; appears on block       | Migrate/Media       |
+------------------------------+-------------------------------+---------------------+

Portal Layout Summary
======================

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_summary         | Paragraphs; limited to portal | Migrate             |
|                              | text                          |                     |
+------------------------------+-------------------------------+---------------------+



   
Portal message
===============

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_media                  | File; media file              | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_summary                | Long text w/ summary          | Migrate             |
+------------------------------+-------------------------------+---------------------+

Portal layout timeline
=======================

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_tab             | List; options for step, alert | Migrate             |
|                              | turning point, decision       |                     |
+------------------------------+-------------------------------+---------------------+
| field_timeline_boxes         | Paragraphs; limited to portal | Migrate             |
|                              | message                       |                     |
+------------------------------+-------------------------------+---------------------+

.. note::
   The portal tab field then relies on custom CSS to display the correct image based on the selection



Portal layout sidebar
======================

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_sidebar_content | Paragraphs; limited to portal | Migrate             |
|                              | CTA, Portal CTA image         |                     |
+------------------------------+-------------------------------+---------------------+


Portal layout split column
===========================
+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_split_columns   | Paragraphs; limited to portal | Migrate             |
|                              | text                          |                     |
+------------------------------+-------------------------------+---------------------+


Portal layout structured content
=================================

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; title field for block   | Migrate             |
+------------------------------+-------------------------------+---------------------+ 
| field_structured_paragraphs  | Paragraphs; limited to portal | Migrate             |
|                              | text                          |                     |
+------------------------------+-------------------------------+---------------------+


Portal text
============

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_icons           | List; class of icon to display| Migrate             |
+------------------------------+-------------------------------+---------------------+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_summary                | Long text w/ summary          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_url                    | Link for button               | Migrate             |
+------------------------------+-------------------------------+---------------------+




                         

