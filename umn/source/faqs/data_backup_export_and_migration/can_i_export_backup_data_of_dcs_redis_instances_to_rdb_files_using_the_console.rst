:original_name: dcs-faq-0730054.html

.. _dcs-faq-0730054:

Can I Export Backup Data of DCS Redis Instances to RDB Files Using the Console?
===============================================================================

-  Redis 3.0

   No. On the console, backup data of a DCS Redis 3.0 instance can be exported only to AOF files. To export data to RDB files, run the following command in redis-cli:

   **redis-cli -h {redis_address} -p 6379 [-a password] --rdb {output.rdb}**

-  Redis 4.0 and 5.0

   Yes. Backup data of a DCS Redis 4.0 or 5.0 instance is exported from the console to RDB files. You cannot use redis-cli to export such data to RDB files.
