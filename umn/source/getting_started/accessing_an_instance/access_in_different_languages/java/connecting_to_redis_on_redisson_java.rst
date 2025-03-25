:original_name: dcs-ug-211105004.html

.. _dcs-ug-211105004:

Connecting to Redis on Redisson (Java)
======================================

This section describes how to access a Redis instance on Redisson. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

For Spring Boot projects, Spring Data Redis is already integrated with `Jedis <https://github.com/redis/jedis>`__ and `Lettuce <https://github.com/lettuce-io/lettuce-core>`__, but does not support Redisson. `Redisson <https://github.com/redisson/redisson>`__ provides the redisson-spring-boot-starter component (https://mvnrepository.com/artifact/org.redisson/redisson) that can be used with Spring Boot.

Spring Boot 1.x is integrated with Jedis, and Spring Boot 2.x is integrated with Lettuce.

.. note::

   -  If a password was set during DCS Redis instance creation, configure the password for connecting to Redis using Redisson. Do not hard code the plaintext password.
   -  To connect to a single-node, read/write splitting, or Proxy Cluster instance, use the **useSingleServer** method of the **SingleServerConfig** object of Redisson. To connect to a master/standby instance, use the **useMasterSlaveServers** method of the **MasterSlaveServersConfig** object of Redisson. To connect to a Redis Cluster instance, use the **useClusterServers** method of the **ClusterServersConfig** object.
   -  Springboot 2.3.12.RELEASE or later is required. Redisson `3.37.0 <https://github.com/redisson/redisson/releases/tag/redisson-3.37.0>`__ or later is required.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  View the IP address/domain name and port number of the DCS Redis instance to be accessed. For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

Pom Configuration
-----------------

.. code-block::

   <!-- spring-data-redis -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
       <exclusions>
           <!--Lettuce is integrated in Spring Boot 2.x by default. This dependency needs to be deleted. -->
           <exclusion>
               <artifactId>lettuce-core</artifactId>
               <groupId>io.lettuce</groupId>
           </exclusion>
       </exclusions>
   </dependency>
   <!--Redisson's adaptation package for Spring Boot-->
   <dependency>
       <groupId>org.redisson</groupId>
       <artifactId>redisson-spring-boot-starter</artifactId>
       <version>${redisson.version}</version>
   </dependency>

.. _dcs-ug-211105004__en-us_topic_0000001220644435_section113908122580:

Bean Configuration
------------------

Spring Boot does not provide Redisson adaptation, and the **application.properties** configuration file does not have the corresponding configuration item. Therefore, you can only use Bean configuration.

-  Single-node, read/write splitting, and Proxy Cluster

   .. code-block::

      import org.redisson.Redisson;
      import org.redisson.api.RedissonClient;
      import org.redisson.codec.JsonJacksonCodec;
      import org.redisson.config.Config;
      import org.redisson.config.SingleServerConfig;
      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;

      @Configuration
      public class SingleConfig {

          @Value("${redis.address:}")
          private String redisAddress;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.database:0}")
          private Integer redisDatabase = 0;

          @Value("${redis.connect.timeout:3000}")
          private Integer redisConnectTimeout = 3000;

          @Value("${redis.connection.idle.timeout:10000}")
          private Integer redisConnectionIdleTimeout = 10000;

          @Value("${redis.connection.ping.interval:1000}")
          private Integer redisConnectionPingInterval = 1000;

          @Value("${redis.timeout:2000}")
          private Integer timeout = 2000;

          @Value("${redis.connection.pool.min.size:50}")
          private Integer redisConnectionPoolMinSize;

          @Value("${redis.connection.pool.max.size:200}")
          private Integer redisConnectionPoolMaxSize;

          @Value("${redis.retry.attempts:3}")
          private Integer redisRetryAttempts = 3;

          @Value("${redis.retry.interval:200}")
          private Integer redisRetryInterval = 200;

          @Bean
          public RedissonClient redissonClient(){
              Config redissonConfig = new Config();

              SingleServerConfig serverConfig = redissonConfig.useSingleServer();
              serverConfig.setAddress(redisAddress);
              serverConfig.setConnectionMinimumIdleSize(redisConnectionPoolMinSize);
              serverConfig.setConnectionPoolSize(redisConnectionPoolMaxSize);

              serverConfig.setDatabase(redisDatabase);
              serverConfig.setPassword(redisPassword);
              serverConfig.setConnectTimeout(redisConnectTimeout);
              serverConfig.setIdleConnectionTimeout(redisConnectionIdleTimeout);
              serverConfig.setPingConnectionInterval(redisConnectionPingInterval);
              serverConfig.setTimeout(timeout);
              serverConfig.setRetryAttempts(redisRetryAttempts);
              serverConfig.setRetryInterval(redisRetryInterval);

              redissonConfig.setCodec(new JsonJacksonCodec());
              return Redisson.create(redissonConfig);
          }
      }

