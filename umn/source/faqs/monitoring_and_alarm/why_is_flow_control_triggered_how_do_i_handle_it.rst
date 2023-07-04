:original_name: dcs-faq-0220721.html

.. _dcs-faq-0220721:

Why Is Flow Control Triggered? How Do I Handle It?
==================================================

Flow control is triggered when the traffic used by a Redis instance in a period exceeds the maximum bandwidth.

.. note::

   For details about the maximum allowed bandwidth, see the "Assured/Maximum Bandwidth" column of different instance types listed in :ref:`DCS Instance Specifications <en-us_topic_0054235835>`.

Even if the bandwidth usage is low, flow control may still be triggered. The real-time bandwidth usage is reported once in each reporting period. Flow controls are checked every second. The traffic may surge within seconds and then fall back between reporting periods. By the time the bandwidth usage is reported, it may have already restored to the normal level.

For master/standby instances:

-  If flow control is always triggered when the bandwidth usage is low, there may be service microbursts or big or hot keys. In this case, check for big or hot keys.
-  If the bandwidth usage remains high, the bandwidth limit may be exceeded. In this case, expand the capacity. Larger capacity supports higher bandwidth.

For cluster instances:

-  If flow control is triggered only on one or a few shards, the shards may have big or hot keys.
-  If flow control or high bandwidth usage occurs on all or most shards at the same time, bandwidth usage of the instance has reached the limit. In this case, expand the instance capacity.

.. note::

   -  You can analyze big keys and hot keys on the DCS console. For details, see :ref:`Analyzing Big Keys and Hot Keys <dcs-ug-190808001>`.
   -  Running commands (such as **KEYS**) that consume lots of resources may cause high CPU and bandwidth usage. As a result, flow control is triggered.
