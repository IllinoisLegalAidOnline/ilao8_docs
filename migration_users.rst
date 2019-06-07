=============================
Users and user profiles
=============================

Roles
=======
We have more roles in Drupal 7 than we need to migrate over to Drupal 8.

+-------------------+-----------------------------------------+------------------------+
| Role              | Purpose                                 | Status                 |
+-------------------+-----------------------------------------+------------------------+
| Legal self-help   | For legal self-help center navigators   | Migrate                |
| center navigator  |                                         |                        |
+-------------------+-----------------------------------------+------------------------+
| Public member     | Default authenticated user role         | Delete*                |
+-------------------+-----------------------------------------+------------------------+
| Law student member| For law students; anyone registering w/ | Migrate                |
|                   | a .edu address receives this by default |                        |
+-------------------+-----------------------------------------+------------------------+
| Pro bono member   | For legal professionals outside of legal| Migrate                |
|                   | aid                                     |                        |
+-------------------+-----------------------------------------+------------------------+
| Legal aid member  | For employees of legal aid organizations| Migrate                |
+-------------------+-----------------------------------------+------------------------+
| Translator        | For external translators of content     | Migrate                |
+-------------------+-----------------------------------------+------------------------+
| Subject matter    | For approved content editors            | Migrate                |
| expert            |                                         |                        |
+-------------------+-----------------------------------------+------------------------+
| Intern            | For ILAO interns                        | Migrate                |
+-------------------+-----------------------------------------+------------------------+
| Staff             | For ILAO staff                          | Migrate                |
+-------------------+-----------------------------------------+------------------------+
| User Experience   |                                         | Delete                 |
+-------------------+-----------------------------------------+------------------------+
| Developer         | For developers                          | Delete                 |
+-------------------+-----------------------------------------+------------------------+
| Site architect    | Administrator role                      | Migrate but rename     |
|                   |                                         | Administrator          |
+-------------------+-----------------------------------------+------------------------+
| Content manager   | For ILAO content managers               | Migrate                |
+-------------------+-----------------------------------------+------------------------+

The public member role and the default authenticated user role should serve the same function.  As long as we can filter the people list on "has no role" then I don't think we need to preserve this.

Fields
========

We have many fields associated with users.  Different fields are tracked for different roles.  We currently have one registration form that shows/hides based on role.  I'd like to replace with multiple_registration module so it looks better.

+--------------------+--------------------------------+---------------------------------+
| Field              | Description                    | Status                          |
+====================+================================+=================================+
| field_user_type    | User-selected member type      |Replace w/ multiple-registration |
+--------------------+--------------------------------+---------------------------------+
| field_first_name   | Text; required for all roles   | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_last_name    | Text; required for all roles   | Migrate                         |               
| field_notification | List (text); required for all  | Migrate                         |
| _preferences       |                                |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_opt_in_sms   | Boolean; displays for all      | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_mobile_phone | Text                           | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_biography    | Long text; roles:              | Migrate                         |              
+--------------------+--------------------------------+---------------------------------+
| field_twitter      | Text                           | Delete                          |
| _account_name      |                                |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_gender       | Term reference (gender taxonomy| Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_year_born    | Integer                        | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_law_school   | Term reference (law schools)   | Migrate                         |
|                    | Law student members only       |                                 |
+--------------------+--------------------------------+---------------------------------+
| og_user_node       | Organization term reference    | Migrate*                        |
|                    | Legal aid members only         |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_areas_of     | Term reference to legal issues | Migrate                         |
| _expertise         | Some roles                     |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_areas_of     | Term references to legal issues| Migrate                         |
| _interest          | Some roles                     |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_newsletters  | List (text)                    | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_zipcodes     | Text                           | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_work_phone   | Telephone number               | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_website      | Boolean; participate in user   | Migrate                         |
| _improvement       | studies                        |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_internal     | Text                           | Migrate to field_job_title      |
| _title             | Staff and board only           |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_accept_terms | Boolean                        | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_company      | Text; pro bono only            | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_legal_aid    | Organization entity reference  | Migrate                         |
| _affiliation       |                                |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_job_title    | Text (select or other          | Migrate but fix                 |
+--------------------+--------------------------------+---------------------------------+
| field_location_ref | Location associated with user  | Migrate                         |
|                    | Legal aid and LSHC only        |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_work_address | Work address (Postal address)  | Migrate                         |
+--------------------+--------------------------------+---------------------------------+
| field_skills       | Term reference-skills taxonomy | Delete                          |
|                    | All but public members         |                                 |
+--------------------+--------------------------------+---------------------------------+
| field_languages    | Entity reference to languages  | Delete                          |
+--------------------+--------------------------------+---------------------------------+
| field_internal     | Term reference-internal org;   | Delete                          |
|                    | used to determine support tix  |                                 |
+--------------------+--------------------------------+---------------------------------+                                                    



