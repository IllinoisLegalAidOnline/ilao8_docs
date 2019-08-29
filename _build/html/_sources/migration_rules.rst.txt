===================
Custom Rules
===================

Rules to be deleted
=====================

* all inactive rules
* support ticket response - legal help (spanish)
* test og
* content updated by advocates (currently emails stephanie)
* create ticket for sent email
* email link to registration to contact of event
* email link to registration to creator of event
* email site architect on landing page creation
* Notify content team on edit
* Route support requests
* Save service practice area from legal category
* Stop registrations
* Subscribe Community engagement users to Opportunity node type
* Subscribe to bugs
* Subscribe users to support ticket - Admin
* Subscribe users to support ticket - Bugs
* Subscribe users to support ticket - Community
* Subscribe users to support ticket - Fundraising
* Subscribe users to support ticket - Intern
* Subscribe users to support ticket - Live Help
* Subscribe users to support ticket - Media
* Subscribe users to support ticket - UX
* Subscribe users to support ticket - YPB
* Subscribe UX users to FAQ node type
* Support ticket response - Account
* Support ticket response - Closing message
* Support ticket response - General redirect
* Support ticket response - legal help
* Support ticket response - LSHC redirect
* test
* ticket comment state defaults
* ticket comment client defaults
* ticket comment assignee defaults
* ticket comment priority defaults


Content Management Rules
==========================
.. note::
   * Can the re-translation rules be combined?
   
.. warning:: 
   If we delete the field-translation-outdated field and go with the core fields, the retrnaslation rules would need to be updated
   
Portal Content needs re-translated
--------------------------------------

Triggers:  after updating existing content type Portal main page
When: field-translation-outdated is true and the prior value wasn't true
Then:
Sends an HTML email to translationmgmt@illinoislegalaid.org with the subject of "Translation needs updated: node:title]" and a body of [node:title] (Node ID:  [node:nid]) has been flagged as needing its translations updated. 

.. warning:: 
   If we delete the field-translation-outdated field and go with the core fields, this rule needs updated
   
Content needs re-translated
----------------------------
Triggers:  after updating existing content type Legal content
When: field-translation-outdated is true and the prior value wasn't true
Then:
Sends an HTML email to translationmgmt@illinoislegalaid.org with the subject of "Translation needs updated: node:title]" and a body of [node:title] (Node ID:  [node:nid]) has been flagged as needing its translations updated. 

Notify legal comments
----------------------
Triggers:  when a new comment is saved
Condition: User is not anonymous
Then:  Sends an email to contentteam@illinoislegalaid.org with message of <p>A new comment by [comment:name]/[comment:mail] was just posted</p>
[comment:body]
<p>The comment can be found here:  [comment:url]</p>

.. todo::
   Should not trigger if the user has the staff role
   
Unpublish inappropriate comments
---------------------------------
Triggers: when a comment is flagged as inappropriate
Condtion:  count of inappropriate flags is 3 or more
Action: Unpublishes the comment   
   
   
   
Send mail on creating events and indicates recording
------------------------------------------------------
Triggers:  When saving a new event
When:  User does not indicates that they do not want an event recorded
Then: Sends an email to all users with the content manager role with a subject of [node:title]: Event recording notification and a body of he following event on [node:field-start-date:value] is set to be recorded. Please follow up with the sponsoring organization. Event details: [node:url]

.. todo::
   Should send to the contnet managers gmail account, not role-based
   
Send mail on updating events and indicates recording
-----------------------------------------------------
Triggers:  When updating an event
When:  User does not indicates that they do not want an event recorded and this and previously had indicated that they did not want the event recorded
Then: Sends an email to all users with the content manager role with a subject of [node:title]: Event recording notification and a body of he following event on [node:field-start-date:value] is set to be recorded. Please follow up with the sponsoring organization. Event details: [node:url]

.. todo::
   Should send to the contnet managers gmail account, not role-based
   
   
