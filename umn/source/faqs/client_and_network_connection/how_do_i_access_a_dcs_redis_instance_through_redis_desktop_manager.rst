:original_name: dcs-faq-0730008.html

.. _dcs-faq-0730008:

How Do I Access a DCS Redis Instance Through Redis Desktop Manager?
===================================================================

You can access a DCS Redis instance through the Redis Desktop Manager within a VPC.

#. Enter the address, port number (6379), and authentication password of the DCS instance you want to access.

#. Click **Test Connection**.

   The system displays a success message if the connection is successful.


   .. figure:: /_static/images/en-us_image_0266315618.png
      :alt: **Figure 1** Accessing a DCS Redis instance through Redis Desktop Manager over the intranet

      **Figure 1** Accessing a DCS Redis instance through Redis Desktop Manager over the intranet

   .. note::

      When accessing a cluster DCS instance, the Redis command is run properly, but an error message may display on the left because DCS clusters are based on Codis, which differs from the native Redis in terms of the **INFO** command output.
