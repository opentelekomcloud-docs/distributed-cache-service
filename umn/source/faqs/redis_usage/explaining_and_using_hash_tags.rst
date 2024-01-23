:original_name: dcs-faq-211228001.html

.. _dcs-faq-211228001:

Explaining and Using Hash Tags
==============================

Hash Tag Design
---------------

Multi-key operations, such as those using the **MSET** command or Lua scripts, are atomic. All specified keys are executed at the same time. However, in a cluster, each key is hashed to a given shard, and multi-key operations are no longer atomic. The keys may be allocated to different slots. As a result, some keys are updated, while others are not. If there is a hash tag, the cluster determines which slot to allocate a key based on the hash tag. Keys with the same hash tag are allocated to the same slot.

Using Hash Tags
---------------

Only the content between the first left brace ({) and the following first right brace (}) is hashed.

For example:

-  In keys **{user1000}.following** and **{user1000}.followers**, there is only one pair of braces. **user1000** will be hashed.
-  In key **foo{}{bar}**, there is no content between the first { and the first }. The whole key **foo{}{bar}** will be hashed as usual.
-  In key **foo{{bar}}zap**, **{bar** (the content between the first { and the first }) is hashed.
-  In key **foo{bar}{zap}**, **bar** is hashed because it is between the first pair of { and }.

Hash Tag Example
----------------

When the following operation is performed:

.. code-block::

   EVAL "redis.call('set',KEYS[1],ARGV[1]) redis.call('set',KEYS[2],ARGV[2])" 2 key1 key2 value1 value2

The following error is displayed:

ERR 'key1' and 'key2' not in the same slot

You can use a hash tag to solve this issue:

.. code-block::

   EVAL "redis.call('set',KEYS[1],ARGV[1]) redis.call('set',KEYS[2],ARGV[2])" 2 {user}key1 {user}key2 value1 value2
