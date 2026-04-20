:original_name: dcs-faq-020220331.html

.. _dcs-faq-020220331:

How Do I Create a Multi-DB Proxy Cluster Instance?
==================================================

When you create a Proxy Cluster instance, there is only one database by default. This section describes how to create a Proxy Cluster instance with multiple databases.

.. note::

   Before getting started, learn about :ref:`the constraints on implementing multi-DB <dcs-faq-210804001>`.

#. Log in to the DCS console.

#. Click |image1| in the upper left corner to select a region.

#. In the navigation pane, choose **Parameter Templates**.

#. In the row that contains the template with the desired cache engine version and instance type (Proxy Cluster), click **Customize**.

#. Set **multi-db** to **yes**.

#. Enter a new template name and click **OK**. The custom template is created successfully.

#. In the navigation pane, choose **Cache Manager**. Then click Create DCS Instance to create a Proxy Cluster instance.

   Set **Parameter Configuration** to **Use custom template** and select the custom template created in the preceding step.

   |image2|

   After the instance is created, connect to it to check whether it has multiple databases.

.. |image1| image:: /_static/images/en-us_image_0000001227937166.png
.. |image2| image:: /_static/images/en-us_image_0000002477627670.png
