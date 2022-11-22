:original_name: dcs-faq-0730006.html

.. _dcs-faq-0730006:

What Should I Do If an Error Is Returned When I Use the Jedis Connection Pool?
==============================================================================

The error message that will possibly be displayed when you use the Jedis connection pool is as follows:

.. code-block::

   redis.clients.jedis.exceptions.JedisConnectionException: Could not get a resource from the pool

If this error message is displayed, check whether your instance is running properly. If it is running properly, perform the following checks:

#. Network

   a. Check the IP address configurations.

      Check whether the IP address configured on the Jedis client is the same as the subnet address configured for your DCS instance.

   b. Test the network.

      Use the ping command and telnet on the client to test the network.

      -  If the network cannot be pinged:

         For intra-VPC access to a DCS Redis 3.0 instance, ensure that the client and your DCS instance belong to the same VPC and security group, or the security group of your DCS instance allows access through port 6379. For details, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

      -  If the IP address can be pinged but telnet failed, restart your instance. If the problem persists after the restart, contact technical support.

#. Check the number of connections.

   Check whether the number of established network connections exceeds the upper limit configured for the Jedis connection pool. If the number of established connections approaches the configured upper limit, restart the DCS service and check whether the problem persists. If the number of established connections is far below the upper limit, continue with the following checks.

   In Unix or Linux, run the following command to query the number of established network connections:

   **netstat -an \| grep 6379 \| grep ESTABLISHED \| wc -l**

   In Windows, run the following command to query the number of established network connections:

   **netstat -an \| find "6379" \| find "ESTABLISHED" /C**

#. Check the JedisPool code.

   If the number of established connections approaches the upper limit, determine whether the problem is caused by service concurrency or incorrect usage of JedisPool.

   When using JedisPool, you must call **jedisPool.returnResource()** or **jedis.close()** (recommended) to release the resources after you call **jedisPool.getResource()**.

#. Check the number of TIME_WAIT connections.

   Run the **ss -s** command to check whether there are too many **TIME_WAIT** connections on the client.

   |image1|

   If there are too many **TIME_WAIT** connections, modify the kernel parameters by running the **/etc/sysctl.conf** command as follows:

   .. code-block::

      ##Uses cookies to prevent some SYN flood attacks when the SYN waiting queue overflows.
      net.ipv4.tcp_syncookies = 1
      ##Reuses TIME_WAIT sockets for new TCP connections.
      net.ipv4.tcp_tw_reuse = 1
      ##Enables quick reclamation of TIME_WAIT sockets in TCP connections.
      net.ipv4.tcp_tw_recycle = 1
      ##Modifies the default timeout time of the system.
      net.ipv4.tcp_fin_timeout = 30

   After the modification, run the **/sbin/sysctl -p** command for the modification to take effect.

#. If the problem persists after you perform the preceding checks, perform the following steps.

   Capture packets and send packet files along with the time and description of the exception to technical support for analysis.

   Run the following command to capture packets:

   **tcpdump -i eth0 tcp and port 6379 -n -nn -s 74 -w dump.pcap**

   In Windows, you can also install the Wireshark tool to capture packets.

   .. note::

      Replace the NIC name to the actual one.

.. |image1| image:: /_static/images/en-us_image_0266315615.png
