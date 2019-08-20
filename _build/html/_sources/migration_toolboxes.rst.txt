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
The ilao_toolbox module provides the functionality to:

* Set a record when a user starts a new toolbox, tool, or tool step.
* Updates records when a user completes a toolbox, tool or tool step.  When a user completes the last step in a tool, then the tool is marked complete.  When a user completes every step in every tool, the toolbox is marked complete.
* Gathers a user's history based on their UID or a return code
* Generates return codes
* Warns users who come into a process in the middle that they need to review the rest
* Warns users who have skipped tests
* Schedules ticklers

  * Determines when, who, and where to send ticklers
  * Alters tickler emails
  * Invokes rules to execute tickler sending
  
* Manages returning users with options to:

  * Enter a return code on the home page to come back where the left off
  
    * Displays the form
    * Validates the form
    * Displays a message and provides a my return block
  * See a list of their toolboxes on their dashboard if they are logged in

* Manages toolbox selection

  * Builds out toolbox selector forms on portal pages by taking all the toolboxes in a portal and building a form
  * Builds out a toolbox "My issues" page where users can start or save toolboxes they selected in the toolbox selector form
  
The ilao_portal module provides the functionality to:  

  * Builds out a form on toolbox pages that list all of the tools in a toolbox for the user to pick which tools they want to start
  * Builds out a tool "My issues" page from the tool selection form on a toolbox page so that users can start or save tools they selected.
  * Create toolbox user and toolbox usage entry
  





Open issues
============

* Toolboxes currently must be tied to a portal
* Toolboxes have no QA protocols or workflow integration
* Return codes are unwieldy and difficult to use; replace this with account login
* Some users may come into the site already in the middle of the process
* See User testing report
* There are so many problems with these



