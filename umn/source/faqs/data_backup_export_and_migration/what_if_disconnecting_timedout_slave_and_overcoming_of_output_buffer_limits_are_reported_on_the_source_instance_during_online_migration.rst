:original_name: dcs-migration-211125001.html

.. _dcs-migration-211125001:

What If "Disconnecting timedout slave" and "overcoming of output buffer limits" Are Reported on the Source Instance During Online Migration?
============================================================================================================================================

The following error messages may be displayed during online migration:

-  "Disconnecting timedout slave" is reported on the source instance, as shown in the following figure:

   |image1|

   Solution: Set the **repl-timeout** parameter of the source Redis instance to 300s.

-  "overcoming of output buffer limits" is reported on the source instance, as shown in the following figure:

   |image2|

   Solution: Set the **client-output-buffer-limit** parameter of the source Redis instance to 20% of the maximum memory of the instance.

.. |image1| image:: /_static/images/en-us_image_0000001227082869.png
.. |image2| image:: /_static/images/en-us_image_0000001226966281.png
