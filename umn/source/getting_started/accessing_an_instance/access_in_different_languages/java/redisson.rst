:original_name: dcs-ug-211105004.html

.. _dcs-ug-211105004:

Redisson
========

Access a DCS Redis instance through Redisson on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

.. note::

   -  If a password was set during DCS Redis instance creation, configure the password for connecting to Redis using Redisson. Do not hard code the plaintext password.
   -  To connect to a single-node, master/standby, or Proxy Cluster instance, use the **useSingleServer** method of the **SingleServerConfig** object of Redisson. To connect to a Redis Cluster instance, use the **useClusterServers** method of the **ClusterServersConfig** object.

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

   .. code-block::

      <dependency>
        <groupId>org.redisson</groupId>
        <artifactId>redisson</artifactId>
        <version>3.16.8</version>
      </dependency>

#. Configure the connection pool.

   Recommended keepalive configurations:

   .. code-block::

      # ping connection interval. Configuring this parameter will increase Redis load. Set a value based on the number of connections. The more the connections, the larger the value. Minimum value: 1000. If the number of active Redis connections exceeds 5000, do not set this parameter.
      pingConnectionInterval: 3000


   The following is a configuration example for a single-node instance. (Set the timeout interval and connection pool size based on the site requirements. The following settings are examples only.)

   .. code-block::

            redisson:
                  config:
                      singleServerConfig:
                          # Connection timeout, in milliseconds.
                          connectTimeout: 10000
                          # Command waiting timeout, in milliseconds.
                          timeout: 3000
                          # Number of retry times upon a command failure.
                          retryAttempts: 3
                          # Interval for retrying sending commands, in milliseconds.
                          retryInterval: 1500
                          # Minimum number of idle connections.
                          connectionMinimumIdleSize: 30
                          # Connection pool size.
                          connectionPoolSize: 50
                         # Redis database ID.
                          database: 0
                         # DNS monitoring interval, in milliseconds.
                          dnsMonitoringInterval: 5000
                      # ping connection interval.
                      pingConnectionInterval: 3000


   The following is a configuration example for a cluster instance. (Set the timeout interval and connection pool size based on the site requirements.)

   .. code-block::

              redisson:
                  config:
                      clusterServersConfig:
                          # Idle connection timeout, in milliseconds.
                          idleConnectionTimeout: 100000
                          # Connection timeout, in milliseconds.
                          connectTimeout: 10000
                          # Command waiting timeout, in milliseconds.
                          timeout: 3000
                          # Number of retry times upon a command failure.
                          retryAttempts: 3
                          # Interval for retrying sending commands, in milliseconds.
                          retryInterval: 1500
                          # Interval for reconnecting a replica node upon a failure.
                          failedSlaveReconnectionInterval: 3000
                          # Interval for checking a replica node upon a failure.
                          failedSlaveCheckInterval: 60000
                          # Maximum number of subscriptions per connection.
                          subscriptionsPerConnection: 5
                          #  Client name.
                          clientName: null
                          #  Minimum number of idle pub/sub connections.
                          subscriptionConnectionMinimumIdleSize: 1
                          #  Pub/Sub connection pool size.
                          subscriptionConnectionPoolSize: 50
                          # Minimum number of idle connections per replica node.
                          slaveConnectionMinimumIdleSize: 24
                          # Connection pool size per replica node.
                          slaveConnectionPoolSize: 64
                          # Minimum number of idle connections of the master node.
                          masterConnectionMinimumIdleSize: 24
                          # Connection pool size of the master node.
                          masterConnectionPoolSize: 64
                          #  Master node status scan interval, in milliseconds.
                          scanInterval: 1000
                          # ping connection interval.
                          pingConnectionInterval: 3000
                          # Whether to keep the connection alive.
                          keepAlive: false
                          # The tcpNoDelay setting is enabled by default.
                          tcpNoDelay: false

