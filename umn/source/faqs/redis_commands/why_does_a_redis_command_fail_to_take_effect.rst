:original_name: dcs-faq-0730041.html

.. _dcs-faq-0730041:

Why Does a Redis Command Fail to Take Effect?
=============================================

Run the command in redis-cli to check whether the command takes effect.

The following describes two scenarios:

-  Scenario 1: Set and query the value of a key to check whether the **SET** and **GET** commands work.

   The **SET** command is used to set the string value. If the value is not changed, run the following commands in redis-cli to access the instance:

   |image1|

-  Scenario 2: If the timeout set using the **EXPIRE** command is incorrect, perform the following operations:

   Set the timeout to 10 seconds and run the **TTL** command to view the remaining time. As shown in the following example, the remaining time is 7 seconds.

   |image2|

.. note::

   Redis clients (including redis-cli, Jedis clients, and Python clients) communicate with Redis server using a binary protocol.

   If Redis commands are run properly in redis-cli, the problem may lie in the service code. In this case, create logs in the code for further analysis.

.. |image1| image:: /_static/images/en-us_image_0266322522.jpg
.. |image2| image:: /_static/images/en-us_image_0266322523.png
