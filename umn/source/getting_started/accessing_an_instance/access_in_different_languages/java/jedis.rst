:original_name: dcs-ug-0713005.html

.. _dcs-ug-0713005:

Jedis
=====

Access a DCS Redis instance through Jedis on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

Spring Data Redis is already integrated with `Jedis <https://github.com/redis/jedis>`__ and `Lettuce <https://github.com/lettuce-io/lettuce-core>`__ for Spring Boot projects. Spring Boot 1.x is integrated with Jedis, and Spring Boot 2.x is integrated with Lettuce. To use Jedis in Spring Boot 2.x and later, you need to solve Lettuce dependency conflicts.

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.

-  View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

-  An ECS has been created. For details about how to create an ECS, see the `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.

-  If the ECS runs the Linux OS, ensure that the Java compilation environment has been installed on the ECS.

Pom Configuration
-----------------

.. code-block::

   <!-- import spring-data-redis -->
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-redis</artifactId>
   <!--In Spring Boot 2.0, Lettuce is used by default. To use Jedis, solve dependency conflicts.-->
       <exclusions>
           <exclusion>
               <groupId>io.lettuce</groupId>
               <artifactId>lettuce-core</artifactId>
           </exclusion>
       </exclusions>
   </dependency>
   <!--Jedis dependency>
   <dependency>
       <groupId>redis.clients</groupId>
       <artifactId>jedis</artifactId>
       <version>3.6.0</version>
   </dependency>

application.properties Configuration
------------------------------------

-  Single-node, master/standby, and Proxy Cluster

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
      #Whether to enable connection pooling
      spring.redis.jedis.pool.enabled=true
      #Minimum connections in the pool
      spring.redis.jedis.pool.min-idle=50
      #Maximum idle connections in the pool
      spring.redis.jedis.pool.max-idle=200
      #Maximum connections in the pool
      spring.redis.jedis.pool.max-active=200
      #Maximum amount of time a connection allocation should block before throwing an exception when the pool is exhausted. The default value -1 indicates to wait indefinitely.
      spring.redis.jedis.pool.max-wait=3000
      #Interval for checking and evicting idle connection. Default: 60s.
      spring.redis.jedis.pool.time-between-eviction-runs=60S

-  Redis Cluster

   .. code-block::

      #Redis Cluster node connection information
      spring.redis.cluster.nodes=<ip:port>,<ip:port>,<ip:port>
      #Redis Cluster password
      spring.redis.password=<password>
      #Redis Cluster max. redirecting times
      spring.redis.cluster.max-redirects=3
      #Redis read/write timeout
      spring.redis.timeout=2000
      #Whether to enable connection pooling
      spring.redis.jedis.pool.enabled=true
      #Minimum connections in the pool
      spring.redis.jedis.pool.min-idle=50
      #Maximum idle connections in the pool
      spring.redis.jedis.pool.max-idle=200
      #Maximum connections in the pool
      spring.redis.jedis.pool.max-active=200
      #Maximum amount of time a connection allocation should block before throwing an exception when the pool is exhausted. The default value -1 indicates to wait indefinitely.
      spring.redis.jedis.pool.max-wait=3000
      #Interval for checking and evicting idle connections. Default: 60s.
      spring.redis.jedis.pool.time-between-eviction-runs=60S

Bean Configuration
------------------

-  Single-node, master/standby, and Proxy Cluster

   .. code-block::

      import java.time.Duration;

      import org.springframework.beans.factory.annotation.Value;
      import org.springframework.context.annotation.Bean;
      import org.springframework.context.annotation.Configuration;
      import org.springframework.data.redis.connection.RedisConnectionFactory;
      import org.springframework.data.redis.connection.RedisStandaloneConfiguration;
      import org.springframework.data.redis.connection.jedis.JedisClientConfiguration;
      import org.springframework.data.redis.connection.jedis.JedisConnectionFactory;

      import redis.clients.jedis.JedisPoolConfig;

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

          @Value("${redis.connect.timeout:3000}")
          private Integer redisConnectTimeout = 3000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Value("${redis.pool.minSize:50}")
          private Integer redisPoolMinSize = 50;

          @Value("${redis.pool.maxSize:200}")
          private Integer redisPoolMaxSize = 200;

          @Value("${redis.pool.maxWaitMillis:3000}")
          private Integer redisPoolMaxWaitMillis = 3000;

          @Value("${redis.pool.softMinEvictableIdleTimeMillis:1800000}")
          private Integer redisPoolSoftMinEvictableIdleTimeMillis = 30 * 60 * 1000;

          @Value("${redis.pool.timeBetweenEvictionRunsMillis:60000}")
          private Integer redisPoolBetweenEvictionRunsMillis = 60 * 1000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(JedisClientConfiguration clientConfiguration) {

              RedisStandaloneConfiguration standaloneConfiguration = new RedisStandaloneConfiguration();
              standaloneConfiguration.setHostName(redisHost);
              standaloneConfiguration.setPort(redisPort);
              standaloneConfiguration.setDatabase(redisDatabase);
              standaloneConfiguration.setPassword(redisPassword);

              return new JedisConnectionFactory(standaloneConfiguration, clientConfiguration);
          }

          @Bean
          public JedisClientConfiguration clientConfiguration() {

              JedisClientConfiguration clientConfiguration = JedisClientConfiguration.builder()
                      .connectTimeout(Duration.ofMillis(redisConnectTimeout))
                      .readTimeout(Duration.ofMillis(redisReadTimeout))
                      .usePooling().poolConfig(redisPoolConfig())
                      .build();

              return clientConfiguration;
          }

          private JedisPoolConfig redisPoolConfig() {

              JedisPoolConfig poolConfig = new JedisPoolConfig();
              //Minimum connections in the pool
              poolConfig.setMinIdle(redisPoolMinSize);
              //Maximum idle connections in the pool
              poolConfig.setMaxIdle(redisPoolMaxSize);
              //Maximum total connections in the pool
              poolConfig.setMaxTotal(redisPoolMaxSize);
              //Wait when pool is exhausted? Set to true to wait. To validate setMaxWait, it has to be true.
              poolConfig.setBlockWhenExhausted(true);
              //Longest time to wait for connection after pool is exhausted. The default value -1 indicates to wait indefinitely.
              poolConfig.setMaxWaitMillis(redisPoolMaxWaitMillis);
              //Set to true to enable connectivity test on creating connections. Default: false.
              poolConfig.setTestOnCreate(false);
              //Set to true to enable connectivity test on borrowing connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnBorrow(true);
              //Set to true to enable connectivity test on returning connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnReturn(false);
              //Indicates whether to check for idle connections. If this is set to false, idle connections are not evicted.
              poolConfig.setTestWhileIdle(true);
              //Duration after which idle connections are evicted. If the idle duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted.
              poolConfig.setSoftMinEvictableIdleTimeMillis(redisPoolSoftMinEvictableIdleTimeMillis);
              //Disable MinEvictableIdleTimeMillis().
              poolConfig.setMinEvictableIdleTimeMillis(-1);
              //Interval for checking and evicting idle connections. Default: 60s.
              poolConfig.setTimeBetweenEvictionRunsMillis(redisPoolBetweenEvictionRunsMillis);
              return poolConfig;
          }
      }

-  Redis Cluster

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
      import org.springframework.data.redis.connection.jedis.JedisClientConfiguration;
      import org.springframework.data.redis.connection.jedis.JedisConnectionFactory;

      import redis.clients.jedis.JedisPoolConfig;

      @Configuration
      public class RedisConfiguration {

          @Value("${redis.cluster.nodes}")
          private String redisClusterNodes;

          @Value("${redis.password:}")
          private String redisPassword;

          @Value("${redis.connect.timeout:3000}")
          private Integer redisConnectTimeout = 3000;

          @Value("${redis.read.timeout:2000}")
          private Integer redisReadTimeout = 2000;

          @Value("${redis.pool.minSize:50}")
          private Integer redisPoolMinSize = 50;

          @Value("${redis.pool.maxSize:200}")
          private Integer redisPoolMaxSize = 200;

          @Value("${redis.pool.maxWaitMillis:3000}")
          private Integer redisPoolMaxWaitMillis = 3000;

          @Value("${redis.pool.softMinEvictableIdleTimeMillis:1800000}")
          private Integer redisPoolSoftMinEvictableIdleTimeMillis = 30 * 60 * 1000;

          @Value("${redis.pool.timeBetweenEvictionRunsMillis:60000}")
          private Integer redisPoolBetweenEvictionRunsMillis = 60 * 1000;

          @Bean
          public RedisConnectionFactory redisConnectionFactory(JedisClientConfiguration clientConfiguration) {

              RedisClusterConfiguration clusterConfiguration = new RedisClusterConfiguration();

              List<RedisNode> clusterNodes = new ArrayList<>();
              for (String clusterNodeStr : redisClusterNodes.split(",")) {
                  String[] nodeInfo = clusterNodeStr.split(":");
                  clusterNodes.add(new RedisNode(nodeInfo[0], Integer.valueOf(nodeInfo[1])));
              }
              clusterConfiguration.setClusterNodes(clusterNodes);

              clusterConfiguration.setPassword(redisPassword);
              clusterConfiguration.setMaxRedirects(3);

              return new JedisConnectionFactory(clusterConfiguration, clientConfiguration);
          }

          @Bean
          public JedisClientConfiguration clientConfiguration() {

              JedisClientConfiguration clientConfiguration = JedisClientConfiguration.builder()
                      .connectTimeout(Duration.ofMillis(redisConnectTimeout))
                      .readTimeout(Duration.ofMillis(redisReadTimeout))
                      .usePooling().poolConfig(redisPoolConfig())
                      .build();

              return clientConfiguration;
          }

          private JedisPoolConfig redisPoolConfig() {

              JedisPoolConfig poolConfig = new JedisPoolConfig();
              //Minimum connections in the pool
              poolConfig.setMinIdle(redisPoolMinSize);
              //Maximum idle connections in the pool
              poolConfig.setMaxIdle(redisPoolMaxSize);
              //Maximum total connections in the pool
              poolConfig.setMaxTotal(redisPoolMaxSize);
              //Wait when pool is exhausted? Set to true to wait. To validate setMaxWait, it has to be true.
              poolConfig.setBlockWhenExhausted(true);
              //Longest time to wait for connection after pool is exhausted. The default value -1 indicates to wait indefinitely.
              poolConfig.setMaxWaitMillis(redisPoolMaxWaitMillis);
              //Set to true to enable connectivity test on creating connections. Default: false.
              poolConfig.setTestOnCreate(false);
              //Set to true to enable connectivity test on borrowing connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnBorrow(true);
              //Set to true to enable connectivity test on returning connections. Default: false. Set to false for heavy-traffic services to reduce overhead.
              poolConfig.setTestOnReturn(false);
              //Indicates whether to check for idle connections. If this is set to false, idle connections are not evicted.
              poolConfig.setTestWhileIdle(true);
              //Duration after which idle connections are evicted. If the idle duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted.
              poolConfig.setSoftMinEvictableIdleTimeMillis(redisPoolSoftMinEvictableIdleTimeMillis);
              //Disable MinEvictableIdleTimeMillis().
              poolConfig.setMinEvictableIdleTimeMillis(-1);
              //Interval for checking and evicting idle connections. Default: 60s.
              poolConfig.setTimeBetweenEvictionRunsMillis(redisPoolBetweenEvictionRunsMillis);
              return poolConfig;
          }
      }

Parameter Description
---------------------

.. table:: **Table 1** RedisStandaloneConfiguration parameters

   +-----------+---------------+---------------------------------------------------------------+
   | Parameter | Default Value | Description                                                   |
   +===========+===============+===============================================================+
   | hostName  | localhost     | IP address/domain name for connecting to a DCS Redis instance |
   +-----------+---------------+---------------------------------------------------------------+
   | port      | 6379          | Port number                                                   |
   +-----------+---------------+---------------------------------------------------------------+
   | database  | 0             | Database number. Default: 0.                                  |
   +-----------+---------------+---------------------------------------------------------------+
   | password  | ``-``         | Password                                                      |
   +-----------+---------------+---------------------------------------------------------------+

.. table:: **Table 2** RedisClusterConfiguration parameters

   +--------------+------------------------------------------------------------------------------------+
   | Parameter    | Description                                                                        |
   +==============+====================================================================================+
   | clusterNodes | Cluster node connection information, including the node IP address and port number |
   +--------------+------------------------------------------------------------------------------------+
   | maxRedirects | Maximum redirecting times                                                          |
   +--------------+------------------------------------------------------------------------------------+
   | password     | Password                                                                           |
   +--------------+------------------------------------------------------------------------------------+

.. _dcs-ug-0713005__en-us_topic_0148195198_table1153832317251:

.. table:: **Table 3** JedisPoolConfig parameters

   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                      | Default Value | Description                                                                                                                                                                                                                                                  |
   +================================+===============+==============================================================================================================================================================================================================================================================+
   | minIdle                        | ``-``         | Minimum connections in the connection pool                                                                                                                                                                                                                   |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxIdle                        | ``-``         | Maximum idle connections in the connection pool                                                                                                                                                                                                              |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxTotal                       | ``-``         | Maximum total connections in the connection pool                                                                                                                                                                                                             |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | blockWhenExhausted             | true          | Indicates whether to wait after the connection pool is exhausted. **true**: Wait. **false**: Do not wait. To validate **maxWaitMillis**, this parameter must be set to **true**.                                                                             |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maxWaitMillis                  | -1            | Maximum amount of time (in milliseconds) to wait for connection after the connection pool is exhausted. The default value **-1** indicates to wait indefinitely.                                                                                             |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnCreate                   | false         | Indicates whether to enable connectivity test on creating connections. **false**: Disable. **true**: Enable.                                                                                                                                                 |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnBorrow                   | false         | Indicates whether to enable connectivity test on obtaining connections. **false**: Disable. **true**: Enable. For heavy-traffic services, set this parameter to **false** to reduce overhead.                                                                |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testOnReturn                   | false         | Indicates whether to enable connectivity test on returning connections. **false**: Disable. **true**: Enable. For heavy-traffic services, set this parameter to **false** to reduce overhead.                                                                |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | testWhileIdle                  | false         | Indicates whether to check for idle connections. If this parameter is set to **false**, idle connections are not evicted. Recommended value: **true**.                                                                                                       |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | softMinEvictableIdleTimeMillis | 1800000       | Duration (in milliseconds) after which idle connections are evicted. If the idle duration is greater than this value and the maximum number of idle connections is reached, idle connections are directly evicted.                                           |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | minEvictableIdleTimeMillis     | 60000         | Minimum amount of time (in milliseconds) a connection may remain idle in the pool before it is eligible for eviction. The recommended value is **-1**, indicating that **softMinEvictableIdleTimeMillis** is used instead of **minEvictableIdleTimeMillis**. |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | timeBetweenEvictionRunsMillis  | 60000         | Interval (in milliseconds) for checking and evicting idle connections.                                                                                                                                                                                       |
   +--------------------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 4** JedisClientConfiguration parameters

   +----------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter      | Default Value | Description                                                                                                               |
   +================+===============+===========================================================================================================================+
   | connectTimeout | 2000          | Connection timeout interval, in milliseconds.                                                                             |
   +----------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
   | readTimeout    | 2000          | Timeout interval for waiting for a response, in milliseconds.                                                             |
   +----------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
   | poolConfig     | ``-``         | Pool configurations. For details, see :ref:`JedisPoolConfig <dcs-ug-0713005__en-us_topic_0148195198_table1153832317251>`. |
   +----------------+---------------+---------------------------------------------------------------------------------------------------------------------------+

Suggestion for Configuring DCS Instances
----------------------------------------

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
