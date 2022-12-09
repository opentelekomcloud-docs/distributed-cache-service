:original_name: dcs-faq-0730047.html

.. _dcs-faq-0730047:

Are Services Interrupted During Specification Modification?
===========================================================

You are advised to change the instance specifications during off-peak hours because specification modification has the following impacts:

-  **Impact of instance type changes:**

   -  From single-node to master/standby for a DCS Redis 3.0 instance:

      The instance cannot be connected for several seconds and remains read-only for about 1 minute.

   -  From master/standby to Proxy Cluster for a DCS Redis 3.0 instance:

      The instance cannot be connected and remains read-only for 5 to 30 minutes.

-  **Impact of capacity expansion and reduction:**

   -  Single-node and master/standby

      The DCS Redis 3.0, 4.0, or 5.0 instance cannot be connected for several seconds and remains read-only for about 1 minute.

      For capacity expansion, only the memory of the instance is expanded. The CPU processing capability is not improved.

      Data of single-node instances may not be retained because they do not support data persistence. After the scaling, check whether the data is complete and import data if required.

   -  Proxy Cluster

      The instance can be connected, but the CPU will be occupied and the latency will increase during data migration. During capacity expansion, new Redis Server nodes are added, and data is automatically balanced to the new nodes.

   -  Redis Cluster

      The instance can be connected, but the CPU usage and latency will increase during data migration. During capacity expansion, new Redis Server nodes are added, and data is automatically balanced to the new nodes.

   -  Backup records created before the capacity change cannot be restored.
