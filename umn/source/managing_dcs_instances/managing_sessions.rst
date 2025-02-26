:original_name: dcs-ug-22121.html

.. _dcs-ug-22121:

Managing Sessions
=================

You can view the client connection information of an instance and disconnect clients.

This function is supported by DCS Redis 4.0 instances and later.

.. note::

   The session management page displays only the information about the external client connections. Information about the Web CLI connections is not displayed.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click a DCS instance to go to the details page.

#. Click the **Sessions** tab.

#. Select desired nodes and click the refresh icon on the right.

   .. note::

      -  For Proxy Cluster and read/write splitting instances, connections to proxy nodes are displayed. For single-node, master/standby, and Redis Cluster instances, connections to Redis Server nodes are displayed.
      -  On the right of the page, you can specify a Redis Server or proxy node to query, enter an address, update the query results, and set columns to display.
      -  For details about the meaning of each column in the query result, see https://redis.io/commands/client-list/.
      -  If you disable client IP pass-through for the instance, the value of **addr** is not the actual IP address of the client. Instead, the internal private network IP address **198.19.xxx.xxx** is displayed.
      -  After client IP pass-through is enabled, the value of **addr** of new connections is the actual IP address of the client.

#. Select connections to kill and click **Kill Selected** to disconnect the corresponding clients. You can also click **Kill All**.

   If a disconnected client can reconnect, it will be automatically reconnected after being disconnected.

#. To export sessions data, click **Export**. You can export all or selected data.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
