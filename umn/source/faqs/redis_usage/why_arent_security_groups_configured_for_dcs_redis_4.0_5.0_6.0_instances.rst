:original_name: dcs-faq-0730014.html

.. _dcs-faq-0730014:

Why Aren't Security Groups Configured for DCS Redis 4.0/5.0/6.0 Instances?
==========================================================================

Currently, DCS Redis 4.0/5.0/6.0 instances use VPC endpoints and do not support security groups. You can configure whitelists instead. For details, see :ref:`Managing IP Address Whitelist <dcs-ug-190812001>`.

To allow access only from specific IP addresses to a DCS Redis instance, add the IP addresses to the instance whitelist.

If no whitelists are added to the instance whitelist or the whitelist function is disabled, all IP addresses that can communicate with the VPC can access the instance.
