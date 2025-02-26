:original_name: dcs-pd-0916002.html

.. _dcs-pd-0916002:

Redis 4.0 and 5.0 Instance Specifications
=========================================

This section describes DCS Redis 4.0 and 5.0 instance specifications, including the total memory, available memory, maximum number of connections allowed, maximum/assured bandwidth, and reference performance.

The following metrics are related to the instance specifications:

-  Used memory: You can check the memory usage of an instance by viewing the **Memory Usage** and **Used Memory** metrics.

-  Maximum connections: The maximum number of connections allowed is the maximum number of clients that can be connected to an instance. To check the number of connections to an instance, view the **Connected Clients** metric. After an instance is created, you can change the maximum number of connections of the instance by modifying the **maxclients** parameter on the **Instance Configuration** > **Parameters** page on the console.

-  QPS represents queries per second, which is the number of commands processed per second.

-  Bandwidth: You can view the **Flow Control Times** metric to check whether the bandwidth has exceeded the limit.

   You can also check the **Bandwidth Usage** metric. This metric is for reference only, because it may be higher than 100%. For details, see :ref:`Why Does Bandwidth Usage Exceed 100%? <dcs-faq-0513001>`

.. note::

   -  DCS Redis 4.0 and 5.0 instances are available in single-node, master/standby, read/write splitting, Proxy Cluster, and Redis Cluster types.
   -  Only the x86 architecture is supported. The Arm architecture is not supported.

Single-Node Instances
---------------------

.. table:: **Table 1** Specifications of single-node DCS Redis 4.0 or 5.0 instances

   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Total Memory | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |              |                  |                                  |                           |                       |                                           |
   | (GB)         | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +==============+==================+==================================+===========================+=======================+===========================================+
   | 0.125        | 0.125            | 10,000/10,000                    | 40/40                     | 80,000                | redis.single.xu1.tiny.128                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 0.25         | 0.25             | 10,000/10,000                    | 80/80                     | 80,000                | redis.single.xu1.tiny.256                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 0.5          | 0.5              | 10,000/10,000                    | 80/80                     | 80,000                | redis.single.xu1.tiny.512                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 1            | 1                | 10,000/50,000                    | 80/80                     | 80,000                | redis.single.xu1.large.1                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 2            | 2                | 10,000/50,000                    | 128/128                   | 80,000                | redis.single.xu1.large.2                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 4            | 4                | 10,000/50,000                    | 192/192                   | 80,000                | redis.single.xu1.large.4                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8            | 8                | 10,000/50,000                    | 192/192                   | 100,000               | redis.single.xu1.large.8                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16           | 16               | 10,000/50,000                    | 256/256                   | 100,000               | redis.single.xu1.large.16                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 24           | 24               | 10,000/50,000                    | 256/256                   | 100,000               | redis.single.xu1.large.24                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32           | 32               | 10,000/50,000                    | 256/256                   | 100,000               | redis.single.xu1.large.32                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 48           | 48               | 10,000/50,000                    | 256/256                   | 100,000               | redis.single.xu1.large.48                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64           | 64               | 10,000/50,000                    | 384/384                   | 100,000               | redis.single.xu1.large.64                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Master/Standby Instances
------------------------

By default, a master/standby instance has two replicas (including the master). There is one master node.

Number of IP addresses occupied by a master/standby instance = Number of master nodes x Number of replicas. For example:

2 replicas: Number of occupied IP addresses = 1 x 2 = 2

3 replicas: Number of occupied IP addresses = 1 x 3 = 3

The following table lists the specification codes (**spec_code**) when there are two default replicas. Change the replica quantity in the specification codes based on the actual number of replicas. For example, if an 8 GB master/standby x86-based instance has two replicas, its specification code is redis.ha.xu1.large. **r2**.8. If it has three replicas, its specification code is redis.ha.xu1.large. **r3**.8.

