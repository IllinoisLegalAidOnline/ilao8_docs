==================================
Toolboxes and related structures
==================================

.. _migration_toolboxes:

Content types and custom entities
===================================

The toolboxes platform relies on 4 content types:

* portal_main_page
* toolboxes
* toolbox_tool
* toolbox_tool_step

See also `End user toolbox documentation <https://ilaodocs.readthedocs.io/en/latest/toolboxes_admin.html>`_

.. toctree::
   :maxdepth: 1
   :caption: See also:

   toolboxes_fields
   toolboxes_paragraphs
   toolboxes_entities
   

Relies on
============

Currently relies on:

* Contributed modules:

  * token_custom allows us to create custom snippets within legal content
  * paragraphs
  * voting_api
  * fivestar
  * block_reference
  * rules
  * views
  * twilio

  
* Custom modules:

  * ilao_portal_pages
  * ilao_toolbox
  * ilao_f_node_toolbox
  * ilao_f_node_toolbox_tool
  * ilao_f_node_toolbox_tool_step

* Taxonomies:

  * legal_issues

.. note::
   The ilao_toolbox defines database schemas and metadata controllers for:
   
   * toolbox_usage
   * toolbox_user
   * toolbox_tickler
   
  

Functionality
===============
The key functionality can be found in our custom modules.  

.. warning:: ILAO really needs to rethink the workflow for the toolboxes and simplify them down, perhaps eliminating the toolbox completely and just using the tool and associated steps.  

ilao_toolbox_entity_info
-------------------------
Exposes the entity properties for toolbox_user, toolbox_usage, and toolbox_tickler for integration with views.

ilao_toolbox_form_alter
------------------------
Form alter applies to all 3 toolbox content types to:
* require the revision log

For the toolbox content type only:
* hides best bet field for toolboxes unless the user is a content manager or site architect (this will need to be updated for new roles)
* adds validation and submit fields for best bet fields


ilao_toolbox_alter_encourage_user_help
----------------------------------------
Deprecate

Basic functionality overview for users
---------------------------------------

When a user starts with a toolbox page:

* 

When a user starts a tool page:

* We need to know if they've already started this tool in the current session
* We need to know if they've already started this tool outside of the current session (either by having a record tied to a user ID or by entering a return code)


When a user starts on a tool step page:
* We need to know if they've already started this tool in the current session
* We need to know if they've already started this tool outside of the current session (either by having a record tied to a user ID or by entering a return code)
* We need to warn them to start at the first step in the process





Open issues
============

* Toolboxes currently must be tied to a portal
* Toolboxes have no QA protocols or workflow integration
* Return codes are unwieldy and difficult to use
* Some users may come into the site already in the middle of the process


