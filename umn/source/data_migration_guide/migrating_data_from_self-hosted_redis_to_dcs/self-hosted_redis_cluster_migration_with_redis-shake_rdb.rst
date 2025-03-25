:original_name: dcs-migrate-demo03.html

.. _dcs-migrate-demo03:

Self-Hosted Redis Cluster Migration with redis-shake (RDB)
==========================================================

redis-shake is an open-source tool for migrating data online or offline (by importing backup files) between Redis Clusters. Data can be migrated to DCS Redis Cluster instances seamlessly because DCS Redis Cluster inherits the native Redis Cluster design.

The following describes how to use Linux redis-shake to migrate self-hosted Redis Cluster to a DCS Redis Cluster instance offline.

.. note::

   If the source Redis and the target Redis cannot be connected, or the source Redis is deployed on other clouds, you can migrate data by importing backup files.

Notes and Constraints
---------------------

To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  A DCS Redis Cluster instance has been created. For details about how to create one, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.

   The memory of the target Redis instance cannot be smaller than that of the source Redis.

-  An Elastic Cloud Server (ECS) has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__. Select the same VPC, subnet, and security group as the DCS Redis Cluster instance.

Obtaining Information of the Source and Target Redis Nodes
----------------------------------------------------------

#. Connect to the source and target Redis instances, respectively. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. In online migration of Redis Clusters, the migration must be performed node by node. Run the following command to query the IP addresses and ports of all nodes in both the source and target Redis Clusters.

   .. code-block::

      redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes

   *{redis_address}* indicates the Redis connection address, *{redis_port}* indicates the Redis port, and *{redis_password}* indicates the Redis connection password.

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image1|

Installing RedisShake
---------------------

#. Log in to the ECS.

#. Run the following command on the ECS to download the redis-shake: This section uses v2.1.2 as an example. You can also download `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__ as required.

   .. code-block::

      wget https://github.com/tair-opensource/RedisShake/releases/download/release-v2.1.2-20220329/release-v2.1.2-20220329.tar.gz

#. Decompress the redis-shake file.

   .. code-block::

      tar -xvf redis-shake-v2.1.2.tar.gz

   |image2|

.. note::

   If the source cluster is deployed in the data center intranet, install redis-shake on the intranet server. Export the source cluster backup file by referring to :ref:`Exporting the Backup File <dcs-migrate-demo03__section03191023122013>`. Upload the backup to the cloud server as instructed by the following steps

.. _dcs-migrate-demo03__section03191023122013:

Exporting the Backup File
-------------------------

#. Go to the redis-shake directory.

   .. code-block::

      cd redis-shake-v2.0.3

#. Edit the **redis-shake.conf** file by providing the following information about all the masters of the source:

   .. code-block::

      vim redis-shake.conf

   The modification is as follows:

   .. code-block::

      source.type = cluster
      # If there is no password, skip the following parameter.
      source.password_raw = {source_redis_password}
      # IP addresses and port numbers of all masters of the source Redis Cluster, which are separated by semicolons (;).
      source.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}

   Press **Esc** to exit the editing mode and enter **:wq!**. Press **Enter** to save the configuration and exit the editing interface.

#. Run the following command to export the RDB file:

   .. code-block::

      ./redis-shake -type dump -conf redis-shake.conf

   If the following information is displayed in the execution log, the backup file is exported successfully:

   .. code-block::

      execute runner[*run.CmdDump] finished!

Importing the Backup File
-------------------------

#. Import the RDB file (or files) to the cloud server. The cloud server must be connected to the target DCS instance.

#. Edit the **redis-shake.conf** file by providing the following information about all the masters of the target:

   .. code-block::

      vim redis-shake.conf

   The modification is as follows:

   .. code-block::

      target.type = cluster
      # If there is no password, skip the following parameter.
      target.password_raw = {target_redis_password}
      # IP addresses and port numbers of all masters of the target instance, which are separated by semicolons (;).
      target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}
      # List the RDB files to be imported, separated by semicolons (;).
      rdb.input = {local_dump.0};{local_dump.1};{local_dump.2};{local_dump.3}

   Press **Esc** to exit the editing mode and enter **:wq!**. Press **Enter** to save the configuration and exit the editing interface.

#. Run the following command to import the RDB file to the target instance:

   .. code-block::

      ./redis-shake -type restore -conf redis-shake.conf

   If the following information is displayed in the execution log, the backup file is imported successfully:

   .. code-block::

      Enabled http stats, set status (incr), and wait forever.

Verifying the Migration
-----------------------

#. After the data synchronization, connect to the Redis Cluster DCS instance by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. Run the **info** command to check whether the data has been successfully imported as required.

   If the data has not been fully imported, run the **flushall** or **flushdb** command to clear the cached data in the target instance, and migrate data again.

#. After the verification is complete, delete the redis shake configuration file.

.. |image1| image:: /_static/images/en-us_image_0000002001365365.png
.. |image2| image:: /_static/images/en-us_image_0000001964888588.png
