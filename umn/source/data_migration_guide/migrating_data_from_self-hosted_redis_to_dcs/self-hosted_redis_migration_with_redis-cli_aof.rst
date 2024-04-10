:original_name: dcs-migration-0312010.html

.. _dcs-migration-0312010:

Self-Hosted Redis Migration with redis-cli (AOF)
================================================

Introduction
------------

redis-cli is the command line tool of Redis, which can be used after you install the Redis server.

Run the following command to download Redis:

**wget http://download.redis.io/releases/redis-5.0.8.tar.gz**

This section describes how to use redis-cli to migrate a data from a self-hosted Redis instance to a DCS instance.

Step 1: Generating an AOF File
------------------------------

.. important::

   -  Before data migration, suspend your services so that data changes newly generated will not be lost during the migration.
   -  Migrate data during off-peak hours.

Run the following command to enable cache persistence and obtain an AOF persistence file:

**redis-cli -h {source_redis_address} -p 6379 -a {password} config set appendonly yes**

If the size of the AOF file does not change after you have enabled persistence, the AOF file contains full cached data.

.. note::

   -  To find out the path for storing the AOF file, use redis-cli to access the Redis instance, and run the **config get dir** command. Unless otherwise specified, the file is named as **appendonly.aof** by default.
   -  To disable synchronization after the AOF file is generated, use redis-cli to log in to the Redis instance and run the **config set appendonly no** command.

Step 2: Uploading the AOF file to ECS
-------------------------------------

#. To save the transmission time, compress the AOF file before transmission.
#. Upload the compressed file to ECS using an appropriate mode (for example, SFTP mode).

.. note::

   Ensure that the ECS has sufficient disk space for data file decompression, and can communicate with the DCS instance. Generally, the ECS and DCS instance are configured to belong to the same VPC and subnet, and the configured security group rules do not restrict access ports. For details about how to configure a security group, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

Step 3: Importing Data
----------------------

**redis-cli -h {dcs_instance_address} -p 6379 -a {password} --pipe < appendonly.aof**

Step 4: Verifying Migration
---------------------------

After the data is imported successfully, access the DCS instance and run the **info** command to check whether the data has been successfully imported as required.

If the data import fails, analyze the cause, modify the data import statement, run the **flushall** or **flushdb** command to clear the cached data in the instance, and import the data again.

Efficiency of Data Export and Import
------------------------------------

An AOF file can be generated quickly. It applies to scenarios where you can access the Redis server and modify the configurations, such as scenarios with self-built Redis servers.

It takes 4s to 10s to import 1 million data records (20 bytes per data record) in a VPC.
