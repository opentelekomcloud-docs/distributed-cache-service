:original_name: dcs-ug-190926001.html

.. _dcs-ug-190926001:

Viewing Redis Slow Logs
=======================

Redis logs queries that exceed a specified execution time. You can view the slow query log on the DCS console to identify performance issues.

For details about the commands, visit the `Redis official website <https://redis.io/commands>`__.

Configure the slow log with the following parameters:

-  **slowlog-log-slower-than**: The maximum time allowed, in microseconds, for command execution. If this threshold is exceeded, Redis will log the command. The default value is **10,000**. That is, if command execution exceeds 10 ms, the command will be logged.
-  **slowlog-max-len**: The maximum allowed number of slow logs that can be logged. The default value is **128**. That is, if the number of slow logs exceeds 128, the earliest record will be deleted to make room for new ones.

For details about the configuration parameters, see :ref:`Modifying Configuration Parameters <dcs-ug-0312024>`.

.. note::

   You can view the slow log of a Proxy Cluster DCS Redis 3.0 instance only if the instance is created after October 14, 2019. If the instance was created earlier, contact technical support to upgrade it. The upgrade adds the slow log function to the console, and does not affect services.

Viewing Slow Logs on the Console
--------------------------------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS instance.

#. Choose **Slow Log**.

#. Select a start date and an end date to view the slow log within the specified period.

   .. note::

      For details about the commands, visit the `Redis official website <https://redis.io/commands>`__.


   .. figure:: /_static/images/en-us_image_0281049655.png
      :alt: **Figure 1** Slow query log of an instance

      **Figure 1** Slow query log of an instance

.. |image1| image:: /_static/images/en-us_image_0000001194523041.png
