:original_name: dcs-faq-0730043.html

.. _dcs-faq-0730043:

Can DCS Redis Instances Be Upgraded, for Example, from Redis 4.0 to 5.0?
========================================================================

No. Different Redis versions use different underlying architectures. The Redis version used by a DCS instance cannot be changed once the instance is created. For example, you cannot change a DCS Redis 4.0 instance to Redis 5.0. However, you will be informed of any defects or problems found in Redis.

If your service requires the features of higher Redis versions, create a DCS Redis instance of a higher version and then migrate data from the original instance to the new one. For details on how to migrate data, see :ref:`Migrating Data with DCS <dcs-ug-0312035>`.