-  Master/Standby

   .. code-block::

      import org.redisson.Redisson;
      import org.redisson.api.RedissonClient;
      import org.redisson.codec.JsonJacksonCodec;
      import org.redisson.config.Config;
      import org.redisson.config.MasterSlaveServersConfig;
      import org.redisson.config.ReadMode;
      import org.redisson.config.SubscriptionMode;
      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;

      import java.util.HashSet;

      @Configuration
      public class MasterStandbyConfig {
          @Value("${redis.master.address}")
          private String redisMasterAddress;

          @Value("${redis.slave.address}")
          private String redisSlaveAddress;

          @Value("${redis.database:0}")
          private Integer redisDatabase = 0;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:3000}")
          private Integer redisConnectTimeout = 3000;

          @Value("${redis.connection.idle.timeout:10000}")
          private Integer redisConnectionIdleTimeout = 10000;

          @Value("${redis.connection.ping.interval:1000}")
          private Integer redisConnectionPingInterval = 1000;

          @Value("${redis.timeout:2000}")
          private Integer timeout = 2000;

          @Value("${redis.master.connection.pool.min.size:50}")
          private Integer redisMasterConnectionPoolMinSize = 50;

          @Value("${redis.master.connection.pool.max.size:200}")
          private Integer redisMasterConnectionPoolMaxSize = 200;

          @Value("${redis.retry.attempts:3}")
          private Integer redisRetryAttempts = 3;

          @Value("${redis.retry.interval:200}")
          private Integer redisRetryInterval = 200;

          @Bean
          public RedissonClient redissonClient() {
              Config redissonConfig = new Config();

              MasterSlaveServersConfig serverConfig = redissonConfig.useMasterSlaveServers();
              serverConfig.setMasterAddress(redisMasterAddress);
              HashSet<String> slaveSet = new HashSet<>();
              slaveSet.add(redisSlaveAddress);
              serverConfig.setSlaveAddresses(slaveSet);

              serverConfig.setDatabase(redisDatabase);
              serverConfig.setPassword(redisPassword);

              serverConfig.setMasterConnectionMinimumIdleSize(redisMasterConnectionPoolMinSize);
              serverConfig.setMasterConnectionPoolSize(redisMasterConnectionPoolMaxSize);

              serverConfig.setReadMode(ReadMode.MASTER);
              serverConfig.setSubscriptionMode(SubscriptionMode.MASTER);

              serverConfig.setConnectTimeout(redisConnectTimeout);
              serverConfig.setIdleConnectionTimeout(redisConnectionIdleTimeout);
              serverConfig.setPingConnectionInterval(redisConnectionPingInterval);
              serverConfig.setTimeout(timeout);
              serverConfig.setRetryAttempts(redisRetryAttempts);
              serverConfig.setRetryInterval(redisRetryInterval);

              redissonConfig.setCodec(new JsonJacksonCodec());
              return Redisson.create(redissonConfig);
          }
      }

