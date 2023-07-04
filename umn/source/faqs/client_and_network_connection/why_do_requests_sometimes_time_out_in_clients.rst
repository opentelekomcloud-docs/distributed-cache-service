:original_name: dcs-faq-0730005.html

.. _dcs-faq-0730005:

Why Do Requests Sometimes Time Out in Clients?
==============================================

Occasional timeout errors are normal because of network connectivity and client timeout configurations.

You are advised to include reconnection operations into your service code to avoid service failure if a single request fails.

If a connection request times out, check if AOF persistence has been enabled. To avoid blocking, ensure that AOF has been enabled.

If timeout errors occur frequently, contact O&M personnel.
