=====================
Event Content Type
=====================

Relies On:
============

Taxonomies:

* Audience
* Legal issues
* Event types

Custom modules:

* ilao_access : controls update access to allow the contact to edit the event.  Unclear if this is needed.

* ilao_events:  Most of this module is registration based and can go in the trash.


Fields
=========

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_start_date             | Date; with optional end date  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_sponsoring_organzation | Entity reference to OG        | Merge & Delete      |
+------------------------------+-------------------------------+---------------------+
| field_organization_other     | Text                          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_event_format           | Select list; in person, remote| Migrate             |
|                              | alert/notice                  |                     |
+------------------------------+-------------------------------+---------------------+
| field_address                | Postal address                | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_instructions           | Long text; event instructions | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_uses_registration      | Boolean                       | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_contact_else           | Boolean                       | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_contact_email          | Email                         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_speakers               | Field collection              | Replace             |
+------------------------------+-------------------------------+---------------------+
| field_audience               | Term reference to audience    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_issues           | Term reference to select      | Migrate             |
|                              | legal issues taxonomy terms   |                     |
+------------------------------+-------------------------------+---------------------+
| field_event_type             | Term reference to event types | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_event_recording        | Select list                   | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_has_mcle               | Boolean                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_mcle_hours             | Float; total hours of MCLE    | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_mcle_ethics_hours      | Float; ethics hours           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_archive_eligible_for   | Boolean                       | TBD                 |
| _mcle                        |                               |                     |
+------------------------------+-------------------------------+---------------------+
| field_email                  | Email; MCLE contact           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_email_for_questions    | Email; Question receiver for  | TBD                 |
|                              | archive CLE                   |                     |
+------------------------------+-------------------------------+---------------------+
| field_deadline               | Date; MCLE deadline           | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_attachments            | File; files for the event     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_registration_required  | Select                        | Migrate & Update    |
+------------------------------+-------------------------------+---------------------+ 
| field_register_or_buy_tickets| List; label for registration  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_legal_link             | Link; registration link       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_registration           |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_capacity               |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_waiting_list           |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_waiting_list_capacity  |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_registration_open      |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_send_reminder          |                               | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image field                   | Migrate as Media    |
+------------------------------+-------------------------------+---------------------+
                




Known Changes
==============

* We are not migrating entity registration or event registration.
* Eliminating the field_sponsoring_organization; the name of the organization should be copied into field_organization_other
* Speakers need to be replaced with a paragraphs bundle over field collection
* Field registration required should not have the ilao option

