:original_name: dcs-faq-0730021.html

.. _dcs-faq-0730021:

Does DCS for Redis Support Sentinel?
====================================

Cluster instances and master/standby DCS Redis 4.0 and later instances support Sentinels. Sentinels monitor the running status of both the master and standby nodes of a master/standby instance and each shard of a cluster instance. If the master node becomes faulty, a failover will be performed.

DCS for Redis 3.0 does not support Redis Sentinel. Instead, it uses keepalive to monitor master and replica nodes and to manage failovers.
