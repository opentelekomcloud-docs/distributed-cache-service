:original_name: dcs-ug-0312028.html

.. _dcs-ug-0312028:

Viewing Background Tasks
========================

After you initiate certain instance operations such as modifying instance specifications and changing or resetting a password, a background task will start for the operation. On the DCS console, you can view the background task status and clear task information by deleting task records.

Procedure
---------

#. Log in to the DCS console.

#. Click |image1| in the upper left corner and select a region and a project.

#. In the navigation pane, choose **Cache Manager**.

#. Click the name of the DCS instance whose background task you want to manage.

#. Click the **Background Tasks** tab.

   A list of background tasks is displayed.

#. Click |image2|, specify **Start Date** and **End Date**, and click **OK** to view tasks started in the corresponding time segment.

   -  Click |image3| to refresh the task status.
   -  To clear the record of a background task, click **Delete** in the **Operation** column.

      .. note::

         You can only delete the records of tasks in the **Successful** or **Failed** state.

.. |image1| image:: /_static/images/en-us_image_0000001148603246.png
.. |image2| image:: /_static/images/en-us_image_0266235508.png
.. |image3| image:: /_static/images/en-us_image_0266235430.png
