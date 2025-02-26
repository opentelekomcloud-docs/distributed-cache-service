:original_name: dcs-ug-221220.html

.. _dcs-ug-221220:

Managing Users
==============

You can create read-only and read/write users to control access permissions.

Prerequisites
-------------

This function is supported only by DCS Redis 4.0 and 5.0 instances.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click an instance.

#. Choose **User Management** in the navigation pane.

   Default user: **default**

#. Click **Create User** to create a normal user.

   .. note::

      -  A maximum of 18 users can be created for an instance.
      -  If **Password Protected** is enabled for a DCS Redis instance, only the default user can be used.
      -  To use a normal user, click **Reset Password** in the row that contains the default user to disable **Password Protected** for the default user.

#. Specify the **Username** and **Description**. Select **Read-only** or **Read/Write**. Specify the **Password** and confirm it.

#. Click **OK**.

   .. note::

      A normal user connects to an instance with password **{username:password}**.


   .. figure:: /_static/images/en-us_image_0000002010627429.png
      :alt: **Figure 1** Managing users

      **Figure 1** Managing users

More Operations
---------------

The following operations can be performed on normal users.

.. table:: **Table 1** Operations

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                         | Description                                                                                                                                                                        |
   +===================================+====================================================================================================================================================================================+
   | Changing the password             | Locate the row that contains the desired normal user and click **Change Password** in the **Operation** column.                                                                    |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resetting the password            | If password is forgot, locate the row that contains the normal user and click **Reset Password** in the **Operation** column.                                                      |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Modifying permissions             | Locate the row that contains the normal user. Choose **More** > **Modify Permission** in the **Operation** column. The **Read-only** or **Read/Write** permissions can be granted. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Edit description                  | Locate the row that contains the normal user. Choose **More** > **Edit Description** in the **Operation** column.                                                                  |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deleting users                    | Locate the row that contains the normal user. Choose **More** > **Delete** in the **Operation** column.                                                                            |
   |                                   |                                                                                                                                                                                    |
   |                                   | The default user cannot be deleted.                                                                                                                                                |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Batch deleting users              | Select the normal users to be deleted and click **Delete** above the list.                                                                                                         |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000002010628601.png
