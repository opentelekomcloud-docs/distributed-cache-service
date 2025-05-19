:original_name: dcs-ug-211105002.html

.. _dcs-ug-211105002:

Connecting to Redis on Lettuce (Java)
=====================================

This section describes how to access a Redis instance on Lettuce. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

Spring Data Redis is already integrated with `Jedis <https://github.com/redis/jedis>`__ and `Lettuce <https://github.com/lettuce-io/lettuce-core>`__ for Spring Boot projects. In addition, Spring Boot 1.x is integrated with Jedis, and Spring Boot 2.x with Lettuce. Therefore, you do not need to import Lettuce in Spring Boot 2.x and later projects.

Notes and Constraints
---------------------

Springboot 2.3.12.RELEASE or later is required. Lettuce `6.3.0.RELEASE <https://github.com/redis/lettuce/releases/tag/6.3.0.RELEASE>`__ or later is required.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  View the IP address/domain name and port number of the DCS Redis instance to be accessed. For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

Pom Configuration
-----------------

.. code-block::

   <!-- Enable Spring Data Redis, Lettuce-supported SDK is integrated by default -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   <dependency>
       <groupId>io.lettuce</groupId>
       <artifactId>lettuce-core</artifactId>
       <version>${lettuce.version}</version>
   </dependency>

application.properties Configuration
------------------------------------

-  Single-node, master/standby, read/write splitting, and Proxy Cluster

   .. code-block::

      #Redis host
      spring.redis.host=<host>
      #Redis port
      spring.redis.port=<port>
      #Redis database number
      spring.redis.database=0
      #Redis password
      spring.redis.password=<password>
      #Redis read/write timeout
      spring.redis.timeout=2000

-  Redis Cluster

   .. code-block::

      #Redis Cluster node information
      spring.redis.cluster.nodes=<ip:port>,<ip:port>,<ip:port>
      #Redis Cluster max redirecting times
      spring.redis.cluster.max-redirects=3
      #Redis Cluster node password
      spring.redis.password=<password>
      #Redis Cluster timeout
      spring.redis.timeout=2000
      #Enable adaptive topology refresh
      spring.redis.lettuce.cluster.refresh.adaptive=true
      #Enable topology refresh every 10 seconds
      spring.redis.lettuce.cluster.refresh.period=10S

.. _dcs-ug-211105002__en-us_topic_0000001220636227_section113908122580:

Bean Configuration
------------------

-  Single-node, master/standby, read/write splitting, and Proxy Cluster

   .. code-block::

      import java.time.Duration;

      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
      import org.springframework.data.redis.connection.RedisConnectionFactory;
      import org.springframework.data.redis.connection.RedisStandaloneConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceClientConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;

      import io.lettuce.core.ClientOptions;
      import io.lettuce.core.SocketOptions;

      /**
      * Lettuce non-pooling configuration (use either this or the application.properties configuration)
      */
      @Configuration
      public class RedisConfiguration {

          @Value("${redis.host}")
          private String redisHost;

          @Value("${redis.port:6379}")
          private Integer redisPort = 6379;

          @Value("${redis.database:0}")
          private Integer redisDatabase = 0;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:2000}")
          private Integer redisConnectTimeout = 2000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(LettuceClientConfiguration clientConfiguration) {

              RedisStandaloneConfiguration standaloneConfiguration = new RedisStandaloneConfiguration();
              standaloneConfiguration.setHostName(redisHost);
              standaloneConfiguration.setPort(redisPort);
              standaloneConfiguration.setDatabase(redisDatabase);
              standaloneConfiguration.setPassword(redisPassword);

              LettuceConnectionFactory connectionFactory = new LettuceConnectionFactory(standaloneConfiguration, clientConfiguration);
              connectionFactory.setDatabase(redisDatabase);
              return connectionFactory;
          }

          @Bean
          public LettuceClientConfiguration clientConfiguration() {

              SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

              ClientOptions clientOptions = ClientOptions.builder()
                      .autoReconnect(true)
                      .pingBeforeActivateConnection(true)
                      .cancelCommandsOnReconnectFailure(false)
                      .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
                      .socketOptions(socketOptions)
                      .build();


              LettuceClientConfiguration clientConfiguration = LettuceClientConfiguration.builder()
                      .commandTimeout(Duration.ofMillis(redisReadTimeout))
                      .readFrom(ReadFrom.MASTER)
                      .clientOptions(clientOptions)
                      .build();

              return clientConfiguration;
          }
      }

