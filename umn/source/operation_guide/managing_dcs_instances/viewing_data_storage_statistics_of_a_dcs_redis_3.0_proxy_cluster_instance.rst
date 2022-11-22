:original_name: dcs-ug-0312029.html

.. _dcs-ug-0312029:

Viewing Data Storage Statistics of a DCS Redis 3.0 Proxy Cluster Instance
=========================================================================

You can view the data storage statistics of all nodes of a DCS Redis 3.0 Proxy Cluster instance. If data storage is unevenly distributed across nodes, you can scale up the instance or clear data.

You can only view data storage statistics of DCS Redis 3.0 Proxy Cluster instances. Instances of other types, for example, master/standby, only have one node, and you can view the used memory on the instance details page.

.. note::

   A Redis Cluster instance has multiple storage nodes. You can check the data storage statistics of a Redis Cluster instance in its Redis Server monitoring data.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS Redis cluster instance to view the basic information.

#. Click the **Node Management** tab.

   The data volume of each node in the cluster instance is displayed.

   When the data storage capacity of a node in a cluster is used up, you can scale up the instance according to :ref:`Modifying DCS Instance Specifications <dcs-ug-0326011>`.

.. |image1| image:: /_static/images/en-us_image_0000001194523043.png
