:original_name: dcs-faq-0730021.html

.. _dcs-faq-0730021:

Does DCS for Redis Support Sentinel?
====================================

Yes. Redis Sentinel is supported by DCS for Redis 4.0 and 5.0 and is enabled by default. Sentinel constantly checks if master and replica nodes are running properly. If the master is not running properly, Sentinel starts a failover process and promotes a replica to master.

However, DCS for Redis 3.0 does not support Redis Sentinel. Instead, it uses keepalive to monitor master and replica nodes and to manage failovers.
