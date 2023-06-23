:original_name: dcs-ug-0326013.html

.. _dcs-ug-0326013:

Restarting DCS Instances
========================

On the DCS console, you can restart one or multiple DCS instances at a time.

.. important::

   -  After a single-node DCS instance is restarted, data will be deleted from the instance.
   -  While a DCS instance is restarting, it cannot be read from or written to.
   -  An attempt to restart a DCS instance while it is being backed up may result in a failure.
   -  Restarting a DCS instance will disconnect the original client. You are advised to configure automatic reconnection in your application.

Prerequisites
-------------

The DCS instances you want to restart are in the **Running** or **Faulty** state.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. On the **Cache Manager** page, select one or more DCS instances you want to restart.

#. Click **Restart** above the DCS instance list.

#. In the displayed dialog box, click **Yes**.

   It takes 10 seconds to 30 minutes to restart DCS instances. After DCS instances are restarted, their status changes to **Running**.

   .. note::

      -  To restart a single instance, you can also click **Restart** in the same row as the instance.
      -  The time required for restarting a DCS instance depends on the cache size of the instance.

.. |image1| image:: /_static/images/en-us_image_0000001148443460.png
