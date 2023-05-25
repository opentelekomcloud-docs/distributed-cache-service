:original_name: dcs-faq-0730012.html

.. _dcs-faq-0730012:

Why Is CPU Usage of a DCS Redis Instance 100%?
==============================================

-  Possible cause 1:

   The service QPS is so high that the CPU usage spikes to 100%.

-  Possible cause 2:

   You have run commands that consume a lot of resources, such as **KEYS**. This will make CPU usage spike and can easily trigger a master/standby switchover.
