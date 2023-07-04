:original_name: dcs-ug-210107001.html

.. _dcs-ug-210107001:

Managing Shards and Replicas
============================

This section describes how to query the shards and replicas of a DCS Redis 4.0/5.0/6.0 instance and how to manually promote a replica to master.

Currently, **this function is supported only by Redis Cluster DCS Redis 4.0 or 5.0 instances.**

-  A Redis Cluster instance has multiple shards. Each shard has one master and one replica by default. On the **Shards and Replicas** page, you can view the sharding information and manually switch the master and replica roles. For details about the number of shards corresponding to different instance specifications, see :ref:`Redis Cluster <cacheproxy>`.

Promoting a Replica to Master
-----------------------------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**. The **Cache Manager** page is displayed.

4. Click an instance.

5. Click the **Shards and Replicas** tab.

   The page displays all shards in the instance and the list of replicas of each shard.

6. Click |image2| to show all replicas of a shard.


   .. figure:: /_static/images/en-us_image_0000001322339434.png
      :alt: **Figure 1** Lists of shards and replicas

      **Figure 1** Lists of shards and replicas

   -  For a cluster instance, you can promote a replica in a shard to be master.

      a. Click **Promote to Master** in the row containing another replica which is in the "Replica" role.
      b. Click **Yes**.

.. |image1| image:: /_static/images/en-us_image_0000001241411631.png
.. |image2| image:: /_static/images/en-us_image_0000001241691605.png
