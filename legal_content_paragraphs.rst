==================================
Legal content paragraphs
==================================

Text
==============
Machine name: text_article

Purpose:  Simple text field

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_body                   | Body field                    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+

Automated documents
=====================
Machine name: automated_documents

Purpose: To capture and display information related to an ILAO Easy Form

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_legal_links            | Link to easy form             | Migrate but alter   |
|                              |                               | label to Form URL   |
+------------------------------+-------------------------------+---------------------+
| field_link_language          | Select list of languages      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_document_type          | Select list of document types | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_form_qualifications    | Long text field to describe   | Migrate             |
|                              | who can use the interview     |                     |
+------------------------------+-------------------------------+---------------------+
| field_form_requirements      | Long text field to list info  | Migrate             |
|                              | required to do the interview  |                     |
+------------------------------+-------------------------------+---------------------+
| field_forms_produced         | Long text field to list the   | Migrate             |
|                              | forms the interview produces  |                     |
+------------------------------+-------------------------------+---------------------+
| field_inc_statewide_form_info| Boolean; display statewide    | Migrate             |
|                              | form information/PDF          |                     |
+------------------------------+-------------------------------+---------------------+
| field_printable_form_link    | Select for type of form link  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_direct_link_url        | Link; links to printable form | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_time_to_complete_start | Integer; number of minutes    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_time_to_complete_end   | Integer; number of minutes    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_save_answers_allowed   | Boolean                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+

Video
===========

Machine name: video_content
Purpose:  Supports the embed and display of Youtube videos on the site

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_video                  | Youtube or vimeo url          | Replace w/ Media*   |
+------------------------------+-------------------------------+---------------------+
| field_closed_captioned       | Is the video closed captioned?| Delete              |
+------------------------------+-------------------------------+---------------------+
| field_file_single            | Transcript file               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_tie_to_calendar        | Boolean; Should we pull data  |                     |
|                              | from the calendar             |                     |
+------------------------------+-------------------------------+---------------------+
| field_associated_content     | Calendar event                |                     |
+------------------------------+-------------------------------+---------------------+
| field_video_presenters       | Text                          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_has_mcle               | Boolean (yes/no)              | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_mcle_hours             | Float                         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_mcle_ethics_hours      | Float                         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_deadline               | Date; MCLE deadline           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_email                  | Email; MCLE contact email     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_email_for_questions    | Email; MCLE question contact  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_file                   | Attachments to include        | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_author                 | text; created by field        | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_script_author          | text; script author           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_funded_by              | text; funded by information   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


.. note:: 
   Need to evaluate whether to keep the tied to calendar functionality.  There are problems with the current field however.

Process Step
==============
Machine name: 

Purpose:  Used to build linear processes.  When displayed, each step in a node is auto-numbered.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_title                  | Text; title of the step       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; body of the step   | Migrate             |
+------------------------------+-------------------------------+---------------------+

.. note::
   The auto-sequencing on display is a problem for when we want to have non-linear processes.
 
Static Form   
====================== 
Machine name: static_form  

Purpose:  container for a form that is either an uploaded file or a link on another website.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_file_or_link           | Select list of link or file   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_file_single            | File; uploaded form           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_link             | Link; link to an external form| Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_brief_description      | Text; Form name               | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_form_qualifications    | Long text; who can use form   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_form_requirements      | Long text; what is required   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


File (non-form)
=====================
Machine name: file_non_form_

Purpose: container for file content that is not a legal form. 

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_file_single            | File; uploaded file           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_brief_description      | Text; file title              | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; description        | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


Link (non-form)
====================
Machine name: link_not_form_
Purpose: container for link content that is not a legal form

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_legal_link             | Link; external link           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; Description        | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


IICLE Content
===============
Machine name:  iicle_content

Purpose: container for IICLE content.  

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_legal_link             | Link; external link           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_body                   | Long text; Description        | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_ilao_cid               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+


.. note::
   IICLE content has a whole set of issues related to the need to proxy the content from IICLE to ILAO's platform.  This is one reason it is flagged as a separate bundle.  It is also restricted to legal aid members.

Legal Bundle
=============

Machine name: legal_bundle

Purpose: container to create a Guide.  It consists of an overview and links to other articles.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_body                   | Long text; Overview           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_learn_more_links       | Entity reference to nodes     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_take_action_links      | Entity reference to nodes     | Migrate             |
+------------------------------+-------------------------------+---------------------+



TeachMe
============
Machine name:  teach_me

Purpose:  Container to hold an articulate storyline module

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_legal_link             | Link to the teach me          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image for embed display       | Migrate             |
+------------------------------+-------------------------------+---------------------+


.. note::
   Teach Me's are complicated to work with. The teach me files must be uploaded by developers over SSH and who will then provide a link to the html file.  

Decision Tree
================
Machine name:  decision_tree

Purpose:  Similar to an Easy form, this is designed to help a user reach a decision point but produces something other than a legal document while still hosted on LHI.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_legal_link             | Link; Link to interview       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_link_language          | Select list of languages      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| description_field            | Long text; description        | Migrate but make    |
|                              |                               | long text only      |
+------------------------------+-------------------------------+---------------------+
| field_form_qualifications    | Long text field to describe   | Migrate             |
|                              | who can use the interview     |                     |
+------------------------------+-------------------------------+---------------------+
| field_form_requirements      | Long text field to list info  | Migrate             |
|                              | required to do the interview  |                     |
+------------------------------+-------------------------------+---------------------+
| field_time_to_complete_start | Integer; number of minutes    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_time_to_complete_end   | Integer; number of minutes    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_save_answers_allowed   | Boolean                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_document_description   | List; eligibility checker,    | Migrate             |
|                              | decision tree, evaluator      |                     |
+------------------------------+-------------------------------+---------------------+

Portal layout timeline
========================
Machine name:  portal_layout_timeline

Purpose: generates a nice looking linear timeline 

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_portal_tab             | Select list for Portal tab    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_timeline_boxes         | Paragraph; limited to portal  | Migrate             |
|                              | message type                  |                     |
+------------------------------+-------------------------------+---------------------+

Portal_message paragraph bundle
-----------------------------------
Machine name: portal_message

Purpose:  Displays a portal message consisting of a heading, image, and body.

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; Title/heading           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_media                  | File / Media                  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_summary                | Long text and summary         | Migrate             |
+------------------------------+-------------------------------+---------------------+

A2J Author
============

Machine name:  a2j_author

Purpose:  Container to embed a locally hosted A2J interview

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_a2j_file               | File; XML file of interview   | Migrate             |
+------------------------------+-------------------------------+---------------------+





