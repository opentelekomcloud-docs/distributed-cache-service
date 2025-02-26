:original_name: dcs-ug-0312017.html

.. _dcs-ug-0312017:

Performing a Master/Standby Switchover for a DCS Instance
=========================================================

On the DCS console, you can manually switch the master and standby nodes of a DCS instance. This operation is used for special purposes, for example, releasing all service connections or terminating ongoing service operations.

Only master/standby and read/write splitting instances support a master/standby node switchover.

.. important::

   -  Services may be interrupted for up to 10 seconds during the switchover. Before performing a switchover, ensure that your application supports reconnection.
   -  During a master/standby node switchover, a large amount of resources will be consumed for data synchronization between the master and standby nodes. You are advised to perform this operation during off-peak hours.
   -  Data of the maser and standby nodes is synchronized asynchronously. Therefore, a small amount of data that is being operated on during the switchover may be lost.

Prerequisites
-------------

The DCS instance for which you want to perform a master/standby node switchover is in the **Running** state.

Procedure
---------

#. Log in to the DCS console.
#. Click |image1| in the upper left corner and select a region and a project.
#. In the navigation pane, choose **Cache Manager**.
#. In the **Operation** column of the instance, choose **More** > **Master/Standby Switchover**, then click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
