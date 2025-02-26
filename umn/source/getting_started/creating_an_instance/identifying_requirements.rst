:original_name: PurchasePreparation.html

.. _PurchasePreparation:

Identifying Requirements
========================

Before creating a DCS instance, identify your requirements and complete the following preparations:

#. Decide on the required cache engine version.

   Different Redis versions have different features. For details, see :ref:`Comparing Redis Versions <redisdifference>`.

#. Decide on the required instance type.

   DCS provides single-node, master/standby, read/write splitting, Proxy Cluster, and Redis Cluster types of instances. Each type has its own architecture. For details about the instance architectures, see :ref:`DCS Instance Types <dcs-pd-200312001>`.

#. Decide on the required instance specification.

   Each specification specifies the maximum available memory, number of connections, and bandwidth. For details, see :ref:`DCS Instance Specifications <en-us_topic_0054235835>`.

#. Decide on the region and whether cross-AZ deployment is required.

   Choose a region closest to your application to reduce latency.

   A region consists of multiple availability zones (AZs) with physically isolated power supplies and networks. Master/Standby, read/write splitting, and cluster DCS instances can be deployed across AZs.

   .. note::

      -  If a master/standby, read/write splitting, or cluster DCS instance is deployed across AZs, faults in an AZ do not affect cache nodes in other AZs. This is because when the master node is faulty, the standby cache node will automatically become the master node to provide services. Such deployment achieves better disaster recovery.
      -  Deploying a DCS instance across AZs slightly reduces network efficiency compared with deploying an instance within an AZ. Therefore, if a DCS instance is deployed across AZs, synchronization between master and standby cache nodes is slightly less efficient.

#. Decide whether backup policies are required.

   Currently, backup restoration policies can be configured for instances other than single-node ones. For details about backup and restoration, see :ref:`Overview <en-us_topic_0079835992>`.
