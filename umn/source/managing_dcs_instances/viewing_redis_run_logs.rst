:original_name: dcs-ug-1009001.html

.. _dcs-ug-1009001:

Viewing Redis Run Logs
======================

You can create run log files on the DCS console to collect run logs of DCS Redis instances within a specified period. After the logs are collected, you can download the log files to view the logs.

This function is supported by DCS Redis 4.0 instances and later.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS instance.

#. Click **Run Logs**.

#. Click **Create Log File**.

   For a master/standby, read/write splitting, or cluster instance, logs will be collected from the specified shard and replica. If the instance is the single-node type, logs of the only node of the instance will be collected.

   Select the collection period and click **OK**.

#. After the log file is successfully collected, click **Download** to download it.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
