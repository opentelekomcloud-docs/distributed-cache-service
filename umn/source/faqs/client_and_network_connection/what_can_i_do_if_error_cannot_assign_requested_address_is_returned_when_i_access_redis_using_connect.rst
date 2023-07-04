:original_name: dcs-faq-210721003.html

.. _dcs-faq-210721003:

What Can I Do If Error "Cannot assign requested address" Is Returned When I Access Redis Using connect?
=======================================================================================================

Symptom
-------

Error message "Cannot assign requested address" is returned when you access Redis using **connect**.

Analysis
--------

Applications that encounter this error typically use php-fpm and phpredis. In high-concurrency scenarios, a large number of TCP connections are in the TIME-WAIT state. As a result, the client cannot allocate new ports and the error message will be returned.

Solutions
---------

-  Solution 1: Use **pconnect** instead of **connect**.

   Using **pconnect** reduces the number of TCP connections and prevents connections from being re-established for each request, and therefore reduces latency.

   When using **connect**, the code for connecting to Redis is as follows:

   .. code-block::

      $redis->connect('${Hostname}',${Port});
      $redis->auth('${Inst_Password}');

   Replace **connect** with **pconnect**, and the code becomes:

   .. code-block::

      $redis->pconnect('${Hostname}', ${Port}, 0, NULL, 0, 0, ['auth' => ['${Inst_Password}']]);

   .. note::

      -  Replace the connection parameters in the example with actual values. *${Hostname}*, *${Port}*, and *${Inst_Password}* are the connection address, port number, and password of the Redis instance, respectively.
      -  phpredis must be v5.3.0 or later. You are advised to use this **pconnect** initialization mode to avoid NOAUTH errors during disconnection.

-  Solution 2: Modify the **tcp_max_tw_buckets** parameter of the ECS where the client is located.

   In this solution, the ports used by TIME-WAIT connections are reused. However, if retransmission occurs between the ECS and the backend service, the connection may fail. Therefore, the **pconnect** solution is recommended.

   #. Connect to the ECS where the client is located

   #. Run the following command to check the **ip_local_port_range** and **tcp_max_tw_buckets** parameters:

      **sysctl net.ipv4.tcp_max_tw_buckets net.ipv4.ip_local_port_range**

      Information similar to the following is displayed:

      .. code-block::

         net.ipv4.tcp_max_tw_buckets = 262144
         net.ipv4.ip_local_port_range = 32768  61000

   #. Run the following command to set the **tcp_max_tw_buckets** parameter to a value smaller than the value of **ip_local_port_range**:

      **sysctl -w net.ipv4.tcp_max_tw_buckets=10000**

Generally, solution 1 is recommended. In special scenarios (for example, the service code involves too many components and is difficult to change), solution 2 can be used to meet high concurrency requirements.
