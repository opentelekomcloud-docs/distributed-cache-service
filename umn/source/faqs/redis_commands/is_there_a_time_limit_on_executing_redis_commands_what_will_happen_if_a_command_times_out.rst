:original_name: dcs-faq-0427057.html

.. _dcs-faq-0427057:

Is There a Time Limit on Executing Redis Commands? What Will Happen If a Command Times Out?
===========================================================================================

Redis timeouts happen on the client or server.

-  Timeouts on the client are managed in the client code. Services can determine an appropriate timeout. For example, parameter **timeout** can be configured on Java Lettuce.

   When a command times out on the client, errors, command blocks, or client connection retries may occur.

-  On the server, the **timeout** parameter is set to **0** by default, indicating that connections will not be terminated. To modify the setting, see :ref:`Modifying Configuration Parameters <dcs-ug-0312024>`.

   If the **timeout** parameter is not **0**, idle connections between the client and server will be terminated as specified.