-  Pooling configuration for single-node, master/standby, read/write splitting, and Proxy Cluster instances

   Enable the pooling component

   .. code-block::

      <dependency>
          <groupId>org.apache.commons</groupId>
          <artifactId>commons-pool2</artifactId>
          <version>2.11.1</version>
      </dependency>

   Code

   .. code-block::

      import java.time.Duration;

      import org.apache.commons.pool2.impl.GenericObjectPoolConfig;
      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
      import org.springframework.data.redis.connection.RedisConnectionFactory;
      import org.springframework.data.redis.connection.RedisStandaloneConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceClientConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
      import org.springframework.data.redis.connection.lettuce.LettucePoolingClientConfiguration;

      import io.lettuce.core.ClientOptions;
      import io.lettuce.core.SocketOptions;

      /**
      * Lettuce pooling configuration
      */
      @Configuration
      public class RedisPoolConfiguration {
          @Value("${redis.host}")
          private String redisHost;

          @Value("${redis.port:6379}")
          private Integer redisPort = 6379;

          @Value("${redis.database:0}")
          private Integer redisDatabase = 0;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:2000}")
          private Integer redisConnectTimeout = 2000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Value("${redis.pool.minSize:50}")
          private Integer redisPoolMinSize = 50;

          @Value("${redis.pool.maxSize:200}")
          private Integer redisPoolMaxSize = 200;

          @Value("${redis.pool.maxWaitMillis:2000}")
          private Integer redisPoolMaxWaitMillis = 2000;

          @Value("${redis.pool.softMinEvictableIdleTimeMillis:1800000}")
          private Integer redisPoolSoftMinEvictableIdleTimeMillis = 30 * 60 * 1000;

          @Value("${redis.pool.timeBetweenEvictionRunsMillis:60000}")
          private Integer redisPoolBetweenEvictionRunsMillis = 60 * 1000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(LettuceClientConfiguration clientConfiguration) {

              RedisStandaloneConfiguration standaloneConfiguration = new RedisStandaloneConfiguration();
              standaloneConfiguration.setHostName(redisHost);
              standaloneConfiguration.setPort(redisPort);
              standaloneConfiguration.setDatabase(redisDatabase);
              standaloneConfiguration.setPassword(redisPassword);

              LettuceConnectionFactory connectionFactory = new LettuceConnectionFactory(standaloneConfiguration, clientConfiguration);
              connectionFactory.setDatabase(redisDatabase);
              //Disable sharing native connection before enabling pooling
              connectionFactory.setShareNativeConnection(false);
              return connectionFactory;
          }

          @Bean
          public LettuceClientConfiguration clientConfiguration() {

              SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

              ClientOptions clientOptions = ClientOptions.builder()
                      .autoReconnect(true)
                      .pingBeforeActivateConnection(true)
                      .cancelCommandsOnReconnectFailure(false)
                      .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
                      .socketOptions(socketOptions)
                      .build();


              LettucePoolingClientConfiguration clientConfiguration = LettucePoolingClientConfiguration.builder()
                      .poolConfig(poolConfig())
                      .commandTimeout(Duration.ofMillis(redisReadTimeout))
                      .clientOptions(clientOptions)
                      .readFrom(ReadFrom.MASTER)
                      .build();
              return poolingClientConfiguration;
          }

          private GenericObjectPoolConfig redisPoolConfig() {
              GenericObjectPoolConfig poolConfig = new GenericObjectPoolConfig();
              //Minimum idle connections in the pool
              poolConfig.setMinIdle(redisPoolMinSize);
              //Maximum idle connections in the pool
              poolConfig.setMaxIdle(redisPoolMaxSize);
              //Maximum total connections in the pool
              poolConfig.setMaxTotal(redisPoolMaxSize);
              //Wait when pool is exhausted? Set to true to wait. To validate setMaxWait, it has to be true.
              poolConfig.setBlockWhenExhausted(true);
              //Max allowed time to wait for connection after pool is exhausted. The default value -1 indicates to wait indefinitely.
              poolConfig.setMaxWait(Duration.ofMillis(redisPoolMaxWaitMillis));
              //Set to true to enable connectivity test on creating connections. Default: false.
              poolConfig.setTestOnCreate(false);
              //Set to true to enable connectivity test on borrowing connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnBorrow(true);
              //Set to true to enable connectivity test on returning connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnReturn(false);
              //Indicates whether to check for idle connections. If this is set to false, idle connections are not evicted.
              poolConfig.setTestWhileIdle(true);
              //Idle duration after which a connection is evicted. If the actual duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted.
              poolConfig.setSoftMinEvictableIdleTime(Duration.ofMillis(redisPoolSoftMinEvictableIdleTimeMillis));
              //Disable eviction policy MinEvictableIdleTimeMillis().
              poolConfig.setMinEvictableIdleTime(Duration.ofMillis(-1));
              //Interval for checking and evicting idle connections. Default: 60s.
              poolConfig.setTimeBetweenEvictionRuns(Duration.ofMillis(redisPoolBetweenEvictionRunsMillis));
              return poolConfig;
          }
      }

