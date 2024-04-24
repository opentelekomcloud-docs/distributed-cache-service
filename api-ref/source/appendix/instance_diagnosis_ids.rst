:original_name: dcs-api-0312050.html

.. _dcs-api-0312050:

Instance Diagnosis IDs
======================

.. table:: **Table 1** cause_ids

   +----+-------+---------------------------------------------------------------------------+
   | ID | Type  | Description                                                               |
   +====+=======+===========================================================================+
   | 1  | cause | The number of connected clients exceeds {THRESHOLD}.                      |
   +----+-------+---------------------------------------------------------------------------+
   | 2  | cause | The instantaneous traffic is too high.                                    |
   +----+-------+---------------------------------------------------------------------------+
   | 3  | cause | The underlying disk is abnormal.                                          |
   +----+-------+---------------------------------------------------------------------------+
   | 4  | cause | Data persistence failed.                                                  |
   +----+-------+---------------------------------------------------------------------------+
   | 5  | cause | Memory usage exceeds {THRESHOLD}.                                         |
   +----+-------+---------------------------------------------------------------------------+
   | 6  | cause | RDB persistence is enabled. Memory usage exceeds {THRESHOLD}.             |
   +----+-------+---------------------------------------------------------------------------+
   | 7  | cause | Excessive memory fragmentation.                                           |
   +----+-------+---------------------------------------------------------------------------+
   | 8  | cause | Cache hit rate is lower than {THRESHOLD}.                                 |
   +----+-------+---------------------------------------------------------------------------+
   | 9  | cause | Too many keys have expired at the same time.                              |
   +----+-------+---------------------------------------------------------------------------+
   | 10 | cause | The following commands with time complexity O(N) are executed: {COMMANDS} |
   +----+-------+---------------------------------------------------------------------------+
   | 11 | cause | CPU usage exceeds {THRESHOLD}.                                            |
   +----+-------+---------------------------------------------------------------------------+
   | 12 | cause | Data is persisted.                                                        |
   +----+-------+---------------------------------------------------------------------------+
   | 13 | cause | QPS has increased.                                                        |
   +----+-------+---------------------------------------------------------------------------+

.. table:: **Table 2** impact_ids

   == ====== ==================================
   ID Type   Description
   == ====== ==================================
   1  impact Redis connections will be refused.
   2  impact Redis will be disconnected.
   3  impact Redis responses will slow down.
   4  impact RDB persistence will fail.
   5  impact Cache hit ratio will decrease.
   6  impact AOF persistence will fail.
   == ====== ==================================

.. table:: **Table 3** advice_ids

   +----+--------+---------------------------------------------------------------------------------+
   | ID | Type   | Description                                                                     |
   +====+========+=================================================================================+
   | 1  | advice | Retrieve connections from the connection pool.                                  |
   +----+--------+---------------------------------------------------------------------------------+
   | 2  | advice | Use read/write splitting or a cluster.                                          |
   +----+--------+---------------------------------------------------------------------------------+
   | 3  | advice | Expand the capacity of the instance.                                            |
   +----+--------+---------------------------------------------------------------------------------+
   | 4  | advice | Manually run the **MEMORY PURGE** command during low-demand hours.              |
   +----+--------+---------------------------------------------------------------------------------+
   | 5  | advice | Check the Redis usage or reduce the cache granularity to avoid memory eviction. |
   +----+--------+---------------------------------------------------------------------------------+
   | 6  | advice | Set different expiration time for the keys.                                     |
   +----+--------+---------------------------------------------------------------------------------+
   | 7  | advice | Do not use commands with time complexity of O(N).                               |
   +----+--------+---------------------------------------------------------------------------------+
