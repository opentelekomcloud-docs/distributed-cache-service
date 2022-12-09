:original_name: dcs-ug-190905001.html

.. _dcs-ug-190905001:

Configuring Alarm Rules for Critical Metrics
============================================

This section describes the alarm rules of some metrics and how to configure the rules. In actual scenarios, configure alarm rules for metrics by referring to the following alarm policies.

Alarm Policies for DCS Redis Instances
--------------------------------------

.. table:: **Table 1** DCS Redis instance metrics to configure alarm rules for

   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Metric            | Normal Range | Alarm Policy                                  | Approach Upper Limit | Handling Suggestion                                                                                                                                                          |
   +===================+==============+===============================================+======================+==============================================================================================================================================================================+
   | CPU Usage         | 0-100        | Alarm threshold: 70                           | No                   | Consider capacity expansion based on the service analysis.                                                                                                                   |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Number of consecutive periods: 2              |                      | The CPU capacity of a single-node or master/standby instance cannot be expanded. If you need larger capacity, use a cluster instance instead.                                |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Major                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Memory Usage      | 0-100        | Alarm threshold: 70                           | No                   | Expand the capacity of the instance.                                                                                                                                         |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Number of consecutive periods: 2              |                      |                                                                                                                                                                              |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Major                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Connected Clients | 0-10,000     | Alarm threshold: 8000                         | No                   | Optimize the connection pool in the service code to prevent the number of connections from exceeding the maximum limit.                                                      |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Number of consecutive periods: 2              |                      | For single-node and master/standby instances, the maximum number of connections allowed is 10,000. You can adjust the threshold based on service requirements.               |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Major                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | New Connections   | 0-10,000     | Alarm threshold: 10,000                       | ``-``                | Check whether **connect** is used and whether the client connection is abnormal. Use persistent connections ("pconnect" in Redis terminology) to ensure performance.         |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   | (Count/min)       |              | Number of consecutive periods: 2              |                      |                                                                                                                                                                              |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Minor                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Input Flow        | > 0          | Alarm threshold: 80% of the assured bandwidth | Yes                  | Consider capacity expansion based on the service analysis and bandwidth limit.                                                                                               |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Number of consecutive periods: 2              |                      | Configure this alarm only for single-node and master/standby DCS Redis 3.0 instances and set the alarm threshold to 80% of the assured bandwidth of DCS Redis 3.0 instances. |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Major                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Output Flow       | > 0          | Alarm threshold: 80% of the assured bandwidth | Yes                  | Consider capacity expansion based on the service analysis and bandwidth limit.                                                                                               |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Number of consecutive periods: 2              |                      | Configure this alarm only for single-node and master/standby DCS Redis 3.0 instances and set the alarm threshold to 80% of the assured bandwidth of DCS Redis 3.0 instances. |
   |                   |              |                                               |                      |                                                                                                                                                                              |
   |                   |              | Alarm severity: Major                         |                      |                                                                                                                                                                              |
   +-------------------+--------------+-----------------------------------------------+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Procedure
---------

In the following example, an alarm rule is set for the **CPU Usage** metric.

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. In the same row as the DCS instance whose metrics you want to view, choose **More** > **View Metric**.


   .. figure:: /_static/images/en-us_image_0270432745.png
      :alt: **Figure 1** Viewing instance metrics

      **Figure 1** Viewing instance metrics

#. Locate the **CPU Usage** metric. Hover over the metric and click |image2| to create an alarm rule for the metric.

   The **Create Alarm Rule** page is displayed.

#. Specify the alarm rule details.

   a. Specify the alarm policy and alarm severity.

      For example, the alarm policy shown in the following figure indicates that an alarm will be triggered if the CPU usage exceeds the threshold for two consecutive periods.


      .. figure:: /_static/images/en-us_image_0000001321666164.png
         :alt: **Figure 2** Setting the alarm content

         **Figure 2** Setting the alarm content

   b. Set the alarm notification configurations. If you enable **Alarm Notification**, set the validity period, notification object, and trigger condition.

   c. Click **Create**.

      .. note::

         For more information about creating alarm rules, see the *Cloud Eye User Guide* > *Using the Alarm Function* > *Creating Alarm Rules*.

.. |image1| image:: /_static/images/en-us_image_0000001148670664.png
.. |image2| image:: /_static/images/en-us_image_0227732778.png
