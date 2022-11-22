:original_name: dcs-faq-0730004.html

.. _dcs-faq-0730004:

What Should I Do If Access to DCS Fails After Server Disconnects?
=================================================================

Analysis: If persistent connections ("pconnect" in Redis terminology) or connection pooling is used and connections are closed after being used for connecting to DCS instances, errors will be returned at attempts to reuse the connections.

Solution: When using pconnect or connection pooling, do not close the connection after the end of a request. If the connection is dropped, re-establish it.
