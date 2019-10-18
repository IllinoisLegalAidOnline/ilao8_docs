==========================
SEO Settings
==========================

This includes:

* Metatags
* Path aliases
* URL redirects

Metatags
============

Settings:

* We output meta tags for all pages, whether or not specific settings are implement
* We do not use default language values
* We load the module's default configuration
* We cache meta tag output

Maximum Lengths:

* Basic description: 380 characters
* Twitter card title: 70 characters
* Twitter card description: 200 characters

Metatag Defaults
------------------

.. note::
  
   * OG: Open Graph and is used for Facebook primarily.
   * Global defaults are used if more specific options are not set
   * Keywords are not used by search engines, even if provided
   * [node:title] is not translatable but [node:title-field] is
   * Node:summary refers to the summary in the body field, where used.

+------------------------+----------------------+------------------------------------+
| Content Type           | Metatag              | Default                            |
+========================+======================+====================================+
| Global default         | Page title           | [current-page:title] \\ [site:name]|
+------------------------+----------------------+------------------------------------+
| Global default         | Description          | empty                              |
+------------------------+----------------------+------------------------------------+
| Global default         | Image                | empty                              |
+------------------------+----------------------+------------------------------------+
| Global default         | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Global default         | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Global default         | OG: Site name        | empty                              |
+------------------------+----------------------+------------------------------------+
| Global default         | OG: Page URL         | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Global default         | hreflang             | empty                              |
+------------------------+----------------------+------------------------------------+
| Global default         | Site Twitter         | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Global default         | Twitter page URL     | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Global default         | Title                | current-page:title                 |
+------------------------+----------------------+------------------------------------+
| Global home page       | Title                | Site:name                          |
+------------------------+----------------------+------------------------------------+
| Global home page       | Description          | Manually entered on site           |
+------------------------+----------------------+------------------------------------+
| Global home page       | Abstract             | Manually entered on site           |
+------------------------+----------------------+------------------------------------+
| Global home page       | Keywords             | Manually entered on site           |
+------------------------+----------------------+------------------------------------+
| Global home page       | OG:Content type      | Website                            |
+------------------------+----------------------+------------------------------------+
| Global home page       | OG:Page url          | site:url                           |
+------------------------+----------------------+------------------------------------+
| Global home page       | OG:Content title     | site:name                          |
+------------------------+----------------------+------------------------------------+
| Global home page       |OG:Content description| site:slogan                        |
+------------------------+----------------------+------------------------------------+
| Node default           | Page title           | [node:title] \\ [site:name]        |
+------------------------+----------------------+------------------------------------+
| Node default           | Description          | [node:summary]                     |
+------------------------+----------------------+------------------------------------+
| Node default           | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Node default           | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Node default           | OG:Content type      | Empty                              |
+------------------------+----------------------+------------------------------------+
| Node default           | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Node default           | OG: Content title    | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Node default           | OG: Description      | Empty                              |
+------------------------+----------------------+------------------------------------+
| Node default           | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Node default           | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Node default           | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Node default           | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Node default           | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter title        | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter description  | [node:summary]                     |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Node default           | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Page title           | [node:title-field] \\ [site:name]  |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Description          | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | OG:Content type      | Article (including blog)           |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | OG: Content title    | [node:title-field] \\ [site:name]  |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | OG: Description      | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter title        | [node:title-field] | [site:name]   |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter description  | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| ADRM Content           | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Event                  | Page title           | [node:title] \\ [site:name]        |
+------------------------+----------------------+------------------------------------+
| Event                  | Description          | [node:summary]                     |
+------------------------+----------------------+------------------------------------+
| Event                  | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Event                  | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Event                  | OG:Content type      | Activity                           |
+------------------------+----------------------+------------------------------------+
| Event                  | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Event                  | OG: Content title    | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Event                  | OG: Description      | Empty                              |
+------------------------+----------------------+------------------------------------+
| Event                  | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Event                  | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Event                  | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Event                  | Hreflang (polish)    | empty (needs fixed)                |
+------------------------+----------------------+------------------------------------+
| Event                  | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter title        | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter description  | [node:summary]                     |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Event                  | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Page title           | [node:title-field] \\ [site:name]  |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Description          | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Legal Content          | OG:Content type      | Article (including blog)           |
+------------------------+----------------------+------------------------------------+
| Legal Content          | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Legal Content          | OG: Content title    | [node:title-field]                 |
+------------------------+----------------------+------------------------------------+
| Legal Content          | OG: Description      | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Legal Content          | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter title        | [node:title-field] \\ [site:name]  |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter description  | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Legal Content          | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Location               | Page title           | [node:field-sponsoring-org-single: |
|                        |                      | title]: [node:title] \\ [site:name]|
+------------------------+----------------------+------------------------------------+
| Location               | Description          | [node:field-sponsoring-org-single  |
|                        |                      | :summary]                          |
+------------------------+----------------------+------------------------------------+
| Location               | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Location               | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Location               | OG:Content type      | Government                         |
+------------------------+----------------------+------------------------------------+
| Location               | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Location               | OG:Page title        | [node:field-sponsoring-org-single: |
|                        |                      | title]: [node:title] \\ [site:name]|
+------------------------+----------------------+------------------------------------+
| Location               | OG: Description      | [node:field-sponsoring-org-single  |
|                        |                      | :summary]                          |
+------------------------+----------------------+------------------------------------+
| Location               | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Location               | OG: street address   | [field_work_address:thoroughfare]  |
+------------------------+----------------------+------------------------------------+
| Location               | OG: Locality         | [field_work_address:locality]      |
+------------------------+----------------------+------------------------------------+
| Location               | OG: Region           | [field_work_address:admin-area]    |
+------------------------+----------------------+------------------------------------+
| Location               | OG: Postal/Zip code  | [field_work_address:postal-code]   |
+------------------------+----------------------+------------------------------------+
| Location               | OG: Country          | [field_work_address:country]       |
+------------------------+----------------------+------------------------------------+
| Location               | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Location               | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Location               | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Location               | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Location               | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Location               | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Location               | Twitter:Page title   | [node:field-sponsoring-org-single: |
|                        |                      | title]: [node:title] \\ [site:name]|
+------------------------+----------------------+------------------------------------+
| Location               | Twitter: Description | [node:field-sponsoring-org-single  |
|                        |                      | :summary]                          |
+------------------------+----------------------+------------------------------------+
| Location               | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Location               | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Page title           | [node:field-hero-title]            |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Description          | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | OG:Content type      | Article (including blog)           |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | OG: Content title    | [node:field-hero-title]            |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | OG: Description      | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter title        | [[node:field-hero-title]           |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter description  | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Portal Main Page       | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Page title           | [node:title-field] \\ [site:name]  |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Description          | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Toolbox                | OG:Content type      | Empty                              |
+------------------------+----------------------+------------------------------------+
| Toolbox                | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Toolbox                | OG: Content title    | [node:title-field]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox                | OG: Description      | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox                | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter title        | [node:title-field]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter description  | [node:field-meta-description]      |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Page title           | [node:title] \\ [site:name]        |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Description          | [node:field-purpose-description]   |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Canonical URL        | current-page:url:absolute          |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Shortlink URL        | current-page:url:unaliased         |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | OG:Content type      | Article                            |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | OG: Page URL         | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | OG: Content title    | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | OG: Description      | [node:field-purpose-description]   |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | OG: image            | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | X-default            | [node:source:url]                  |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Hreflang (english)   | [node:url-en]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Hreflang (polish)    | [node:url-pl]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Hreflang (spanish)   | [node:url-es]                      |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Twitter account      | @ilao                              |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Twitter page URL     | [current-page:url:absolute]        |
+------------------------+----------------------+------------------------------------+
| Toolbox tool           | Twitter title        | [node:title]                       |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter description  | [node:field-purpose-description]   |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter image url    | [node:field_image]                 |
+------------------------+----------------------+------------------------------------+
| Toolbox                | Twitter alt text     | Empty                              |
+------------------------+----------------------+------------------------------------+

Metatags for Legal Issue Category and Subcategory Pages
----------------------------------------------------------
These pages are just taxonomy term pages and use the taxonomy metatag defaults.

+------------------------+-----------------------------------------------------------+
|  Metatag               | Default                                                   |
+========================+===========================================================+
| Page title             | [term:name] | [site:name]                                 |
+------------------------+-----------------------------------------------------------+
| Description            | [term:description]                                        |
+------------------------+-----------------------------------------------------------+
| OG: Content Type       | none                                                      |
+------------------------+-----------------------------------------------------------+
| OG: Page URL           | [current-page:url:absolute]                               |
+------------------------+-----------------------------------------------------------+
| OG: Content title      | [current-page:title]                                      |
+------------------------+-----------------------------------------------------------+
| OG: Description        | [term:description]                                        |
+------------------------+-----------------------------------------------------------+
| X-Default              | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| hreflang (English)     | [site:url-root][current-page:url:relative]                |
+------------------------+-----------------------------------------------------------+
| hreflang (Spanish)     | [site:url-root]/es[current-page:url:relative]             |
+------------------------+-----------------------------------------------------------+
| hreflang (Polish)      | [site:url-root]/pl[current-page:url:relative]             |
+------------------------+-----------------------------------------------------------+
| Twitter card type      | Summary (default)                                         |
+------------------------+-----------------------------------------------------------+
| Twitter creator        | @ilao                                                     |
+------------------------+-----------------------------------------------------------+
| Twitter: Page URL      | [current-page:url:absolute]                               |
+------------------------+-----------------------------------------------------------+
| Twitter: Content title | [current-page:title]                                      |
+------------------------+-----------------------------------------------------------+
| Twitter: Description   | [term:description]                                        |
+------------------------+-----------------------------------------------------------+
| Twitter: image         | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| Twitter: alt text      | Empty                                                     |
+------------------------+-----------------------------------------------------------+

Metatag for Views
--------------------

We use views as pages to display specific information.

+------------------------+-----------------------------------------------------------+
|  Metatag               | Default                                                   |
+========================+===========================================================+
| Page title             | [view:title] | [site:name]                                |
+------------------------+-----------------------------------------------------------+
| Description            | [view:description]                                        |
+------------------------+-----------------------------------------------------------+
| OG: Content Type       | none                                                      |
+------------------------+-----------------------------------------------------------+
| OG: Page URL           | [current-page:url:absolute]                               |
+------------------------+-----------------------------------------------------------+
| OG: Content title      | [current-page:title]                                      |
+------------------------+-----------------------------------------------------------+
| OG: Description        | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| X-Default              | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| hreflang (English)     | Empty (probably needs reviewed)                           |
+------------------------+-----------------------------------------------------------+
| hreflang (Spanish)     | Empty (probably needs reviewed)                           |
+------------------------+-----------------------------------------------------------+
| hreflang (Polish)      | Empty (probably needs reviewed)                           |
+------------------------+-----------------------------------------------------------+
| Twitter card type      | Summary (default)                                         |
+------------------------+-----------------------------------------------------------+
| Twitter creator        | @ilao                                                     |
+------------------------+-----------------------------------------------------------+
| Twitter: Page URL      | [current-page:url:absolute]                               |
+------------------------+-----------------------------------------------------------+
| Twitter: Content title | [current-page:title]                                      |
+------------------------+-----------------------------------------------------------+
| Twitter: Description   | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| Twitter: image         | Empty                                                     |
+------------------------+-----------------------------------------------------------+
| Twitter: alt text      | Empty                                                     |
+------------------------+-----------------------------------------------------------+

Path Aliases
==============

Settings
----------

* The - is our separator which replaces spaces and punctuation.
* All characters are changed to lower case
* Maximum alias length is 100 characters
* Maximum component in the alias is 100 characters
* Transliterates prior to creating alias (replaces accented characters to acceptable characters)
* Removes common strings: a, an, as, at, before, but, by, for, from, is, in, into, like, of, off, on, onto, per, since, than, the, this, that, to, up, via, with
* Removes punctuation
 

Content paths
----------------
These are the default patterns.  They can, and in some instances, have been overwritten.

+------------------------+-----------------------------------------+-----------------+
| Content Type           | Pattern                                 | Language        |
+========================+=========================================+=================+
| ADRM                   | legal-information/[node:title]          | All             |
+------------------------+-----------------------------------------+-----------------+
| Basic Pages            | No default pattern                      | All             |
+------------------------+-----------------------------------------+-----------------+
| Blog posts             | About/our-work/blog/[node:title]        | All             |
+------------------------+-----------------------------------------+-----------------+
| Event                  | for-legal-professionals/calendar/[node: | All             |
|                        | title]                                  |                 |
+------------------------+-----------------------------------------+-----------------+
| Job Posting            | for-legal-professionals/job-postings/   | All             |
|                        | [node:title]                            |                 |
+------------------------+-----------------------------------------+-----------------+
| Legal Content          | legal-information/[node:title-field]    | English         |
+------------------------+-----------------------------------------+-----------------+
| Legal Content          | informacje-prawne/[node:title-field]    | Polish          |
+------------------------+-----------------------------------------+-----------------+
| Legal Content          | informacion-legal/[node:title-field]    | Spanish         |
+------------------------+-----------------------------------------+-----------------+
| Location               | organizations/location/[node:title]     | All             |
+------------------------+-----------------------------------------+-----------------+
| Location Services      | organizations/locations/services/       | All             |
|                        | [node:title]                            |                 |
+------------------------+-----------------------------------------+-----------------+
| Organization           | organizations/[node:title]              | All             |
+------------------------+-----------------------------------------+-----------------+
| Portal Main Page       |[node:field_subdomain]/[node:title-field]| English         |
+------------------------+-----------------------------------------+-----------------+
| Portal Main Page       | [node:field_subdomain]/pl-              | Polish          |
|                        | [node:title-field]                      |                 |
+------------------------+-----------------------------------------+-----------------+
| Portal Main Page       | [node:field_subdomain]/es-              | Spanish         |
|                        | [node:title-field]                      |                 |
+------------------------+-----------------------------------------+-----------------+
| Site FAQ               | site-faq/[node:title-field]             | All             |
+------------------------+-----------------------------------------+-----------------+
| Toolbox                | legal-information/toolboxes/            | English         |
|                        | [node:title-field]                      |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox                | informacje-prawne/toolboxes/            | Polish          |
|                        | [node:title-field]                      |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox                | informacion-legal/toolboxes/            | Spanish         |
|                        | [node:title-field]                      |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox step           | legal-information/toolboxes/            | English         |
|                        | [node:field-tool:title]/[node:title]    |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox step           | informacje-prawne/toolboxes/            | Polish          |
|                        | [node:field-tool:title]/[node:title]    |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox step           | informacion-legal/toolboxes/            | Spanish         |
|                        | [node:field-tool:title]/[node:title]    |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox tool           | legal-information/toolboxes/[node:field | English         |
|                        | ]-toolbox:title-field]/[node:title]     |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox tool           | informacje-prawne/toolboxes/[node:field | Polish          |
|                        | ]-toolbox:title-field]/[node:title]     |                 |
+------------------------+-----------------------------------------+-----------------+
| Toolbox tool           | informacion-legal/toolboxes/[node:field | Spanish         |
|                        | ]-toolbox:title-field]/[node:title]     |                 |
+------------------------+-----------------------------------------+-----------------+
| Triage Rules           | get-legal-help/triage-rules/[node:nid]  | All             |
+------------------------+-----------------------------------------+-----------------+


Known issues
--------------

* Legal Self-Help Centers use a different path of /counties/[county name].  This makes it impossible to regenerate organization, location, location services.
* Path aliases are automatically changed when new titles are created.  This breaks Google analytics data.  





