:original_name: dcs-migration-0312010.html

.. _dcs-migration-0312010:

Self-Hosted Redis Migration with redis-cli (AOF)
================================================

redis-cli is the command line tool of Redis, which can be used after you install the Redis server. This section describes how to use redis-cli to migrate a data from a self-hosted Redis instance to a DCS instance.

An AOF file can be generated quickly. It applies to scenarios where you can access the Redis server and modify the configurations, such as scenarios with self-built Redis servers.

Notes and Constraints
---------------------

-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.
-  Smaller target instance specifications than source instance specifications may cause failures.
-  Migrate data during off-peak hours.
-  Before data migration, suspend your services so that data changes newly generated will not be lost during the migration.

Prerequisites
-------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.
-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.
-  An Elastic Cloud Server (ECS) has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.

Generating an AOF File
----------------------

#. Log in to the ECS.

#. Install redis-cli. The following steps assume that your client is installed on the Linux OS.

   a. Run the following command to download Redis: You can also install other Redis versions. For details, see the `Redis official website <https://redis.io/download?spm=a2c4g.11186623.2.15.4e732074zS4LSS#installation>`__.

      .. code-block::

         wget http://download.redis.io/releases/redis-5.0.8.tar.gz

   b. Run the following command to decompress the source code package of your Redis client:

      .. code-block::

         tar -xzf redis-5.0.8.tar.gz

   c. Run the following commands to go to the Redis directory and compile the source code of your Redis client:

      .. code-block::

         cd redis-5.0.8
         make
         cd src

#. Run the following command to enable cache persistence and obtain the AOF persistence file:

   .. code-block::

      redis-cli -h {source_redis_address} -p {port} -a {password}  config set appendonly yes

   *{source_redis_address}* is the connection address of the source Redis, *{port}* is the port of the source Redis, and *{password}* is the connection password of the source Redis.

   If the size of the AOF file does not change after you have enabled persistence, the AOF file contains full cached data.

   .. note::

      -  To find out the path for storing the AOF file, use redis-cli to access the Redis instance, and run the **config get dir** command. Unless otherwise specified, the file is named as **appendonly.aof** by default.
      -  To disable synchronization after the AOF file is generated, use redis-cli to log in to the Redis instance and run the **config set appendonly no** command.

Uploading the AOF file to ECS
-----------------------------

To save time, you are advised to compress the AOF file and upload it to ECS using an appropriate mode (for example, SFTP mode).

.. note::

   Ensure that the ECS has sufficient disk space for data file decompression, and can communicate with the DCS instance. Generally, the ECS and DCS instance are configured to belong to the same VPC and subnet, and the configured security group rules do not restrict access ports. For details about how to configure a security group, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

Importing Data
--------------

Log in to the ECS and run the following command to import data.

.. code-block::

   redis-cli -h {dcs_instance_address} -p {port} -a {password} --pipe < appendonly.aof

*{dcs_instance_address}* indicates the address of the target Redis instance, *{port}* indicates the port of the target Redis instance, and *{password}* indicates the password for connecting to the target Redis instance.

It takes 4 to 10 seconds to import an AOF file of 1 million data (20 bytes per data segment) to a VPC.

Verifying the Migration
-----------------------

After the data is imported successfully, access the DCS instance and run the **info** command to check whether the data has been successfully imported as required. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

If the import fails, check the procedure. If the import command is incorrect, run the **flushall** or **flushdb** command to clear the cache data in the target instance, modify the import command, and try again.
