:original_name: dcs-ug-0713005.html

.. _dcs-ug-0713005:

Jedis
=====

Access a DCS Redis instance through Jedis on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see the `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the Java compilation environment has been installed on the ECS.

Procedure
---------

#. .. _dcs-ug-0713005__en-us_topic_0148195198_li695671074019:

   View the IP address and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Log in to the ECS.

#. Use Maven to add the following dependency to the **pom.xml** file:

   .. code-block::

      <dependency>
          <groupId>redis.clients</groupId>
          <artifactId>jedis</artifactId>
          <version>4.1.1</version>
      </dependency>

#. Access the DCS instance by using Jedis.

   Obtain the `source code <https://github.com/xetorthio/jedis>`__ of the Jedis client. Use either of the following two methods to access a DCS Redis instance through Jedis:

   -  Single Jedis connection
   -  Jedis pool

   Example code:

   a. Example of using Jedis to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with a single connection

      .. code-block::

         //Creating a connection in password mode
          String host = "192.168.0.150";
          int port = 6379;
          String pwd = "passwd";

          Jedis client = new Jedis(host, port);
          client.auth(pwd);
          client.connect();
         //Run the SET command.
          String result = client.set("key-string", "Hello, Redis!");
          System.out.println( String.format("set command result:%s", result) );
         //Run the GET command.
          String value = client.get("key-string");
         System.out.println( String.format("get command result:%s", value) );

         //Creating a connection in password-free mode
          String host = "192.168.0.150";
          int port = 6379;

          Jedis client = new Jedis(host, port);
          client.connect();
         //Run the SET command.
          String result = client.set("key-string", "Hello, Redis!");
          System.out.println( String.format("set command result:%s", result) );
         //Run the GET command.
          String value = client.get("key-string");
          System.out.println( String.format("get command result:%s", value) );

      *host* indicates the example IP address of the DCS instance and *port* indicates the port number of the DCS instance. For details about how to obtain the IP address and port, see :ref:`1 <dcs-ug-0713005__en-us_topic_0148195198_li695671074019>`. Change them as required. *pwd* indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

   b. Example of using Jedis to connect to a single-node, master/standby, or Proxy Cluster DCS Redis instance with connection pooling

      .. code-block::

         //Generate configuration information of a Jedis pool
          String ip = "192.168.0.150";
          int port = 6379;
          String pwd = "passwd";
          GenericObjectPoolConfig config = new GenericObjectPoolConfig();
          config.setTestOnBorrow(false);
          config.setTestOnReturn(false);
          config.setMaxTotal(100);
          config.setMaxIdle(100);
          config.setMaxWaitMillis(2000);
         JedisPool pool = new JedisPool(config, ip, port, 100000, pwd);//Generate a Jedis pool when the application is being initialized
         //Get a Jedis connection from the Jedis pool when a service operation occurs
          Jedis client = pool.getResource();
          try {
              //Run commands
              String result = client.set("key-string", "Hello, Redis!");
              System.out.println( String.format("set command result:%s", result) );
              String value = client.get("key-string");
              System.out.println( String.format("get command result:%s", value) );
          } catch (Exception e) {
              // TODO: handle exception
          } finally {
              //Return the Jedis connection to the Jedis pool when the service operation is completed
              if (null != client) {
                  pool.returnResource(client);
              }
          } // end of try block
          //Destroy the Jedis pool when the application is closed
          pool.destroy();

         //Configure the connection pool in password-free mode
          String ip = "192.168.0.150";
          int port = 6379;
          GenericObjectPoolConfig config = new GenericObjectPoolConfig();
          config.setTestOnBorrow(false);
          config.setTestOnReturn(false);
          config.setMaxTotal(100);
          config.setMaxIdle(100);
          config.setMaxWaitMillis(2000);
          JedisPool pool = new JedisPool(config, ip, port, 100000);//Generate a JedisPool when the application is being initialized
          //Get a Jedis connection from the Jedis pool when a service operation occurs
          Jedis client = pool.getResource();
          try {
              //Run commands
              String result = client.set("key-string", "Hello, Redis!");
              System.out.println( String.format("set command result:%s", result) );
              String value = client.get("key-string");
              System.out.println( String.format("get command result:%s", value) );
          } catch (Exception e) {
              // TODO: handle exception
          } finally {
              //Return the Jedis connection to the Jedis pool when the service operation is completed
              if (null != client) {
                  pool.returnResource(client);
              }
          } // end of try block
          //Destroy the Jedis pool when the application is closed
          pool.destroy();

      *ip* indicates the IP address of the DCS instance and *port* indicates the port number of the DCS instance. For details about how to obtain the IP address and port, see :ref:`1 <dcs-ug-0713005__en-us_topic_0148195198_li695671074019>`. Change them as required. *pwd* indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

   c. Example code for connecting to Redis Cluster using a single connection

      -  With a password

         .. code-block::

            //The following shows password-protected access.
            int port = 6379;
            String host = "192.168.144.37";
            //Create JedisCluster.
            Set<HostAndPort> nodes = new HashSet<HostAndPort>();
            nodes.add(new HostAndPort(host, port));
            JedisCluster cluster = new JedisCluster(nodes, 5000, 3000, 10, "password", new JedisPoolConfig());
            cluster.set("key", "value");
            System.out.println("Connected to RedisCluster:" + cluster.get("key"));
            cluster.close();

      -  Without a password

         .. code-block::

            int port = 6379;
            String host = "192.168.144.37";
            //Create JedisCluster.
            Set<HostAndPort> nodes = new HashSet<HostAndPort>();
            nodes.add(new HostAndPort(host, port));
            JedisCluster cluster = new JedisCluster(nodes);
            cluster.set("key", "value");
            System.out.println("Connected to RedisCluster:" + cluster.get("key"));
            cluster.close();

      *host* indicates the example IP address of the DCS instance and *port* indicates the port number of the DCS instance. For details about how to obtain the IP address and port, see :ref:`1 <dcs-ug-0713005__en-us_topic_0148195198_li695671074019>`. Change them as required. *password* indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

#. Compile code according to the **readme** file in the source code of the Jedis client. Run the Jedis client to access the chosen DCS Redis instance.
