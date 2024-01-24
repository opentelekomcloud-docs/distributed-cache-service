:original_name: dcs-ug-0312010.html

.. _dcs-ug-0312010:

hiredis in C++
==============

Access a DCS Redis instance through hiredis on an ECS in the same VPC. For more information about how to use other Redis clients, visit `the Redis official website <https://redis.io/clients>`__.

.. note::

   The operations described in this section apply only to single-node, master/standby, and Proxy Cluster instances. To use C++ to connect to a Redis Cluster instance, see the `C++ Redis client description <https://github.com/sewenew/redis-plus-plus?_ga=2.64990636.268662337.1603553558-977760105.1588733325#redis-cluster>`__.

Prerequisites
-------------

-  A DCS Redis instance has been created and is in the **Running** state.
-  An ECS has been created. For details about how to create an ECS, see `Elastic Cloud Server User Guide <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0163572588.html>`__.
-  If the ECS runs the Linux OS, ensure that the GCC compilation environment has been installed on the ECS.

Procedure
---------

#. .. _dcs-ug-0312010__en-us_topic_0148195243_li1655151054317:

   View the IP address/domain name and port number of the DCS Redis instance to be accessed.

   For details, see :ref:`Viewing Details of a DCS Instance <dcs-ug-0312016>`.

#. Log in to the ECS.

   The following uses CentOS as an example to describe how to access an instance in C++.

#. Install GCC, Make, and hiredis.

   If the system does not provide a compiling environment, run the following **yum** command to install the environment:

   **yum install gcc make**

#. Run the following command to download and decompress the hiredis package:

   **wget https://github.com/redis/hiredis/archive/master.zip**

   **unzip** **master.zip**

#. Go to the directory where the decompressed hiredis package is saved, and compile and install hiredis.

   **make**

   **make install**

#. Access the DCS instance by using hiredis.

   The following describes connection and password authentication of hiredis. For more information on how to use hiredis, visit the Redis official website.

   a. Edit the sample code for connecting to a DCS instance, and then save the code and exit.

      **vim connRedis.c**

      Example:

      .. code-block::

         #include <stdio.h>
         #include <stdlib.h>
         #include <string.h>
         #include <hiredis.h>
         int main(int argc, char **argv) {
              unsigned int j;
              redisContext *conn;
              redisReply *reply;
              if (argc < 3) {
                      printf("Usage: example {instance_ip_address} 6379 {password}\n");
                      exit(0);
              }
              const char *hostname = argv[1];
              const int port = atoi(argv[2]);
              const char *password = argv[3];
              struct timeval timeout = { 1, 500000 }; // 1.5 seconds
              conn = redisConnectWithTimeout(hostname, port, timeout);
              if (conn == NULL || conn->err) {
                 if (conn) {
                      printf("Connection error: %s\n", conn->errstr);
                      redisFree(conn);
                 } else {
                      printf("Connection error: can't allocate redis context\n");
                 }
              exit(1);
              }
              /* AUTH */
              reply = redisCommand(conn, "AUTH %s", password);
              printf("AUTH: %s\n", reply->str);
              freeReplyObject(reply);

              /* Set */
              reply = redisCommand(conn,"SET %s %s", "welcome", "Hello, DCS for Redis!");
              printf("SET: %s\n", reply->str);
              freeReplyObject(reply);

              /* Get */
              reply = redisCommand(conn,"GET welcome");
              printf("GET welcome: %s\n", reply->str);
              freeReplyObject(reply);

              /* Disconnects and frees the context */
              redisFree(conn);
              return 0;
         }

   b. Run the following command to compile the code:

      **gcc connRedis.c -o connRedis -I /usr/local/include/hiredis -lhiredis**

      If an error is reported, locate the directory where the **hiredis.h** file is saved and modify the compilation command.

      After the compilation, an executable **connRedis** file is obtained.

   c. Run the following command to access the chosen DCS Redis instance:

      **./connRedis** **{redis_instance_address}** **6379** **{password}**

      *{redis_instance_address}* indicates the IP address/domain name of DCS instance and **6379** is an example port number of DCS instance. For details about how to obtain the IP address/domain name and port, see :ref:`1 <dcs-ug-0312010__en-us_topic_0148195243_li1655151054317>`. Change them as required. *{password}* indicates the password used to log in to the chosen DCS Redis instance. This password is defined during DCS Redis instance creation.

      You have successfully accessed the instance if the following command output is displayed:

      .. code-block::

         AUTH: OK
         SET: OK
         GET welcome: Hello, DCS for Redis!

   .. important::

      If an error is reported, indicating that the hiredis library files cannot be found, run the following commands to copy related files to the system directories and add dynamic links:

      **mkdir /usr/lib/hiredis**

      **cp /usr/local/lib/libhiredis.so.0.13 /usr/lib/hiredis/**

      **mkdir /usr/include/hiredis**

      **cp /usr/local/include/hiredis/hiredis.h /usr/include/hiredis/**

      **echo '/usr/local/lib' >>;>>;/etc/ld.so.conf**

      **ldconfig**

      Replace the locations of the **so** and **.h** files with actual ones before running the commands.
