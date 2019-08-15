==============================
Toolbox-related entities
==============================

 
Toolbox user
================

Tracks each instance of a toolbox experience.  If a user returns either logged in or with a return code, the system should pull the related toolbox experience rather than create a new record.

+------------------------------+-------------------------------+---------------------+
| Property                     | Description                   | Status              |
+==============================+===============================+=====================+
| toolbox_id                   | Serial; unique toolbox user ID| Migrate             |
+------------------------------+-------------------------------+---------------------+
| uid                          | int; uid of the user          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| return_code                  | text; return code to come back| Migrate             |
+------------------------------+-------------------------------+---------------------+
| created                      | date; date record was created | Migrate             |
+------------------------------+-------------------------------+---------------------+
| changed                      | date; date record was changed | Migrate             |
+------------------------------+-------------------------------+---------------------+

Toolbox usage
===============

Tracks progress through a toolbox experience.  Relates to the toolbox user entity on toolbox_id.

+------------------------------+-------------------------------+---------------------+
| Property                     | Description                   | Status              |
+==============================+===============================+=====================+
| toolbox_usage_id             | Serial; unique identifier     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| toolbox_id                   | Serial; unique toolbox user ID| Migrate             |
+------------------------------+-------------------------------+---------------------+
| entity_type                  | text; entity type (node)      | Migrate             |
+------------------------------+-------------------------------+---------------------+
| bundle                       | text; bundle of the entity    | Migrate             |
|                              | type (toolbox, tool, step)    |                     |
+------------------------------+-------------------------------+---------------------+
| created                      | date; timestamp record created| Migrate             |
+------------------------------+-------------------------------+---------------------+
| changed                      | date; timestamp record changed| Migrate             |
+------------------------------+-------------------------------+---------------------+
| status                       | text; started, saved, or      | Migrate             |
|                              | completed                     |                     |
+------------------------------+-------------------------------+---------------------+



Toolbox Tickler
================

Defined in ilao_toolbox module.

+------------------------------+-------------------------------+---------------------+
| Property                     | Description                   | Status              |
+==============================+===============================+=====================+
| tickler_id                   | Serial; unique ID             | Migrate             |
+------------------------------+-------------------------------+---------------------+
| uid                          | Int; uid of user sent tickler | Migrate             |
+------------------------------+-------------------------------+---------------------+
| format                       | Text; format of the tickler   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| entity_id                    | int; NID of tool step         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| subject                      | text; subject of email sent   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| message                      | text; message sent            | Migrate             |
+------------------------------+-------------------------------+---------------------+
| receiver                     | text; email/phone message sent| Migrate             |
|                              | to                            |                     |
+------------------------------+-------------------------------+---------------------+
| created                      | date; date tickler sent       | Migrate             |
+------------------------------+-------------------------------+---------------------+
| changed                      | date; date record updated     | Migrate             |
+------------------------------+-------------------------------+---------------------+
| parent_entity                | int; nid of the parent entity | Migrate             |
+------------------------------+-------------------------------+---------------------+
| language                     | text; language code of the    | Migrate             |
|                              | page when viewed              |                     |
+------------------------------+-------------------------------+---------------------+




