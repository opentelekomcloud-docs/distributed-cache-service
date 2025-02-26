:original_name: dcs-ug-0312013.html

.. _dcs-ug-0312013:

Connecting to Redis on StackExchange.Redis (C#)
===============================================

This section describes how to access a Redis instance on StackExchange.Redis. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

.. note::

   If you use the StackExchange client to connect to a Proxy Cluster instance, the multi-DB function cannot be used.

   To access a Redis 7.0 instance, use a hiredis `2.6.111 <https://github.com/StackExchange/StackExchange.Redis/releases/tag/2.6.111>`__ or later client. `2.7.0 <https://github.com/StackExchange/StackExchange.Redis/blob/2.8.16/docs/ReleaseNotes.md#2710>`__ and later versions are recommended.

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__
-  If the ECS runs the Linux OS, ensure that the GCC compilation environment has been installed on the ECS.

Connecting to Redis on StackExchange.Redis
------------------------------------------

#. .. _dcs-ug-0312013__en-us_topic_0148195355_li457118182512:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.

#. Log in to the ECS.

   A Windows ECS is used as an example.

#. Install Visual Studio Community 2017 on the ECS.

#. Start Visual Studio 2017 and create a project.

   Set the project name to **redisdemo**.

#. Install StackExchange.Redis by using the NuGet package manager of Visual Studio.

   Access the NuGet package manager console according to :ref:`Figure 1 <dcs-ug-0312013__en-us_topic_0148195355_fig394516508313>`, and enter **Install-Package StackExchange.Redis -Version 2.2.79**. (The version number is optional).

   .. _dcs-ug-0312013__en-us_topic_0148195355_fig394516508313:

   .. figure:: /_static/images/en-us_image_0148195318.png
      :alt: **Figure 1** Accessing the NuGet package manager console

      **Figure 1** Accessing the NuGet package manager console

#. Write the following code, and use the String Set and Get methods to test the connection.

   .. code-block::

      using System;
      using StackExchange.Redis;

      namespace redisdemo
      {
          class Program
          {
              // redis config
              private static ConfigurationOptions connDCS = ConfigurationOptions.Parse("{instance_ip_address}:{port},password=********,connectTimeout=2000");
              //the lock for singleton
              private static readonly object Locker = new object();
              //singleton
              private static ConnectionMultiplexer redisConn;
              //singleton
              public static ConnectionMultiplexer getRedisConn()
              {
                  if (redisConn == null)
                  {
                      lock (Locker)
                      {
                          if (redisConn == null || !redisConn.IsConnected)
                          {
                              redisConn = ConnectionMultiplexer.Connect(connDCS);
                          }
                      }
                  }
                  return redisConn;
              }
              static void Main(string[] args)
              {
                  redisConn = getRedisConn();
                  var db = redisConn.GetDatabase();
                  //set get
                  string strKey = "Hello";
                  string strValue = "DCS for Redis!";
                  Console.WriteLine( strKey + ", " + db.StringGet(strKey));

                  Console.ReadLine();
              }
          }
      }

   *{instance_ip_address}* and *{port}* are the IP address/domain name and port number of the DCS Redis instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312013__en-us_topic_0148195355_li457118182512>`. Change them as required. ``********`` indicates the password used for logging in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

#. Run the code. You have successfully accessed the instance if the following command output is displayed:

   .. code-block::

      Hello, DCS for Redis!

   For more information about other commands of StackExchange.Redis, visit `StackExchange.Redis <https://stackexchange.github.io/StackExchange.Redis/>`__.
