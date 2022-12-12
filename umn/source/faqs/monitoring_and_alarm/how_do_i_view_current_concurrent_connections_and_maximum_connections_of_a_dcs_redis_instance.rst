:original_name: dcs-faq-0427070.html

.. _dcs-faq-0427070:

How Do I View Current Concurrent Connections and Maximum Connections of a DCS Redis Instance?
=============================================================================================

Viewing Concurrent Connections of a DCS Redis Instance
------------------------------------------------------

The number of connections received by a DCS instance is a metric that is monitored by Cloud Eye. For details on how to view metrics, see :ref:`Viewing DCS Monitoring Metrics <dcs-ug-0312045>`.

On the Cloud Eye console, find the **Connected Clients** metric. Click |image1| to view monitoring details on an enlarged graph.

Specify a time range to view the metric in a specific monitoring period. For example, you can select a 10-minute period to view the number of connections received during the period. On the graph, you can view the trend and the total number of connections received during the period.

On the Cloud Eye console, you can also view other monitoring metrics of your DCS instances, for example:

-  CPU Usage
-  Memory Usage
-  Used Memory
-  Ops per Second

Viewing or Modifying the Maximum Connections of an Instance
-----------------------------------------------------------

When creating an instance on the console, you can view the default maximum number of connections and the limit that can be configured.

After an instance is created, you can view or change the value of **maxclients** (the maximum number of connections) on the **Parameters** page of the DCS console. (This parameter cannot be modified for Proxy Cluster instances.)

.. |image1| image:: /_static/images/en-us_image_0000001383077054.png
