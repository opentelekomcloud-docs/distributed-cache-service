:original_name: dcs-faq-0730043.html

.. _dcs-faq-0730043:

Can the Major Version of a DCS Redis Instance Be Upgraded, for Example, from Redis 4.0 to 5.0?
==============================================================================================

No. It is unavailable. Different Redis versions use different underlying architectures. The Redis version used by a DCS instance cannot be changed once the instance is created. For example, you cannot change a DCS Redis 4.0 instance to Redis 5.0. If your service requires the features of higher Redis versions, create a DCS Redis instance of a higher version and then migrate data from the original instance to the new one. For details on how to migrate data, see :ref:`Migrating Data with DCS <dcs-ug-0312035>`.
