==============================
Legal content workflows
==============================

.. _legal_content_workflows:

Workbench Configuration
=========================

States
---------


+------------------------------+-------------------------------+---------------------+
| Name                         | Machine name                  | Status              |
+==============================+===============================+=====================+
| Draft/revise                 | draft                         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| Draft/Revise attorney content| draft_revise_attorney_content | TBD                 |
+------------------------------+-------------------------------+---------------------+
| Copy Edit                    | copy_edit                     | TBD                 |
+------------------------------+-------------------------------+---------------------+
| Ready to review              | ready_to_review               | TBD                 |
+------------------------------+-------------------------------+---------------------+
| Published                    | published                     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| Metadata review              | metadata_review               | TBD                 |
+------------------------------+-------------------------------+---------------------+
| Substantive update           | substantive_update            | TBD                 |
+------------------------------+-------------------------------+---------------------+
| Plain language review        | plain_language_review         | TBD                 |
+------------------------------+-------------------------------+---------------------+

.. note::
   All states except for Draft/Revise attorney content apply to the legal content content type.  That state belongs to the ADRM content type.
   
Transitions
-------------


+------------------------------+------------------+------------------+----------------+
| Name                         | From             | To               | Status         |
+==============================+==================+==================+================+
| draft-copy_edit              | Draft/Revise     | Copy Edit        |                |
+------------------------------+------------------+------------------+----------------+
| draft-ready_to_review        | Draft/Revise     | Ready to review  |                |
+------------------------------+------------------+------------------+----------------+
| draft-published              | Draft/Revise     | Published        | Migrate        |
+------------------------------+------------------+------------------+----------------+
| draft-substantive_update     | Draft/Revise     | Sub. Update      |                |
+------------------------------+------------------+------------------+----------------+
| draft_revise_attorney        | Draft/Revise     | Published        |                |
| _content-published           | attorney content |                  |                |
+------------------------------+------------------+------------------+----------------+
| copy_edit-draft              | Copy edit        | Draft/revise     |                |
+------------------------------+------------------+------------------+----------------+
| copy_edit-plain_language     | Copy edit        | Plain language   |                |
| _review                      |                  | Review           |                |
+------------------------------+------------------+------------------+----------------+
| ready_to_review-published    | Ready to review  | Published        |                |
+------------------------------+------------------+------------------+----------------+
| published-draft_revise       | Published        | Draft/Revise     |                |
| _attorney_content            |                  | Attorney content |                |
+------------------------------+------------------+------------------+----------------+
| metadata_review-draft        | Metadata review  | Draft/revise     |                |
+------------------------------+------------------+------------------+----------------+
| metadata_review-copy_edit    | Metadata review  | Copy edit        |                |
+------------------------------+------------------+------------------+----------------+
| metadata_review-ready_to     | Metadata review  | Ready to review  |                |
| _review                      |                  |                  |                |
+------------------------------+------------------+------------------+----------------+
| metadata_review-published    | Metadata review  | Published        |                |
+------------------------------+------------------+------------------+----------------+
| metadata_review-plain        | Metadata review  | Plain language   |                |
| _language_review             |                  | review           |                |
+------------------------------+------------------+------------------+----------------+
| substantive_update-draft     | Sub. Update      | Draft            |                |
+------------------------------+------------------+------------------+----------------+
| substantive_update-copy_edit | Sub. Update      | Copy edit        |                |
+------------------------------+------------------+------------------+----------------+
| substantive_update-metadata  | Sub. Update      | Metadata review  |                |
| _review                      |                  |                  |                |
+------------------------------+------------------+------------------+----------------+
| substantive_update-plain     | Sub. update      | Plain language   |                |
| _language_review             |                  | review           |                |
+------------------------------+------------------+------------------+----------------+
| published-draft_review       | Published        | Draft review     | Migrate        |
+------------------------------+------------------+------------------+----------------+
| plain_language_review-draft  | Draft            | Plain language   |                |
|                              |                  | review           |                |
+------------------------------+------------------+------------------+----------------+
| plain_language_review-copy   | Plain language   | Copy edit        |                |
| _edit                        | review           |                  |                |
+------------------------------+------------------+------------------+----------------+
| plain_language_review-       | Plain language   | Metadata review  |                |
| metadata_review              |                  |                  |                |
+------------------------------+------------------+------------------+----------------+


Permissions
=================

The ilao_workbench module defines 4 permissions:

* publish without notification => users with this permission can publish without triggering an email notification to the content managers that they need to review the content
* receive workbench transition alerts => users with this permission will receive alerts when content is changed in some circumstances
* publish without review => can publish minor updates to the content automatically
* mark as substantive => can mark a revision as a substantive update

Access controls
================

The ilao_workbench module contains an access control such that:

* If content is marked "ready to review," only users with the publish without review permission can edit it.
* If content is marked "copy edit," only users who can transition from copy edit to plain language can edit it.

Sending notifications
======================

The ilao_workbench_workbench_moderation_transition function fires whenever there is a transition between states and calls _ilao_workbench_workbench_notifications to send notifications as follows:

* to any user with the 'receive workbench transition alerts' permission
* where the content type is either adrm or legal content
* the edit wasn't done anonymously (indication of a system update)
* if the new state is published, fires the rules component "rules_send_publish_notification"
* if the new state is ready to review, fires the rules component "rules_send_content_review_notification"
* if the new state is copy edit, fires the rules component "rules_send_content_copyedit_notification"

*Relies on Rules module*
 




