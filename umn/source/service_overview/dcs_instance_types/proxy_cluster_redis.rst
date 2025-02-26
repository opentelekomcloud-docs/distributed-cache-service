:original_name: CacheCluster.html

.. _CacheCluster:

Proxy Cluster Redis
===================

DCS for Redis provides Proxy Cluster instances, which use Linux Virtual Server (LVS) and proxies to achieve high availability. Proxy Cluster instances have the following features:

-  The client is decoupled from the cloud service.
-  They support millions of concurrent requests, equivalent to Redis Cluster instances.
-  A wide range of memory specifications adapt to different scenarios.

.. note::

   -  A Proxy Cluster instance can be connected in the same way that a single-node or master/standby instance is connected, without any special settings on the client. You can use the IP address of the instance, and do not need to know or use the proxy or shard addresses.

Proxy Cluster DCS Redis 4.0/5.0 Instances
-----------------------------------------

Proxy Cluster DCS Redis 4.0/5.0 instances are built based on open-source Redis 4.0/5.0 and compatible with `open source codis <https://github.com/CodisLabs/codis>`__. They provide multiple large-capacity specifications ranging from 4 GB to 1024 GB and .

:ref:`Table 1 <cachecluster__table3552324111>` lists the number of shards corresponding to different specifications. You can customize the shard size when creating an instance. Currently, the number of shards and replicas cannot be customized. By default, each shard has two replicas.

**Memory per shard = Instance specification/Number of shards**. For example, if a 48 GB instance has 6 shards, the size of each shard is 48 GB/6 = 8 GB.

.. _cachecluster__table3552324111:

.. table:: **Table 1** Specifications of Proxy Cluster DCS Redis 4.0/5.0 instances

   ============ ======= ====== =====================
   Total Memory Proxies Shards Memory per Shard (GB)
   ============ ======= ====== =====================
   4 GB         3       3      1.33
   8 GB         3       3      2.67
   16 GB        3       3      5.33
   24 GB        3       3      8
   32 GB        3       3      10.67
   48 GB        6       6      8
   64 GB        8       8      8
   96 GB        12      12     8
   128 GB       16      16     8
   192 GB       24      24     8
   256 GB       32      32     8
   384 GB       48      48     8
   512 GB       64      64     8
   768 GB       96      96     8
   1024 GB      128     128    8
   ============ ======= ====== =====================


.. figure:: /_static/images/en-us_image_0000001433519397.png
   :alt: **Figure 1** Architecture of a Proxy Cluster DCS Redis 4.0/5.0 instance

   **Figure 1** Architecture of a Proxy Cluster DCS Redis 4.0/5.0 instance

Architecture description:

-  **VPC**

   All server nodes of the cluster instance run in the same VPC.

   .. note::

      The client and the cluster instance must be in the same VPC, and the instance whitelist must allow access from the client IP address.

-  **Application**

   The client used to access the instance.

   DCS Redis instances can be accessed through open-source clients. For details about accessing DCS instances in different languages, see :ref:`Accessing an Instance <dcs-ug-0916002>`.

-  **VPC endpoint service**

   You can configure your DCS Redis instance as a VPC endpoint service and access the instance at the VPC endpoint service address.

   The IP address of the Proxy Cluster DCS Redis instance is the address of the VPC endpoint service.

-  **ELB**

   The load balancers, which are deployed in cluster HA mode.

-  **Proxy**

   The proxy server used to achieve high availability and process high-concurrency client requests.

   You cannot connect to a Proxy Cluster instance at the IP addresses of its proxies.

-  **Redis cluster**

   A shard of the cluster.

   By default, each shard is a master/standby dual-replica Redis instance. When the master instance is faulty, the standby node will be switched to the master one after 15 to 30 seconds. Access to the shard will fail until the switchover is complete.

   If both the master and standby nodes of a shard are faulty, the cluster can still provide services but the data on the faulty shard is inaccessible.
