=========================
Job content type
=========================

Notes
========
Our current platform uses organic groups to control ownership of a job and then has an intricate set of conditional fields that control supporting both internal and external organizations.  We don't support viewing organization profiles from job postings so this is probably unneeded.

Fields
========

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_my_org_or_ther         | Boolean; controls layout      | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_sponsoring_org_single  | Entity reference to org       | Delete              |
+------------------------------+-------------------------------+---------------------+
| field_organization_other     | Text                          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_address                | Postal address                | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_website                | Link                          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| title                        | Job title                     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_job_type               | Select list of job types      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| body                         | Long text;Job description     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_remote_allowed         | Boolean                       | Transform           |
+------------------------------+-------------------------------+---------------------+
|field_candidate_qualifications| Long text                     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_file                   | Unlimited files; attachments  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_depends_on_experience  | Boolean                       | Merge into          |
|                              |                               | compensation type   |
+------------------------------+-------------------------------+---------------------+
| field_compensation_low       | Integer                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_compensation_high      | Integer                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_compensation_type      | Select list                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_how_to_apply           | Long text                     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_open_until_filled      | Boolean                       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_deadline               | Date                          | Migrate             |
+------------------------------+-------------------------------+---------------------+


Changes
==========

* Make only the compensation low required rather than requiring a range
* Make the single checkbox boolean yes/no
* Add a note that all job postings come down after 45 days, regardless of deadline.
* Add a notification email to the sender at 40 days to remind them to renew their posting
* Add internship as an option in job type select
* Add fellowship as an option in job type select
* Depends on experience field is merged into compensation type


The remote allowed field is currently a yes/no.  Would be nice to offer fully remote, some remote allowed, no remote allowed.

.. note::
   ILAO will manually repost relevant internships as jobs.
   
   