-  Redis Cluster

   .. code-block::

      import org.redisson.Redisson;
      import org.redisson.api.RedissonClient;
      import org.redisson.codec.JsonJacksonCodec;
      import org.redisson.config.ClusterServersConfig;
      import org.redisson.config.Config;
      import org.redisson.config.ReadMode;
      import org.redisson.config.SubscriptionMode;
      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;

      import java.util.List;

      @Configuration
      public class ClusterConfig {

          @Value("${redis.cluster.address}")
          private List<String> redisClusterAddress;

          @Value("${redis.cluster.scan.interval:5000}")
          private Integer redisClusterScanInterval = 5000;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:3000}")
          private Integer redisConnectTimeout = 3000;

          @Value("${redis.connection.idle.timeout:10000}")
          private Integer redisConnectionIdleTimeout = 10000;

          @Value("${redis.connection.ping.interval:1000}")
          private Integer redisConnectionPingInterval = 1000;

          @Value("${redis.timeout:2000}")
          private Integer timeout = 2000;

          @Value("${redis.retry.attempts:3}")
          private Integer redisRetryAttempts = 3;

          @Value("${redis.retry.interval:200}")
          private Integer redisRetryInterval = 200;

          @Value("${redis.master.connection.pool.min.size:50}")
          private Integer redisMasterConnectionPoolMinSize = 50;

          @Value("${redis.master.connection.pool.max.size:200}")
          private Integer redisMasterConnectionPoolMaxSize = 200;

          @Bean
          public RedissonClient redissonClient() {
              Config redissonConfig = new Config();

              ClusterServersConfig serverConfig = redissonConfig.useClusterServers();
              serverConfig.setNodeAddresses(redisClusterAddress);
              serverConfig.setScanInterval(redisClusterScanInterval);

              serverConfig.setPassword(redisPassword);

              serverConfig.setMasterConnectionMinimumIdleSize(redisMasterConnectionPoolMinSize);
              serverConfig.setMasterConnectionPoolSize(redisMasterConnectionPoolMaxSize);

              serverConfig.setReadMode(ReadMode.MASTER);
              serverConfig.setSubscriptionMode(SubscriptionMode.MASTER);

              serverConfig.setConnectTimeout(redisConnectTimeout);
              serverConfig.setIdleConnectionTimeout(redisConnectionIdleTimeout);
              serverConfig.setPingConnectionInterval(redisConnectionPingInterval);
              serverConfig.setTimeout(timeout);
              serverConfig.setRetryAttempts(redisRetryAttempts);
              serverConfig.setRetryInterval(redisRetryInterval);

              redissonConfig.setCodec(new JsonJacksonCodec());
              return Redisson.create(redissonConfig);
          }
      }

(Optional) Configuring SSL Connections
--------------------------------------

If SSL is enabled for an instance, to access it using SSL connections, add the **configRedissonSSL(serverConfig)** logic to the **RedissonClient** construction method **clientConfiguration()** in :ref:`Bean Configuration <dcs-ug-211105004__en-us_topic_0000001220644435_section113908122580>` and change the Redis addresses from **redis://ip:port** to **rediss://ip:port**. For details about whether your DCS Redis instances support SSL, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

.. code-block::

   private void configRedissonSSL(BaseConfig serverConfig) {
       TrustManagerFactory trustManagerFactory = null;
       try {
           //Load the CA certificate in the user-defined path.
           CertificateFactory cf = CertificateFactory.getInstance("X.509");
           Certificate ca;
           try (InputStream is = new FileInputStream(certificationPath)) {
               ca = cf.generateCertificate(is);
           }

           //Create keystore.
           String keyStoreType = KeyStore.getDefaultType();
           KeyStore keyStore = KeyStore.getInstance(keyStoreType);
           keyStore.load(null, null);
           keyStore.setCertificateEntry("ca", ca);

           //Create TrustManager.
           trustManagerFactory = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());
           trustManagerFactory.init(keyStore);
       } catch (CertificateException | IOException | KeyStoreException | NoSuchAlgorithmException e) {
           e.printStackTrace();
           return;
       }

       serverConfig.setSslTrustManagerFactory(trustManagerFactory);
   }

