===============================
Mailchimp Integration
===============================

We currently use Mailchimp integration to:

* Subscribe users to newsletter and blog subscriptions through the master list (these are sent out manually by staff)
* Send out the weekly and monthly eUpdates automatically

We are interested in expanding it to handle all transactional email through the website


User subscription integration
================================

All website users are added to the Master list and then added to the group that they belong to based on subscription:

* Blog
* Newsletter
* Weekly eUpdate
* Monthly eUpdate


Groups & Template configuration
===================================

We have configuration set that allows us to select:

* What group receives the weekly eUpdate (currently uses the weekly eUpdate group)
* What group receives the monthly eUpdate (currently uses the monthly eUpdate group)
* What template to use for the weekly eUpdate (currently uses the eupdate_weekly template)
* What template to use for the monthly eUpdate (currently uses the eupdate_weekly template)

.. warning:
   Check group segment is used for testing.  This is the only group that should ever get mail from staging, dev, or any local instance. We have PHP settings set up to ensure this.

eUpdates
==================
`Monthly example <https://us17.campaign-archive.com/?e=56139dc628&u=9690d96f7e71a177840ef4770&id=7e17e54aae>`_

`Weekly example <https://us17.campaign-archive.com/?e=56139dc628&u=9690d96f7e71a177840ef4770&id=30d22def4e>`_

Legal Content
---------------
Currently, the eUpdate displays legal content updates:

  * is of content type legal content (should be expanded to other legal content types)
  * is not tagged to be suppressed from search
  * is published
  * has a created date of [y] OR has a last substantive updated date within [y] where y is the date/time from the last eUpdate.
  * is grouped by primary legal category
  
.. note:
   The core views for this are in admin/structure/views/view/legal_content/  
  
More from the community
------------------------

 * Open job postings (keep)
 * Upcoming events (keep)
 * Open volunteer opportunities (deprecate)
 * Open internships/fellowships (deprecate)
 
   