.. table:: **Table 2** Specifications of master/standby DCS Redis 4.0 or 5.0 instances

   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Total Memory | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |              |                  |                                  |                           |                       |                                           |
   | (GB)         | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +==============+==================+==================================+===========================+=======================+===========================================+
   | 0.125        | 0.125            | 10,000/10,000                    | 40/40                     | 80,000                | redis.ha.xu1.tiny.r2.128                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 0.25         | 0.25             | 10,000/10,000                    | 80/80                     | 80,000                | redis.ha.xu1.tiny.r2.256                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 0.5          | 0.5              | 10,000/10,000                    | 80/80                     | 80,000                | redis.ha.xu1.tiny.r2.512                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 1            | 1                | 10,000/50,000                    | 80/80                     | 80,000                | redis.ha.xu1.large.r2.1                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 2            | 2                | 10,000/50,000                    | 128/128                   | 80,000                | redis.ha.xu1.large.r2.2                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 4            | 4                | 10,000/50,000                    | 192/192                   | 80,000                | redis.ha.xu1.large.r2.4                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8            | 8                | 10,000/50,000                    | 192/192                   | 100,000               | redis.ha.xu1.large.r2.8                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16           | 16               | 10,000/50,000                    | 256/256                   | 100,000               | redis.ha.xu1.large.r2.16                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 24           | 24               | 10,000/50,000                    | 256/256                   | 100,000               | redis.ha.xu1.large.r2.24                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32           | 32               | 10,000/50,000                    | 256/256                   | 100,000               | redis.ha.xu1.large.r2.32                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 48           | 48               | 10,000/50,000                    | 256/256                   | 100,000               | redis.ha.xu1.large.r2.48                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64           | 64               | 10,000/50,000                    | 384/384                   | 100,000               | redis.ha.xu1.large.r2.64                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Proxy Cluster Instances
-----------------------

Proxy Cluster instances do not support customization of the number of replicas. Each shard has two replicas by default. For details about the default number of shards, see :ref:`Table 1 <cachecluster__table3552324111>`. When creating an instance, you can customize the size of a single shard.

.. note::

   -  The following table lists only the Proxy Cluster instance specifications with default shards. If you customize shards, see the maximum number of connections, assured/maximum bandwidth, and product specification code (flavor) in the **Instance Specification** table on the **Create DCS Instance** page of the DCS console.
   -  The maximum connections of a cluster is for the entire instance, and not for a single shard. Maximum connections per shard = Maximum connections of an instance/Number of shards.
   -  The maximum bandwidth and assured bandwidth of a cluster is for the entire instance, and not for a single shard. The relationship between the instance bandwidth and the bandwidth per shard is as follows:

      -  Instance bandwidth = Bandwidth per shard x Number of shards
      -  For a cluster instance, if the memory per shard is 1 GB, the bandwidth per shard is 384 Mbit/s. If the memory per shard is greater than 1 GB, the bandwidth per shard is 768 Mbit/s.
      -  The upper limit of the bandwidth of a Proxy Cluster instance is 10,000 Mbit/s. That is, even if the bandwidth per shard multiplied by the number of shards is greater than 10,000 Mbit/s, the bandwidth of the instance is still 10,000 Mbit/s.

