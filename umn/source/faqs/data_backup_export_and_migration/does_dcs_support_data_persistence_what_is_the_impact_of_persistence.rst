:original_name: dcs-faq-0427081.html

.. _dcs-faq-0427081:

Does DCS Support Data Persistence? What Is the Impact of Persistence?
=====================================================================

Support for Persistence
-----------------------

-  DCS Redis instances:

   -  Single-node: Data persistence is not supported.
   -  Master/standby and cluster (except single-replica clusters): Data persistence is supported.

Persistence Modes
-----------------

-  DCS supports only AOF persistence by default. You can enable or disable persistence as required. All instances except single-node and single-replica cluster ones are created with AOF persistence enabled.
-  DCS does not support RDB persistence by default and you cannot configure the **save** parameter. If RDB persistence is required for a master/standby or cluster instance of Redis 4.0 or later, you can use the backup and restoration function to back up the instance data to an RDB file and store the data in OBS.

Disk Used for Persistence
-------------------------

For DCS Redis 4.0 and later instances, data is persisted to SSD disks.

Impact of AOF Persistence
-------------------------

After AOF persistence is enabled, the Redis-Server process needs to record operations in the AOF file for data persistence.

-  If the disk or I/O of the underlying compute node is faulty, the latency may increase or a master/standby switchover may occur.
-  Redis-Server periodically rewrites the AOF. During a rewrite, the latency may be high for a short time. For details about the AOF rewriting rules, see :ref:`When Will AOF Rewrites Be Triggered? <dcs-faq-210706001>`

If DCS instances are used to accelerate applications, you are advised to disable persistence for higher performance and stability. Exercise caution when disabling persistence. Without persistence, cached data may be lost in extreme scenarios (for example, when both the master and standby nodes are faulty).

To disable AOF persistence, set parameter **appendonly** to **no** on the instance details page.
