:original_name: dcs-ug-0326009.html

.. _dcs-ug-0326009:

Accessing a DCS Redis Instance Through redis-cli
================================================

Access a DCS Redis instance through redis-cli on an ECS in the same VPC. For more information on how to use other Redis clients, visit https://redis.io/clients.

.. note::

   -  Redis 3.0 does not support port customization and allows only port 6379. For Redis 4.0 and later, you can specify a port or use the default port 6379. The following uses the default port 6379. If you have specified a port, replace 6379 with the actual port.

   -  **When connecting to a Redis Cluster instance, ensure that** **-c** **is added to the command.** Otherwise, the connection will fail.

      -  Run the following command to connect to a Redis Cluster instance:

         ./redis-cli -h *{dcs_instance_address}* -p *6379* -a *{password}* **-c**

      -  Run the following command to connect to a single-node, master/standby, or Proxy Cluster instance:

         *./redis-cli -h* *{dcs_instance_address} -p 6379* -a *{password}*

      For details, see :ref:`3 <dcs-ug-0326009__en-us_topic_0148195299_li1511472544119>` and :ref:`4 <dcs-ug-0326009__en-us_topic_0148195299_li126171140194317>`.

   -  If SSL is enabled for a single-node or master/standby DCS Redis 6.0 instance, set an SSL certificate path.

      *./redis-cli -h* *{dcs_instance_address} -p 6379* -a *{password}* **--tls --cacert {certification file path}**

Prerequisites
-------------

-  The DCS Redis instance you want to access is in the **Running** state.
-  An ECS has been created. For more information on how to create ECSs, see the `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the GCC compilation environment has been installed on the ECS.

Procedure (Linux)
-----------------

#. .. _dcs-ug-0326009__en-us_topic_0148195299_li5799181918288:

   Obtain the IP address and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Install redis-cli.

   The following steps assume that your client is installed on the Linux OS.

   a. Log in to the ECS.

   b. Run the following command to download the source code package of your Redis client from http://download.redis.io/releases/redis-5.0.8.tar.gz:

      **wget http://download.redis.io/releases/redis-5.0.8.tar.gz**

   c. Run the following command to decompress the source code package of your Redis client:

      **tar -xzf redis-5.0.8.tar.gz**

   d. Run the following commands to go to the Redis directory and compile the source code of your Redis client:

      **cd redis-5.0.8**

      **make**

      **cd src**

#. .. _dcs-ug-0326009__en-us_topic_0148195299_li1511472544119:

   Access a DCS instance of a type other than Redis Cluster.

   Perform the following procedure to access a single-node, master/standby instance.

   **./redis-cli -h** *${instance IP}* **-p 6379 -a** *${password}*

   .. note::

      a. If the instance is password-free, connect it by running the **./redis-cli -h** *${instance IP}* **-p 6379** command.
      b. If the instance is password-protected, connect it by running the **./redis-cli -h** *${instance IP}* **-p 6379 -a** *${password}* command.

#. .. _dcs-ug-0326009__en-us_topic_0148195299_li126171140194317:

   Access a DCS instance of the Redis Cluster type.

   Perform the following procedure to access a DCS Redis 4.0 or 5.0 instance in Redis Cluster type.

   a. Run the following commands to access the chosen DCS Redis instance:

      **./redis-cli -h {dcs_instance_address} -p 6379 -a {password} -c**

      *{dcs_instance_address}* indicates the IP address of the DCS Redis instance, **6379** is the port used for accessing the instance, *{password}* is the password of the instance, and **-c** is used for accessing Redis Cluster nodes. The IP address and port number are obtained in :ref:`1 <dcs-ug-0326009__en-us_topic_0148195299_li5799181918288>`.

      Example:

      .. code-block::

         root@ecs-redis:~/redis-5.0.8/src# ./redis-cli -h 192.168.0.85 -p 6379 -a ****** -c
         192.168.0.85:6379>

   b. Run the following command to view the Redis Cluster node information:

      **cluster nodes**

      Each shard in a Redis Cluster has a master and a replica by default. The proceeding command provides all the information of cluster nodes.

      .. code-block::

         192.168.0.85:6379> cluster nodes
         0988ae8fd3686074c9afdcce73d7878c81a33ddc 192.168.0.231:6379@16379 slave f0141816260ca5029c56333095f015c7a058f113 0 1568084030
         000 3 connected
         1a32d809c0b743bd83b5e1c277d5d201d0140b75 192.168.0.85:6379@16379 myself,master - 0 1568084030000 2 connected 5461-10922
         c8ad7af9a12cce3c8e416fb67bd6ec9207f0082d 192.168.0.130:6379@16379 slave 1a32d809c0b743bd83b5e1c277d5d201d0140b75 0 1568084031
         000 2 connected
         7ca218299c254b5da939f8e60a940ac8171adc27 192.168.0.22:6379@16379 master - 0 1568084030000 1 connected 0-5460
         f0141816260ca5029c56333095f015c7a058f113 192.168.0.170:6379@16379 master - 0 1568084031992 3 connected 10923-16383
         19b1a400815396c6223963b013ec934a657bdc52 192.168.0.161:6379@16379 slave 7ca218299c254b5da939f8e60a940ac8171adc27 0 1568084031
         000 1 connected

      Write operations can only be performed on master nodes. The CRC16 of the key modulo 16384 is taken to compute what is the hash slot of a given key.

      As shown in the following, the value of **CRC16 (KEY) mode 16384** determines the hash slot that a given key is located at and redirects the client to the node where the hash slot is located at.

      .. code-block::

         192.168.0.170:6379> set hello world
         -> Redirected to slot [866] located at 192.168.0.22:6379
         OK
         192.168.0.22:6379> set happy day
         OK
         192.168.0.22:6379> set abc 123
         -> Redirected to slot [7638] located at 192.168.0.85:6379
         OK
         192.168.0.85:6379> get hello
         -> Redirected to slot [866] located at 192.168.0.22:6379
         "world"
         192.168.0.22:6379> get abc
         -> Redirected to slot [7638] located at 192.168.0.85:6379
         "123"
         192.168.0.85:6379>

Procedure (Windows)
-------------------

`Download <https://github.com/MicrosoftArchive/redis/tags>`__ the compilation package of the Redis client for Windows. (This is not the source code package.) Decompress the package in any directory, open the CLI tool **cmd.exe**, and go to the directory. Then, run the following command to access the DCS Redis instance:

**redis-cli.exe -h XXX -p 6379**

**XXX** indicates the IP address of the DCS instance and **6379** is an example port number used for accessing the DCS instance. For details about how to obtain the IP address and port number, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`. Change the IP address and port as required.
