:original_name: dcs-pd-200312004.html

.. _dcs-pd-200312004:

Basic Concepts
==============

DCS Instance
------------

An instance is the minimum resource unit provided by DCS.

DCS supports the Redis cache engine, and single-node, master/standby, and cluster instance types. For each instance type, multiple specifications are available.

For details, see :ref:`DCS Instance Specifications <en-us_topic_0054235835>` and :ref:`DCS Instance Types <dcs-pd-200312001>`.

Project
-------

Projects are used to group and isolate OpenStack resources (computing resources, storage resources, and network resources). A project can be a department or a project team. Multiple projects can be created for one account.

Replica
-------

A replica is a node of a DCS instance. No replication indicates that the instance does not have a standby node. Master/Standby replication indicates that the instance has a standby node. For example, a master/standby DCS instance has a master/standby replication. Each node of a cluster DCS Redis instance has a master/standby replication.

Maintenance Time Window
-----------------------

The maintenance time window is the period when the DCS service team upgrade and maintain the instance.

DCS instance maintenance takes place only once a quarter and does not interrupt services. Even so, you are advised to select a time period when the service demand is low.

When creating an instance, you must specify a maintenance time window, which can be modified after the instance is created.

For details, see: :ref:`Modifying Maintenance Time Window <dcs-ug-0312025>`.

Cross-AZ Deployment
-------------------

Master/Standby instances are deployed across different AZs with physically isolated power supplies and networks. Applications can also be deployed across AZs to achieve HA for both data and applications.

When creating a master/standby or cluster DCS Redis instance, you can select a standby AZ for the standby node.

.. _dcs-pd-200312004__en-us_topic_0145956240_section20999323134412:

Shard
-----

A shard is a management unit of a cluster DCS Redis instance. Each shard corresponds to a redis-server process. A cluster consists of multiple shards. Each shard has multiple slots. Data is distributedly stored in the slots. The use of shards increases cache capacity and concurrent connections.
