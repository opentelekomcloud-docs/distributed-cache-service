:original_name: dcs-ug-0312047.html

.. _dcs-ug-0312047:

Viewing Traces on the CTS Console
=================================

After CTS is enabled, the tracker starts recording operations on cloud resources. Operation records for the last seven days can be viewed on the CTS console. This section describes how to query operation records of the last seven days on the CTS console.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner of the management console and select a region and a project.

   .. note::

      Select the same region as your application service.

#. Click **Service List** and choose **Management & Deployment** > **Cloud Trace Service**.

#. In the navigation pane, click **Trace List**.

#. Specify the filters used for querying traces. The following filters are available:

   -  **Search By**:

      Select an option from the drop-down list. Select **DCS** from the **Trace Source** drop-down list.

      When you select **Trace name**, you also need to select a specific trace name.

      When you select **Resource ID**, you also need to select a specific resource ID.

      When you select **Resource name**, you also need to select a specific resource name.

   -  **Operator**: Select a specific operator (a user other than tenant).

   -  **Trace Status**: Available options include **All trace status**, **normal**, **warning**, and **incident**. You can select only one of them.

   -  Start time and end time: You can specify the time period in which to query traces.

#. Click |image2| on the left of a trace to expand its details, as shown in :ref:`Figure 1 <dcs-ug-0312047__en-us_topic_0148195282_fig16275142414395>`.

   .. _dcs-ug-0312047__en-us_topic_0148195282_fig16275142414395:

   .. figure:: /_static/images/en-us_image_0266235352.png
      :alt: **Figure 1** Expanding trace details

      **Figure 1** Expanding trace details

#. Click **View Trace** in the **Operation** column. In the dialog box shown in :ref:`Figure 2 <dcs-ug-0312047__en-us_topic_0148195282_fig6764226461>`, the trace structure details are displayed.

   .. _dcs-ug-0312047__en-us_topic_0148195282_fig6764226461:

   .. figure:: /_static/images/en-us_image_0266235315.png
      :alt: **Figure 2** Viewing traces

      **Figure 2** Viewing traces

.. |image1| image:: /_static/images/en-us_image_0266235405.png
.. |image2| image:: /_static/images/en-us_image_0266235373.png
