===================
OTIS Permissions
===================

General Permissions
=====================

Triage rules and intake settings both rely on the organic groups module to affiliate an organization with the entity. However, they do so differently. 

Organic Group Permissions
==========================

In ILAO's ecosystem, each organization node is also an organic group.  The group includes roles for:

* member
* organization manager
* OAS manager

The OAS manager has permissions managed through organic groups that allow them to manage:

* locations
* location-services
* triage-rules

The organization manager has permissions to manage all of the above plus the organization profile.

Triage rules
--------------
Because of the built-in integration between nodes and organic group, triage rule access is automatically defined when a service is associated with the triage rules when creating or editing the triage rules.

.. warning::
   The code looks only at the first service added.  If triage rules were shared across organizations, this would not work.
   
Intake settings
---------------
Because intake settings are a custom entity, we had to manage the access via custom modules.

The ilao_intake_settings module manages access:

* if the ilao_organizations module is installed, that takes ownership of granting permissions
* if the ilao_organizations module is not installed, the user must have the manage all intake settings permission in the general user permissions tables

The ilao_organizations module uses the ilao_organization_is_oas_manager to check for access.

ilao_organization_is_oas_manager
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Located in ilao_organizations.module

Process:

* Loads the user entity of the currently logged in user
* Loads the organic groups associated with the user
* Checks to see if they are an OAS Manager of the organic group; returns True if they are
* Checks to see if they have the staff role in the general user roles (this should just be ILAO staff); returns TRUE if they do
* Returns FALSE otherwise.

.. warning:: 
   At first glance, it is unclear if this verifies that the user is the OAS manager for the specific organization whose intake settings are being edited.

Views Access Plugins
=========================
In order to grant appropriate access to intake settings and triage rules reports, we created custom views access plugins.  They are in the ilao_organizations module as included files:

* Is org or oas manager in the ilao_organizations_is_admin_views_access_plugin.inc file; checks to see if the current user has either the organization administrator or an OAS manager role for the group
* Is OAS manager in the ilao_organizations_is_oas_admin_views_access_plugin.inc file; checks to see if the current user has the OAS manager role for the group
* Is Org admin in the ilao_organizations_is_org_admin_views_access_plugin.inc file; checks to see if the current user has the organization manager role for the group
* Is OG member in the ilao_organizations_is_og_member_views_access_plugin.inc file; checks to see if the current user is a member of the specific group   
   

