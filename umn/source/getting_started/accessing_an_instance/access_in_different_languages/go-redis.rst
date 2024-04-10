:original_name: dcs-ug-211105001.html

.. _dcs-ug-211105001:

go-redis
========

Access a DCS Redis instance through go-redis on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

.. _dcs-ug-211105001__en-us_topic_0000001174913212_section1502270695932:

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.

-  View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.

Procedure
---------

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