Parameter Description
---------------------

.. table:: **Table 1** Config parameters

   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Default Value                       | Description                                                                                                                                                                                            |
   +=====================+=====================================+========================================================================================================================================================================================================+
   | codec               | org.redisson.codec.JsonJacksonCodec | Encoding format, including JSON, Avro, Smile, CBOR, and MsgPack.                                                                                                                                       |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | threads             | Number of CPU cores x 2             | Thread pool used for executing RTopic Listener, RRemoteService, and RExecutorService.                                                                                                                  |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | executor            | null                                | The function is the same as **threads**. If this parameter is not set, a thread pool is initialized based on **threads**.                                                                              |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nettyThreads        | Number of CPU cores x 2             | Thread pool used by the TCP channel that connects to the redis-server. All channels share this connection pool and are mapped to Netty's **Bootstrap.group(...)**.                                     |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | eventLoopGroup      | null                                | The function is the same as **nettyThreads**. If this parameter is not set, an EventLoopGroup is initialized based on the **nettyThreads** parameter for the bottom-layer TCP channel to use.          |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | transportMode       | TransportMode.NIO                   | Transmission mode. The options are **NIO**, **EPOLL** (additional package required), and **KQUEUE** (additional package required).                                                                     |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | lockWatchdogTimeout | 30000                               | Timeout interval (in milliseconds) of the lock-monitoring watchdog. In the distributed lock scenario, if the **leaseTimeout** parameter is not specified, the default value of this parameter is used. |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | keepPubSubOrder     | true                                | Indicates whether to receive messages in the publish sequence. **If messages can be processed concurrently, you are advised to set this parameter to false.**                                          |
   +---------------------+-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** SingleServerConfig parameters (single-node, read/write splitting,, or Proxy Cluster)

   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | Parameter                             | Default Value | Description                                                                               |
   +=======================================+===============+===========================================================================================+
   | address                               | ``-``         | Node connection information, in redis://*ip*\ **:**\ *port* format.                       |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | database                              | 0             | ID of the database to be used.                                                            |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | connectionMinimumIdleSize             | 32            | Minimum number of connections to the master node of each shard.                           |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | connectionPoolSize                    | 64            | Maximum number of connections to the master node of each shard.                           |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | subscriptionConnectionMinimumIdleSize | 1             | Minimum number of connections to the target node for pub/sub.                             |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | subscriptionConnectionPoolSize        | 50            | Maximum number of connections to the target node for pub/sub.                             |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | subcriptionPerConnection              | 5             | Maximum number of subscriptions on each subscription connection.                          |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | connectionTimeout                     | 10000         | Connection timeout interval, in milliseconds.                                             |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | idleConnectionTimeout                 | 10000         | Maximum time (in milliseconds) for reclaiming idle connections.                           |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | pingConnectionInterval                | 30000         | Heartbeat for detecting available connections, in milliseconds. **Recommended: 3000 ms**. |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | timeout                               | 3000          | Timeout interval for waiting for a response, in milliseconds.                             |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | retryAttempts                         | 3             | Maximum number of retries upon send failures.                                             |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | retryInterval                         | 1500          | Retry interval, in milliseconds. **Recommended: 200 ms**.                                 |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+
   | clientName                            | null          | Client name.                                                                              |
   +---------------------------------------+---------------+-------------------------------------------------------------------------------------------+

