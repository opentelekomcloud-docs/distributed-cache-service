:original_name: dcs-pd-0220606.html

.. _dcs-pd-0220606:

Read/Write Splitting Redis
==========================

This section describes read/write splitting DCS Redis 4.0/5.0/6.0 instances. Read/write splitting is implemented on the server side by default. Proxies distinguish between read requests and write requests, and forward write requests to the master node and read requests to the standby node.

Read/write splitting is suitable for scenarios with high read concurrency and few write requests, aiming to improve the performance of high concurrency and reducing O&M costs.

When using read/write splitting instances, note the following:

#. Read requests are sent to replicas. There is a delay when data is synchronized from the master to the replicas.

   If your services are sensitive to the delay, do not use read/write splitting instances. Instead, use master/standby or cluster instances.

#. Read/write splitting is suitable when there are more read requests than write requests. If there are a lot of write requests, the master and replicas may be disconnected, or the data synchronization between them may fail after the disconnection. As a result, the read performance deteriorates.

   If your services are write-heavy, use master/standby or cluster instances.

#. If a replica is faulty, it takes some time to synchronize all data from the master. During the synchronization, the replica does not provide services, and the read performance of the instance deteriorates.

   To reduce the impact of the interruption, use an instance with less than 32 GB memory. The smaller the memory, the shorter the time for full data synchronization between the master and replicas, and the smaller the impact of the interruption.

Architecture
------------


.. figure:: /_static/images/en-us_image_0000001273950310.png
   :alt: **Figure 1** Architecture of a read/write splitting instance

   **Figure 1** Architecture of a read/write splitting instance

Architecture description:

-  **VPC endpoint service**

   You can configure your DCS Redis instance as a VPC endpoint service and access the instance at the VPC endpoint service address.

   The IP address of the read/write splitting DCS Redis instance is the address of the VPC endpoint service.

-  **ELB**

   The load balancers are deployed in cluster HA mode and support multi-AZ deployment.

-  **Proxy**

   A proxy cluster is used to distinguish between read requests and write requests, and forward write requests to the master node and read requests to the standby node. You do not need to configure the client.

-  **Sentinel cluster**

   Sentinels monitor the status of the master and replicas. If the master node is faulty or abnormal, a failover is performed to ensure that services are not interrupted.

-  **Master/standby instance**

   A read/write splitting instance is essentially a master/standby instance that consists of a master node and a standby node. By default, data persistence is enabled and data is synchronized between the two nodes.

   The master and standby nodes can be deployed in different AZs.
