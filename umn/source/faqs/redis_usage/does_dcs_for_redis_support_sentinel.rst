:original_name: dcs-faq-0730021.html

.. _dcs-faq-0730021:

Does DCS for Redis Support Sentinel?
====================================

Master/Standby, read/write splitting, and cluster DCS Redis 4.0 and later instances support Sentinels (Each shard of a cluster is a master/standby instance.). Sentinels monitor the running status of both the master and standby nodes of a master/standby instance and each shard of a cluster instance. If the master node becomes faulty, a failover will be performed.

DCS Redis 3.0 does not support Sentinels.
