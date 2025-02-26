:original_name: dcs-migration-0312011.html

.. _dcs-migration-0312011:

Self-Hosted Redis Migration with redis-cli (RDB)
================================================

redis-cli is the command line tool of Redis, which can be used after you install the Redis server. redis-cli supports data export as an RDB file. If your Redis service does not support AOF file export, use redis-cli to obtain an RDB file. Then, use another tool (such as redis-shake) to import the file to a DCS instance.

Notes and Constraints
---------------------

-  Migrate data during off-peak hours.
-  When the source is Redis native cluster data, individually export the data of each node in the cluster, and then import the data node by node.
-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.
-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

-  An Elastic Cloud Server (ECS) has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  **The source self-hosted Redis instance must support the** **SYNC** **command.** Otherwise, the RDB file cannot be exported using redis-cli.

Exporting the RDB File
----------------------

#. Prepare for the export.

   For master/standby or cluster DCS instances, there is a delay in writing data into an RDB file based on the delay policies configured in the **redis.conf** file. Before data export, learn the RDB policy configurations of the Redis instance to be migrated, suspend your service systems, and then write the required number of test data into the Redis instance. This ensures that the RDB file is newly generated.

   For example, the default RDB policy configurations in the **redis.conf** file are as follows:

   .. code-block::

      save 900 1 //Writes changed data into an RDB file if there is any data change within 900s.
      save 300 10 //Writes changed data into an RDB file if there are more than 10 data changes within 300s.
      save 60 10000 //Writes changed data into an RDB file if there are more than 10,000 data changes within 60s.

   Based on the preceding policy configurations, after stopping your service systems from writing data into the Redis instances, you can write test data to trigger the policies, so that all service data can be synchronized to the RDB file.

   You can delete the test data after data import.

   .. note::

      -  If there is any DB not used by your service systems, you can write test data into the DB, and run the **flushdb** command to clear the database after importing data into DCS.
      -  Compared with master/standby instances, single-node instances without data persistence configured require a longer time for export of an RDB file, because the RDB file is temporarily generated.

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

#. Run the following command to export the RDB file:

   .. code-block::

      redis-cli -h {source_redis_address} -p {port} -a {password} --rdb {output.rdb}

   *{source_redis_address}* is the connection address of the source Redis, *{port}* is the port of the source Redis, *{password}* is the connection password of the source Redis, and *{output.rdb}* is the RDB file name.

   If "Transfer finished with success." is displayed after the command is executed, the file is exported successfully.

Uploading the RDB File to ECS
-----------------------------

To save time, you are advised to compress the RDB file and upload it to ECS using an appropriate mode (for example, SFTP mode).

.. note::

   Ensure that the ECS has sufficient disk space for data file decompression, and can communicate with the DCS instance. Generally, the ECS and DCS instance are configured to belong to the same VPC and subnet, and the configured security group rules do not restrict access ports. For details about how to configure a security group, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

Importing Data
--------------

Use redis-shake to import data.

It takes 4 to 10 seconds to import an RDB file of 1 million data (20 bytes per data segment) to a VPC.

Verifying the Migration
-----------------------

After the data is imported successfully, access the DCS instance and run the **info** command to check whether the data has been successfully imported as required. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

If the import fails, check the procedure. If the import command is incorrect, run the **flushall** or **flushdb** command to clear the cache data in the target instance, modify the import command, and try again.