-  Configuration for Redis Cluster instances

   .. code-block::

      import java.time.Duration;
      import java.util.ArrayList;
      import java.util.List;

      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
      import org.springframework.data.redis.connection.RedisClusterConfiguration;
      import org.springframework.data.redis.connection.RedisConnectionFactory;
      import org.springframework.data.redis.connection.RedisNode;
      import org.springframework.data.redis.connection.lettuce.LettuceClientConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;

      import io.lettuce.core.ClientOptions;
      import io.lettuce.core.SocketOptions;
      import io.lettuce.core.cluster.ClusterClientOptions;
      import io.lettuce.core.cluster.ClusterTopologyRefreshOptions;

      /**
      * Lettuce Cluster non-pooling configuration (use either this or the application.properties configuration)
      */
      @Configuration
      public class RedisConfiguration {

          @Value("${redis.cluster.nodes}")
          private String redisClusterNodes;

          @Value("${redis.cluster.maxDirects:3}")
          private Integer redisClusterMaxDirects;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:2000}")
          private Integer redisConnectTimeout = 2000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Value("${redis.cluster.topology.refresh.period.millis:10000}")
          private Integer redisClusterTopologyRefreshPeriodMillis = 10000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(LettuceClientConfiguration clientConfiguration) {

              RedisClusterConfiguration clusterConfiguration = new RedisClusterConfiguration();

              List<RedisNode> clusterNodes = new ArrayList<>();
              for (String clusterNodeStr : redisClusterNodes.split(",")) {
                  String[] nodeInfo = clusterNodeStr.split(":");
                  clusterNodes.add(new RedisNode(nodeInfo[0], Integer.valueOf(nodeInfo[1])));
              }
              clusterConfiguration.setClusterNodes(clusterNodes);

              clusterConfiguration.setPassword(redisPassword);
              clusterConfiguration.setMaxRedirects(redisClusterMaxDirects);

              LettuceConnectionFactory connectionFactory = new LettuceConnectionFactory(clusterConfiguration, clientConfiguration);
              return connectionFactory;
          }

          @Bean
          public LettuceClientConfiguration clientConfiguration() {

              SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

              ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                      .enableAllAdaptiveRefreshTriggers()
                      .enablePeriodicRefresh(Duration.ofMillis(redisClusterTopologyRefreshPeriodMillis))
                      .build();

              ClusterClientOptions clientOptions = ClusterClientOptions.builder()
                      .autoReconnect(true)
                      .pingBeforeActivateConnection(true)
                      .cancelCommandsOnReconnectFailure(false)
                      .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
                      .socketOptions(socketOptions)
                      .topologyRefreshOptions(topologyRefreshOptions)
                      .build();


              LettuceClientConfiguration clientConfiguration = LettuceClientConfiguration.builder()
                      .commandTimeout(Duration.ofMillis(redisReadTimeout))
                      .readFrom(ReadFrom.MASTER)
                      .clientOptions(clientOptions)
                      .build();
              return clientConfiguration;
          }
      }

