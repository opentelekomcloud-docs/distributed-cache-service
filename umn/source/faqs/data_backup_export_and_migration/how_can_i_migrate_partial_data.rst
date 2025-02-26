:original_name: dcs-migration-0312018.html

.. _dcs-migration-0312018:

How Can I Migrate Partial Data?
===============================

The online migration function provided on the console does not support migration of specified DBs. If you want to migrate **specified Redis DBs**, use redis-shake to export or import the specified DBs.

For details about how to install and use redis-shake, see :ref:`Self-Hosted Redis Cluster Migration with redis-shake (Online) <dcs-migrate-demo02>` and `redis-shake configuration instructions <https://github.com/alibaba/RedisShake/blob/release-v2.1.1-20210903/conf/redis-shake.conf>`__.

To migrate **specified data**, develop a script to obtain the specified keys and data and then import the data to a DCS instance.
