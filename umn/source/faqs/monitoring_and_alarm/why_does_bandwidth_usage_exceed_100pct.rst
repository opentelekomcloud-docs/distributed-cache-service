:original_name: dcs-faq-0513001.html

.. _dcs-faq-0513001:

Why Does Bandwidth Usage Exceed 100%?
=====================================

The basic information about the bandwidth usage metric is as follows.

+-----------------+-----------------+-----------------------------------------------------------------+-------------+------------------------------------------------------+------------------------------+
| Metric ID       | Metric Name     | Description                                                     | Value Range | Monitored Object and Dimension                       | Monitoring Period (Raw Data) |
+=================+=================+=================================================================+=============+======================================================+==============================+
| bandwidth_usage | Bandwidth Usage | Percentage of the used bandwidth to the maximum bandwidth limit | 0-200%      | Monitored object:                                    | 1 minute                     |
|                 |                 |                                                                 |             |                                                      |                              |
|                 |                 |                                                                 |             | Redis 4.0 and later                                  |                              |
|                 |                 |                                                                 |             |                                                      |                              |
|                 |                 |                                                                 |             | Redis Server of a master/standby or cluster instance |                              |
|                 |                 |                                                                 |             |                                                      |                              |
|                 |                 |                                                                 |             | Dimension:                                           |                              |
|                 |                 |                                                                 |             |                                                      |                              |
|                 |                 |                                                                 |             | dcs_cluster_node                                     |                              |
+-----------------+-----------------+-----------------------------------------------------------------+-------------+------------------------------------------------------+------------------------------+

Bandwidth usage = (Input flow + Output flow)/(2 x Maximum bandwidth) x 100%

According to the formula, the bandwidth usage counts in the input flow and output flow, which include the traffic for replication between the master and replicas. Therefore, the total bandwidth usage is larger than the normal service traffic, and may exceed 100%.

If the value of the **Flow Control Times** metric is larger than 0, the maximum bandwidth has been reached and flow control has been performed.

However, flow control decisions are made without considering the traffic for replication between the master and replicas. Therefore, sometimes the bandwidth usage exceeds 100% but the number of flow control times is 0.