.. table:: **Table 3** MasterSlaveServersConfig parameters (master/standby)

   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                             | Default Value          | Description                                                                                                                                                                                                   |
   +=======================================+========================+===============================================================================================================================================================================================================+
   | masterAddress                         | ``-``                  | Master node connection information, in redis://*ip*\ **:**\ *port* format.                                                                                                                                    |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | slaveAddresses                        | ``-``                  | Standby node connection information, in Set<redis://*ip:port*> format.                                                                                                                                        |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | readMode                              | SLAVE                  | Read mode. By default, read traffic is distributed to replica nodes. The value can be **MASTER** (recommended), **SLAVE**, or **MASTER_SLAVE**. Other values may cause access failures in failover scenarios. |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | loadBalancer                          | RoundRobinLoadBalancer | Load balancing algorithm. This parameter is valid only when **readMode** is set to **SLAVE** or **MASTER_SLAVE**. Read traffic is distributed evenly.                                                         |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | masterConnectionMinimumIdleSize       | 32                     | Minimum number of connections to the master node of each shard.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | masterConnectionPoolSize              | 64                     | Maximum number of connections to the master node of each shard.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | slaveConnectionMinimumIdleSize        | 32                     | Minimum number of connections to each replica node of each shard. If **readMode** is set to **MASTER**, the value of this parameter is invalid.                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | slaveConnectionPoolSize               | 64                     | Maximum number of connections to each replica node of each shard. If **readMode** is set to **MASTER**, the value of this parameter is invalid.                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionMode                      | SLAVE                  | Subscription mode. By default, only replica nodes handle subscription. The value can be **SLAVE** or **MASTER** (recommended).                                                                                |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionConnectionMinimumIdleSize | 1                      | Minimum number of connections to the target node for pub/sub.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionConnectionPoolSize        | 50                     | Maximum number of connections to the target node for pub/sub.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subcriptionPerConnection              | 5                      | Maximum number of subscriptions on each subscription connection.                                                                                                                                              |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | connectionTimeout                     | 10000                  | Connection timeout interval, in milliseconds.                                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | idleConnectionTimeout                 | 10000                  | Maximum time (in milliseconds) for reclaiming idle connections.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | pingConnectionInterval                | 30000                  | Heartbeat for detecting available connections, in milliseconds. **Recommended: 3000 ms**.                                                                                                                     |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | timeout                               | 3000                   | Timeout interval for waiting for a response, in milliseconds.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retryAttempts                         | 3                      | Maximum number of retries upon send failures.                                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retryInterval                         | 1500                   | Retry interval, in milliseconds. **Recommended: 200 ms**.                                                                                                                                                     |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | clientName                            | null                   | Client name.                                                                                                                                                                                                  |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 4** ClusterServersConfig parameters (Redis Cluster)

   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                             | Default Value          | Description                                                                                                                                                                                                   |
   +=======================================+========================+===============================================================================================================================================================================================================+
   | nodeAddress                           | ``-``                  | Connection addresses of cluster nodes. Each address uses the redis://*ip*\ **:**\ *port* format. Use commas (,) to separate connection addresses of different nodes.                                          |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | password                              | null                   | Password for logging in to the cluster.                                                                                                                                                                       |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scanInterval                          | 1000                   | Interval for periodically checking the cluster node status, in milliseconds.                                                                                                                                  |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | readMode                              | SLAVE                  | Read mode. By default, read traffic is distributed to replica nodes. The value can be **MASTER** (recommended), **SLAVE**, or **MASTER_SLAVE**. Other values may cause access failures in failover scenarios. |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | loadBalancer                          | RoundRobinLoadBalancer | Load balancing algorithm. This parameter is valid only when **readMode** is set to **SLAVE** or **MASTER_SLAVE**. Read traffic is distributed evenly.                                                         |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | masterConnectionMinimumIdleSize       | 32                     | Minimum number of connections to the master node of each shard.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | masterConnectionPoolSize              | 64                     | Maximum number of connections to the master node of each shard.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | slaveConnectionMinimumIdleSize        | 32                     | Minimum number of connections to each replica node of each shard. If **readMode** is set to **MASTER**, the value of this parameter is invalid.                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | slaveConnectionPoolSize               | 64                     | Maximum number of connections to each replica node of each shard. If **readMode** is set to **MASTER**, the value of this parameter is invalid.                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionMode                      | SLAVE                  | Subscription mode. By default, only replica nodes handle subscription. The value can be **SLAVE** or **MASTER** (recommended).                                                                                |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionConnectionMinimumIdleSize | 1                      | Minimum number of connections to the target node for pub/sub.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subscriptionConnectionPoolSize        | 50                     | Maximum number of connections to the target node for pub/sub.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subcriptionPerConnection              | 5                      | Maximum number of subscriptions on each subscription connection.                                                                                                                                              |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | connectionTimeout                     | 10000                  | Connection timeout interval, in milliseconds.                                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | idleConnectionTimeout                 | 10000                  | Maximum time (in milliseconds) for reclaiming idle connections.                                                                                                                                               |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | pingConnectionInterval                | 30000                  | Heartbeat for detecting available connections, in milliseconds. **Recommended: 3000**.                                                                                                                        |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | timeout                               | 3000                   | Timeout interval for waiting for a response, in milliseconds.                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retryAttempts                         | 3                      | Maximum number of retries upon send failures.                                                                                                                                                                 |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | retryInterval                         | 1500                   | Retry interval, in milliseconds. **Recommended: 200**.                                                                                                                                                        |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | clientName                            | null                   | Client name.                                                                                                                                                                                                  |
   +---------------------------------------+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Suggestion for Configuring DCS Instances
