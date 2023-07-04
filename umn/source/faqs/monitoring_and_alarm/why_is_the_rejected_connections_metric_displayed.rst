:original_name: dcs-faq-0603001.html

.. _dcs-faq-0603001:

Why Is the Rejected Connections Metric Displayed?
=================================================

If the **Rejected Connections** metric is displayed, check if the number of connected clients exceeds the maximum allowed number of connections of the instances.

-  To check the maximum allowed number of connections, go to the **Parameters** tab page of the instance and check the value of the **maxclients** parameter. (Proxy Cluster instances do not have this parameter. You can view the maximum number of connections on the instance creation page.)
-  To check the current number of connections, go to the **Performance Monitoring** tab page of the instance and check the **Connected Clients** metric.

If the current number of connections reaches the upper limit, you can adjust the value of **maxclients**. If the value of **maxclients** can no longer be increased, increase the instance specifications.
