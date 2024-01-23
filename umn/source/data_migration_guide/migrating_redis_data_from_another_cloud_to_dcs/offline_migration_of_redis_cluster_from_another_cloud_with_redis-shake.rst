:original_name: dcs-migrate-1117003.html

.. _dcs-migrate-1117003:

Offline Migration of Redis Cluster from Another Cloud with redis-shake
======================================================================

redis-shake is an open-source tool for migrating data online or offline (by importing backup files) between Redis Clusters. If the source Redis Cluster is deployed in another cloud, and online migration is not supported, you can migrate data by importing backup files.

The following describes how to use redis-shake for backup migration to a DCS Redis Cluster instance.

Importing Backup Files
----------------------

If the source Redis and the destitution Redis cannot be connected, or the source Redis is deployed on other clouds, you can migrate data by importing backup files.

#. Create a Redis Cluster instance on the DCS console.

   The memory of this instance cannot be smaller than that of the source Redis.

#. Run the following command to obtain the IP addresses and port numbers of all masters of the source Redis and target Redis:

   **redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes**

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image1|

   .. note::

      After Redis is installed, it runs with redis-cli. To install Redis on CentOS, run the **yum install redis** command.

#. Prepare a cloud server and install redis-shake.

   redis-shake must be able to access the target Redis and bound to an EIP.

   You can use ECS and configure the same VPC, subnet, and security group for the ECS and the DCS instance.

   `Download <https://github.com/tair-opensource/RedisShake/releases/download/release-v2.1.2-20220329/release-v2.1.2-20220329.tar.gz>`__ and decompress the release version of redis-shake. (The following uses v2.1.2 as an example. You can also use `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__.)

   |image2|

   .. note::

      If the source Redis is deployed in the data center intranet, install redis-shake on the intranet server. Export data and then upload the data to the cloud server as instructed by the following steps

#. Export the RDB file.

   -  Edit the **redis-shake.conf** file by providing the following information about all the masters of both the source and the target:

      .. code-block::

         source.type = cluster
         # If there is no password, skip the following parameter.
         source.password_raw = {source_redis_password}
         # IP addresses and port numbers of all masters of the source Redis Cluster, which are separated by semicolons (;).
         source.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}

   -  Run the following command to export the RDB file:

      **./redis-shake -type dump -conf redis-shake.conf**

      If the following information is displayed in the execution log, the backup file is exported successfully:

      .. code-block::

         execute runner[*run.CmdDump] finished!

#. Import the RDB file.

   a. Import the RDB file (or files) to the cloud server. The cloud server must be connected to the target DCS instance.

   b. Edit the redis-shake configuration file.

      Edit the **redis-shake.conf** file by providing the following information about all the masters of both the source and the target:

      .. code-block::

         target.type = cluster
         # If there is no password, skip the following parameter.
         target.password_raw = {target_redis_password}
         # IP addresses and port numbers of all masters of the target instance, which are separated by semicolons (;).
         target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}
         # List the RDB files to be imported, separated by semicolons (;).
         rdb.input = local_dump.0;local_dump.1;local_dump.2;local_dump.3

      Save and exit.

   c. Run the following command to import the RDB file to the target instance:

      **./redis-shake -type restore -conf redis-shake.conf**

      If the following information is displayed in the execution log, the backup file is imported successfully:

      .. code-block::

         Enabled http stats, set status (incr), and wait forever.

#. Verify the migration.

   After data synchronization, access the DCS Redis Cluster instance using redis-cli. Run the **info** command to query the number of keys in the **Keyspace** section to confirm that data has been fully imported.

   If the data has not been fully imported, run the **flushall** or **flushdb** command to clear the cached data in the instance, and synchronize data again.

.. |image1| image:: /_static/images/en-us_image_0293282053.png
.. |image2| image:: /_static/images/en-us_image_0293282054.png