-  Pooling configuration for Redis Cluster instances

   Enable the pooling component

   .. code-block::

      <dependency>
          <groupId>org.apache.commons</groupId>
          <artifactId>commons-pool2</artifactId>
          <version>2.11.1</version>
      </dependency>

   Code

   .. code-block::

      import java.time.Duration;
      import java.util.ArrayList;
      import java.util.List;

      import org.apache.commons.pool2.impl.GenericObjectPoolConfig;
      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
      import org.springframework.data.redis.connection.RedisClusterConfiguration;
      import org.springframework.data.redis.connection.RedisConnectionFactory;
      import org.springframework.data.redis.connection.RedisNode;
      import org.springframework.data.redis.connection.lettuce.LettuceClientConfiguration;
      import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
      import org.springframework.data.redis.connection.lettuce.LettucePoolingClientConfiguration;

      import io.lettuce.core.ClientOptions;
      import io.lettuce.core.SocketOptions;
      import io.lettuce.core.cluster.ClusterClientOptions;
      import io.lettuce.core.cluster.ClusterTopologyRefreshOptions;

      /**
      * Lettuce pooling configuration
      */
      @Configuration
      public class RedisPoolConfiguration {

          @Value("${redis.cluster.nodes}")
          private String redisClusterNodes;

          @Value("${redis.cluster.maxDirects:3}")
          private Integer redisClusterMaxDirects;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:2000}")
          private Integer redisConnectTimeout = 2000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Value("${redis.cluster.topology.refresh.period.millis:10000}")
          private Integer redisClusterTopologyRefreshPeriodMillis = 10000;

          @Value("${redis.pool.minSize:50}")
          private Integer redisPoolMinSize = 50;

          @Value("${redis.pool.maxSize:200}")
          private Integer redisPoolMaxSize = 200;

          @Value("${redis.pool.maxWaitMillis:2000}")
          private Integer redisPoolMaxWaitMillis = 2000;

          @Value("${redis.pool.softMinEvictableIdleTimeMillis:1800000}")
          private Integer redisPoolSoftMinEvictableIdleTimeMillis = 30 * 60 * 1000;

          @Value("${redis.pool.timeBetweenEvictionRunsMillis:60000}")
          private Integer redisPoolBetweenEvictionRunsMillis = 60 * 1000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(LettuceClientConfiguration clientConfiguration) {

              RedisClusterConfiguration clusterConfiguration = new RedisClusterConfiguration();

              List<RedisNode> clusterNodes = new ArrayList<>();
              for (String clusterNodeStr : redisClusterNodes.split(",")) {
                  String[] nodeInfo = clusterNodeStr.split(":");
                  clusterNodes.add(new RedisNode(nodeInfo[0], Integer.valueOf(nodeInfo[1])));
              }
              clusterConfiguration.setClusterNodes(clusterNodes);

              clusterConfiguration.setPassword(redisPassword);
              clusterConfiguration.setMaxRedirects(redisClusterMaxDirects);

              LettuceConnectionFactory connectionFactory = new LettuceConnectionFactory(clusterConfiguration, clientConfiguration);
              //Disable native connection sharing before validating connection pool
              connectionFactory.setShareNativeConnection(false);
              return connectionFactory;
          }

          @Bean
          public LettuceClientConfiguration clientConfiguration() {

              SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

              ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                      .enableAllAdaptiveRefreshTriggers()
                      .enablePeriodicRefresh(Duration.ofMillis(redisClusterTopologyRefreshPeriodMillis))
                      .build();

              ClusterClientOptions clientOptions = ClusterClientOptions.builder()
                      .autoReconnect(true)
                      .pingBeforeActivateConnection(true)
                      .cancelCommandsOnReconnectFailure(false)
                      .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
                      .socketOptions(socketOptions)
                      .topologyRefreshOptions(topologyRefreshOptions)
                      .build();


              LettucePoolingClientConfiguration clientConfiguration = LettucePoolingClientConfiguration.builder()
                      .poolConfig(poolConfig())
                      .commandTimeout(Duration.ofMillis(redisReadTimeout))
                      .clientOptions(clientOptions)
                      .readFrom(ReadFrom.MASTER)
                      .build();
              return clientConfiguration;
          }

          private GenericObjectPoolConfig poolConfig() {
              GenericObjectPoolConfig poolConfig = new GenericObjectPoolConfig();
              //Minimum connections in the pool
              poolConfig.setMinIdle(redisPoolMinSize);
              //Maximum idle connections in the pool
              poolConfig.setMaxIdle(redisPoolMaxSize);
              //Maximum total connections in the pool
              poolConfig.setMaxTotal(redisPoolMaxSize);
              //Wait when pool is exhausted? Set to true to wait. To validate setMaxWait, it has to be true.
              poolConfig.setBlockWhenExhausted(true);
              //Max allowed time to wait for connection after pool is exhausted. The default value -1 indicates to wait indefinitely.
              poolConfig.setMaxWait(Duration.ofMillis(redisPoolMaxWaitMillis));
              //Set to true to enable connectivity test on creating connections. Default: false.
              poolConfig.setTestOnCreate(false);
              //Set to true to enable connectivity test on borrowing connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnBorrow(true);
              //Set to true to enable connectivity test on returning connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnReturn(false);
              //Indicates whether to check for idle connections. If this is set to false, idle connections are not evicted.
              poolConfig.setTestWhileIdle(true);
              //Disable connection closure when the minimum idle time is reached.
              poolConfig.setMinEvictableIdleTime(Duration.ofMillis(-1));
              //Idle duration before a connection being evicted. If the actual duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted. MinEvictableIdleTimeMillis (default eviction policy) is no longer used.
              poolConfig.setSoftMinEvictableIdleTime(Duration.ofMillis(redisPoolSoftMinEvictableIdleTimeMillis));
              //Interval for checking and evicting idle connections. Default: 60s.
              poolConfig.setTimeBetweenEvictionRuns(Duration.ofMillis(redisPoolBetweenEvictionRunsMillis));

              return poolConfig;
          }

      }

