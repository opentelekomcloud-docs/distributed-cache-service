:original_name: dcs-ug-0312033.html

.. _dcs-ug-0312033:

Restoring a DCS Instance
========================

On the DCS console, you can restore backup data to a chosen DCS instance.

Prerequisites
-------------

-  At least one master/standby or cluster DCS instance is in the **Running** state.
-  A backup task has been run to back up data in the instance to be restored and the status of the backup task is **Succeeded**.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of the DCS instance to display more details about the DCS instance.

#. On the instance details page, click **Backups & Restorations**.

   A list of historical backup tasks is then displayed.

#. Click **Restore** in the same row as the chosen backup task.

#. Click **OK** to start instance restoration.

   Information in the **Description** text box cannot exceed 128 bytes.

   The **Restoration History** tab page displays the result of the instance restoration task.

   .. note::

      Instance restoration takes 1 to 30 minutes.

      While being restored, DCS instances do not accept data operation requests from clients because existing data is being overwritten by the backup data.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