.. table:: **Table 3** Specifications of Proxy Cluster DCS Redis 4.0 and 5.0 instances

   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Total Memory | Available Memory | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |              |                  |                                  |                           |                       |                                           |
   | (GB)         | (GB)             | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +==============+==================+==================================+===========================+=======================+===========================================+
   | 4            | 4                | 20,000/20,000                    | 1000/1000                 | 240,000               | redis.proxy.xu1.large.4                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8            | 8                | 30,000/30,000                    | 2000/2000                 | 240,000               | redis.proxy.xu1.large.8                   |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16           | 16               | 30,000/30,000                    | 3072/3072                 | 240,000               | redis.proxy.xu1.large.16                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 24           | 24               | 30,000/30,000                    | 3072/3072                 | 240,000               | redis.proxy.xu1.large.24                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32           | 32               | 30,000/30,000                    | 3072/3072                 | 240,000               | redis.proxy.xu1.large.32                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 48           | 48               | 60,000/60,000                    | 4608/4608                 | 480,000               | redis.proxy.xu1.large.48                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64           | 64               | 80,000/80,000                    | 6144/6144                 | 640,000               | redis.proxy.xu1.large.64                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 96           | 96               | 120,000/120,000                  | 9216/9216                 | 960,000               | redis.proxy.xu1.large.96                  |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 128          | 128              | 160,000/160,000                  | 10,000/10,000             | 1,280,000             | redis.proxy.xu1.large.128                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 192          | 192              | 240,000/240,000                  | 10,000/10,000             | 1,920,000             | redis.proxy.xu1.large.192                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 256          | 256              | 320,000/320,000                  | 10,000/10,000             | > 2,000,000           | redis.proxy.xu1.large.256                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 384          | 384              | 480,000/480,000                  | 10,000/10,000             | > 2,000,000           | redis.proxy.xu1.large.384                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 512          | 512              | 500,000/500,000                  | 10,000/10,000             | > 2,000,000           | redis.proxy.xu1.large.512                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 768          | 768              | 500,000/500,000                  | 10,000/10,000             | > 2,000,000           | redis.proxy.xu1.large.768                 |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 1024         | 1024             | 500,000/500,000                  | 10,000/10,000             | > 2,000,000           | redis.proxy.xu1.large.1024                |
   +--------------+------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Redis Cluster Instances
-----------------------

In addition to larger memory, Redis Cluster instances feature more connections allowed, higher bandwidth allowed, and more QPS than single-node and master/standby instances.

-  The following table lists the x86 specification codes (**spec_code**) when there are two default replicas. Change the replica quantity in the specification codes based on the actual number of replicas. For example, if an 8 GB x86-based instance has two replicas, its specification code is redis.cluster.xu1.large.\ **r2**.8. If it has three replicas, its specification code is redis.cluster.xu1.large.\ **r3**.8.

-  IP addresses: Number of occupied IP addresses = Number of shards x Number of replicas. For example:

   4 GB \| Redis Cluster \| 3 replicas \| 3 shards: Number of occupied IP addresses = 3 x 3 = 9

-  Available memory per node = Instance available memory/Master node quantity. For example:

   For example, a 64 GB instance has 64 GB available memory and 8 master nodes. The available memory per node is 64/8 = 8 GB.

-  Maximum connections limit per node = Maximum connections limit/Master node quantity For example:

   For example, a 4 GB instance has 3 master nodes and the maximum connections limit is 150,000. The maximum connections limit per node = 150,000/3 = 50,000.

.. note::

   -  The following table lists only the Redis Cluster instance specifications with default shards. If you customize shards, see the maximum number of connections, assured/maximum bandwidth, and product specification code (flavor) in the **Instance Specification** table the **Create DCS Instance** page of the DCS console.
   -  The maximum connections of a cluster is for the entire instance, and not for a single shard. Maximum connections per shard = Maximum connections of an instance/Number of shards.
   -  The maximum bandwidth and assured bandwidth of a cluster is for the entire instance, and not for a single shard. The relationship between the instance bandwidth and the bandwidth per shard is as follows:

      -  Instance bandwidth = Bandwidth per shard x Number of shards
      -  For a cluster instance, if the memory per shard is 1 GB, the bandwidth per shard is 384 Mbit/s. If the memory per shard is greater than 1 GB, the bandwidth per shard is 768 Mbit/s.

