===============================
Legal content comments
===============================

..note :: The big decision with comments is its integration with ratings and whether we keep the 5 star rating or move to a simpler helpful/not helpful rating.

Fields
=======

+------------------------------+-------------------------------+---------------------+
| Field                        | Description                   | Status              |
+==============================+===============================+=====================+
| field_rating                 | Fivestar rating tied          | Migrate             |
+------------------------------+-------------------------------+---------------------+
| author                       | System field                  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| subject                      | System field                  | Migrate             |
+------------------------------+-------------------------------+---------------------+
| comment_body                 | Long text; Body of comment    | Migrate             |
+------------------------------+-------------------------------+---------------------+

Considerations
===============

* Staff and intern users must be able to reply to comments without needing to leave a rating
* Ratings need to be aggregated at the node level.  See ilao_legal_articles' function ilao_legal_articles_comment_publish


         