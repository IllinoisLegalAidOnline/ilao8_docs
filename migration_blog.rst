===========================
Migration Blog Posts
===========================

.. note::
   There is some internal confusion about the blog and whether it should be merged with legal content or remain a standalone content type.

Relies on
===========

* image (D8: media)
* AddThis (to be replaced with whatever new tool we are using to share with)


Fields
=========

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| title_field                  | Text; title                   | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_blog_category          | Term reference                | TBD                 |
+------------------------------+-------------------------------+---------------------+
| field_legal_topic            | Term reference to legal issues| Migrate             |
+------------------------------+-------------------------------+---------------------+
| body                         | Long text and summary         | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_image                  | Image                         | Migrate to media    |
+------------------------------+-------------------------------+---------------------+  
| field_tags                   | Term reference                | Do not migrate      |
+------------------------------+-------------------------------+---------------------+
| field_share                  | AddThis                       | Migrate based on    |
|                              |                               | new tools           |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_keyword   | Term reference                | Migrate             |
+------------------------------+-------------------------------+---------------------+
| field_lift_content_section   | Term reference                | Migrate             |
+------------------------------+-------------------------------+---------------------+
     

Known changes
===============
None known
