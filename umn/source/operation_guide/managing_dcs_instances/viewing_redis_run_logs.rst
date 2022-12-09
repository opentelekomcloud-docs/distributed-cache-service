:original_name: dcs-ug-1009001.html

.. _dcs-ug-1009001:

Viewing Redis Run Logs
======================

You can create run log files on the DCS console to collect run logs of DCS Redis instances within a specified period. After the logs are collected, you can download the log files to view the logs.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS instance.

#. Click the **Run Logs** tab.

#. Click **Create Log File**.

   If the instance is the master/standby or cluster type, you can specify the shard and replica whose run logs you want to collect. If the instance is the single-node type, logs of the only node of the instance will be collected.

.. |image1| image:: /_static/images/en-us_image_0000001148443514.png
