=================
IICLE Proxy
=================

IICLE content is any legal content that has a paragraph block of type "iicle" attached to it.

Because of ILAO's agreement with IICLE, we must use a proxy server to display IICLE content.  The proxy server grabs the entire web page from IICLE, including stylesheet information and renders it on our site.

.. note:: 
   Unlike must of ILAO's code, the IICLE proxy code is contained within a feature.  See features/ilao_f_iicle_proxy

Relies on
===========

* Proxy contributed module
* ilao_f_iicle_proxy feature with the proxy_processor_ilao.inc file


Configuration
===============

.. warning::
   The current proxy module throws an error when trying to access configuration.
   
+----------------------------------------+-----------------------------------+
| Variable                               | Value                             |
+========================================+===================================+
| proxy_flood_interval                   | 3600                              |
+----------------------------------------+-----------------------------------+
| proxy_flood_control                    | 1                                 |
+----------------------------------------+-----------------------------------+
| proxy_processor_proxy_processor_ilao   | 1                                 |
+----------------------------------------+-----------------------------------+
| proxy_processor_proxy_processor_proxify| 0                                 |
| _urls                                  |                                   |
+----------------------------------------+-----------------------------------+
| proxy_whitelist_control                | 1                                 |
+----------------------------------------+-----------------------------------+
| proxy_whitelist_domains                | iicle.com                         |
+----------------------------------------+-----------------------------------+

   
   
   



   