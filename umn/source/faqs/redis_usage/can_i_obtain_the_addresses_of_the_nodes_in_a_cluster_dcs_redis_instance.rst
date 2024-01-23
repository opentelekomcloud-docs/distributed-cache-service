:original_name: dcs-faq-0730017.html

.. _dcs-faq-0730017:

Can I Obtain the Addresses of the Nodes in a Cluster DCS Redis Instance?
========================================================================

Cluster DCS Redis 3.0 instances (Proxy Cluster type) are used in the same way that you use single-node or master/standby instances. You do not need to know the backend node addresses.

For a cluster DCS Redis 4.0 or later instance (Redis Cluster type), run the **CLUSTER NODES** command to obtain node addresses:

**redis-cli -h {redis_address} -p {redis_port} -a {redis_password} cluster nodes**

In the output similar to the following, obtain the IP addresses and port numbers of all the master nodes.

|image1|

.. |image1| image:: /_static/images/en-us_image_0266316213.png