#. Access the DCS instance by using Redisson (a Java client).

   -  Example of using Redisson to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with a single connection

      .. code-block::

         Config config = new Config();
         SingleServerConfig singleServerConfig = config.useSingleServer();
         singleServerConfig.setAddress("redis://host:port");
         // singleServerConfig.setPassword("********");
         RedissonClient redisson = Redisson.create(config);
         //Test concurrentMap. Data is synchronized to Redis when the put method is used.
         ConcurrentMap<String, Object> map = redisson.getMap("FirstMap");
         map.put("wanger", "male");
         map.put("zhangsan", "nan");
         map.put("lisi", "female");
         ConcurrentMap resultMap = redisson.getMap("FirstMap");
         System.out.println("resultMap==" + resultMap.keySet());
         //Test Set
         Set mySet = redisson.getSet("MySet");
         mySet.add("wanger");
         mySet.add("lisi");
         Set resultSet = redisson.getSet("MySet");
         System.out.println("resultSet===" + resultSet.size());
         //Test Queue
         Queue myQueue = redisson.getQueue("FirstQueue");
         myQueue.add("wanger");
         myQueue.add("lili");
         myQueue.add("zhangsan");
         myQueue.peek();
         myQueue.poll();
         Queue resultQueue = redisson.getQueue("FirstQueue");
         System.out.println("resultQueue===" + resultQueue);
         //Close the connection.
         redisson.shutdown();

   -  Example of using Redisson to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with connection pooling

      .. code-block::

         //1. Initialization
         Config config = new Config();
         SingleServerConfig singleServerConfig = config.useSingleServer();
         singleServerConfig.setAddress("redis://host:6379");
         //Set the maximum number of connections in the connection pool of the master node to 500.
         singleServerConfig.setConnectionPoolSize(500);
         //The connections will be automatically closed and removed from the connection pool. The time unit is millisecond.
         singleServerConfig.setIdleConnectionTimeout(10000);
         RedissonClient redisson = Redisson.create(config);
         //Test concurrentMap. Data is synchronized to Redis when the put method is used.
         ConcurrentMap<String, Object> map = redisson.getMap("FirstMap");
         map.put("wanger", "male");
         map.put("zhangsan", "nan");
         map.put("lisi", "female");
         ConcurrentMap resultMap = redisson.getMap("FirstMap");
         System.out.println("resultMap==" + resultMap.keySet());
         //Test Set
         Set mySet = redisson.getSet("MySet");
         mySet.add("wanger");
         mySet.add("lisi");
         Set resultSet = redisson.getSet("MySet");
         System.out.println("resultSet===" + resultSet.size());
         //Test Queue
         Queue myQueue = redisson.getQueue("FirstQueue");
         myQueue.add("wanger");
         myQueue.add("lili");
         myQueue.add("zhangsan");
         myQueue.peek();
         myQueue.poll();
         Queue resultQueue = redisson.getQueue("FirstQueue");
         System.out.println("resultQueue===" + resultQueue);
         //Close the connection.
         redisson.shutdown();

   -  Example of using Redisson to connect to a Redis Cluster

      .. code-block::

         Config config = new Config();
         ClusterServersConfig clusterServersConfig = config.useClusterServers();
         clusterServersConfig.addNodeAddress("redis://host:port");
         //Set a password.
         // clusterServersConfig.setPassword("********");
         RedissonClient redisson = Redisson.create(config);
         ConcurrentMap<String, Object> map = redisson.getMap("FirstMap");
         map.put("wanger", "male");
         map.put("zhangsan", "nan");
         map.put("lisi", "female");
         ConcurrentMap resultMap = redisson.getMap("FirstMap");
         System.out.println("resultMap==" + resultMap.keySet());
         //2. Test Set
         Set mySet = redisson.getSet("MySet");
         mySet.add("wanger");
         mySet.add("lisi");
         Set resultSet = redisson.getSet("MySet");
         System.out.println("resultSet===" + resultSet.size());
         //3. Test Queue
         Queue myQueue = redisson.getQueue("FirstQueue");
         myQueue.add("wanger");
         myQueue.add("lili");
         myQueue.add("zhangsan");
         myQueue.peek();
         myQueue.poll();
         Queue resultQueue = redisson.getQueue("FirstQueue");
         System.out.println("resultQueue===" + resultQueue);
         //Close the connection.
         redisson.shutdown();
