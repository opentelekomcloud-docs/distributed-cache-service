:original_name: dcs-faq-022025.html

.. _dcs-faq-022025:

Should I Use a Domain Name or an IP Address to Connect to a DCS Redis Instance?
===============================================================================

-  Single-node, read/write splitting, and Proxy Cluster:

   Each instance has only one IP address and one domain name address. The addresses remain unchanged before and after master/standby switchover. You can use either address to connect to the instance.

-  Master/Standby:

   Each instance has one IP address and two domain name addresses. One of the domain name addresses is used only for processing read requests. The addresses remain unchanged after master/standby switchover. You can use any address to connect to the instance.

   When you use a domain name address, distinguish between read and write requests. If you use **Connection Address** or **IP Address**, functions are not affected. If you use **Read-only Address**, only read requests are processed. You are advised to use read/write splitting instances if you have read/write splitting requirements.

-  Redis Cluster:

   A Redis Cluster instance has multiple pairs of master and replica IP addresses and one domain name address. You can use any address to connect to the instance.

   The connected node sends requests to the correct node. All nodes in the cluster can receive requests. **Configure multiple or all IP addresses** to prevent single points of failure.

.. note::

   -  Domain names cannot be resolved across regions. If the client server and the DCS Redis instance are not in the same region, the instance cannot be accessed using its domain name address. You can manually map the domain name to the IP address in the **hosts** file or access the instance using its IP address.
   -  For details about how to connect to an instance, see :ref:`Accessing an Instance <dcs-ug-0916002>`.
