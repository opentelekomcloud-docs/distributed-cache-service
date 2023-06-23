:original_name: en-us_topic_0054235826.html

.. _en-us_topic_0054235826:

What Is DCS?
============

Distributed Cache Service (DCS) is an online, distributed, in-memory cache service compatible with Redis. It is reliable, scalable, usable out of the box, and easy to manage, meeting your requirements for high read/write performance and fast data access.

-  Usability out of the box

   DCS provides single-node, master/standby, and cluster instances with specifications ranging from 128 MB to 1024 GB. DCS instances can be created with just a few clicks on the console, without requiring you to prepare servers.

   DCS Redis 3.0 instances are deployed on VMs. DCS Redis 4.0/5.0/6.0 instances are containerized and can be created within seconds.

-  Security and reliability

   Instance data storage and access are securely protected through security management services, including Identity and Access Management (IAM), Virtual Private Cloud (VPC), Cloud Eye, and Cloud Trace Service (CTS).

   Master/Standby and cluster instances can be deployed within an availability zone (AZ) or across AZs.

-  Auto scaling

   DCS instances can be scaled up or down online, helping you control costs based on service requirements.

-  Easy management

   A web-based console is provided for you to perform various operations, such as restarting instances, modifying configuration parameters, and backing up and restoring data. RESTful application programming interfaces (APIs) are also provided for automatic instance management.

-  Online migration

   You can create a data migration task on the console to import backup files or migrate data online.

DCS for Redis
-------------

Redis is a storage system that supports multiple types of data structures, including key-value pairs. It can be used in such scenarios as data caching, event publication/subscription, and high-speed queuing, as described in :ref:`Application Scenarios <dcs-pd-0326002>`. Redis is written in ANSI C, supporting direct read/write of strings, hashes, lists, sets, streams, and sorted sets. Redis works with an in-memory dataset which can be persisted on disk.

DCS Redis instances can be customized based on your requirements.

.. table:: **Table 1** DCS Redis instance configuration

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Instance type                     | DCS for Redis provides the following types of instances to suit different service scenarios:                                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                                                     |
   |                                   | Single-node: Suitable for caching temporary data in low reliability scenarios. Single-node instances support highly concurrent read/write operations, but do not support data persistence. Data will be deleted after instances are restarted.                                                                      |
   |                                   |                                                                                                                                                                                                                                                                                                                     |
   |                                   | Master/Standby: Each master/standby instance runs on two nodes (one master and one standby). The standby node replicates data synchronously from the master node. If the master node fails, the standby node automatically becomes the master node.                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                                                     |
   |                                   | Cluster: Each cluster DCS instance consists of multiple :ref:`shards <dcs-pd-200312004__en-us_topic_0145956240_section20999323134412>` and each shard includes a master node and zero or multiple replicas. Shards are not visible to users. If the master node fails, a standby node in the same shard takes over. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Instance specification            | DCS for Redis provides instances of different specifications, ranging from 128 MB to 1024 GB.                                                                                                                                                                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Redis version                     | DCS instances are compatible with open-source Redis 3.0, 4.0, 5.0, and 6.0.                                                                                                                                                                                                                                         |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Underlying architecture           | **Standard** Redis based on VMs: supports up to 100,000 queries per second (QPS) at a single node.                                                                                                                                                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | High availability (HA) and DR     | Master/standby and cluster DCS Redis instances can be deployed across AZs in the same region with physically isolated power supplies and networks.                                                                                                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

For more information about open-source Redis, visit https://redis.io/.
