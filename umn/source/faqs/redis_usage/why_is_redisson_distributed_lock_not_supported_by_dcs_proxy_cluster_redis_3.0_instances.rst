:original_name: dcs-faq-0730025.html

.. _dcs-faq-0730025:

Why Is Redisson Distributed Lock Not Supported by DCS Proxy Cluster Redis 3.0 Instances?
========================================================================================

Redisson implements lock acquisition and unlocking in the following process:

#. Redisson lock acquisition and unlocking are implemented by running Lua scripts.
#. During lock acquisition, the **EXISTS**, **HSET**, **PEXPIRE**, **HEXISTS**, **HINCRBY**, **PEXPIRE**, and **PTTL** commands must be executed in the Lua script.
#. During unlocking, the **EXISTS**, **PUBLISH**, **HEXISTS**, **PEXPIRE**, and **DEL** commands must be executed in the Lua script.

In a proxy-based cluster, the proxy processes **PUBLISH** and **SUBSCRIBE** commands and forwards requests to the Redis server. The **PUBLISH** command cannot be executed in the Lua script.

As a result, Proxy Cluster DCS Redis 3.0 instances do not support Redisson distributed locks. To use Redisson, resort to Redis 4.0 or 5.0 instead.
