:original_name: dcs-faq-0730053.html

.. _dcs-faq-0730053:

How Do I Export DCS Redis Instance Data?
========================================

-  For master/standby or cluster instances:

   Perform the following operations to export the data:

   #. On the **Backups & Restorations** page, view the backup records.
   #. If there are no backup records, create a backup manually and download the backup file as prompted.

   .. note::

      If your DCS instances were created a long time ago, the versions of these instances may not be advanced enough to support some new functions (such as backup and restoration). You can contact technical support to upgrade your DCS instances. After the upgrade, you can back up and restore your instances.

-  For single-node instances:

   Single-node instances do not support the backup function. You can use redis-cli to export RDB files. This operation depends on **SYNC** command.

   -  If the instance allows the **SYNC** command (such as a Redis 3.0 single-node instance), run the following command to export the instance data:

      **redis-cli -h {source_redis_address} -p 6379 [-a password] --rdb {output.rdb}**

   -  If the instance does not allow the **SYNC** command (such as a Redis 4.0 or 5.0 single-node instance), migrate the instance data to a master/standby instance and export the data by using the backup function.
