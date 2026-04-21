:original_name: dcs-faq-0603001.html

.. _dcs-faq-0603001:

Why Is the Rejected Connections Metric Displayed?
=================================================

If the **Rejected Connections** metric is displayed, check if the number of connected clients exceeds the maximum allowed number of connections of the instances.

.. note::

   The **Rejected Connections** metric of data nodes can be checked only for master/standby, cluster, and read/write splitting DCS Redis 4.0 and later instances.

-  To check the maximum number of connections, go to the **Instance** > **Parameters** tab page of the instance and check the **maxclients** metric. (Currently, read/write splitting instances do not have this parameter. To query the maximum connections of them, see :ref:`DCS Instance Specifications <en-us_topic_0054235835>`.)
-  To check the current number of connections, go to the **Performance Monitoring** tab page of the instance and check the **Connected Clients** metric.

If the current number of connections reaches the upper limit, you can adjust the value of **maxclients**. If the value of **maxclients** can no longer be increased, consider adding shards.
