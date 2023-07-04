:original_name: dcs-faq-0730010.html

.. _dcs-faq-0730010:

How Do I Troubleshoot Redis Connection Failures?
================================================

**Preliminary checks:**

-  Check the connection address.

   Obtain the connection address from the instance basic information page on the DCS console.

-  Check the instance password.

   If the instance password is incorrect, the port can still be accessed but the authentication will fail.

-  Check the port.

   Port 6379 is the default port used in intra-VPC access to a DCS Redis instance.

-  Check if the maximum bandwidth has been reached.

   If the bandwidth reaches the maximum bandwidth for the corresponding instance specifications, Redis connections may time out.

-  For a DCS Redis 3.0 instance, check the inbound access rules of the security group.

   Intra-VPC access: If the Redis client and the Redis instance are bound with different security groups, allow inbound access over port 6379 for the security group of the instance.

   For details, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

-  For a DCS Redis 4.0/5.0/6.0 instance, check the whitelist configuration.

   If the instance has a whitelist, ensure that the client IP address is included in the whitelist. Otherwise, the connection will fail.

   For details, see :ref:`Managing IP Address Whitelist <dcs-ug-190812001>`.

   If the client IP address has changed, add the new IP address to the whitelist.

-  Check the configuration parameter **notify-keyspace-events**.

   Set **notify-keyspace-events** to **Egx**.

**Further checks:**

-  Jedis connection pool error

-  Error "Read timed out" or "Could not get a resource from the pool"

   Check if the **KEYS** command has been used. This command consumes a lot of resources and can easily block Redis. Instead, use the **SCAN** command and avoid executing the command frequently.