.. table:: **Table 4** Specifications of Redis Cluster DCS Redis 4.0 or 5.0 instances

   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | Specification | Available Memory | Shards (Master Nodes) | Max. Connections (Default/Limit) | Assured/Maximum Bandwidth | Reference Performance | Specification Code (spec_code in the API) |
   |               |                  |                       |                                  |                           |                       |                                           |
   | (GB)          | (GB)             |                       | (Count)                          | (Mbit/s)                  | (QPS)                 |                                           |
   +===============+==================+=======================+==================================+===========================+=======================+===========================================+
   | 4             | 4                | 3                     | 30,000                           | 2304/2304                 | 240,000               | redis.cluster.xu1.large.r2.4              |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /150,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 8             | 8                | 3                     | 30,000                           | 2304/2304                 | 240,000               | redis.cluster.xu1.large.r2.8              |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /150,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 16            | 16               | 3                     | 30,000                           | 2304/2304                 | 240,000               | redis.cluster.xu1.large.r2.16             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /150,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 24            | 24               | 3                     | 30,000                           | 2304/2304                 | 300,000               | redis.cluster.xu1.large.r2.24             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /150,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 32            | 32               | 3                     | 30,000                           | 2304/2304                 | 300,000               | redis.cluster.xu1.large.r2.32             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /150,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 48            | 48               | 6                     | 60,000                           | 4608/4608                 | > 300,000             | redis.cluster.xu1.large.r2.48             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /300,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 64            | 64               | 8                     | 80,000                           | 6144/6144                 | 500,000               | redis.cluster.xu1.large.r2.64             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /400,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 96            | 96               | 12                    | 120,000                          | 9216/9216                 | > 500,000             | redis.cluster.xu1.large.r2.96             |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /600,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 128           | 128              | 16                    | 160,000                          | 12,288/12,288             | 1,000,000             | redis.cluster.xu1.large.r2.128            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /800,000                         |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 192           | 192              | 24                    | 240,000                          | 18,432/18,432             | > 1,000,000           | redis.cluster.xu1.large.r2.192            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /1,200,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 256           | 256              | 32                    | 320,000                          | 24,576/24,576             | > 2,000,000           | redis.cluster.xu1.large.r2.256            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /1,600,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 384           | 384              | 48                    | 480,000                          | 36,864/36,864             | > 2,000,000           | redis.cluster.xu1.large.r2.384            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /2,400,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 512           | 512              | 64                    | 640,000                          | 49,152/49,152             | > 2,000,000           | redis.cluster.xu1.large.r2.512            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /3,200,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 768           | 768              | 96                    | 960,000                          | 73,728/73,728             | > 2,000,000           | redis.cluster.xu1.large.r2.768            |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /4,800,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+
   | 1024          | 1024             | 128                   | 1,280,000                        | 98,304/98,304             | > 2,000,000           | redis.cluster.xu1.large.r2.1024           |
   |               |                  |                       |                                  |                           |                       |                                           |
   |               |                  |                       | /6,400,000                       |                           |                       |                                           |
   +---------------+------------------+-----------------------+----------------------------------+---------------------------+-----------------------+-------------------------------------------+

Read/Write Splitting
--------------------

-  Maximum connections of a read/write splitting DCS Redis 4.0 or 5.0 instance cannot be modified.
-  Bandwidth limit per Redis server (MB/s) = Total bandwidth limit (MB/s)/Number of replicas (masters included)
-  Reference performance (QPS) per node = Reference performance (QPS)/Number of replicas (masters included)
-  Constraints:

   #. Read/Write splitting instances send read requests to replicas, causing a delay before synchronizing the replicas from the master.

      If your services are sensitive to the delay, do not use read/write splitting instances. Instead, you can use master/standby or cluster instances.

   #. Read/Write splitting is suitable when there are more read requests than write ones. If there are a lot of write requests, the replicas may be disconnected from the master or fail to be synchronized from the master. As a result, the read performance deteriorates.

      Use master/standby or cluster instances in write-heavy scenarios.

   #. When a replica is faulty, it takes some time to synchronize all data from the master. During the synchronization, the replica is out of service, and the read performance of the instance deteriorates.

      Instances with less than 32 GB of memory are recommended. The smaller the memory, the faster the full synchronization and the smaller the impact of interruption.

