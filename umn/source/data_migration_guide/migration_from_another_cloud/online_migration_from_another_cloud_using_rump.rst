:original_name: dcs-migration-090626001_0.html

.. _dcs-migration-090626001_0:

Online Migration from Another Cloud Using Rump
==============================================

Redis instances provided by some cloud service vendors do not allow **SLAVEOF**, **BGSAVE**, and **PSYNC** commands to be issued from Redis clients. As a result, redis-cli, redis-shake, and other tools cannot be used to export data. Using the **KEYS** command may block Redis. Cloud service vendors usually only support downloading backup files. This method is suitable only for offline migration, featuring longer service interruption.

`Rump <https://github.com/stickermule/rump>`__ is an open-source tool designed for migrating Redis data online. It supports migration between DBs of the same instance and between DBs of different instances. This section describes how to migrate another cloud to DCS by using Rump.

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

Notes and Constraints
---------------------

-  The target cannot be a cluster DCS instance.
-  To prevent migration command resolution errors, do not include special characters (#@:) in the instance password.
-  Before data migration, suspend your services. If data is kept being written in during the migration, some keys might be lost.
-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.

-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

-  An Elastic Cloud Server (ECS) has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.

   Select the same VPC, subnet, and security group as the DCS Redis Cluster instance, and bind EIPs to the ECS.

Installing the Rump
-------------------

#. Log in to the ECS.

#. Download `Rump (release version) <https://github.com/stickermule/rump/releases>`__.

   On 64-bit Linux, run the following command:

   .. code-block::

      wget https://github.com/stickermule/rump/releases/download/0.0.3/rump-0.0.3-linux-amd64;

#. After decompression, run the following commands to add the execution permission:

   .. code-block::

      mv rump-0.0.3-linux-amd64 rump;
      chmod +x rump;

Migrating Data
--------------

Run the following command to migrate data:

.. code-block::

   rump -from {source_redis_address}  -to {target_redis_address}

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
