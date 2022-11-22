:original_name: dcs-faq-0730058.html

.. _dcs-faq-0730058:

When Does a Master/Standby Switchover Occur?
============================================

A master/standby switchover may occur in the following scenarios:

-  A master/standby switchover operation is initiated on the DCS Console.

-  If the master node of a master/standby instance fails, a master/standby switchover will be triggered.

   For example, running commands that consume a lot of resources, such as **KEYS** commands, will cause CPU usage to spike and as result triggers a master/standby switchover.

-  If you restart a master/standby instance on the DCS console, a master/standby switchover will be triggered.

After a master/standby switchover occurs, you will receive a notification. Check whether the client services are running properly. If not, check whether the TCP connection is normal and whether it can be re-established after the master/standby switchover to restore the services.