.. table:: **Table 5** Specifications of read/write splitting DCS Redis 4.0 or 5.0 instances

   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | Cache Size | Available Memory (GB) | Replicas (Masters Included) | Max. Connections (Default/Limit) | Bandwidth Limit (MB/s) | Bandwidth Limit per Redis Server (MB/s) | Reference Performance (QPS) | Reference Performance per Node (QPS) | Specification Code (spec_code in the API) |
   +============+=======================+=============================+==================================+========================+=========================================+=============================+======================================+===========================================+
   | 1          | 1                     | 2                           | 20,000                           | 96                     | 48                                      | 160,000                     | 80,000                               | redis.ha.xu1.large.p2.1                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 1          | 1                     | 3                           | 30,000                           | 144                    | 48                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.1                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 1          | 1                     | 4                           | 40,000                           | 192                    | 48                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.1                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 1          | 1                     | 5                           | 50,000                           | 240                    | 48                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.1                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 1          | 1                     | 6                           | 60,000                           | 288                    | 48                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.1                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 2          | 2                     | 2                           | 20,000                           | 96                     | 48                                      | 160,000                     | 80,000                               | redis.ha.xu1.large.p2.2                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 2          | 2                     | 3                           | 30,000                           | 144                    | 48                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.2                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 2          | 2                     | 4                           | 40,000                           | 192                    | 48                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.2                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 2          | 2                     | 5                           | 50,000                           | 240                    | 48                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.2                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 2          | 2                     | 6                           | 60,000                           | 288                    | 48                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.2                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 4          | 4                     | 2                           | 20,000                           | 96                     | 48                                      | 160,000                     | 80,000                               | redis.ha.xu1.large.p2.4                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 4          | 4                     | 3                           | 30,000                           | 144                    | 48                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.4                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 4          | 4                     | 4                           | 40,000                           | 192                    | 48                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.4                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 4          | 4                     | 5                           | 50,000                           | 240                    | 48                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.4                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 4          | 4                     | 6                           | 60,000                           | 288                    | 48                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.4                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 8          | 8                     | 3                           | 30,000                           | 288                    | 96                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.8                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 8          | 8                     | 4                           | 40,000                           | 384                    | 96                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.8                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 8          | 8                     | 5                           | 50,000                           | 480                    | 96                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.8                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 8          | 8                     | 6                           | 60,000                           | 576                    | 96                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.8                   |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 16         | 16                    | 2                           | 20,000                           | 192                    | 96                                      | 160,000                     | 80,000                               | redis.ha.xu1.large.p2.16                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 16         | 16                    | 3                           | 30,000                           | 288                    | 96                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.16                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 16         | 16                    | 4                           | 40,000                           | 384                    | 96                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.16                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 16         | 16                    | 5                           | 50,000                           | 480                    | 96                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.16                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 16         | 16                    | 6                           | 60,000                           | 576                    | 96                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.16                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 32         | 32                    | 2                           | 20,000                           | 192                    | 96                                      | 160,000                     | 80,000                               | redis.ha.xu1.large.p2.32                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 32         | 32                    | 3                           | 30,000                           | 288                    | 96                                      | 240,000                     | 80,000                               | redis.ha.xu1.large.p3.32                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 32         | 32                    | 4                           | 40,000                           | 384                    | 96                                      | 320,000                     | 80,000                               | redis.ha.xu1.large.p4.32                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 32         | 32                    | 5                           | 50,000                           | 480                    | 96                                      | 400,000                     | 80,000                               | redis.ha.xu1.large.p5.32                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
   | 32         | 32                    | 6                           | 60,000                           | 576                    | 96                                      | 480,000                     | 80,000                               | redis.ha.xu1.large.p6.32                  |
   +------------+-----------------------+-----------------------------+----------------------------------+------------------------+-----------------------------------------+-----------------------------+--------------------------------------+-------------------------------------------+
