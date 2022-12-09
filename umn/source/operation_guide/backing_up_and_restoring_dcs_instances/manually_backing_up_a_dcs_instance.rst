:original_name: dcs-ug-0312032.html

.. _dcs-ug-0312032:

Manually Backing Up a DCS Instance
==================================

You need to manually back up data in DCS instances in a timely manner. This section describes how to manually back up data in master/standby instances using the DCS console.

By default, manually backed up data is permanently retained. If backup data is no longer in use, you can delete it manually.

Prerequisites
-------------

At least one master/standby DCS instance is in the **Running** state.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of the DCS instance to display more details about the DCS instance.

#. On the instance details page, click **Backups & Restorations**.

#. Click **Create Backup**.

#. Select a backup file format.

   Only DCS Redis 4.0 and 5.0 instances support backup file format selection.

#. In the **Create Backup** dialog box, click **OK**.

   Information in the **Description** text box cannot exceed 128 bytes.

   .. note::

      Instance backup takes 10 to 15 minutes. The data added or modified during the backup process will not be backed up.

.. |image1| image:: /_static/images/en-us_image_0000001148603242.png
