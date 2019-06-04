============================
Migrating Organization Data
============================

Drupal 7 Configuration
========================

Three content types:

* Organization
* Location
* Location Services

Relies on:

* Organic groups.  Organization nodes own location and location services nodes
* Conditional fields to show/hide field elements on the add/edit form
* Register preapproved to allow users from specific organizations to automatically receive the legal aid member permission when they register on the website.
* Office hours for setting hours.


Taxonomies in use:

* Legal issues
* Holidays
* Amenities
* Service types
* Intake populations
* Region


Custom modules and configuration:

.. note:: There is some outdated code in the modules that reference the user of inline entity forms that we tried to implement initially and then discontinued.

* ilao_organization_inheritance module ensures that data that exists in an upstream entity (organization or location) is copied to the downstream node (location or location services) when a user picks "Same [x] as [node type]" in the add/edit form

* ilao_organizations.  This module is kind of a hot mess of mixed functionality that mixes in code related to OTIS, the OTIS widget as well as organizational information.  I've added documentation within the module.  To be carried over to Drupal 8:

  * Copy postal to mailing address on organizations
  * Ensure organization names are unique to prevent duplicate organizations from being added
  * Ensure that fields for email domain and "doesn't provide services to the public" are only visible to staff and intern users
  * Group access integration for views
  * Handling pre-approval for users who register with an email address that matches an associated email domain
  
* ilao_locations.  There is a lot of legacy mess in this module as well.
  * Custom form submit to ensure that organization inheritance happens
  * Custom logic for changing the page title to reference the parent organization of the location (this has been passed in via url reference)
  * Custom validation
    
* ilao-service.  Again a lot of unnecessary legacy details.  Key functions that will carry over include:
  * Custom logic for changing the page title
  * Node presave to ensure that data is save correctly
  * Custom validation

  