(Optional) Configuring SSL Connections
--------------------------------------

If SSL is enabled for an instance, to access it using SSL connections, use the following content to replace the **LettuceClientConfiguration** construction method **clientConfiguration()** in :ref:`Bean Configuration <dcs-ug-211105002__en-us_topic_0000001220636227_section113908122580>`. For details about whether your DCS Redis instances support SSL, see :ref:`Transmitting DCS Redis Data with Encryption Using SSL <dcs-ug-023129>`.

-  Single-node, master/standby, read/write splitting, and Proxy Cluster

   .. code-block::

      @Bean
      public LettuceClientConfiguration clientConfiguration() {

          SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

          SslOptions sslOptions = SslOptions.builder()
              .trustManager(new File(certificationPath))
              .build();

          ClientOptions clientOptions = ClientOptions.builder()
              .sslOptions(sslOptions)
              .autoReconnect(true)
              .pingBeforeActivateConnection(true)
              .cancelCommandsOnReconnectFailure(false)
              .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
              .socketOptions(socketOptions)
              .build();
          LettuceClientConfiguration clientConfiguration = LettuceClientConfiguration.builder()
              .commandTimeout(Duration.ofMillis(redisReadTimeout))
              .readFrom(ReadFrom.MASTER)
              .clientOptions(clientOptions)
              .useSsl()
              .build();

          return clientConfiguration;
      }

