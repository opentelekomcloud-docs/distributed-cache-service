:original_name: dcs-migrate-1117003.html

.. _dcs-migrate-1117003:

Backup Import from Another Cloud Using redis-shake
==================================================

redis-shake is an open-source tool for migrating data online or offline (by importing backup files) between Redis Clusters. If the source Redis Cluster is deployed in another cloud, and online migration is not supported, you can migrate data by importing backup files.

If the source Redis and the target Redis cannot be connected, or the source Redis is deployed on other clouds, you can migrate data by importing backup files.

The following describes how to use redis-shake for backup migration to a DCS Redis Cluster instance.

Notes and Constraints
---------------------

To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  A :ref:`DCS Redis instance <dcs-ug-0312003>` has been created. Note that the memory of the DCS Redis Cluster instance cannot be smaller than that of the source cluster.
-  An ECS has been created for running redis-shake. The ECS must use the same VPC, subnet, and security group as the Redis instance.

Procedure
---------

#. Access the target Redis instance using :ref:`redis-cli <dcs-ug-0326009>`. Obtain the IP address and port of the master node of the target instance.

   .. code-block::

      redis-cli -h {target_redis_address} -p {target_redis_port} -a {target_redis_password} cluster nodes

   -  *{target_redis_address}*: connection address of the target DCS Redis instance.
   -  *{target_redis_port}*: port of the target DCS Redis instance.
   -  *{target_redis_password}*: password for connecting to the target DCS Redis instance.

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image1|

#. Install redis-shake on the prepared ECS.

   a. Log in to the ECS.

   b. Download redis-shake on the ECS. Version 2.0.3 is used as an example. You can use `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__ as required.

      .. code-block::

         wget https://github.com/tair-opensource/RedisShake/releases/download/release-v2.0.3-20200724/redis-shake-v2.0.3.tar.gz

   c. Decompress the redis-shake file.

      .. code-block::

         tar -xvf redis-shake-v2.0.3.tar.gz

      If the source Redis is deployed in the data center intranet, install redis-shake on the intranet server. Export data and then upload the data to the cloud server as instructed by the following steps.

#. Export the RDB file from the source Redis console. If the RDB file cannot be exported, contact customer service of the source.

#. Import the RDB file.

   a. Import the RDB file (or files) to the cloud server. The cloud server must be connected to the target DCS instance.

   b. Edit the redis-shake configuration file **redis-shake.conf**.

      .. code-block::

         vim redis-shake.conf

      Add the following information about all the masters of the target:

      .. code-block::

         target.type = cluster
         # If there is no password, skip the following parameter.
         target.password_raw = {target_redis_password}
         # IP addresses and port numbers of all masters of the target instance, which are separated by semicolons (;).
         target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}
         # List the RDB files to be imported, separated by semicolons (;).
         rdb.input = {local_dump.0};{local_dump.1};{local_dump.2};{local_dump.3}

      Press **Esc** to exit the editing mode and enter **:wq!**. Press **Enter** to save the configuration and exit the editing interface.

   c. Run the following command to import the RDB file to the target instance:

      .. code-block::

         ./redis-shake -type restore -conf redis-shake.conf

      If the following information is displayed in the execution log, the backup file is imported successfully:

      .. code-block::

         Enabled http stats, set status (incr), and wait forever.

#. Verify the migration.

   Before data migration, if the target Redis has no data, check data integrity after the migration is complete in the following way:

   a. Connect to the source Redis and the target Redis. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

   b. Run the **info keyspace** command to check the values of **keys** and **expires**.

      |image2|

   c. Calculate the differences between the values of **keys** and **expires** of the source Redis and the target Redis. If the differences are the same, the data is complete and the migration is successful.

.. |image1| image:: /_static/images/en-us_image_0293282053.png
.. |image2| image:: /_static/images/en-us_image_0293255709.png
