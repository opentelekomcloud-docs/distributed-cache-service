:original_name: dcs-faq-0730036.html

.. _dcs-faq-0730036:

How Do I Clear Redis Data?
==========================

**Exercise caution when clearing data.**

-  Redis 3.0

   Data of a DCS Redis 3.0 instance cannot be cleared on the console, and can only be cleared by the **FLUSHDB** or **FLUSHALL** command in redis-cli.

   Run the **FLUSHALL** command to clear all the data in the instance.

   Run the **FLUSHDB** command to clear the data in the currently selected DB.

-  Redis 4.0 and 5.0

   To clear data of a DCS Redis 4.0 or 5.0 instance, you can run the **FLUSHDB** or **FLUSHALL** command in redis-cli, use the data clearing function on the DCS console, or run the **FLUSHDB** command on Web CLI.

   To clear data of a Redis Cluster instance, run the **FLUSHDB** or **FLUSHALL** command on every shard of the instance. Otherwise, data may not be completely cleared.

   .. note::

      -  Currently, only DCS Redis 4.0 and 5.0 instances support data clearing by using the DCS console and by running the **FLUSHDB** command on Web CLI.
      -  When you run the **FLUSHDB** command on Web CLI, only one shard is cleared at a time. If there are multiple shards, connect to and run the **FLUSHDB** command on each master node.
      -  Redis Cluster data cannot be cleared by using Web CLI.
