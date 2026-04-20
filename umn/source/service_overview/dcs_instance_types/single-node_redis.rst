:original_name: CacheSingleNode.html

.. _CacheSingleNode:

Single-Node Redis
=================

A single-node DCS Redis instance has only one node and does not support data persistence. They are suitable for cache services that do not require data reliability.

.. note::

   -  The major version cannot be upgraded. For example, a single-node DCS Redis 4.0 instance cannot be upgraded to a single-node DCS Redis 5.0 one. If you need Redis features of later versions, create a DCS Redis instance of a later version and then migrate data from the earlier instance to the new one.
   -  Single-node instances cannot ensure data persistence and do not support manual or scheduled data backup. Exercise caution before using them.

Features
--------

#. Low-cost and suitable for development and testing

   Single-node instances are 40% cheaper than master/standby DCS instances, suitable for setting up development or testing environments.

#. Non-persistent data

   Data persistence is not ensured through one master node for single-node instances. The data cannot be backed up.

Architecture
------------

:ref:`Figure 1 <cachesinglenode__fig1674742511276>` shows the architecture of single-node DCS Redis instances.

.. note::

   To access a DCS Redis 3.0 instance, you must use port 6379. To access a DCS Redis 4.0 or later instance, you can customize the port. If no port is specified, the default port 6379 will be used. In the following architecture, port 6379 is used. If you have customized a port, replace **6379** with the actual port.

.. _cachesinglenode__fig1674742511276:

.. figure:: /_static/images/en-us_image_0000002416373129.png
   :alt: **Figure 1** Single-node DCS Redis instance architecture

   **Figure 1** Single-node DCS Redis instance architecture

Architecture description:

-  **VPC**

   All server nodes of the instance run in the same VPC.

   .. note::

      For intra-VPC access, the client and the instance must be in the same VPC.

-  **Application**

   The client of the instance, which is the application running on an Elastic Cloud Server (ECS).

   DCS Redis instances are compatible with the Redis protocol, and can be accessed through open-source clients. For details about accessing DCS instances, see :ref:`Accessing an Instance <dcs-ug-0916002>`.

-  **DCS instance**

   A single-node DCS instance, which has only one node and one Redis process.
