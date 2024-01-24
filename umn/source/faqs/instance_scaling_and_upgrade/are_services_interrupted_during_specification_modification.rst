:original_name: dcs-faq-0730047.html

.. _dcs-faq-0730047:

Are Services Interrupted During Specification Modification?
===========================================================

You are advised to change the instance specifications during off-peak hours because specification modification has the following impacts:

-  **Impact of scaling:**

   -  Single-node and master/standby

      -  A DCS Redis 4.0/5.0/6.0 instance will be disconnected for several seconds and remain read-only for about 1 minute.
      -  A DCS Redis 3.0 instance will be disconnected and remain read-only for 5 to 30 minutes.
      -  For scaling up, only the memory of the instance is expanded. The CPU processing capability is not improved.
      -  Data of single-node instances may be lost because they do not support data persistence. After scaling, check whether the data is complete and import data if required.
      -  Backup records of master/standby instances cannot be used after scaling down.

   -  Cluster

      -  If the shard quantity is not decreased, the instance can always be connected, but the CPU usage will increase, compromising performance by up to 20%, and the latency will increase during data migration.
      -  During scaling up, new Redis Server nodes are added, and data is automatically balanced to the new nodes.
      -  Nodes will be deleted if the shard quantity decreases. To prevent disconnection, ensure that the deleted nodes are not directly referenced in your application.
      -  Ensure that the used memory of each node is less than 70% of the maximum memory per node of the new flavor. Otherwise, you cannot perform the scale-in.
      -  If the memory becomes full during scaling due to a large amount of data being written, scaling will fail. Modify specifications during off-peak hours.
      -  Scaling involves data migration. The latency for accessing the key being migrated increases. For a Redis Cluster instance, ensure that the client can properly process the **MOVED** and **ASK** commands. Otherwise, requests will fail.
      -  Before scaling, perform cache analysis to ensure that no big keys (>= 512 MB) exist in the instance. Otherwise, scaling may fail.
      -  Backup records created before scaling cannot be restored.

-  **Notes on changing the number of replicas of a DCS Redis instance:**

   Deleting replicas interrupts connections. If your application cannot reconnect to Redis or handle exceptions, you need to restart the application after scaling.
