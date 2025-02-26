:original_name: CacheProxy.html

.. _CacheProxy:

Redis Cluster
=============

Redis Cluster DCS instances use the native distributed implementation of Redis. Redis Cluster instances have the following features:

-  They are compatible with native Redis clusters.
-  They inherit the smart client design from Redis.
-  They deliver many times higher performance than master/standby instances.


Redis Cluster
-------------

The Redis Cluster instance type provided by DCS is compatible with the `native Redis Cluster <https://redis.io/topics/cluster-spec>`__, which uses smart clients and a distributed architecture to perform sharding.

:ref:`Table 1 <cacheproxy__table3552324111>` lists the shard specification for different instance specifications.

**Size of a shard = Instance specification/Number of shards**. For example, if a 48 GB instance has 6 shards, the size of each shard is 48 GB/6 = 8 GB.

.. _cacheproxy__table3552324111:

.. table:: **Table 1** Specifications of Redis Cluster DCS instances

   =========================== ======
   Total Memory                Shards
   =========================== ======
   4 GB/8 GB/16 GB/24 GB/32 GB 3
   48 GB                       6
   64 GB                       8
   96 GB                       12
   128 GB                      16
   192 GB                      24
   256 GB                      32
   384 GB                      48
   512 GB                      64
   768 GB                      96
   1024 GB                     128
   =========================== ======

-  Distributed architecture

   Any node in a Redis Cluster can receive requests. Received requests are then redirected to the right node for processing. Each node consists of a subset of one master and one (by default) or multiple replicas. The master or replica roles are determined through an election algorithm.


   .. figure:: /_static/images/en-us_image_0277578727.png
      :alt: **Figure 1** Distributed architecture of Redis Cluster

      **Figure 1** Distributed architecture of Redis Cluster

-  Presharding

   There are 16,384 hash slots in each Redis Cluster. The mapping between hash slots and Redis nodes is stored in Redis Servers. To compute what is the hash slot of a given key, simply take the CRC16 of the key modulo 16384. Example command output


   .. figure:: /_static/images/en-us_image_0000001280621500.png
      :alt: **Figure 2** Redis Cluster presharding

      **Figure 2** Redis Cluster presharding

   .. note::

      -  Each shard of a Redis Cluster is a master/standby Redis instance. When the master node on a shard is faulty, the connections on the shard are interrupted in seconds, and the shard becomes unavailable. The standby node is automatically switched over within 15 to 30 seconds. The fault only affects the shard itself.
      -  When a master node on a single shard in a redis cluster is faulty, after a master/standby switchover is complete, the master node (already switched to the replica) is not recovered immediately and services will fail to access it. In this case, configure a Redis SDK by referring to :ref:`Access in Different Languages <dcs-ug-0512002>`.
