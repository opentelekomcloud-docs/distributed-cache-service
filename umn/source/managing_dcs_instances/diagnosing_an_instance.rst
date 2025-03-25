:original_name: dcs-ug-210818001.html

.. _dcs-ug-210818001:

Diagnosing an Instance
======================

Scenario
--------

If a fault or performance issue occurs, you can ask DCS to diagnose your instance to learn about the cause and impact of the issue and how to handle it.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner of the console and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of a DCS Redis instance.

#. Choose **Analysis and Diagnosis** > **Instance Diagnosis**.

#. Specify the tested object and time range, and click **Start Diagnosis**.

   -  **Tested Object**: You can select a single node or all nodes. By default, all nodes are tested.

   -  **Range**: You can specify up to 10 minutes before a point in time in the last 7 days.


      .. figure:: /_static/images/en-us_image_0000001968993633.png
         :alt: **Figure 1** Specifying the tested object and time range

         **Figure 1** Specifying the tested object and time range

      .. note::

         Instance diagnosis may fail during specification modification.

#. After the diagnosis is complete, you can view the result in the **Test History** list. If the result is abnormal, click **View Report** for details. You can click **Delete** to delete a record.

   In the report, you can view the cause and impact of abnormal items and suggestions for handling them.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
