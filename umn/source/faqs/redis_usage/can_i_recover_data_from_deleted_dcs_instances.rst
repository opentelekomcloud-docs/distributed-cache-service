:original_name: dcs-faq-0730034.html

.. _dcs-faq-0730034:

Can I Recover Data from Deleted DCS Instances?
==============================================

If a DCS instance is automatically deleted or manually deleted through the Redis client, its data cannot be retrieved. If you have backed up the instance, you can restore its data from the backup. However, the restoration will overwrite the data written in during the period from the backup and the restoration.

By default, data is not evicted from DCS instances. You can modify the instance configuration parameters to adjust the eviction policy so that the instance can evict key values.
