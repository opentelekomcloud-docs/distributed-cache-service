:original_name: dcs-faq-0730024.html

.. _dcs-faq-0730024:

Why Is Memory Usage More Than 100%?
===================================

This is normal due to Redis functions (such as master/replica replication and lazyfree). When the memory becomes full, scale up the instance or remove unnecessary data.
