:original_name: dcs-faq-0730027.html

.. _dcs-faq-0730027:

Can I Modify the Connection Addresses for Accessing a DCS Instance?
===================================================================

After a DCS instance is created, its intra-VPC connection addresses cannot be modified.

To use a different IP address, you must create a new instance and manually specify an IP address. After the instance is created, migrate the data from the old instance to the new instance.

For details about accessing DCS instances through clients, see :ref:`Accessing a DCS Redis Instance Through redis-cli <dcs-ug-0326009>`.
