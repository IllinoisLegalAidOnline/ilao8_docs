===============================
Translation
===============================

Content types that support translation
=======================================

* Legal content
* Basic pages(page)
* Blog posts (article)
* ADRM
* Events
* Location
* Location services
* Organization
* Site faq
* Surveys
* Toolbox
* Toolbox tool
* Toolbox tool step
* Triage rules
* Webform
* Portla main page

Current workflow
==================

The current workflow is a bit of a mess:

* Lingotek was installed to do automatic translation; it does not work correctly.
* We created some fields on content to track translations that entity translation provides equivalent fields.
* Our staff now copies and pastes fields from content into Google Docs, sends to a professional translator and then copies and pastes back into fields


Current customization
======================

On legal content, we added fields to better support translation:

* added a boolean field to indicate if the translation needs updated (duplicative of the flag translation as outdated)
* added a request translation field to allow staff to indicate that content should be translated (need to keep)

We created reports and rules to help with the workflow:

* When legal content and portal content is updated, a rule fires that sends an email to translationmgmt@illinoislegalaid.org if the translation outdated has been changed from false to true


Drupal 8
===========

Lingotek should not be migrated in any form.  ILAO custom fields that can be handled just as easily with core features should be migrated to the core fields

The translation management module should be installed and enabled with the ability to:

* use Google translate for automated translation (but this should only happen if the staff requests Google to translate it)
* create jobs and export as xliff files
* import xliff files back into the system





