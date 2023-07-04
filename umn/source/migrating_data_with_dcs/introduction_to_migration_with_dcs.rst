:original_name: dcs-ug-0312036.html

.. _dcs-ug-0312036:

Introduction to Migration with DCS
==================================

Migration Modes
---------------

DCS for Redis supports online migration (in full or incrementally) and backup migration (by importing backup files).

-  Backup migration is suitable when the source and target Redis instances are not connected, and the source Redis instance does not support the **SYNC** and **PSYNC** commands. The data source can be an OBS bucket or a Redis instance.

   -  Importing data from an OBS bucket: Download the source Redis data and then upload it to an OBS bucket in the same region as the target DCS Redis instance. DCS will read the backup data from the OBS bucket and migrate the data into the target instance.

      **This migration mode can be used for migrating data from other Redis vendors or self-hosted Redis to DCS for Redis.**

   -  Importing data from a Redis instance: Back up the source Redis data and then migrate the backup data to DCS for Redis.

-  Migrating data online: If the source and target instances are interconnected and the **SYNC** and **PSYNC** commands are supported in the source instance, data can be migrated online in full or incrementally from the source to the target.

The following table describes data migration modes supported by DCS.

.. table:: **Table 1** DCS data migration modes

   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   | Migration Mode         | Source                                                                                                                         | Target: DCS                   |               |               |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        |                                                                                                                                | Single-node or master/standby | Proxy Cluster | Redis Cluster |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   | Importing backup files | AOF file                                                                                                                       | Y                             | Y             | x             |
   |                        |                                                                                                                                |                               |               |               |
   |                        | .. note::                                                                                                                      |                               |               |               |
   |                        |                                                                                                                                |                               |               |               |
   |                        |    AOF files exported from Redis 4.0/5.0/6.0 instances and other instances with RDB compression enabled cannot be imported.    |                               |               |               |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | RDB file                                                                                                                       | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   | Migrating data online  | DCS for Redis: single-node or master/standby                                                                                   | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | DCS for Redis: Proxy Cluster                                                                                                   | Y                             | Y             | Y             |
   |                        |                                                                                                                                |                               |               |               |
   |                        | .. note::                                                                                                                      |                               |               |               |
   |                        |                                                                                                                                |                               |               |               |
   |                        |    Proxy Cluster DCS Redis 3.0 instances cannot be used as the source, while Proxy Cluster DCS Redis 4.0 or 5.0 instances can. |                               |               |               |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | DCS for Redis: Redis Cluster                                                                                                   | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Self-hosted Redis: single-node or master/standby                                                                               | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Self-hosted Redis: proxy-based cluster                                                                                         | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Self-hosted Redis: Redis Cluster                                                                                               | Y                             | Y             | Y             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Other Redis: single-node or master/standby                                                                                     | x                             | x             | x             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Other Redis: proxy-based cluster                                                                                               | x                             | x             | x             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+
   |                        | Other Redis: Redis Cluster                                                                                                     | x                             | x             | x             |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------+-------------------------------+---------------+---------------+

.. note::

   -  **DCS for Redis** refers to Redis instances provided by DCS
   -  **Self-hosted Redis** refers to self-hosted Redis on the cloud, from other cloud vendors, or in on-premises data centers.
   -  **Other Redis** refers to Redis services provided by other cloud vendors.
   -  **Y**: Supported. **x**: Not supported.
