:original_name: dcs-ug-0911001.html

.. _dcs-ug-0911001:

Starting DCS Instances
======================

Scenario
--------

On the DCS console, you can start one or multiple DCS instances at a time.

.. note::

   This function is not supported by recent instances. You can only start old instances that have been stopped. Once started, these instances can only be restarted and can no longer be stopped or started.

Prerequisites
-------------

The DCS instances you want to start are in the **Stopped** state.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. On the **Cache Manager** page, select one or more DCS instances you want to restart.
#. Click **Start** above the DCS instance list.
#. In the **Start** dialog box, click **Yes** to confirm that you want to start the instances.

   -  It takes 1 to 30 minutes to start DCS instances.
   -  After DCS instances are started, their statuses change from **Stopped** to **Running**.

   .. note::

      To start a single instance, you can also click **Start** in the **Operation** column in the same row as the instance.

.. |image1| image:: /_static/images/en-us_image_0000001148443450.png
