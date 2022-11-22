:original_name: dcs-ug-0326014.html

.. _dcs-ug-0326014:

Deleting DCS Instances
======================

On the DCS console, you can delete one or multiple DCS instances at a time. You can also delete all instance creation tasks that have failed to run.

.. important::

   -  After a DCS instance is deleted, the instance data will also be deleted without backup. In addition, any backup data of the instance will be deleted. Therefore, download the backup files of the instance for permanent storage before deleting the instance.
   -  If the instance is in cluster mode, all cluster nodes will be deleted.

Prerequisites
-------------

-  The DCS instances you want to delete have been created.
-  The DCS instances you want to delete are in the **Running** or **Faulty** state.

Procedure
---------

Deleting DCS Instances

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. On the **Cache Manager** page, select one or more DCS instances you want to delete.

   DCS instances in the **Creating**, **Restarting**, **Upgrading**, **Resizing**, **Clearing data**, **Backing up**, or **Restoring** state cannot be deleted.

#. Choose **More** > **Delete** above the instance list.

#. In the displayed dialog box, click **Yes**.

   It takes 1 to 30 minutes to delete DCS instances.

   .. note::

      To delete a single instance, choose **Operation** > **More** > **Delete** in the same row as the instance.

Deleting Instance Creation Tasks That Have Failed to Run

#. Log in to the DCS console.

#. Click |image2| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. If there are DCS instances that have failed to be created, **Instance Creation Failures** is displayed above the instance list.

#. Click the icon or the number of failed tasks next to **Instance Creation Failures**.

   The **Instance Creation Failures** dialog box is displayed.

#. Choose failed instance creation tasks to delete.

   -  To delete all failed tasks, click **Delete All** above the task list.
   -  To delete a single failed task, click **Delete** in the same row as the task.

.. |image1| image:: /_static/images/en-us_image_0000001194403157.png
.. |image2| image:: /_static/images/en-us_image_0000001148603250.png
