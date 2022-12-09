:original_name: dcs-faq-0730042.html

.. _dcs-faq-0730042:

Is There a Time Limit on Executing Redis Commands? What Will Happen If a Command Times Out?
===========================================================================================

The time limit for executing a Redis command is 1 minute. This limit cannot be configured. After the execution of a command times out, your client will be automatically disconnected.
