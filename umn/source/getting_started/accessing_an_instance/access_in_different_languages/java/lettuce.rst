:original_name: dcs-ug-211011001.html

.. _dcs-ug-211011001:

Lettuce
=======

Access a Redis Cluster instance through Lettuce on an ECS in the same VPC. For more information on how to use other Redis clients, visit https://redis.io/clients.

.. note::

   If a password was set during DCS Redis instance creation, configure the password for connecting to Redis using Lettuce. Do not hard code the plaintext password.

   To connect to a single-node, master/standby, or Proxy Cluster instance, use the RedisClient object of Lettuce. To connect to a Redis Cluster instance, use the RedisClusterClient object.

Prerequisites
-------------

-  The DCS Redis instance you want to access is in the **Running** state.
-  An ECS has been created. For more information on how to create ECSs, see the `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the Java compilation environment has been installed on the ECS.

Procedure
---------

#. View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Use Maven to add the following dependency to the **pom.xml** file:

   .. code-block::

      <dependency>
        <groupId>io.lettuce</groupId>
        <artifactId>lettuce-core</artifactId>
        <version>6.1.6.RELEASE</version>
      </dependency>

#. Use Lettuce (a Java client) to connect to the DCS instance.

   -  Example of using Lettuce to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with a single connection

      .. code-block::

         // password indicates the connection password. If there is no password, delete "password@". If there is a password and it contains special characters, conversion is required.
         RedisClient redisClient = RedisClient.create("redis://password@host:port");
         StatefulRedisConnection<String, String> connection = redisClient.connect();
         RedisCommands<String, String> syncCommands = connection.sync();
         syncCommands.set("key", "value");
         System.out.println("Connected to Redis:" + syncCommands.get("key"));
         // Close the connection.
         connection.close();
         // Close the client.
         redisClient.shutdown();

   -  Example of using Lettuce to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with connection pooling

      .. code-block::

         // password indicates the connection password. If there is no password, delete "password@". If there is a password and it contains special characters, conversion is required.
         RedisClient clusterClient = RedisClient.create("redis://password@host:port");
         GenericObjectPoolConfig<StatefulRedisConnection<String, String>> genericObjectPoolConfig = new GenericObjectPoolConfig();
         // Connection pool parameters
         genericObjectPoolConfig.setMaxIdle(3);
         genericObjectPoolConfig.setMinIdle(2);
         genericObjectPoolConfig.setMaxTotal(3);
         genericObjectPoolConfig.setMaxWaitMillis(-1);
         GenericObjectPool<StatefulRedisConnection<String, String>> pool = ConnectionPoolSupport
                 .createGenericObjectPool(() -> clusterClient.connect(), genericObjectPoolConfig);
         // Obtain a connection to perform operations.
         try (StatefulRedisConnection<String, String> con = pool.borrowObject()) {
             RedisCommands<String, String> sync = con.sync();
             sync.set("key", "value");
             System.out.println("Connected by pool:" + sync.get("key"));
         } catch (Exception e) {
             e.printStackTrace();
         }finally {
             // Close the resources.
             pool.close();
             clusterClient.shutdown();
         }

   -  Example of using Lettuce to connect to a Redis Cluster

      .. code-block::

         // password indicates the connection password. If there is no password, delete "password@". If there is a password and it contains special characters, conversion is required.
         RedisClusterClient redisClient = RedisClusterClient.create("redis://password@host:port");
         StatefulRedisClusterConnection<String, String> connection = redisClient.connect();
         RedisAdvancedClusterCommands<String, String> syncCommands = connection.sync();
         syncCommands.set("key", "value");
         System.out.println("Connected to RedisCluster:"+syncCommands.get("key"));
         // Close the connection.
         connection.close();
         // Close the client.
         redisClient.shutdown();