-  Redis Cluster

   .. code-block::

      @Bean
      public LettuceClientConfiguration clientConfiguration() {

          SocketOptions socketOptions = SocketOptions.builder().connectTimeout(Duration.ofMillis(redisConnectTimeout)).build();

          SslOptions sslOptions = SslOptions.builder()
              .trustManager(new File(certificationPath))
              .build();

          ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
              .enableAllAdaptiveRefreshTriggers()
              .enablePeriodicRefresh(Duration.ofMillis(redisClusterTopologyRefreshPeriodMillis))
              .build();

          ClusterClientOptions clientOptions = ClusterClientOptions.builder()
              .sslOptions(sslOptions)
              .autoReconnect(true)
              .pingBeforeActivateConnection(true)
              .cancelCommandsOnReconnectFailure(false)
              .disconnectedBehavior(ClientOptions.DisconnectedBehavior.ACCEPT_COMMANDS)
              .socketOptions(socketOptions)
              .topologyRefreshOptions(topologyRefreshOptions)
              .build();


          LettuceClientConfiguration clientConfiguration = LettuceClientConfiguration.builder()
              .commandTimeout(Duration.ofMillis(redisReadTimeout))
              .readFrom(ReadFrom.MASTER)
              .clientOptions(clientOptions)
              .useSsl()
              .build();

          return clientConfiguration;
      }

Parameter Description
---------------------

.. table:: **Table 1** LettuceConnectionFactory parameters

   +-----------------------+----------------------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                       | Default Value   | Description                                                                                                             |
   +=======================+============================+=================+=========================================================================================================================+
   | configuration         | RedisConfiguration         | ``-``           | Redis connection configuration. Two subsclasses:                                                                        |
   |                       |                            |                 |                                                                                                                         |
   |                       |                            |                 | -  RedisStandaloneConfiguration                                                                                         |
   |                       |                            |                 | -  RedisClusterConfiguration                                                                                            |
   +-----------------------+----------------------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+
   | clientConfiguration   | LettuceClientConfiguration | ``-``           | Client configuration parameter. Common subclass:                                                                        |
   |                       |                            |                 |                                                                                                                         |
   |                       |                            |                 | LettucePoolingClientConfiguration                                                                                       |
   +-----------------------+----------------------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+
   | shareNativeConnection | boolean                    | true            | Indicates whether to share native connections. Set to **true** to share. Set to **false** to enable connection pooling. |
   +-----------------------+----------------------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** RedisStandaloneConfiguration parameters

   +-----------+---------------+---------------------------------------------------------------+
   | Parameter | Default Value | Description                                                   |
   +===========+===============+===============================================================+
   | hostName  | localhost     | IP address/domain name for connecting to a DCS Redis instance |
   +-----------+---------------+---------------------------------------------------------------+
   | port      | 6379          | Port number                                                   |
   +-----------+---------------+---------------------------------------------------------------+
   | database  | 0             | Database subscript                                            |
   +-----------+---------------+---------------------------------------------------------------+
   | password  | ``-``         | Password                                                      |
   +-----------+---------------+---------------------------------------------------------------+

.. table:: **Table 3** RedisClusterConfiguration parameters

   +--------------+------------------------------------------------------------------------------------+
   | Parameter    | Description                                                                        |
   +==============+====================================================================================+
   | clusterNodes | Cluster node connection information, including the node IP address and port number |
   +--------------+------------------------------------------------------------------------------------+
   | maxRedirects | Maximum redirecting times. Recommended value: **3**.                               |
   +--------------+------------------------------------------------------------------------------------+
   | password     | Password                                                                           |
   +--------------+------------------------------------------------------------------------------------+

