:original_name: dcs-migration-0312007.html

.. _dcs-migration-0312007:

Migrating Data from DCS to Self-Hosted Redis
============================================

Scenario
--------

You can use the online migration function of the DCS console to migrate DCS Redis instances to your self-hosted Redis. You can also export the DCS instance data to an RDB file and import it to local or self-hosted Redis.

Recommended Solutions
---------------------

-  Online migration on the DCS console

   For details, see :ref:`Online Migration of Self-Hosted Redis <dcs-migration-190703003>`. Select **Self-hosted Redis** and enter the target Redis address when configuring the target Redis.

-  Use redis-cli or the DCS console to export the DCS instance data to an RDB file, and then use redis-shake to import the file to the target.

   For details about how to install and use redis-shake, see :ref:`Self-Hosted Redis Cluster Migration with redis-shake <dcs-migrate-demo02>` and `redis-shake configuration instructions <https://github.com/alibaba/RedisShake/blob/release-v2.1.1-20210903/conf/redis-shake.conf>`__.

-  Rump

   This tool is recommended for online migration if possible. For details, see :ref:`Online Migration with Rump <dcs-migration-090626001_0>`.
