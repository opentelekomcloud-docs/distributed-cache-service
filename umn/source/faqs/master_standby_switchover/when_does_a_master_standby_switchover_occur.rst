:original_name: dcs-faq-0730058.html

.. _dcs-faq-0730058:

When Does a Master/Standby Switchover Occur?
============================================

A master/standby switchover may occur in the following scenarios:

-  A master/standby switchover operation is initiated on the DCS Console.

-  If the master node of a master/standby instance fails, a master/standby switchover will be triggered.

   For example, if commands (such as **KEYS**) that consume a lot of resources are used or logs are aged and deleted in batches, the CPU usage will surge, triggering a master/standby switchover.

-  If you restart a master/standby instance on the DCS console, a master/standby switchover will be triggered.

-  A master/standby switchover is triggered during Redis instance scale-out.

   During scale-up, a new standby node with the new specifications is created. After full and incremental data on the master node is synchronized to the standby node, a master/standby switchover is performed and the original node is deleted.

To monitor master/standby switchovers of instances, create event monitoring on Cloud Eye. Then, the system reports master/standby switchovers based on event alarm rules. Check whether the client services are abnormal if needed. If the services are abnormal, check whether the client connections are normal, and whether client connections can be retried after master/standby switchovers. Restart the client if the connections cannot be retried.
