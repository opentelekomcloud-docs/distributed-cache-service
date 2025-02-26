:original_name: dcs-migrate-demo02.html

.. _dcs-migrate-demo02:

Self-Hosted Redis Cluster Migration with redis-shake (Online)
=============================================================

redis-shake is an open-source tool for migrating data online or offline (by importing backup files) between Redis Clusters. Data can be migrated to DCS Redis Cluster instances seamlessly because DCS Redis Cluster inherits the native Redis Cluster design.

The following describes how to use Linux redis-shake to migrate self-hosted Redis Cluster to a DCS Redis Cluster instance online.

Notes and Constraints
---------------------

-  To migrate data from a self-hosted Redis Cluster instance to a DCS Redis Cluster instance online, ensure that the source Redis is connected to the target Redis, or use a transit cloud server to connect the source and target cluster instances.
-  To migrate to an instance with SSL enabled, disable the SSL setting first. For details, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

Prerequisites
-------------

-  If a target DCS Redis instance is not available, create one first. For details, see :ref:`Creating a DCS Redis Instance <dcs-ug-0312003>`.
-  If you already have a DCS Redis instance, you do not need to create one again. For comparing migration data and reserving sufficient memory, you are advised to clear the instance data before the migration. For details, see :ref:`Clearing DCS Instance Data <dcs-ug-0312018>`. If any data exists on the target instance, duplicate data between the source and target is overwritten. If the data exists only on the target instance, the data will be retained.

-  An Elastic Cloud Server (ECS) has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.

   Select the same VPC, subnet, and security group as the DCS Redis Cluster instance, and bind EIPs to the ECS.

-  If the source self-hosted Redis Cluster is deployed on cloud servers of another cloud, allow public access to the servers.

Obtaining Information of the Source and Target Redis Nodes
----------------------------------------------------------

#. Connect to the source and target Redis instances, respectively. Connect to Redis by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. In online migration of Redis Clusters, the migration must be performed node by node. Run the following command to query the IP addresses and ports of all nodes in both the source and target Redis Clusters.

   .. code-block::

      redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes

   *{redis_address}* indicates the Redis connection address, *{redis_port}* indicates the Redis port, and *{redis_password}* indicates the Redis connection password.

   In the command output similar to the following, obtain the IP addresses and ports of all masters.

   |image1|

Configuring the redis-shake Tool
--------------------------------

#. Log in to the ECS.

#. Run the following command on the ECS to download the redis-shake: This section uses v2.1.2 as an example. You can also download `other redis-shake versions <https://github.com/alibaba/RedisShake/releases>`__ as required.

   .. code-block::

      wget https://github.com/tair-opensource/RedisShake/releases/download/release-v2.1.2-20220329/release-v2.1.2-20220329.tar.gz

#. Decompress the redis-shake file.

   .. code-block::

      tar -xvf redis-shake-v2.1.2.tar.gz

   |image2|

#. Go to the redis-shake directory.

   .. code-block::

      cd redis-shake-v2.0.3

#. Edit the **redis-shake.conf** file by providing the following information about all the masters of both the source and the target:

   .. code-block::

      vim redis-shake.conf

   The modification is as follows:

   .. code-block::

      source.type = cluster
      # If there is no password, skip the following parameter.
      source.password_raw = {source_redis_password}
      # IP addresses and port numbers of all masters of the source Redis Cluster, which are separated by semicolons (;).
      source.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}
      target.type = cluster
      # If there is no password, skip the following parameter.
      target.password_raw = {target_redis_password}
      # IP addresses and port numbers of all masters of the target instance, which are separated by semicolons (;).
      target.address = {master1_ip}:{master1_port};{master2_ip}:{master2_port}...{masterN_ip}:{masterN_port}

   Press **Esc** to exit the editing mode and enter **:wq!**. Press **Enter** to save the configuration and exit the editing interface.

Migrating Data Online
---------------------

Run the following command to synchronize data between the source and the target Redis:

.. code-block::

   ./redis-shake -type sync -conf redis-shake.conf

If the following information is displayed, the full synchronization has been completed and incremental synchronization begins.

.. code-block::

   sync rdb done.

If the following information is displayed, no new data is incremented. You can stop the incremental synchronization by pressing **Ctrl**\ +\ **C**.

.. code-block::

   sync:  +forwardCommands=0  +filterCommands=0  +writeBytes=0


.. figure:: /_static/images/en-us_image_0000002000818973.png
   :alt: **Figure 1** Online migration using redis-shake

   **Figure 1** Online migration using redis-shake

Verifying the Migration
-----------------------

#. After the data synchronization, connect to the Redis Cluster DCS instance by referring to :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.

#. Run the **info** command to check whether the data has been successfully imported as required.

   If the data has not been fully imported, run the **flushall** or **flushdb** command to clear the cached data in the target instance, and migrate data again.

#. After the verification is complete, delete the redis shake configuration file.

.. |image1| image:: /_static/images/en-us_image_0000002001365365.png
.. |image2| image:: /_static/images/en-us_image_0000001964418130.png
