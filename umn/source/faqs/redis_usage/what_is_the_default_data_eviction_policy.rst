:original_name: dcs-faq-0730022.html

.. _dcs-faq-0730022:

What Is the Default Data Eviction Policy?
=========================================

Data is evicted from cache based on a user-defined space limit in order to make space for new data. For details, see the `Redis official website <https://redis.io/topics/lru-cache?spm=a2c4g.11186623.2.2.7a465a76HeE7QM>`__. You can :ref:`view or change the eviction policy <dcs-faq-0730022__section2022722111124>` by configuring an instance parameter on the DCS console.

Eviction Policies Supported by DCS Redis Instances
--------------------------------------------------

When **maxmemory** is reached, you can select one of the following eight eviction policies:

-  **noeviction**: When the memory limit is reached, DCS instances return errors to clients and no longer process write requests and other requests that could result in more memory to be used. However, **DEL** and a few more exception requests can continue to be processed.
-  **allkeys-lru**: DCS instances try to evict the least recently used keys first, in order to make space for new data.
-  **volatile-lru**: DCS instances try to evict the least recently used keys with an expire set first, in order to make space for new data.
-  **allkeys-random**: DCS instances recycle random keys so that new data can be stored.
-  **volatile-random**: DCS instances evict random keys with an expire set, in order to make space for new data.
-  **volatile-ttl**: DCS instances evict keys with an expire set, and try to evict keys with a shorter time to live (TTL) first, in order to make space for new data.
-  **allkeys-lfu**: DCS instances evict the least frequently used keys from all keys.
-  **volatile-lfu**: DCS instances evict the least frequently used keys with an **expire** field from all keys.

.. note::

   If no key can be recycled, **volatile-lru**, **volatile-random**, and **volatile-ttl** are the same as **noeviction**. For details, see the description of **noeviction**.

.. _dcs-faq-0730022__section2022722111124:

Viewing or Changing Eviction Policies
-------------------------------------

You can view or change the eviction policy with the **maxmemory-policy** parameter.

|image1|

.. |image1| image:: /_static/images/en-us_image_0000001591550122.png
