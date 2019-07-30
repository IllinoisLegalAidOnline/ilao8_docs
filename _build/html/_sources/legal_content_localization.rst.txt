======================================
Legal Content Localization
======================================

The custom module ckeditor_rsm creates a CKeditor plug in to add tags for local information.  The module:

* creates a button on the CKeditor
* when used, adds span tags to indicate what region (city, county, or zip code) the enclosed text should display for.  

.. code-block:: html

   <span county="Cook">In Cook county, you are allowed to do whatever you want</span>
   
In the above example, if the user is detected to be in Cook county, this text displays.  If they are not in Cook county, the snippet does not display.   

.. note:: Vishal wrote this module and has the most expertise on how the code works.
