:original_name: dcs-faq-0730007.html

.. _dcs-faq-0730007:

Why Is "ERR unknown command" Displayed When I Access a DCS Redis Instance Through a Redis Client?
=================================================================================================

The possible causes are as follows:

#. The command is spelled incorrectly.

   As shown in the following figure, the error message is returned because the correct command for deleting a string should be **del**.

   |image1|

#. A command available in a higher Redis version is run in a lower Redis version.

   As shown in the following figure, the error message is returned because a stream command (available in Redis 5.0) is run in Redis 3.0.

   |image2|

#. Some commands are disabled.

   DCS Redis instance interfaces are fully compatible with the open-source Redis in terms of data access. However, for ease of use and security purposes, some operations cannot be initiated through Redis clients. For details about disabled commands, see :ref:`Command Compatibility <dcs-pd-200312003>`.

.. |image1| image:: /_static/images/en-us_image_0266315616.png
.. |image2| image:: /_static/images/en-us_image_0266315617.png
