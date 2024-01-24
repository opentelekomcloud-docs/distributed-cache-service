:original_name: dcs-migration-0312011.html

.. _dcs-migration-0312011:

Self-Hosted Redis Migration with redis-cli (RDB)
================================================

Introduction
------------

redis-cli is the command line tool of Redis, which can be used after you install the Redis server.

redis-cli supports data export as an RDB file. If your Redis service does not support AOF file export, use redis-cli to obtain an RDB file. Then, use another tool (such as redis-shake) to import the file to a DCS instance.

Operations described in this section are performed on the Linux OS.

Run the following command to download Redis. redis-cli can be used after installation and compilation.

**wget http://download.redis.io/releases/redis-5.0.8.tar.gz**

.. important::

   The source Redis instance must support the **SYNC** command, which is required when exporting the RDB file using redis-cli.

   The **SYNC** command is not supported by DCS Reds 4.0/5.0/6.0 instances and cannot be used to export RDB files. To back up master/standby instance data, use the backup and restoration function provided by the DCS console.

Step 1: Preparation for Data Export
-----------------------------------

For master/standby or cluster DCS instances, there is a delay in writing data into an RDB file based on the delay policies configured in the **redis.conf** file. Therefore, before data export, learn the RDB policy configurations of the Redis instance to be migrated, suspend your service systems, and then write the required number of test keys into the Redis instance. This ensures that the RDB file is newly generated.

For the Redis service provided by a third-party cloud platform, you can contact its technical support to learn data writing policy configurations of an RDB file.

For example, the default RDB policy configurations in the **redis.conf** file are as follows:

.. code-block::

   save 900 1 //Writes changed data into an RDB file if there is any data change within 900s.
   save 300 10 //Writes changed data into an RDB file if there are more than 10 data changes within 300s.
   save 60 10000 //Writes changed data into an RDB file if there are more than 10,000 data changes within 60s.

Based on the preceding policy configurations, after stopping your service systems from writing data into the Redis instances, you can manually write test data to trigger the policies, so that all service data can be synchronized to the RDB file.

You can delete the test data after data import.

.. note::

   If there is any DB not used by your service systems, you can write test data into the DB, and run the **flushdb** command to clear the DB after importing data into DCS.

Step 2: Exporting an RDB File
-----------------------------

.. important::

   #. Migrate data during off-peak hours.
   #. When exporting Redis Cluster data, individually export the data of each node in the cluster, and then import the data node by node.

Run the following command to export the RDB file:

**redis-cli -h {source_redis_address} -p 6379 -a {password} --rdb {output.rdb}**

If "Transfer finished with success." is displayed after the command is executed, the file is exported successfully.

Step 3: Uploading the RDB File to ECS
-------------------------------------

#. To save the transmission time, compress the RDB file before transmission.
#. Upload the compressed file to ECS using an appropriate mode (for example, SFTP mode).

.. note::

   Ensure that the ECS has sufficient disk space for data file decompression, and can communicate with the DCS instance. Generally, the ECS and DCS instance are configured to belong to the same VPC and subnet, and the configured security group rules do not restrict access ports. For details about how to configure a security group, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

Step 4: Importing Data
----------------------

Use redis-shake to import data.

Step 5: Verifying Migration
---------------------------

After the data is imported successfully, access the DCS instance and run the **info** command to check whether the data has been successfully imported as required.

If the data import fails, analyze the cause, modify the data import statement, run the **flushall** or **flushdb** command to clear the cached data in the instance, and import the data again.

Efficiency of Data Export and Import
------------------------------------

Compared with master/standby instances, single-node instances without data persistence configured require a longer time for export of an RDB file, because the RDB file is temporarily generated.

It takes 4s to 10s to import 1 million data records (20 bytes per data record) in a VPC.
