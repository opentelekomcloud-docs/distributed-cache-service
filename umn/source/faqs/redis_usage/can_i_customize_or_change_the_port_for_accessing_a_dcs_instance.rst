:original_name: dcs-faq-0730026.html

.. _dcs-faq-0730026:

Can I Customize or Change the Port for Accessing a DCS Instance?
================================================================

You cannot customize or change the port for accessing a DCS Redis 3.0 instance. You can customize and change the port for accessing a DCS Redis 4.0 or 5.0 instance.

-  Redis 3.0

   Use port 6379 for intra-VPC access.

-  Redis 4.0 and Redis 5.0

   You can specify a port (ranging from 1 to 65535) or use the default port (6379) for accessing a DCS Redis 4.0 or 5.0 instance. If no port is specified, the default port will be used.

If the instance and the client use different security groups, you must configure access rules for the security groups, allowing access through the specified port. For details, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.
