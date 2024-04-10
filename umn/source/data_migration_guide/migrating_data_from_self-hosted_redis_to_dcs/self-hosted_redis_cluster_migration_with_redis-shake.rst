:original_name: dcs-migrate-demo02.html

.. _dcs-migrate-demo02:

Self-Hosted Redis Cluster Migration with redis-shake
====================================================

redis-shake is an open-source tool for migrating data online or offline (by importing backup files) between Redis Clusters. Data can be migrated to DCS Redis Cluster instances seamlessly because DCS Redis Cluster inherits the native Redis Cluster design.

The following describes how to use redis-shake to migrate data to a DCS Redis Cluster instance.

Migrating Data Online
---------------------

You can migrate data online from a self-hosted Redis Cluster to a DCS Redis Cluster instance as long as the two clusters are directly connected or connected through a transit server.

Data in Redis Clusters of another cloud cannot be migrated online because the **SYNC** and **PSYNC** commands are disabled by some vendors.

#. Create a Redis Cluster instance on the DCS console.

   The memory of this instance cannot be smaller than that of the source Redis.

#. Prepare a cloud server and install redis-shake.

   redis-shake must be able to access both the source and target Redis. Bound an EIP to the cloud server.

   You can use ECS and configure the same VPC, subnet, and security group for the ECS and the DCS instance. If the source Redis is deployed on cloud servers of another cloud, allow public access to the servers.

   `Download <https://github.com/tair-opensource/RedisShake/releases/download/release-v2.1.2-20220329/release-v2.1.2-20220329.tar.gz>`__ and decompress the release version of redis-shake. (The following uses v2.1.2 as an example. You can also use `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__.)

   |image1|

#. Locate the masters of the source and target Redis Clusters and obtain the IP addresses of the masters.

   Online data migration must be performed node by node. Run the following command to query the IP addresses and port numbers of all nodes in both the source and target Redis Clusters.

   **redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes**

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image2|

   .. note::

      After Redis is installed, it runs with redis-cli. To install Redis on CentOS, run the **yum install redis** command.

#. Edit the redis-shake configuration file.

   Edit the **redis-shake.conf** file by providing the following information about all the masters of both the source and the target:

   .. code-block::

      source.type = cluster
      # If there is no password, skip the following parameter.
      source.password_raw = {source_redis_password}
      # IP addresses and port numbers of all masters of the source Redis Cluster, which are separated by semicolons (;).
      source.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}…{masterN_ip}:{masterN_port}
      target.type = cluster
      # If there is no password, skip the following parameter.
      target.password_raw = {target_redis_password}
      # IP addresses and port numbers of all masters of the target instance, which are separated by semicolons (;).
      target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}…{masterN_ip}:{masterN_port}

   Save and exit.

#. Migrate data online.

   Run the following command to synchronize data between the source and the target Redis:

   **./redis-shake -type sync -conf redis-shake.conf**

   If the following information is displayed, the full synchronization has been completed and incremental synchronization begins.

   .. code-block::

      sync rdb done.

   If the following information is displayed, no new data is incremented. You can stop the incremental synchronization by pressing **Ctrl**\ +\ **C**.

   .. code-block::

      sync:  +forwardCommands=0  +filterCommands=0  +writeBytes=0


   .. figure:: /_static/images/en-us_image_0177653842.png
      :alt: **Figure 1** Online migration using redis-shake

      **Figure 1** Online migration using redis-shake

#. Verify the migration.

   After data synchronization, access the DCS Redis Cluster instance using redis-cli. Run the **info** command to query the number of keys in the **Keyspace** section to confirm that data has been fully imported.

   If the data has not been fully imported, run the **flushall** or **flushdb** command to clear the cached data in the instance, and synchronize data again.

#. Clear the redis-shake configuration file.

Importing Backup Files
----------------------

If the source Redis and the destitution Redis cannot be connected, or the source Redis is deployed on other clouds, you can migrate data by importing backup files.

#. Create a Redis Cluster instance on the DCS console.

   The memory of this instance cannot be smaller than that of the source Redis.

#. Run the following command to obtain the IP addresses and port numbers of all masters of the source Redis and target Redis:

   **redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes**

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image3|

   .. note::

      After Redis is installed, it runs with redis-cli. To install Redis on CentOS, run the **yum install redis** command.

#. Prepare a cloud server and install redis-shake.

   redis-shake must be able to access the target Redis and bound to an EIP.

   You can use ECS and configure the same VPC, subnet, and security group for the ECS and the DCS instance.

   `Download <https://github.com/tair-opensource/RedisShake/releases/download/release-v2.1.2-20220329/release-v2.1.2-20220329.tar.gz>`__ and decompress the release version of redis-shake. (The following uses v2.1.2 as an example.)

   |image4|

   .. note::

      If the source Redis is deployed in the data center intranet, install redis-shake on the intranet server. Export data and then upload the data to the cloud server as instructed by the following steps

#. Export the RDB file.

   -  Edit the **redis-shake.conf** file by providing the following information about all the masters of both the source and the target:

      .. code-block::

         source.type = cluster
         # If there is no password, skip the following parameter.
         source.password_raw = {source_redis_password}
         # IP addresses and port numbers of all masters of the source Redis Cluster, which are separated by semicolons (;).
         source.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}…{masterN_ip}:{masterN_port}

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
         target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}…{masterN_ip}:{masterN_port}
         # List the RDB files to be imported, separated by semicolons (;).
         rdb.input = {local_dump.0};{local_dump.1};{local_dump.2};{local_dump.3}

      Save and exit.

   c. Run the following command to import the RDB file to the target instance:

      **./redis-shake -type restore -conf redis-shake.conf**

      If the following information is displayed in the execution log, the backup file is imported successfully:

      .. code-block::

         Enabled http stats, set status (incr), and wait forever.

#. Verify the migration.

   After data synchronization, access the DCS Redis Cluster instance using redis-cli. Run the **info** command to query the number of keys in the **Keyspace** section to confirm that data has been fully imported.

   If the data has not been fully imported, run the **flushall** or **flushdb** command to clear the cached data in the instance, and synchronize data again.

.. |image1| image:: /_static/images/en-us_image_0000001420267897.png
.. |image2| image:: /_static/images/en-us_image_0177600650.png
.. |image3| image:: /_static/images/en-us_image_0177654980.png
.. |image4| image:: /_static/images/en-us_image_0000001420151641.png