Send mail on adrm content update
----------------------------------
Triggers:  When an ADRM content is updated
Conditions:  The user does not have the content manager role; the user has the legal aid member or SME role
Action:  Sends email to all users with the content manager role
with a subject line of Attorney manual [node:title]
and subject of: The attorney manual [node:title] has been updated by [node:current-revision-author-name]. Please review: [node:url]
      
   

User Management Rules
======================

Law students get pro bono automatically
-----------------------------------------
Triggers:  After saving a new user account
Condition:  Email address contains .edu
Then:  Adds the role of Law student member to account

Add user to group based on email
-----------------------------------
Triggers:  After updating an existing user account
Condition:  User has legal aid member role AND email is not empty
Then: no action

.. warning::
   Need to evaluate
   
Email upon validating account
--------------------------------- 
Purpose is to get user to complete a user testing demographics survey

Triggers: When user logs in for the first time
Then: Send an HTML email with a subject of "Help improve IllinoisLegalAid.org"
and a body of "Thank you for expressing an interest in participating in user research activities to help improve IllinoisLegalAid.org. Please take <a href="https://www.surveymonkey.com/r/?sm=0dJuQigsoARhzLV8oPf3EmVTgBKyM664pn2IwhSkZbU_3D" rel="noopener" target="_blank">this short survey</a>, so that we know which types of user research opportunities to share with you. If you are no longer interested in participating, log in to IllinoisLegalAid.org and update your preferences. Thanks for your time!"

.. warning::
   This should check that the user opted in to user test but doesn't

Legal Aid Member Role Organization Grant
-----------------------------------------
Purpose is to associate a legal aid user with an organization when they create or update their account

Triggers:  User updates an existing account or saves a new account
When:  Legal aid affiliation field is not empty AND user is not a group member AND user has the legal aid member role OR (current user is ILAO staff and email domain matches an organization domain
Actions:  Add the user to the organic group of the organization associated with the organization domain

Relies on:  ilao_user_utilities to define the condition.

Legal self help center navigator Role Organization Grant
----------------------------------------------------------

Purpose is to associate a legal aid user with an organization when they create or update their account

Triggers:  User updates an existing account or saves a new account
When:  User has the legal self help center role
Actions:  Add the user to the organic group of the organization associated with the organization domain

.. note:: Why are these 2 organization grants so different?

Revoke OG memberships if Legal self-help center navigator Role is lost
------------------------------------------------------------------------
Triggers; when an existing user account is updated
When: user had the LSHC role and now does not
Then: Revokes OG memebership in LSHC organization and display a message on screen that says Revoked membership in [og-user-node-list:title] group for [account:name]

Revoke OG memberships if Legal aid member Role is lost
--------------------------------------------------------
Triggers; when an existing user account is updated
When: user had the legal aid member role and now does not
Then: Revokes OG memebership in LSHC organization and display a message on screen that says Revoked membership in [og-user-node-list:title] group for [account:name]

   
Block anonymous access to user profiles
-----------------------------------------

Triggers: User account page is viewed   
When:  Current user has the anonymous role
Then: Redirect to node/85641 (access denied)

.. warning::
   URL may change with migration
   
OTIS-related Rules
=====================
Send Email to Site Architect upon updating Intake Settings
------------------------------------------------------------
Triggers:  when an intake settings entity is created or updated
Condition: User is not a site architect or anonymous
Then Sends an HTML email with a subject of Intake Settings updated or added at [site:name] and a body of: <p>[site:current-user] has added or updated the following Intake Settings <a href="/admin/intake/[oas-intake-settings:intake-settings-id]/edit">[oas-intake-settings:name]</a>.</p>

.. todo::
   Rule needs cleaned in Drupal 7 to send to otissupport@illinoislegalaid.org rather than site architect.


Send Email to Site Architect upon updating Triage Rules
--------------------------------------------------------
Trigger:  When an existing triage rule content is updated
Condition: And the user does not have the site architect role
Then:  Sends an html email to otissupport with a subject of Triage rules updated or added at [site:name] and body of Please edit the triage rules for node [node:nid] to enable the translation settings:
1) Add translations for each language
2) Enable string translation in the webform
3) Go to translate interface and filter on webform localization and add the translations using Google translate. 

