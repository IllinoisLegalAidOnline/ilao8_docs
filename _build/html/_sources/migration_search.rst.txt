=======================
Search migration
=======================

Current search set up
=======================

Current search settings rely on ApacheSolr modules and Acquia Search:

* apachesolr
* apachesolr_attachments
* apachesolr_exclude_node
* apachesolr_multilingual
* apachesolr_nan
* apachesolr_paragraphs
* apachesolr_views

As well as custom modules:

* ilao_search
* ilao_search_synonyms

And a custom best bet field attached to certain content types.

Configuration
================

.. note::
   The search feature contains configuration data, which is not documented in full below.  For nodes that use paragraphs, those paragraph should be indexed.  Multilingual search is also required.

The following content types are included in the search:

* Attorney desk reference module (ADRM)
* Basic pages
* Blog posts
* Events
* Internship/fellowships (deprecated in Drupal 8)
* Job postings
* Legal content
* Portal main pages
* Site FAQs
* Toolboxes


Attachments are also included in the search:

* ADRM, as part of parent entity 
* Event, attachments as separate entity (Deprecate in Drupal 8)
* Job posting, as part of parent entity
* Legal content, as part of parent entity
* Basic page, change to as part of parent entity
* Portal main page, as part of parent entity
* Toolboxe, as part of parent entity

Not-a-node pages

We use the not-a-node to index pages that are not nodes.  These include:
* form-library view
* get-legal-help main page
* legal self-help library view

Custom functionality
======================

ilao_search
-------------

The ilao_search module alters search queries so that:

* Guides are weighted heavier than other types of content
* If the search term contains forms, easy forms are weighted higher than other types of content, including Guides (which are still weighted higher than other forms)
* If the search term contains videos, videos are weighted higher than other types of content, including Guides (which are still weighted higher than other forms)
* remove stop words from queries (see the module for a list of stop words)
* add in or replace any defined synonyms (see the ilao_search_synonyms documentation below)

It also provides functionality to:

* highlight search terms
* strip out languages and Add rating text added by the fivestar and language modules

ilao_search_synonyms
----------------------

The search synonyms module relies on the search synonym taxonomy.  

The search synonym taxonomy contains:

* name is the string to look for in a search query
* description is the string to add or replace in the search query
* field_synonym_type, which defines the type of synonym:
  * replace, which replaces the name with the description
  * expand, which adds the description to the name

.. note::
   Examples
   
   For the search query i received a notice of forcible entry and detainer: if the taxonomy defines forcible entry and detainer as a name with eviction as the description, a type set for replace would result in a query of I received a notice of eviction and with add would result in a query of I received a notcie of forcible entry and detainer, eviction.
   

Best Bets
----------

In the current iteration, best bets are available on legal content types to promote these to the top of search queries that exactly match the best bet

.. note::
   Example: A legal content node is marked as a best bet for "op"; a user searching for op would see that node as the #1 result regardless of the actual Solr scoring.
   
Best Bets:

* are found in the ilao_legal_articles module
* do not allow duplicates across node.  Only 1 node can be a best bet for a search term

      

