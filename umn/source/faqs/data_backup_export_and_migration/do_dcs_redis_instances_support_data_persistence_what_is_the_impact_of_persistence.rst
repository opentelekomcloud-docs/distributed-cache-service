:original_name: dcs-faq-0427081.html

.. _dcs-faq-0427081:

Do DCS Redis Instances Support Data Persistence? What Is the Impact of Persistence?
===================================================================================

Is Persistence Supported?
-------------------------

Single-node: No

Master/Standby, read/write splitting, and cluster (except single-replica clusters): Yes

How Is Data Persisted?
----------------------

-  DCS Redis instances supports only AOF persistence by default. You can enable or disable persistence as required. All instances except single-node and single-replica cluster ones are created with AOF persistence enabled.
-  DCS Redis instances do not support RDB persistence by default and the **save** parameter cannot be manually configured. If RDB persistence is required for a master/standby or cluster instance of Redis 4.0 or later, you can use the backup and restoration function to back up the instance data in an RDB file and store the data in OBS.

Disk Used for Persistence
-------------------------

For DCS Redis 4.0 and later instances, data is persisted to SSD disks.

Impact of AOF Persistence
-------------------------

After AOF persistence is enabled, the Redis-Server process records operations in the AOF file for data persistence. This may have the following impacts:

-  If the disk or I/O of the underlying compute node is faulty, the latency may increase or a master/standby switchover may occur.
-  Redis-Server periodically rewrites the AOF. During a rewrite, the latency may be high for a short time. For details about the AOF rewriting rules, see :ref:`When Will AOF Rewrites Be Triggered? <dcs-faq-210706001>`

If DCS instances are used for application acceleration, you are advised to disable AOF persistence for higher performance and stability.

**Exercise caution when disabling AOF persistence. After it is disabled, cached data may be lost in extreme scenarios, for example, when both the master and standby nodes are faulty.**

Configuring Redis Persistence
-----------------------------

Set the instance configuration parameter **appendonly** to **no** to disable, or **yes** to enable AOF persistence. (Not available for single-node instances.)

For details, see :ref:`Modifying Configuration Parameters <dcs-ug-0312024>`.
