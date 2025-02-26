:original_name: dcs-faq-0730026.html

.. _dcs-faq-0730026:

Can I Customize or Change the Port for Accessing a DCS Instance?
================================================================

You cannot customize or change the port for accessing a DCS Redis 3.0 instance. You can customize (during instance creation) and change the port (on the instance details page) for accessing a DCS Redis 4.0 or later instance.

-  Redis 3.0

   Intra-VPC access: port 6379.

-  Redis 4.0 and later

   You can specify a port (ranging from 1 to 65535) or use the default port (6379) for accessing an instance. If no port is specified, the default port will be used.

If the instance and the client use different security groups, you must configure access rules for the security groups, allowing access through the specified port. For details, see :ref:`Security Group Configurations <en-us_topic_0090662012>`.

Customizing a Port
------------------

When creating a DCS Redis 4.0, 5.0, or 6.0 instance, you can enter a port number for **IP Address**. If you do not specify a port, the default port 6379 is used.

Changing the Port
-----------------

After a DCS Redis 4.0 or later instance is created, you can change its port.

#. In the navigation pane of the DCS console, choose **Cache Manager**.
#. Click a DCS Redis instance.
#. In the **Connection** area, click |image1| next to **Connection Address**.

   .. important::

      After the port is changed, all connections to the Redis instance are interrupted, and services are connected to the new port.

.. |image1| image:: /_static/images/en-us_image_0000001785451408.png
