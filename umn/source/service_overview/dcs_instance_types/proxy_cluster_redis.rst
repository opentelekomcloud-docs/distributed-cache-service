:original_name: CacheCluster.html

.. _CacheCluster:

Proxy Cluster Redis
===================

DCS provides two types of cluster Redis instances: Proxy Cluster and Redis Cluster. Proxy Cluster uses Linux Virtual Server (LVS) and proxies. Redis Cluster is the native distributed implementation of Redis. Proxy Cluster instances are compatible with Redis 3.0, while Redis Cluster instances are compatible with Redis 4.0 and 5.0.

This section describes Proxy Cluster DCS Redis 3.0 instances.

.. note::

   -  A Proxy Cluster instance can be connected in the same way that a single-node or master/standby instance is connected, without any special settings on the client. You can use the IP address or domain name of the instance, and do not need to know or use the proxy or shard addresses.

Proxy Cluster DCS Redis 3.0 Instances
-------------------------------------

Proxy Cluster DCS Redis 3.0 instances are compatible with `codis <https://github.com/CodisLabs/codis>`__. The specifications range from 64 GB to 1024 GB, meeting requirements for **millions of concurrent connections** and **massive data cache**. Distributed data storage and access is implemented by DCS, without requiring development or maintenance.

Each Proxy Cluster instance consists of load balancers, proxies, cluster managers, and :ref:`shards <dcs-pd-200312004__en-us_topic_0145956240_section20999323134412>`.

.. table:: **Table 1** Specifications of Proxy Cluster DCS Redis 3.0 instances

   ============ ======= ======
   Total Memory Proxies Shards
   ============ ======= ======
   64 GB        3       8
   128 GB       6       16
   256 GB       8       32
   512 GB       16      64
   ============ ======= ======


.. figure:: /_static/images/en-us_image_0000001383102132.png
   :alt: **Figure 1** Proxy Cluster DCS Redis instance architecture

   **Figure 1** Proxy Cluster DCS Redis instance architecture

Architecture description:

-  **VPC**

   All server nodes of the instance run in the same VPC.

   .. note::

      For intra-VPC access, the client and the instance must be in the same VPC with specified security group rule configurations.

      For details, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

-  **Application**

   The client used to access the instance.

   DCS Redis instances can be accessed through open-source clients. For details about accessing DCS instances, see :ref:`Accessing an Instance <dcs-ug-0916002>`.

-  **LB-M/LB-S**

   The load balancers, which are deployed in master/standby HA mode. The connection addresses (**IP address:Port**) of the cluster DCS Redis instance are the addresses of the load balancers.

-  **Proxy**

   The proxy server used to achieve high availability and process high-concurrency client requests.

   You can connect to a Proxy Cluster instance at the IP addresses of its proxies.

-  **Redis shard**

   A shard of the cluster.

   Each shard consists of a pair of master/standby nodes. If the master node becomes faulty, the standby node automatically takes over cluster services.

   If both the master and standby nodes of a shard are faulty, the cluster can still provide services but the data on the faulty shard is inaccessible.

-  **Cluster manager**

   The cluster configuration managers, which store configurations and partitioning policies of the cluster. You cannot modify the information about the configuration managers.
