:original_name: RedisDifference.html

.. _RedisDifference:

Comparing Redis Versions
========================

When creating a DCS Redis instance, you can select the cache engine version and the instance type.

-  **Version**

   DCS supports Redis 3.0, 4.0, and 5.0. The following table describes the differences between these versions.

   .. table:: **Table 1** Differences between Redis versions

      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Feature                                | Redis 3.0                                             | Redis 4.0 and Redis 5.0                                                                                                                                                                          |
      +========================================+=======================================================+==================================================================================================================================================================================================+
      | Instance deployment mode               | Based on VMs                                          | Containerized based on physical servers                                                                                                                                                          |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Time required for creating an instance | 3-15 minutes, or 10-30 minutes for cluster instances. | 8 seconds                                                                                                                                                                                        |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | QPS                                    | 100,000 QPS per node                                  | 100,000 QPS per node                                                                                                                                                                             |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Instance type                          | Single-node, master/standby, and Proxy Cluster        | Single-node, master/standby and Redis Cluster                                                                                                                                                    |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Instance total memory                  | Ranges from 2 GB, 4 GB, 8 GB, to 1024 GB.             | Regular specifications range from 2 GB, 4 GB, 8 GB, to 1024 GB. Small specifications, such as 128 MB, 256 MB, 512 MB, and 1 GB, are also available for single-node and master/standby instances. |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scale-up or scale-down                 | Online scale-up and scale-down                        | Online scale-up and scale-down                                                                                                                                                                   |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Backup and restoration                 | Supported for master/standby and cluster instances    | Supported for master/standby and cluster instances                                                                                                                                               |
      +----------------------------------------+-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The underlying architectures vary by Redis version. Once a Redis version is chosen, it cannot be changed. For example, you cannot upgrade a DCS Redis 3.0 instance to Redis 4.0 or 5.0. If you require a higher Redis version, create a new instance that meets your requirements and then migrate data from the old instance to the new one.

-  **Instance type**

   Select from single-node, master/standby, and cluster types. For details about their architectures and application scenarios, see :ref:`DCS Instance Types <dcs-pd-200312001>`.