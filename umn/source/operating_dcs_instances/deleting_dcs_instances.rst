:original_name: dcs-ug-0326014.html

.. _dcs-ug-0326014:

Deleting DCS Instances
======================

On the DCS console, you can delete one or multiple DCS instances at a time. You can also delete all instance creation tasks that have failed to run.

Notes and Constraints
---------------------

-  DCS instances already exist. They are in the **Running** or **Faulty** state.
-  Deleted DCS instances as well as the data in these instances and the backup files cannot be recovered. Exercise caution when performing this operation. To retain data backups, before deleting instances, download and save their backups locally.
-  If the instance is in cluster mode, all cluster nodes will be deleted.

Procedure
---------

Deleting DCS Instances

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Select one or more DCS instances to be deleted and choose **Delete** above.

   To delete a single instance, choose **More** > **Delete** in the **Operation** column in the row containing the instance.

#. Click **Yes** to delete the instance.

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

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