.. table:: **Table 4** LettuceClientConfiguration parameters

   +---------------+---------------+---------------+---------------------------------------------------------------------------------------------------+
   | Parameter     | Type          | Default Value | Description                                                                                       |
   +===============+===============+===============+===================================================================================================+
   | timeout       | Duration      | 60s           | Command timeout: Recommended: **2s**.                                                             |
   +---------------+---------------+---------------+---------------------------------------------------------------------------------------------------+
   | clientOptions | ClientOptions | ``-``         | Configuration options.                                                                            |
   +---------------+---------------+---------------+---------------------------------------------------------------------------------------------------+
   | readFrom      | readFrom      | MASTER        | Read mode. Recommended: **MASTER**. Other values may cause access failures in failover scenarios. |
   +---------------+---------------+---------------+---------------------------------------------------------------------------------------------------+

.. table:: **Table 5** LettucePoolingClientConfiguration parameters

   +---------------+-------------------------+---------------+---------------------------------------------------------------------------------------------------+
   | Parameter     | Type                    | Default Value | Description                                                                                       |
   +===============+=========================+===============+===================================================================================================+
   | timeout       | Duration                | 60s           | Command timeout: Recommended: **2s**.                                                             |
   +---------------+-------------------------+---------------+---------------------------------------------------------------------------------------------------+
   | clientOptions | ClientOptions           | ``-``         | Configuration options.                                                                            |
   +---------------+-------------------------+---------------+---------------------------------------------------------------------------------------------------+
   | poolConfig    | GenericObjectPoolConfig | ``-``         | Connection pool configuration.                                                                    |
   +---------------+-------------------------+---------------+---------------------------------------------------------------------------------------------------+
   | readFrom      | readFrom                | MASTER        | Read mode. Recommended: **MASTER**. Other values may cause access failures in failover scenarios. |
   +---------------+-------------------------+---------------+---------------------------------------------------------------------------------------------------+

.. table:: **Table 6** ClientOptions parameters

   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                        | Type                 | Default Value                | Description                                                                                                                                                                           |
   +==================================+======================+==============================+=======================================================================================================================================================================================+
   | autoReconnect                    | boolean              | true                         | Indicates whether to automatically reconnect after disconnection. Recommended: **true**.                                                                                              |
   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | pingBeforeActivateConnection     | boolean              | true                         | Indicates whether to test connectivity on established connections. Recommended: **true**.                                                                                             |
   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cancelCommandsOnReconnectFailure | boolean              | true                         | Indicates whether to cancel commands after a failed reconnection attempt. Recommended: **false**.                                                                                     |
   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | disconnectedBehavior             | DisconnectedBehavior | DisconnectedBehavior.DEFAULT | Indicates what to do when a connection drops. Recommended: **ACCEPT_COMMANDS**.                                                                                                       |
   |                                  |                      |                              |                                                                                                                                                                                       |
   |                                  |                      |                              | -  **DEFAULT**: When **autoReconnect** is set **true**, commands are allowed to wait in queue. When **autoReconnect** is set to **false**, commands are not allowed to wait in queue. |
   |                                  |                      |                              | -  **ACCEPT_COMMANDS**: Allow commands to wait in queue.                                                                                                                              |
   |                                  |                      |                              | -  **REJECT_COMMANDS**: Do not allow commands to wait in queue.                                                                                                                       |
   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | socketOptions                    | SocketOptions        | ``-``                        | Socket configuration.                                                                                                                                                                 |
   +----------------------------------+----------------------+------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 7** SocketOptions parameters

   ============== ============= ========================================
   Parameter      Default Value Description
   ============== ============= ========================================
   connectTimeout 10s           Connection timeout. Recommended: **2s**.
   ============== ============= ========================================

