:original_name: dcs-faq-0730030.html

.. _dcs-faq-0730030:

Why Does It Take a Long Time to Start a Cluster DCS Instance?
=============================================================

Possible cause: When a cluster instance is started, status and data are synchronized between the nodes of the instance. If a large amount of data is continuously written into the instance before the synchronization is complete, the synchronization will be prolonged and the instance remains in the **Starting** state. After the synchronization is complete, the instance enters the **Running** state.

Solution: Start writing data to an instance only after the instance has been started.
