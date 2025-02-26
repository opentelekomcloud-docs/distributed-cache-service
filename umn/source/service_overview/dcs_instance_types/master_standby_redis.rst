:original_name: CacheMasterSlave.html

.. _CacheMasterSlave:

Master/Standby Redis
====================

This section describes master/standby DCS Redis instances.

.. note::

   You cannot upgrade the Redis version for an instance. For example, a master/standby DCS Redis 4.0 instance cannot be upgraded to a master/standby DCS Redis 5.0 instance. If your service requires the features of higher Redis versions, create a DCS Redis instance of a higher version and then migrate data from the old instance to the new one.

Features
--------

Master/Standby DCS instances have higher availability and reliability than single-node DCS instances.

Master/Standby DCS instances have the following features:

#. **Data persistence and high reliability**

   By default, data persistence is enabled by both the master and the standby node of a master/standby instance.

   The standby node of a Redis 4.0 or later instance is visible to you. You can read data from the standby node by connecting to it using the instance read-only address.

#. **Data synchronization**

   Data in the master and standby nodes is kept consistent through incremental synchronization.

   .. note::

      After recovering from a network exception or node fault, master/standby instances perform a full synchronization to ensure data consistency.

#. **Automatic master/standby switchover**

   If the master node becomes faulty, the instance is disconnected and unavailable for several seconds. The standby node takes over within 30 seconds without manual operations to resume stable services.

   .. note::

      -  Disconnections and unavailability occur during the failover. The service client should be able to reconnect or retry.
      -  After a master/standby switchover is complete, the last master node (already switched to the replica) is not recovered immediately and services will fail to access it. In this case, configure a Redis SDK by referring to :ref:`Access in Different Languages <dcs-ug-0512002>`.

#. **DR policies**

   Each master/standby, read/write splitting, or cluster DCS instance can be deployed across AZs with physically isolated power supplies and networks. Applications can also be deployed across AZs to achieve high availability for both data and applications.

#. **Read/Write splitting**

   Master/Standby DCS Redis 4.0 and later instances support client read/write splitting. When connecting to such an instance, you can use the read/write address to connect to the master node or use the read-only address to connect to the standby node.

   To implement read/write splitting for a master/standby instance, configure it on a client. To use the read/write splitting function, you are advised to use :ref:`read/write splitting instances <dcs-pd-0220606>`.

.. _cachemasterslave__section5805185095215:

Architecture of Master/Standby DCS Redis 4.0/5.0/6.0/7.0 Instances
------------------------------------------------------------------

The following figure shows the architecture of a master/standby DCS Redis 4.0/5.0/6.0/7.0 instance.


.. figure:: /_static/images/en-us_image_0000001528638365.png
   :alt: **Figure 1** Architecture of a master/standby DCS Redis 4.0/5.0/6.0/7.0 instance

   **Figure 1** Architecture of a master/standby DCS Redis 4.0/5.0/6.0/7.0 instance

Architecture description:

#. Each master/standby DCS Redis 4.0 or later instance has two connection addresses. When connecting to such an instance, you can use the read/write domain name address to connect to the master node or use the read-only domain name address to connect to the standby node.

   The connection addresses can be obtained on the instance details page on the DCS console.

#. Master/Standby DCS Redis 4.0 and later instances support Sentinels. Sentinels monitor the running status of the master and standby nodes. If the master node becomes faulty, a failover will be performed.

   Sentinels are invisible to you and is used only in the service.

#. A standby node has the same specifications as a master node. A master/standby instance consists of a pair of master and standby nodes by default.

#. To access a DCS Redis 4.0 or later instance, you can customize the port. If no port is specified, the default port 6379 will be used. In the architecture diagram, port 6379 is used. If you have customized a port, replace **6379** with the actual port.

.. note::

   -  To implement read/write splitting using a master/standby instance, ensure that your client can distinguish between read and write requests. The client directs write requests to the read/write domain name and read requests to the read-only domain name.
   -  Requests to the read-only domain name address may fail if the standby node of a master/standby DCS Redis 4.0 or later instance is faulty. For higher reliability and lower latency, **do not use the read-only address**.
