:original_name: dcs-migration-090626001_0.html

.. _dcs-migration-090626001_0:

Online Migration with Rump
==========================

Background
----------

-  Redis instances provided by some cloud service vendors do not allow **SLAVEOF**, **BGSAVE**, and **PSYNC** commands to be issued from Redis clients. As a result, redis-cli, redis-shake, and other tools cannot be used to export data.
-  Using the **KEYS** command may block Redis.
-  Cloud service vendors usually only support downloading backup files. This method is suitable only for offline migration, featuring longer service interruption.

`Rump <https://github.com/stickermule/rump>`__ is an open-source tool designed for migrating Redis data online. It supports migration between DBs of the same instance and between DBs of different instances.

Migration Principles
--------------------

Rump uses the **SCAN** command to acquire keys and the **DUMP**/**RESTORE** command to get or set values.

Featuring time complexity O(1), **SCAN** is capable of quickly getting all keys. **DUMP**/**RESTORE** is used to read/write values independent from the key type.

Rump brings the following benefits:

-  The **SCAN** command replaces the **KEYS** command to avoid blocking Redis.
-  Any type of data can be migrated.
-  **SCAN** and **DUMP**/**RESTORE** operations are pipelined, improving the network efficiency during data migration.
-  No temporary file is involved, saving disk space.
-  Buffered channels are used to optimize performance of the source server.

.. important::

   #. To cluster DCS instances, you cannot use Rump. Instead, use redis-shake or redis-cli.
   #. To prevent migration command resolution errors, do not include special characters (#@:) in the instance password.
   #. Stop the service before migrating data. If data is kept being written in during the migration, some keys might be lost.

Step 1: Installing Rump
-----------------------

#. Download `Rump (release version) <https://github.com/stickermule/rump/releases>`__.

   On 64-bit Linux, run the following command:

   **wget https://github.com/stickermule/rump/releases/download/0.0.3/rump-0.0.3-linux-amd64;**

#. After decompression, run the following commands to add the execution permission:

   **mv rump-0.0.3-linux-amd64 rump;**

   **chmod +x rump;**

Step 2: Migrating Data
----------------------

**rump** **-from** {*source_redis_address*} **-to** {*target_redis_address*}

Parameter/Option description:

-  *{source_redis_address}*

   Source Redis instance address, in the format of redis://[user:password@]host:port/db. **[user:password@]** is optional. If the instance is accessed in password-protected mode, you must specify the password in the RFC 3986 format. **user** can be omitted, but the colon (:) cannot be omitted. For example, the address may be **redis://:mypassword@192.168.0.45:6379/1**.

   **db** is the sequence number of the database. If it is not specified, the default value is 0.

-  {*target_redis_address*}

   Address of the target Redis instance, in the same format as the source.

   In the following example, data in DB0 of the source Redis is migrated to the target Redis whose connection address is 192.168.0.153. **\*****\*** stands for the password.

   .. code-block:: console

      [root@ecs ~]# ./rump -from redis://127.0.0.1:6379/0  -to redis://:******@192.168.0.153:6379/0
      .Sync done.
      [root@ecs ~]#
