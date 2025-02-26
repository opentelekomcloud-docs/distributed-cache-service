:original_name: dcs-faq-0521003.html

.. _dcs-faq-0521003:

What Are Big Keys and Hot Keys?
===============================

+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Term                              | Definition                                                                                                                                                                          |
+===================================+=====================================================================================================================================================================================+
| Big key                           | There are two types of big keys:                                                                                                                                                    |
|                                   |                                                                                                                                                                                     |
|                                   | -  Keys that have a large value. If the size of a single String key exceeds 10 KB, or if the size of all elements of a key combined exceeds 50 MB, the key is defined as a big key. |
|                                   | -  Keys that have a large number of elements. If the number of elements in a key exceeds 5000, the key is defined as a big key.                                                     |
+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Hot key                           | A hot key is most frequently accessed, or consumes significant resources. For example:                                                                                              |
|                                   |                                                                                                                                                                                     |
|                                   | -  In a cluster instance, a shard processes 10,000 requests per second, among which 3000 are performed on the same key.                                                             |
|                                   | -  In a cluster instance, a shard uses a total of 100 Mbits/s inbound and outbound bandwidth, among which 80 Mbits/s is used by the **HGETALL** operation on a Hash key.            |
+-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
