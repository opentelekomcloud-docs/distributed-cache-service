:original_name: dcs-pd-200813003.html

.. _dcs-pd-200813003:

Command Restrictions
====================

Some Redis commands are supported by Redis Cluster DCS instances for multi-key operations in the same slot. For details, see :ref:`Table 1 <dcs-pd-200813003__table7589193113396>`.

Some commands support multiple keys but do not support cross-slot access. For details, see :ref:`Table 2 <dcs-pd-200813003__table152098710112>`.

.. _dcs-pd-200813003__table7589193113396:

.. table:: **Table 1** Redis commands restricted in Redis Cluster DCS instances

   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Category        | Description                                                                                                                                                       |
   +=================+===================================================================================================================================================================+
   | **Set**         |                                                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SINTER          | Returns the members of the set resulting from the intersection of all the given sets.                                                                             |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SINTERSTORE     | Equal to **SINTER**, but instead of returning the result set, it is stored in *destination*.                                                                      |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SUNION          | Returns the members of the set resulting from the union of all the given sets.                                                                                    |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SUNIONSTORE     | Equal to **SUNION**, but instead of returning the result set, it is stored in *destination*.                                                                      |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SDIFF           | Returns the members of the set resulting from the difference between the first set and all the successive sets.                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SDIFFSTORE      | Equal to **SDIFF**, but instead of returning the result set, it is stored in *destination*.                                                                       |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SMOVE           | Moves **member** from the set at **source** to the set at *destination*.                                                                                          |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Sorted Set**  |                                                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZUNIONSTORE     | Computes the union of *numkeys* sorted sets given by the specified keys.                                                                                          |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZINTERSTORE     | Computes the intersection of *numkeys* sorted sets given by the specified keys.                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **HyperLogLog** |                                                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PFCOUNT         | Returns the approximated cardinality computed by the HyperLogLog data structure stored at the specified variable.                                                 |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | PFMERGE         | Merges multiple HyperLogLog values into a unique value.                                                                                                           |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **Keys**        |                                                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RENAME          | Renames *key* to *newkey*.                                                                                                                                        |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RENAMENX        | Renames *key* to *newkey* if *newkey* does not yet exist.                                                                                                         |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | BITOP           | Performs a bitwise operation between multiple keys (containing string values) and stores the result in the destination key.                                       |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | RPOPLPUSH       | Returns and removes the last element (tail) of the list stored at source, and pushes the element at the first element (head) of the list stored at *destination*. |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | **String**      |                                                                                                                                                                   |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MSETNX          | Merges multiple HyperLogLog values into a unique value.                                                                                                           |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   While running commands that take a long time to run, such as **FLUSHALL**, DCS instances may not respond to other commands and may change to the faulty state. After the command finishes executing, the instance will return to normal.

.. _dcs-pd-200813003__table152098710112:

.. table:: **Table 2** Multi-key commands of Proxy Cluster instances

   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Category                                                 | Command                                                                                                                                               |
   +==========================================================+=======================================================================================================================================================+
   | Multi-key commands that support cross-slot access        | DEL, MGET, MSET, EXISTS, SUNION, SINTER, SDIFF, SUNIONSTORE, SINTERSTORE, SDIFFSTORE, ZUNIONSTORE, ZINTERSTORE                                        |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Multi-key commands that do not support cross-slot access | SMOVE, SORT, BITOP, MSETNX, RENAME, RENAMENX, BLPOP, BRPOP, RPOPLPUSH, BRPOPLPUSH, PFMERGE, PFCOUNT, BLMOVE, COPY, GEOSEARCHSTORE, LMOVE, ZRANGESTORE |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
