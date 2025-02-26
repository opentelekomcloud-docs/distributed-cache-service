:original_name: dcs-faq-221222.html

.. _dcs-faq-221222:

Is the Read-only Address of a Master/Standby Instance Connected to the Master or Standby Node?
==============================================================================================

A master/standby DCS Redis 4.0 or later instance has a **Connection Address** and a **Read-only Address**. The connection address is used to connect to the master node of the instance, and the read-only address is used to connect to the standby node of the instance.

For details, see :ref:`Architecture of Master/Standby DCS Redis Instances <cachemasterslave__section5805185095215>`.


.. figure:: /_static/images/en-us_image_0000001431665772.png
   :alt: **Figure 1** Instance addresses

   **Figure 1** Instance addresses

By default, the client reads and writes data on the master node. Data is synchronized to the standby node. To implement read/write splitting, ensure that your client can distinguish between read and write requests. The client directs write requests to the read/write domain name and read requests to the read-only domain name.
