:original_name: dcs-pd-0326002.html

.. _dcs-pd-0326002:

Application Scenarios
=====================

Redis Application Scenarios
---------------------------

Many large-scale e-commerce websites and video streaming and gaming applications require fast access to large amounts of data that has simple data structures and does not need frequent join queries. In such scenarios, you can use Redis to achieve fast yet inexpensive access to data. Redis enables you to retrieve data from in-memory data stores instead of relying entirely on slower disk-based databases. In addition, you no longer need to perform additional management tasks. These features make Redis an important supplement to traditional disk-based databases and a basic service essential for internet applications receiving high-concurrency access.

Typical application scenarios of DCS for Redis are as follows:

#. **E-commerce flash sales**

   E-commerce product catalogue, deals, and flash sales data can be cached to Redis.

   For example, the high-concurrency data access in flash sales can be hardly handled by traditional relational databases. It requires the hardware to have higher configuration such as disk I/O. By contrast, Redis supports 100,000 QPS per node and allows you to implement locking using simple commands such as **SET**, **GET**, **DEL**, and **RPUSH** to handle flash sales.

#. **Live video commenting**

   In live streaming, online user, gift ranking, and bullet comment data can be stored as sorted sets in Redis.

   For example, bullet comments can be returned using the **ZREVRANGEBYSCORE** command. The **ZPOPMAX** and **ZPOPMIN** commands in Redis 5.0 can further facilitate message processing.

#. **Game leaderboard**

   In online gaming, the highest ranking players are displayed and updated in real time. The leaderboard ranking can be stored as sorted sets, which are easy to use with up to 20 commands.

#. **Social networking comments**

   In web applications, queries of post comments often involve sorting by time in descending order. As comments pile up, sorting becomes less efficient.

   By using lists in Redis, a preset number of comments can be returned from the cache, rather than from disk, easing the load off the database and accelerating application responses.
