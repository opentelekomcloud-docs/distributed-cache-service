:original_name: dcs-faq-0730015.html

.. _dcs-faq-0730015:

Do DCS Redis Instances Limit the Size of a Key or Value?
========================================================

-  The maximum allowed size of a key is 512 MB.

   To reduce memory usage and facilitate key query, ensure that each key does not exceed 1 KB.

-  The maximum allowed size of a string is 512 MB.

-  The maximum allowed size of a Set, List, or Hash is 512 MB.

   In essence, a Set is a collection of Strings; a List is a list of Strings; a Hash contains mappings between string fields and string values.

Prevent the client from constantly writing large values in Redis. Otherwise, network transmission efficiency will be lowered and the Redis server would take a longer time to process commands, resulting in higher latency.
