:original_name: RedisDifference.html

.. _RedisDifference:

Comparing Redis Versions
========================

When creating a DCS Redis instance, you can select the cache engine version and the instance type.

-  **Version**

   DCS supports Redis 3.0/4.0/5.0/6.0/7.0. The following table describes the differences between these versions.

   .. table:: **Table 1** Differences between Redis versions

      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Feature                                | Redis 3.0                                             | Redis 4.0 and Redis 5.0                                                             | Redis 6.0/7.0                                      |
      +========================================+=======================================================+=====================================================================================+====================================================+
      | Open-source compatibility              | Redis 3.0.7                                           | Redis 4.0.14 and 5.0.14, respectively                                               | Redis 6.2.7 and 7.2, respectively                  |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Instance deployment mode               | Based on VMs                                          | Containerized based on physical servers                                             | Containerized based on physical servers            |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Time required for creating an instance | 3-15 minutes, or 10-30 minutes for cluster instances. | 8 seconds                                                                           | 8 seconds                                          |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | QPS                                    | 100,000 QPS per node                                  | 100,000 QPS per node                                                                | 100,000 QPS per node                               |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Visualized data management             | Not supported                                         | Web CLI for connecting to Redis and managing data                                   | Web CLI for connecting to Redis and managing data  |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Instance type                          | Single-node, master/standby, and Proxy Cluster        | Single-node, master/standby, Proxy Cluster, read/write splitting, and Redis Cluster | Single-node, master/standby, and Redis Cluster     |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Scale-up or scale-down                 | Online scale-up and scale-down                        | Online scale-up and scale-down                                                      | Online scale-up and scale-down                     |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+
      | Backup and restoration                 | Supported for master/standby and cluster instances    | Supported for master/standby, read/write splitting, and cluster instances           | Supported for master/standby and cluster instances |
      +----------------------------------------+-------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------------+

   .. note::

      The underlying architectures vary by Redis version. Once a Redis version is chosen, it cannot be changed. For example, you cannot upgrade a DCS Redis 3.0 instance to Redis 4.0 or 5.0. If you require a higher Redis version, create a new instance that meets your requirements and then migrate data from the old instance to the new one.

-  **Instance type**

   Select from single-node, master/standby, read/write splitting, and cluster types. For details about their architectures and application scenarios, see :ref:`DCS Instance Types <dcs-pd-200312001>`.
