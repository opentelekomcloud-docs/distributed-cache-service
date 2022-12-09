:original_name: dcs-faq-0730011.html

.. _dcs-faq-0730011:

What Should Be Noted When Using Redis for Pub/Sub?
==================================================

Pay attention to the following issues when using Redis for pub/sub:

-  Your client must process messages in a timely manner.

   Your client subscribes to a channel. If it does not receive messages in a timely manner, DCS instance messages may be overstocked. If the size of accumulated messages reaches the threshold (32 MB by default) or remains at a certain level (8 MB by default) for a certain period of time (1 minute by default), your client will be automatically disconnected to prevent server memory exhaustion.

-  Your client must support connection re-establishment in case of disconnection.

   In the event of a disconnection, you need to run the **subscribe** or **psubscribe** command on your client to subscribe to a channel again. Otherwise, your client cannot receive messages.

-  Do not use pub/sub in scenarios with high message reliability requirements.

   The Redis pub/sub is not a reliable messaging system. Messages that are not retrieved will be discarded when your client is disconnected or a master/standby switchover occurs.
