:original_name: dcs-ug-211105001.html

.. _dcs-ug-211105001:

Connecting to Redis on go-redis (Go)
====================================

This section describes how to access a Redis instance on go-redis. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

The following operations are based on an example of accessing a Redis instance on a client on an elastic cloud server (ECS).

.. note::

   To access a Redis 7.0 instance, use a go-redis `9.2.0 <https://github.com/redis/go-redis/releases/tag/v9.2.0>`__ or later client.

.. _dcs-ug-211105001__en-us_topic_0000001174913212_section1502270695932:

Prerequisites
-------------

-  A Redis instance is created, and is in the **Running** state.
-  View the IP address/domain name and port number of the DCS Redis instance to be accessed. For details, see :ref:`Viewing and Modifying DCS Instance Information <dcs-ug-0312016>`.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__

Connecting to Redis on go-redis
-------------------------------

#. Log in to the ECS.

   A Windows ECS is used as an example.

#. Install Visual Studio Community 2017 on the ECS.

#. Start Visual Studio and create a project. The project name can be customized. In this example, the project name is set to **redisdemo**.

#. Import the dependency package of go-redis and enter **go get github.com/go-redis/redis** on the terminal.

#. Write the following code:

   .. code-block::

      package main

      import (
          "fmt"
          "github.com/go-redis/redis"
      )

      func main() {
          // Single-node
          rdb := redis.NewClient(&redis.Options{
              Addr:     "host:port",
              Password: "********", // no password set
              DB:       0,  // use default DB
          })

          val, err := rdb.Get("key").Result()
          if err != nil {
              if err == redis.Nil {
                  fmt.Println("key does not exists")
                  return
              }
              panic(err)
          }
          fmt.Println(val)

          //Cluster
          rdbCluster := redis.NewClusterClient(&redis.ClusterOptions{
              Addrs:    []string{"host:port"},
              Password: "********",
          })
          val1, err1 := rdbCluster.Get("key").Result()
          if err1 != nil {
              if err == redis.Nil {
                  fmt.Println("key does not exists")
                  return
              }
              panic(err)
          }
          fmt.Println(val1)
      }

   *host:port* are the IP address/domain name and port number of the DCS Redis instance. For details about how to obtain the IP address/domain name and port, see :ref:`Prerequisites <dcs-ug-211105001__en-us_topic_0000001174913212_section1502270695932>`. Change them as required. ``********`` indicates the password used to log in to the DCS Redis instance. This password is defined during DCS Redis instance creation.

#. Run the **go build -o test main.go** command to package the code into an executable file, for example, **test**.

   .. caution::

      To run the package in the Linux OS, set the following parameters before packaging:

      **set GOARCH=amd64**

      **set GOOS=linux**

#. Run the **./test** command to access the DCS instance.
