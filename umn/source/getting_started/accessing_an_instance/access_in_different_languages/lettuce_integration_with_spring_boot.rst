:original_name: dcs-ug-211203001.html

.. _dcs-ug-211203001:

Lettuce Integration with Spring Boot
====================================

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the Java compilation environment has been installed on the ECS.

Procedure
---------

#. View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Use Maven to add the following dependency to the **pom.xml** file:

   .. note::

      -  Since Spring Boot 2.0, Lettuce is used as the default client for connections.
      -  Spring Boot 2.6.6 and Lettuce 6.1.8 are used.

   .. code-block::

      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
      </dependency>

#. Use Spring Boot integrated with Lettuce to connect to the instance.

   -  Example of using Spring Boot and Lettuce to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with a single connection

      a. Add the Redis configuration to the **application.properties** configuration file.

         .. code-block::

            spring.redis.host=host
            spring.redis.database=0
            spring.redis.password=pwd
            spring.redis.port=port

      b. Redis configuration class RedisConfiguration

         .. code-block::

            @Bean
            public RedisTemplate<String, Object> redisTemplate(LettuceConnectionFactory lettuceConnectionFactory) {
                RedisTemplate<String, Object> template = new RedisTemplate<>();
                template.setConnectionFactory(lettuceConnectionFactory);
                  // Replace the default JdkSerializationRedisSerializer with Jackson2JsonRedisSerializer to serialize and deserialize the Redis value.
                Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
                ObjectMapper mapper = new ObjectMapper();
                mapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
                mapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance,
                    ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
                jackson2JsonRedisSerializer.setObjectMapper(mapper);
                StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
                  // String serialization of keys
                template.setKeySerializer(stringRedisSerializer);
                  // String serialization of hash keys
                template.setHashKeySerializer(stringRedisSerializer);
                  // Jackson serialization of values
                template.setValueSerializer(jackson2JsonRedisSerializer);
                  // Jackson serialization of hash values
                template.setHashValueSerializer(jackson2JsonRedisSerializer);
                template.afterPropertiesSet();
                return template;
            }

      c. Redis operation class RedisUtil

         .. code-block::

             /**
              * Obtain data from the cache.
              * @param key
              * @return value
              */
             public Object get(String key){
                 return key==null?null:redisTemplate.opsForValue().get(key);
             }

             /**
              * Write data to the cache.
              * @param key
              * @param value
              * @return true (successful) false (failed)
              */
             public boolean set(String key,Object value) {
                 try {
                     redisTemplate.opsForValue().set(key, value);
                     return true;
                 } catch (Exception e) {
                     e.printStackTrace();
                     return false;
                 }
             }

      d. Write the controller class for testing.

         .. code-block::

              @RestController
            public class HelloRedis {
                @Autowired
                RedisUtil redisUtil;


                @RequestMapping("/setParams")
                @ResponseBody
                public String setParams(String name) {
                        redisUtil.set("name", name);
                        return "success";
                    }

                @RequestMapping("/getParams")
                @ResponseBody
                public String getParams(String name) {
                System.out.println("--------------" + name + "-------------");
                String retName = redisUtil.get(name) + "";
                return retName;
                }

                }

   -  Example of using Spring Boot and Lettuce to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with connection pooling

      a. Add the following dependency in addition to the preceding Maven dependency:

         .. code-block::

            <dependency>
              <groupId>org.apache.commons</groupId>
              <artifactId>commons-pool2</artifactId>
            </dependency>

      b. Add the Redis configuration to the **application.properties** configuration file.

         .. code-block::

            spring.redis.host=host
            spring.redis.database=0
            spring.redis.password=pwd
            spring.redis.port=port
            # Connection timeout.
            spring.redis.timeout=1000
            # Maximum number of connections in the connection pool. A negative value indicates no limit.
            spring.redis.lettuce.pool.max-active=50
            # Minimum number of idle connections in the connection pool.
            spring.redis.lettuce.pool.min-idle=5
            # Maximum number of idle connections in the connection pool.
            spring.redis.lettuce.pool.max-idle=50
            # Maximum time for waiting for connections in the connection pool. A negative value indicates no limit.
            spring.redis.lettuce.pool.max-wait=5000
            # Interval for scheduling an eviction thread.
            spring.redis.pool.time-between-eviction-runs-millis=2000

      c. Redis connection configuration class RedisConfiguration

         .. code-block::

            @Bean
            public RedisTemplate<String, Object> redisTemplate(LettuceConnectionFactory lettuceConnectionFactory) {
                lettuceConnectionFactory.setShareNativeConnection(false);
                RedisTemplate<String, Object> template = new RedisTemplate<>();
                template.setConnectionFactory(lettuceConnectionFactory);
                // Use Jackson2JsonRedisSerializer to replace the default JdkSerializationRedisSerializer to serialize and deserialize the Redis value.
                Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
                ObjectMapper mapper = new ObjectMapper();
                mapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
                mapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance,
                    ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
                jackson2JsonRedisSerializer.setObjectMapper(mapper);
                StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
                // String serialization of keys
                template.setKeySerializer(stringRedisSerializer);
                // String serialization of hash keys
                template.setHashKeySerializer(stringRedisSerializer);
                // Jackson serialization of values
                template.setValueSerializer(jackson2JsonRedisSerializer);
                // Jackson serialization of hash values
                template.setHashValueSerializer(jackson2JsonRedisSerializer);
                template.afterPropertiesSet();
                return template;
            }

   -  Example code for using Spring Boot and Lettuce to connect to Redis Cluster using a single connection

      a. Add the Redis configuration to the **application.properties** configuration file.

         .. code-block::

            spring.redis.cluster.nodes=host:port
            spring.redis.cluster.max-redirects=3
            spring.redis.password= pwd
            # Automated refresh interval
            spring.redis.lettuce.cluster.refresh.period=60
            # Enable automated refresh
            spring.redis.lettuce.cluster.refresh.adaptive=true
            spring.redis.timeout=60

      b. Redis configuration class RedisConfiguration (automated topology refresh must be enabled).

         .. code-block::

            @Bean
            public LettuceConnectionFactory lettuceConnectionFactory() {
                 String[] nodes = clusterNodes.split(",");
                 List<RedisNode> listNodes = new ArrayList();
                 for (String node : nodes) {
                     String[] ipAndPort = node.split(":");
                     RedisNode redisNode = new RedisNode(ipAndPort[0], Integer.parseInt(ipAndPort[1]));
                     listNodes.add(redisNode);
                 }
                 RedisClusterConfiguration redisClusterConfiguration = new RedisClusterConfiguration();
                 redisClusterConfiguration.setClusterNodes(listNodes);
                 redisClusterConfiguration.setPassword(password);
                 redisClusterConfiguration.setMaxRedirects(maxRedirects);
                  // Configure automated topology refresh.
                 ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                     .enablePeriodicRefresh(Duration.ofSeconds(period)) // Refresh the topology periodically.
                     .enableAllAdaptiveRefreshTriggers() // Refresh the topology based on events.
                     .build();

                 ClusterClientOptions clusterClientOptions = ClusterClientOptions.builder()
                     // Redis command execution timeout. Only when the command execution times out will a reconnection be triggered using the new topology.
                     .timeoutOptions(TimeoutOptions.enabled(Duration.ofSeconds(period)))
                     .topologyRefreshOptions(topologyRefreshOptions)
                     .build();
                 LettuceClientConfiguration clientConfig = LettucePoolingClientConfiguration.builder()
                         .commandTimeout(Duration.ofSeconds(timeout))
                         .readFrom(ReadFrom.REPLICA_PREFERRED) // Preferentially read data from the replicas.
                         .clientOptions(clusterClientOptions)
                         .build();
                 LettuceConnectionFactory factory = new LettuceConnectionFactory(redisClusterConfiguration, clientConfig);
                 return factory;
            }

            @Bean
            public RedisTemplate<String, Object> redisTemplate(LettuceConnectionFactory lettuceConnectionFactory) {
                RedisTemplate<String, Object> template = new RedisTemplate<>();
                template.setConnectionFactory(lettuceConnectionFactory);
                 // Use Jackson2JsonRedisSerializer to replace the default JdkSerializationRedisSerializer to serialize and deserialize the Redis value.
                Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
                ObjectMapper mapper = new ObjectMapper();
                mapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
                mapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance,
                    ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
                jackson2JsonRedisSerializer.setObjectMapper(mapper);
                StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
                 // String serialization of keys
                template.setKeySerializer(stringRedisSerializer);
                 // String serialization of hash keys
                template.setHashKeySerializer(stringRedisSerializer);
                 // Jackson serialization of values
                template.setValueSerializer(jackson2JsonRedisSerializer);
                 // Jackson serialization of hash values
                template.setHashValueSerializer(jackson2JsonRedisSerializer);
                template.afterPropertiesSet();
                return template;
            }

   -  Example code for using Spring Boot and Lettuce to connect to Redis Cluster with connection pooling

      a. Add the Redis configuration to the **application.properties** configuration file.

         .. code-block::

            spring.redis.cluster.nodes=host:port
            spring.redis.cluster.max-redirects=3
            spring.redis.password=pwd
            spring.redis.lettuce.cluster.refresh.period=60
            spring.redis.lettuce.cluster.refresh.adaptive=true
            # Connection timeout.
            spring.redis.timeout=60s
            # Maximum number of connections in the connection pool. A negative value indicates no limit.
            spring.redis.lettuce.pool.max-active=50
            # Minimum number of idle connections in the connection pool.
            spring.redis.lettuce.pool.min-idle=5
            # Maximum number of idle connections in the connection pool.
            spring.redis.lettuce.pool.max-idle=50
            # Maximum time for waiting for connections in the connection pool. A negative value indicates no limit.
            spring.redis.lettuce.pool.max-wait=5000
            # Interval for scheduling an eviction thread.
            spring.redis.lettuce.pool.time-between-eviction-runs=2000

      b. Redis configuration class RedisConfiguration (automated topology refresh must be enabled).

         .. code-block::

            @Bean
             public LettuceConnectionFactory lettuceConnectionFactory() {
                 GenericObjectPoolConfig genericObjectPoolConfig = new GenericObjectPoolConfig();
                 genericObjectPoolConfig.setMaxIdle(maxIdle);
                 genericObjectPoolConfig.setMinIdle(minIdle);
                 genericObjectPoolConfig.setMaxTotal(maxActive);
                 genericObjectPoolConfig.setMaxWait(Duration.ofMillis(maxWait));
                 genericObjectPoolConfig.setTimeBetweenEvictionRuns(Duration.ofMillis(timeBetweenEvictionRunsMillis));
                 String[] nodes = clusterNodes.split(",");
                 List<RedisNode> listNodes = new ArrayList();
                 for (String node : nodes) {
                     String[] ipAndPort = node.split(":");
                     RedisNode redisNode = new RedisNode(ipAndPort[0], Integer.parseInt(ipAndPort[1]));
                     listNodes.add(redisNode);
                 }
                 RedisClusterConfiguration redisClusterConfiguration = new RedisClusterConfiguration();
                 redisClusterConfiguration.setClusterNodes(listNodes);
                 redisClusterConfiguration.setPassword(password);
                 redisClusterConfiguration.setMaxRedirects(maxRedirects);
                  // Configure automated topology refresh.
                 ClusterTopologyRefreshOptions topologyRefreshOptions = ClusterTopologyRefreshOptions.builder()
                     .enablePeriodicRefresh(Duration.ofSeconds(period)) // Refresh the topology periodically.
                     .enableAllAdaptiveRefreshTriggers() // Refresh the topology based on events.
                     .build();

                 ClusterClientOptions clusterClientOptions = ClusterClientOptions.builder()
                     // Redis command execution timeout. Only when the command execution times out will a reconnection be triggered using the new topology.
                     .timeoutOptions(TimeoutOptions.enabled(Duration.ofSeconds(period)))
                     .topologyRefreshOptions(topologyRefreshOptions)
                     .build();
                 LettuceClientConfiguration clientConfig = LettucePoolingClientConfiguration.builder()
                         .commandTimeout(Duration.ofSeconds(timeout))
                         .poolConfig(genericObjectPoolConfig)
                         .readFrom(ReadFrom.REPLICA_PREFERRED) // Preferentially read data from the replicas.
                         .clientOptions(clusterClientOptions)
                         .build();
                 LettuceConnectionFactory factory = new LettuceConnectionFactory(redisClusterConfiguration, clientConfig);
                 return factory;
             }

            @Bean
            public RedisTemplate<String, Object> redisTemplate(LettuceConnectionFactory lettuceConnectionFactory) {
                lettuceConnectionFactory.setShareNativeConnection(false);
                RedisTemplate<String, Object> template = new RedisTemplate<>();
                template.setConnectionFactory(lettuceConnectionFactory);
                 // Use Jackson2JsonRedisSerializer to replace the default JdkSerializationRedisSerializer to serialize and deserialize the Redis value.
                Jackson2JsonRedisSerializer<Object> jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);
                ObjectMapper mapper = new ObjectMapper();
                mapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
                mapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance,
                    ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);
                jackson2JsonRedisSerializer.setObjectMapper(mapper);
                StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
                 // String serialization of keys
                template.setKeySerializer(stringRedisSerializer);
                 // String serialization of hash keys
                template.setHashKeySerializer(stringRedisSerializer);
                 // Jackson serialization of values
                template.setValueSerializer(jackson2JsonRedisSerializer);
                 // Jackson serialization of hash values
                template.setHashValueSerializer(jackson2JsonRedisSerializer);
                template.afterPropertiesSet();
                return template;
            }

   **host** is the IP address/domain name of the DCS instance, **port** is the port number of the DCS instance, and **pwd** is the password of the DCS instance. Specify these parameters as required before running the code. Connection pooling is recommended. Adjust parameters such as **TimeOut**, **MaxTotal** (maximum number of connections), **MinIdle** (minimum number of idle connections), **MaxIdle** (maximum number of idle connections), and **MaxWait** (maximum waiting time) based on service requirements.
