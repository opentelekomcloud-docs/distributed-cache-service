:original_name: CacheSingleNode.html

.. _CacheSingleNode:

Single-Node Redis
=================

A single-node DCS Redis instance has only one node and does not support data persistence. They are suitable for cache services that do not require data reliability.

.. note::

   -  You cannot upgrade the Redis version of an instance. For example, a single-node DCS instance cannot be upgraded from Redis 4.0 to Redis 5.0. If you need Redis features of later versions, create a DCS Redis instance of a later version and then migrate data from the earlier instance to the new one.
   -  Single-node instances cannot ensure data persistence and do not support manual or scheduled data backup. Exercise caution before using them.

Features
--------

#. Low system overhead and high QPS

   Single-node instances do not support data synchronization or data persistence, reducing system overhead and supporting higher concurrency. QPS of single-node DCS Redis instances reaches up to 100,000.

#. Process monitoring and automatic fault recovery

   With an HA monitoring mechanism, if a single-node DCS instance becomes faulty, a new process is started within 30 seconds to resume service provisioning.

#. Out-of-the-box usability and no data persistence

   Single-node DCS instances can be used out of the box because they do not involve data loading. If your service requires high QPS, you can warm up the data beforehand to avoid strong concurrency impact on the backend database.

#. Low-cost and suitable for development and testing

   Single-node instances are 40% cheaper than master/standby DCS instances, suitable for setting up development or testing environments.

In summary, single-node DCS instances support highly concurrent read/write operations, but do not support data persistence. Data will be deleted after instances are restarted or stopped. They are suitable for scenarios which do not require data persistence, such as database front-end caching, to accelerate access and ease the concurrency load off the backend. If the desired data does not exist in the cache, requests will go to the database. When restarting the service or the DCS instance, you can pre-generate cache data from the disk database to relieve pressure on the backend during startup.

Architecture
------------

:ref:`Figure 1 <cachesinglenode__fig15457185394718>` shows the architecture of single-node DCS Redis instances.

.. note::

   To access a DCS Redis 3.0 instance, you must use port 6379. To access a DCS Redis 4.0 or later instance, you can customize the port. If no port is specified, the default port 6379 will be used. In the following architecture, port 6379 is used. If you have customized a port, replace **6379** with the actual port.

.. _cachesinglenode__fig15457185394718:

.. figure:: /_static/images/en-us_image_0296784660.png
   :alt: **Figure 1** Single-node DCS Redis instance architecture

   **Figure 1** Single-node DCS Redis instance architecture

Architecture description:

-  **VPC**

   All server nodes of the instance run in the same VPC.

   .. note::

      For intra-VPC access, the client and the instance must be in the same VPC. For a Redis 3.0 instance, security group rules are required.

-  **Application**

   The client of the instance, which is the application running on an Elastic Cloud Server (ECS).

   DCS Redis instances are compatible with the Redis protocol, and can be accessed through open-source clients. For details about accessing DCS instances, see :ref:`Accessing an Instance <dcs-ug-0916002>`.

-  **DCS instance**

   A single-node DCS instance, which has only one node and one Redis process.

   DCS monitors the availability of the instance in real time. If the Redis process becomes faulty, DCS starts a new process to resume service provisioning.
