:original_name: dcs-faq-0606002.html

.. _dcs-faq-0606002:

How Do I Detect Big Keys and Hot Keys in Advance?
=================================================

+--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Method                                                                   | Description                                                                                                                                                                                                                                                                                                                                                 |
+==========================================================================+=============================================================================================================================================================================================================================================================================================================================================================+
| Through **Big Key Analysis** and **Hot Key Analysis** on the DCS console | See :ref:`Analyzing Big Keys and Hot Keys <dcs-ug-190808001>`.                                                                                                                                                                                                                                                                                              |
+--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| By using the **bigkeys** and **hotkeys** options on redis-cli            | -  redis-cli uses the **bigkeys** option to traverse all keys in a Redis instance and returns the overall key statistics and the biggest key of six data types: Strings, Lists, Hashes, Sets, Zsets, and Streams. The command is **redis-cli -h** *<Instance connection address>* **-p** *<Port number>* **-a** *<Password>* **--bigkeys**.                 |
|                                                                          | -  In Redis 4.0 and later, you can use the **hotkeys** option to quickly find hot keys in redis-cli. Run this command during service running to find hot keys: **redis-cli -h** *<Instance connection address>* **-p** *<Port number>* **-a** *<Password>* **--hotkeys**. The hot key details can be obtained from the summary part in the returned result. |
+--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Hot key analysis is not supported by DCS Redis 3.0 instances. You can :ref:`configure alarms <dcs-ug-190905001__en-us_topic_0190235954_section1118571110427>` to detect hot keys.

-  Configure alarm rules for the **Memory Usage** metric of the instance nodes.

   If a node has a big key, the memory usage of the node is much higher than that of other nodes. In this case, an alarm is triggered to help you find the potentially problematic key.

-  Configure alarm rules for the **Maximum Inbound Bandwidth**, **Maximum Outbound Bandwidth**, and **CPU Usage** metrics of the instance nodes.

   If a node has a hot key, the bandwidth and CPU usage of the node is much higher than that of other nodes. In this case, an alarm is triggered to help you find the potentially problematic key.
