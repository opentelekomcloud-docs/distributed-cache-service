:original_name: TagManagement.html

.. _TagManagement:

Managing Tags
=============

Tags facilitate DCS instance identification and management.

You can add tags to an instance when creating it or add, modify, or delete tags on the details page of a created instance. Each instance can have a maximum of 20 tags.

A tag consists of a tag key and a tag value. :ref:`Table 1 <tagmanagement__table193611920984>` lists the tag key and value requirements.

.. _tagmanagement__table193611920984:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------------------+---------------------------------------------------------------------------------------------+
   | Parameter                         | Requirement                                                                                 |
   +===================================+=============================================================================================+
   | Tag key                           | -  Cannot be left blank.                                                                    |
   |                                   | -  Must be unique for the same instance.                                                    |
   |                                   | -  Cannot start or end with a space.                                                        |
   |                                   | -  Consists of a maximum of 128 characters.                                                 |
   |                                   | -  Can contain letters of any language, digits, spaces, and special characters \_.:=+-@     |
   |                                   | -  Cannot start with **\_sys\_**.                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------+
   | Tag value                         | -  Consists of a maximum of 255 characters.                                                 |
   |                                   | -  Can contain letters of any language, digits, spaces, and special characters ``_.:/=+-@`` |
   |                                   | -  Cannot start or end with a space.                                                        |
   +-----------------------------------+---------------------------------------------------------------------------------------------+

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.

4. Click the name of an instance.

5. Choose **Instance Configuration** > **Tags**.

   View the tags of the instance.

6. Perform the following operations as required:

   -  Add a tag

      a. Click **Add/Edit Tag**. You can create new tags by entering **Tag key** and **Tag value**.

         If you have created predefined tags, select a predefined pair of tag key and value. To view predefined tags or create tags, click **View predefined tags**. You will be directed to the TMS console.

      b. Click **OK**.

   -  Modify a tag

      Click **Add/Edit Tag**. In the displayed **Add/Edit Tag** dialog box, delete the desired key, add the key again, enter a new tag value, and click **Add**.

   -  Delete a tag

      In the row containing the tag to be deleted, click **Delete** in the **Operation** column. Then click **Yes**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