.. table:: **Table 8** GenericObjectPoolConfig parameters

   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                      | Default Value | Description                                                                                                                                                                                                                                        |
   +================================+===============+====================================================================================================================================================================================================================================================+
   | minIdle                        | ``-``         | Minimum connections in the pool.                                                                                                                                                                                                                   |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxIdle                        | ``-``         | Maximum idle connections in the connection pool.                                                                                                                                                                                                   |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxTotal                       | ``-``         | Maximum total connections in the connection pool.                                                                                                                                                                                                  |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | blockWhenExhausted             | true          | Indicates whether to wait after the connection pool is exhausted. **true**: Wait. **false**: Do not wait. To validate **maxWaitMillis**, this parameter must be set to **true**.                                                                   |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxWaitMillis                  | -1            | Maximum amount of time a connection allocation should block before throwing an exception when the pool is exhausted. The default value **-1** indicates to wait indefinitely.                                                                      |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnCreate                   | false         | Set to true to enable connectivity test on creating connections. Default: **false**.                                                                                                                                                               |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnBorrow                   | false         | Set to true to enable connectivity test on borrowing connections. Default: **false**. Set to false for heavy-traffic services to reduce overhead.                                                                                                  |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnReturn                   | false         | Set to **true** to enable connectivity test on returning connections. Default: **false**. Set to **false** for heavy-traffic services to reduce overhead.                                                                                          |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testWhileIdle                  | false         | Indicates whether to check for idle connections. If this parameter is set to **false**, idle connections are not evicted. Recommended value: **true**.                                                                                             |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | softMinEvictableIdleTimeMillis | -1            | Duration (in milliseconds) after which idle connections are evicted. If the idle duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted. Recommended value: **1800000**. |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | minEvictableIdleTimeMillis     | 1800000       | An eviction policy, set to **-1** (suggested) to disable it. Use **softminEvictableIdleTimeMillis** instead.                                                                                                                                       |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | timeBetweenEvictionRunsMillis  | -1            | Eviction interval, in milliseconds. Recommended value: **60000**                                                                                                                                                                                   |
   +--------------------------------+---------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Suggestion for Configuring DCS Instances
----------------------------------------

-  Pooling connection

   Different from Jedis's BIO, the bottom layer of Lettuce communicates with Redis Server based on Netty's NIO. Combining persistent connections and queues, Lettuce sends and receives multiple requests and responses spontaneously with sequential sending and receiving features of TCP. A single connection supports 3000 to 5000 QPS, but you are not advised to allow more than 3000 QPS in production systems. Pooling is not supported by Lettuce, and is disabled by default in Spring Boot. To enable pooling, validate the commons-pool2 dependency and disable native connection sharing.

   By default, each Lettuce connection needs two thread pools, I/O thread pool and computation thread pool, to support I/O event reading and asynchronous event processing. If you configure connection pooling, each connection creates two thread pools, consuming high memory resources. **Lettuce is strong at processing single connections based on its bottom-layer implementation, so you are not advised to use Lettuce with pooling.**

-  Topology refresh

   When connecting to a Redis Cluster instance, Lettuce randomly sends **cluster nodes** to the node list during initialization to obtain the distribution of cluster slots. Cluster topology structure changes when the cluster capacity is increased or decreased or a master/standby switchover occurs. Lettuce does not detect such changes by default. You can enable detection with the following configurations:

   -  **application.properties configuration**

      .. code-block::

         #Enable adaptive topology refresh.
         spring.redis.lettuce.cluster.refresh.adaptive=true
         #Enable topology refresh every 10 seconds.
         spring.redis.lettuce.cluster.refresh.period=10S

   -  **API** **configuration**

      .. code-block::

         ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
             .enableAllAdaptiveRefreshTriggers()
             .enablePeriodicRefresh(Duration.ofMillis(redisClusterTopologyRefreshPeriodMillis))
             .build();

         ClusterClientOptions clientOptions = ClusterClientOptions.builder()
                 ...
                 ...
                 .topologyRefreshOptions(topologyRefreshOptions)
                 .build();

-  Blast radius

   The bottom layer of Lettuce uses a combination of single persistent connection and request queue. Once network jitter or intermittent disconnection occurs or connection times out, all requests are affected. Especially when connection times out, an attempt is made to resend TCP pockets until timeout and connection drops. Requests do not recover until connections are reestablished. Requests accumulate during resending attempts. If upper-layer services time out in batches, or the resending timeout is too long in some OSs' kernels, the service system remains unavailable for a long time. **Therefore,** **you are advised to use Jedis** **instead of Lettuce.**
