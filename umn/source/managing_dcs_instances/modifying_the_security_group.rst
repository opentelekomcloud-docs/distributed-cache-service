:original_name: dcs-ug-0312026.html

.. _dcs-ug-0312026:

Modifying the Security Group
============================

On the DCS console, after creating a DCS instance, you can modify the security group of the DCS instance on the instance's **Basic Information** page.

You can modify the security groups of DCS Redis 3.0 instances but cannot modify those of DCS Redis 4.0/5.0/6.0 instances.

Prerequisites
-------------

At least one DCS instance has been created.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of the DCS instance for which you want to modify the security group.

#. Click the **Basic Information** tab. In the **Network** area, click |image2| next to the **Security Group** parameter.

#. Select a new security group from the drop-down list. Click |image3| to save the modification or |image4| to discard the modification.

   .. note::

      Only the security groups that have been created can be selected from the drop-down list. If you need to create a security group, follow the procedure described :ref:`Security Group Configurations <en-us_topic_0090662012>`.

   The modification will take effect immediately, that is, the new maintenance time window will appear on the **Basic Information** tab page immediately.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0266235582.png
.. |image3| image:: /_static/images/en-us_image_0266235377.png
.. |image4| image:: /_static/images/en-us_image_0266235369.png