----------------------------------------

-  .. _dcs-ug-211105004__en-us_topic_0000001220644435_li62417107449:

   **readMode**

   **MASTER** is the recommended value, that is, the master node bears all read and write traffic. This is to avoid data inconsistency caused by master/replica synchronization latency. If the value is **SLAVE**, all read requests will trigger errors when replicas are faulty. If the value is **MASTER_SLAVE**, some read requests will trigger errors. Read errors last for the period specified by **failedSlaveCheckInterval** (180s by default) until the faulty nodes are removed from the available node list.

   If read traffic and write traffic need to be separated, you can use read/write splitting DCS instances. Proxy nodes are deployed in the middle to distribute read and write traffic. When a replica node is faulty, traffic is automatically switched to the master node. The switchover does not interrupt service applications, and the fault detection time window is far shorter than Redisson's window.

-  **subscriptionMode**

   Similar to :ref:`readMode <dcs-ug-211105004__en-us_topic_0000001220644435_li62417107449>`, **MASTER** is the recommended value.

-  Connection pool configuration

   .. note::

      The following calculation is applicable only to common service scenarios. You can customize it based on your service requirements.

   There is no standard connection pool size. You can configure one based on your service traffic. The following formulas are for reference:

   -  Minimum number of connections = (QPS of a single node accessing Redis)/(1000 ms/Average time spent on a single command)
   -  Maximum number of connections = (QPS of a single node accessing Redis)/(1000 ms/Average time spent on a single command) x 150%

   For example, if the QPS of a service application is about 10,000, each request needs to access Redis 10 times (that is, 100,000 accesses to Redis every second), and the service application has 10 hosts, the calculation is as follows:

   QPS of a single node accessing Redis = 100,000/10 = 10,000

   Average time spent on a single command = 20 ms (Redis takes 5 ms to 10 ms to process a single command under normal conditions. If network jitter occurs, it takes 15 ms to 20 ms.)

   Minimum number of connections = 10,000/(1000 ms/20 ms) = 200

   Maximum number of connections = 10,000/(1000 ms/20 ms) x 150% = 300

-  Retry configuration

   Redisson supports retries. You can set the following parameters based on service requirements. Generally, configure three retries, and set the retry interval to about 200 ms.

   -  **retryAttempts**: number of retry times
   -  **retryInterval**: retry interval

.. note::

   In Redisson, some APIs are implemented through LUA, and the performance is low. You are advised to use Jedis instead of Redisson.
