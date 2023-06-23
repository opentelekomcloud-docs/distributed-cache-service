:original_name: dcs-pd-0916001.html

.. _dcs-pd-0916001:

Redis 3.0 Instance Specifications
=================================

This section describes DCS Redis 3.0 instance specifications, including the total memory, available memory, maximum number of connections allowed, maximum/assured bandwidth, and reference performance.

The following metrics are related to the instance specifications:

-  Used memory: You can check the memory usage of an instance by viewing the **Memory Usage** and **Used Memory** metrics.
-  Maximum connections: The maximum number of connections allowed is the maximum number of clients that can be connected to an instance. To check the number of connections to an instance, view the **Connected Clients** metric.
-  QPS represents queries per second, which is the number of commands processed per second.

   .. note::

      -  Single-node, master/standby, and Proxy Cluster types are available.
      -  Only the x86 architecture is supported. The Arm architecture is not supported.

Single-Node Instances
---------------------

For each single-node DCS Redis instance, the available memory is less than the total memory because some memory is reserved for system overheads, as shown in :ref:`Table 1 <dcs-pd-0916001__table2399016819>`.

.. _dcs-pd-0916001__table2399016819:

.. table:: **Table 1** Specifications of single-node DCS Redis 3.0 instances

   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Total Memory | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |              |                  |                                  |                           |                       |                                           |
   | (GB)         | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +==============+==================+==================================+===========================+=======================+===========================================+
   | 2            | 1.5              | 5000/50,000                      | 42/512                    | 50,000                | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 4            | 3.2              | 5000/50,000                      | 64/1536                   | 100,000               | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8            | 6.8              | 5000/50,000                      | 64/1536                   | 100,000               | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16           | 13.6             | 5000/50,000                      | 85/3072                   | 100,000               | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32           | 27.2             | 5000/50,000                      | 85/3072                   | 100,000               | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64           | 58.2             | 5000/60,000                      | 128/5120                  | 100,000               | dcs.single_node                           |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Master/Standby Instances
------------------------

For each master/standby DCS Redis instance, the available memory is less than that of a single-node DCS Redis instance because some memory is reserved for data persistence, as shown in :ref:`Table 2 <dcs-pd-0916001__table1521627154210>`. The available memory of a master/standby instance can be adjusted to support background tasks such as data persistence and master/standby synchronization.

.. _dcs-pd-0916001__table1521627154210:

.. table:: **Table 2** Specifications of master/standby DCS Redis 3.0 instances

   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Total Memory | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |              |                  |                                  |                           |                       |                                           |
   | (GB)         | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +==============+==================+==================================+===========================+=======================+===========================================+
   | 2            | 1.5              | 5000/50,000                      | 42/512                    | 50,000                | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 4            | 3.2              | 5000/50,000                      | 64/1536                   | 100,000               | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8            | 6.4              | 5000/50,000                      | 64/1536                   | 100,000               | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16           | 12.8             | 5000/50,000                      | 85/3072                   | 100,000               | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32           | 25.6             | 5000/50,000                      | 85/3072                   | 100,000               | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64           | 51.2             | 5000/60,000                      | 128/5120                  | 100,000               | dcs.master_standby                        |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Proxy Cluster Instances
-----------------------

In addition to larger memory, cluster instances feature more connections allowed, higher bandwidth allowed, and more QPS than single-node and master/standby instances.

.. table:: **Table 3** Specifications of Proxy Cluster DCS Redis 3.0 instances

   +---------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Specification | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |               |                  |                                  |                           |                       |                                           |
   | (GB)          | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +===============+==================+==================================+===========================+=======================+===========================================+
   | 64            | 64               | 90,000/90,000                    | 600/5120                  | 500,000               | dcs.cluster                               |
   +---------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 128           | 128              | 180,000/180,000                  | 600/5120                  | 500,000               | dcs.cluster                               |
   +---------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 256           | 256              | 240,000/240,000                  | 600/5120                  | 500,000               | dcs.cluster                               |
   +---------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 512           | 512              | 480,000/480,000                  | 600/5120                  | 500,000               | dcs.cluster                               |
   +---------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
