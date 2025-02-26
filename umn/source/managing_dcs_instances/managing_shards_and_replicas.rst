:original_name: dcs-ug-210107001.html

.. _dcs-ug-210107001:

Managing Shards and Replicas
============================

This section describes how to query the shards and replicas of a DCS Redis 4.0 or later instance and how to manually promote a replica to master.

Currently, **this function is supported only by master/standby, read/write splitting, and cluster DCS Redis 4.0 and later instances. DCS Redis 3.0 instances and single-node instances do not support this function.**

-  A master/standby or read/write splitting instance has only one shard with one master and one replica by default. You can view the sharding information on the **Shards and Replicas** page. To manually switch the master and replica roles, see :ref:`Performing a Master/Standby Switchover for a DCS Instance <dcs-ug-0312017>`.
-  A cluster instance has multiple shards. Each shard has two replicas by default. On the **Shards and Replicas** page, you can view the sharding information and manually switch the master and replica roles. For details about the number of shards corresponding to different instance specifications, see :ref:`Redis Cluster <cacheproxy>`.

Managing DCS Instance Shards and Replicas
-----------------------------------------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**. The **Cache Manager** page is displayed.

4. Click an instance.

5. Choose **Shards and Replicas**.

   The page displays all shards in the instance and the list of replicas of each shard.

6. Click |image2| to show all replicas of a shard.


   .. figure:: /_static/images/en-us_image_0000001322339434.png
      :alt: **Figure 1** Lists of shards and replicas (cluster)

      **Figure 1** Lists of shards and replicas (cluster)


   .. figure:: /_static/images/en-us_image_0000001941980352.png
      :alt: **Figure 2** Lists of shards and replicas (master/standby)

      **Figure 2** Lists of shards and replicas (master/standby)

   -  For a cluster instance, you can promote a replica in a shard to be master.

      a. Click **Promote to Master** in the row containing another replica which is in the "Replica" role.
      b. Click **Yes**.

   -  **Failover Priority** can be set for replicas for a master/standby or read/write splitting instance. **Remove IP Address** is supported in master/standby instances.

      Failover priority: If the master fails, the system will be automatically promoted to the replica with the highest priority you specified. If there are multiple replicas sharing the same priority, a selection and switch process will be performed in the internal system. Priority ranges from 0 to 100 in descending order. **0** indicates that the replica will never be automatically promoted, **1** indicates the highest priority, and **100** indicates the lowest priority.

      Remove IP address: If a master/standby instance has more than one replicas (excluding master), click **Remove IP Address** to remove the IP addresses of extra replicas. If a master/standby instance has only one replica, its IP address cannot be removed.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001241691605.png
