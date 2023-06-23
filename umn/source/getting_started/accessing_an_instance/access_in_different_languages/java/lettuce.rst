:original_name: dcs-ug-211105002.html

.. _dcs-ug-211105002:

Lettuce
=======

Access a DCS Redis instance through Lettuce on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the Java compilation environment has been installed on the ECS.

Procedure
---------

#. View the IP address and port number of the DCS Redis instance to be accessed.

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

      a. Add the following dependency in addition to the preceding Maven dependency:

         .. code-block::

            <dependency>
               <groupId>org.apache.commons</groupId>
               <artifactId>commons-pool2</artifactId>
                <version>2.11.1</version>
             </dependency>

      b. The code is as follows:

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

   -  Example of using Lettuce to connect to a Redis Cluster DCS Redis instance with a single connection (automated topology refresh must be enabled)

      .. code-block::

         public class SingleConnectionToCluster {
             public static void main(String[] args) {
                  // Enable automated topology refresh.
                 ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                  // Periodic refresh: every time milliseconds.
                     .enablePeriodicRefresh(Duration.ofMillis(time))
                  // Triggers of adaptive refresh: MOVED redirection, ASK redirection, reconnection, unknown node (since 5.1), and slot not in any of the current shards (since 5.2).
                     .enableAllAdaptiveRefreshTriggers()
                     .build();
                 // password indicates the connection password. If there is no password, delete "password@". If there is a password and it contains special characters, conversion is required.
                 RedisClusterClient redisClient = RedisClusterClient.create("redis://password@host:port");
                 redisClient.setOptions(ClusterClientOptions.builder()
                     .topologyRefreshOptions(topologyRefreshOptions)
                     .build());
                 StatefulRedisClusterConnection<String, String> connection = redisClient.connect();
                  // Preferentially read data from the replicas.
                  connection.setReadFrom(ReadFrom.REPLICA_PREFERRED);
                 RedisAdvancedClusterCommands<String, String> syncCommands = connection.sync();
                 syncCommands.set("key", "value");
                 System.out.println("Connected to RedisCluster:" + syncCommands.get("key"));
                 // Close the connection.
                 connection.close();
                 // Close the client.
                 redisClient.shutdown();
             }
         }

   -  Example code for connecting to Redis Cluster with connection pooling

      a. Add the following dependency in addition to the preceding Maven dependency:

         .. code-block::

            <dependency>
               <groupId>org.apache.commons</groupId>
               <artifactId>commons-pool2</artifactId>
                <version>2.11.1</version>
             </dependency>

      b. The code is as follows (automated topology refresh must be enabled):

         .. code-block::

            public class PoolConnectionToCluster {
                public static void main(String[] args) {
                     // Enable automated topology refresh.
                    ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                     // Periodic refresh every time milliseconds.
                        .enablePeriodicRefresh(Duration.ofMillis(time))
                     // Triggers of adaptive refresh: MOVED redirection, ASK redirection, reconnection, unknown node (since 5.1), and slot not in any of the current shards (since 5.2).
                        .enableAllAdaptiveRefreshTriggers()
                        .build();
                    // password indicates the connection password. If there is no password, delete "password@". If there is a password and it contains special characters, conversion is required.
                    RedisClusterClient redisClient = RedisClusterClient.create("redis://password@host:port");
                    redisClient.setOptions(ClusterClientOptions.builder()
                        .topologyRefreshOptions(topologyRefreshOptions)
                        .build());
                    GenericObjectPoolConfig<StatefulRedisClusterConnection<String, String>> genericObjectPoolConfig
                        = new GenericObjectPoolConfig();
                    // Connection pool parameters
                    genericObjectPoolConfig.setMaxIdle(3);
                    genericObjectPoolConfig.setMinIdle(2);
                    genericObjectPoolConfig.setMaxTotal(3);
                    genericObjectPoolConfig.setTimeBetweenEvictionRuns(Duration.ofMillis(2000));
                    genericObjectPoolConfig.setMaxWait(Duration.ofMillis(5000));
                    GenericObjectPool<StatefulRedisClusterConnection<String, String>> pool = ConnectionPoolSupport
                        .createGenericObjectPool(() -> redisClient.connect(), genericObjectPoolConfig);
                    // Obtain a connection to perform operations.
                    try (StatefulRedisClusterConnection<String, String> con = pool.borrowObject()) {
                        // Preferentially read data from the replicas.
                         con.setReadFrom(ReadFrom.REPLICA_PREFERRED);
                        RedisAdvancedClusterCommands<String, String> syncCommands = con.sync();
                        syncCommands.set("key", "value");
                        System.out.println("Connected to RedisCluster:" + syncCommands.get("key"));
                    } catch (Exception e) {
                        e.printStackTrace();
                    } finally {
                // Close the resources.
                        pool.close();
                        redisClient.shutdown();
                    }
                }
            }

   **host** is the IP address of the DCS instance, **port** is the port number of the DCS instance, and **password** is the password of the DCS instance. Specify these parameters as required before running the code. Connection pooling is recommended. Adjust parameters such as **timeout**, **MaxTotal** (maximum number of connections), **MinIdle** (minimum number of idle connections), **MaxIdle** (maximum number of idle connections), and **MaxWait** (maximum waiting time) based on service requirements.