.. todo::
   Rule needs cleaned in Drupal 7 to reflect only edited triage rules
   
Rule Components
=================
Rule plugins
-------------
The following are all added and defined by the Scheduler contributed module:

* Set scheduled publishing date
* Set scheduled unpublishing date
* Remove scheduled publishing date
* Remove scheduled unpublishing date

Action plugins
---------------- 
Do not migrate:  
* Create email ticket record 
* Support client mapping


Potential problem with eTransfers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sends an html email to site architects with a subject of "Potential problem: No etransfers in 2 days" and body of "The system hasn't recorded any online intakes being transferred to a CMS in 2 days. Please check the system."

Potential problem with surveys
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sends an html email to site architects with a subject of "Potential problem: [surveys:title] hasn't been collecting data." and a body of "The following survey [surveys:title] at [surveys:url] has not had a completed survey in 3 days. Please check the system."

.. todo:: 
   Evaluate whether this is needed in light of surveys generally

Content management notifications
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
These 3 action plugins send emails to users when content changes workbench states and are fired in the ilao_workbench module.  They plugins accept 3 variables:

* the roles list of who to send the email to
* the node that was edited
* the user who made the edits

Roles that receive these are any that have the "receive workbench transition alerts" permission.

Send content copy edit notification  
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sends an email to all users of the provided roles with a subject of "[node:title] is ready for copy edit" and body of:

.. code-block:: php

   The <a href="[node:url]">[node:title]</a> has been updated and is ready for copy edit
   The content, [<a href="[node:url]">[node:title]</a> has been edited and is <a 
   href="[node:edit-url]">ready for review</a>. The content was updated by [user:name]. 


Send content review notification  
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sends an email to all users of the provided roles with a subject of "[node:title] is ready for review" and body of:

.. code-block:: php

   The <a href="[node:url]">[node:title]</a> has been updated and is ready to be reviewed.   
   The content, [<a href="[node:url]">[node:title]</a> has been edited and is 
   <a href="[node:edit-url]">ready for review</a>. The content was updated by [user:name].  

Send publish notificationn  
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Sends an email to all users of the provided roles with a subject of "An unreviewed update to [node:title] has been published." and body of:

.. code-block:: php

   [user:name] just published a revision for <a href="[node:url]">[node:title]</a> on the 
   website.  This revision was not reviewed by ILAO staff prior to publication.
   
Send ticklers
----------------
There are 2 components that are used by the ilao_toolbox module to send tickler messages.

Send email on ticklr
^^^^^^^^^^^^^^^^^^^^^^
Sends a tickler email for a toolbox tool step to a specific user and logs the email sent to the toolbox tickler entity.

Send sms on tickler
^^^^^^^^^^^^^^^^^^^^^^
Sends an sms to a number over Twilio and logs the sms sent to the toolbox tickler entity
   
   
Rules in Code
=================

ilao_events module
--------------------
Invokes the registration_settings_created event.  Do not migrate

ilao_sms_surveys
--------------------
Invokes the rules component rules_potential_problem_with_surveys as part of a cron call

ilao_toolbox
---------------

* Has custom action defined (create_new_toolbox_tickler_entity)
* Custom code schedules tickler messages

ilao_user_utilities
----------------------
* Defines custom actions for first time login and domain check
* Invokes the first time login event

ilao_workbench
-----------------
Invokes rules component based on the workbench state:
* rules_send_publish_notification
* rules_send_content_review_notification
* rules_send_content_copyedit_notification

end

   

   
