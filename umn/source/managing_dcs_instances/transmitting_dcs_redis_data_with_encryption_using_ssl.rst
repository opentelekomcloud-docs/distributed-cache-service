:original_name: dcs-ug-023129.html

.. _dcs-ug-023129:

Transmitting DCS Redis Data with Encryption Using SSL
=====================================================

**Single-node, master/standby, and Redis Cluster** **DCS Redis 6.0/7.0** instances support SSL encryption to ensure data transmission security. This function is not available for other instance versions. RESP (Redis Serialization Protocol), the communication protocol of Redis, only supports plaintext transmission in versions earlier than Redis 6.0.

Notes and Constraints
---------------------

-  Either SSL or client IP pass-through can be enabled. When SSL is enabled, data is encrypted without carrying client IP addresses.
-  **Enabling SSL will deteriorate read/write performance.**
-  **Enabling or disabling SSL will restart the instance and disconnect it for a few seconds. Wait until off-peak hours and ensure that your application can re-connect.**
-  **The restart cannot be undone. For single-node DCS instances and other instances where AOF persistence is disabled ("appendonly" is set to "no"), data will be cleared and ongoing backup tasks will be stopped. Exercise caution when performing this operation.**

Enabling or Disabling SSL
-------------------------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner of the console and select the region where your instance is located.
#. In the navigation pane, choose **Cache Manager**.
#. On the **Cache Manager** page, click a DCS instance.
#. In the navigation pane, choose **SSL**.
#. Click |image2| next to **SSL Certificate** to enable or disable SSL.
#. Click **Download Certificate** to download the SSL certificate.
#. Decompress the SSL certificate and upload the decompressed **ca.crt** file to the server where the Redis client is located.
#. Add the path of the **ca.crt** file to the command for connecting to the instance. For example, to access an instance on redis-cli, see :ref:`Connecting to Redis on redis-cli <dcs-ug-0326009>`.

.. |image1| image:: /_static/images/en-us_image_0000001549115173.png
.. |image2| image:: /_static/images/en-us_image_0000001505063901.png
