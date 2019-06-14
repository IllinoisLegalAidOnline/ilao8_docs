===================================
Drupal 8 OTIS API Implementation
===================================

Referral History API
======================
The referral API will provide referral history information between systems.

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-referral-history   | GET      | Loads a specific referral                         |
+------------------------+----------+---------------------------------------------------+
| get-referral-service   | GET      | Loads a specific referral history service         |
+------------------------+----------+---------------------------------------------------+
| create-referral-history| POST     | Creates a referral history entity                 |
+------------------------+----------+---------------------------------------------------+
| update-referral-history| POST     | Updates a referral history entity                 |
+------------------------+----------+---------------------------------------------------+

Organization API
==================

+------------------------+----------+---------------------------------------------------+
| Endpoint               | Method   | Description                                       |
+========================+==========+===================================================+
| get-organization-name- | GET      | Loads the name of the parent organization         |
| service-id             |          | by service id.                                    |
+------------------------+----------+---------------------------------------------------+
| get-organization-id-   | GET      | Loads the node id of the parent organization      |
| service-id             |          | by service id.                                    |
+------------------------+----------+---------------------------------------------------+




