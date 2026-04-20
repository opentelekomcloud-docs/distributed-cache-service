:original_name: dcs-faq-0427028.html

.. _dcs-faq-0427028:

Does DCS for Redis Support Multi-DB?
====================================

DCS's support for multiple databases (multi-DB) is as follows:

-  Single-node, read/write splitting, and master/standby DCS Redis instances: Multi-DB is supported. By default, there are 256 databases, numbering 0-255. The default database is DB0. Multi-DB is used for data isolation. The size of each database is not evenly allocated. As a result, one database may fully occupy the memory of the instance.
-  Proxy Cluster: There is only one database by default.

   -  For details about how to create a Proxy Cluster instance with multiple databases, see :ref:`How Do I Create a Multi-DB Proxy Cluster Instance? <dcs-faq-020220331>`
   -  For details about how to enable multi-DB for a single-DB Proxy Cluster instance, see :ref:`Notes and Procedure for Enabling Multi-DB for Proxy Cluster Instances <dcs-faq-210804001>`

-  Redis Cluster DCS instances: Multi-DB is not supported. There is only one database (DB0).

**The number of databases cannot be changed, and the size of each database cannot be customized.**
