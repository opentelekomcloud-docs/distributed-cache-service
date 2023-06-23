:original_name: dcs-faq-0427057.html

.. _dcs-faq-0427057:

Is There a Time Limit on Executing Redis Commands? What Will Happen If a Command Times Out?
===========================================================================================

Redis command timeouts can be controlled on the client end or server end.

-  Timeouts on the client end are controlled in the client code. You can determine the timeouts that suit service needs. For example, if you use Lettuce, a Java client, configure the **timeout** parameter.
-  On the server end, the **timeout** parameter is set to **0** by default, indicating that connections will never be terminated. Modify the parameter setting by referring to :ref:`Modifying Configuration Parameters <dcs-ug-0312024>`.
