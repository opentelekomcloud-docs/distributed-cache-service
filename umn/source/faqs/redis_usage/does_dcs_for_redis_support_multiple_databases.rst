:original_name: dcs-faq-0730019.html

.. _dcs-faq-0730019:

Does DCS for Redis Support Multiple Databases?
==============================================

Both single-node and master/standby DCS Redis instances support multiple databases. By default, single-node and master/standby DCS instances can read and write data in 256 databases (databases numbering 0-255). The default database is DB0.

Redis Cluster DCS instances do not support multi-DB. There is only one database (DB0).
