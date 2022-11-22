:original_name: dcs-faq-0730001.html

.. _dcs-faq-0730001:

Does DCS Support Public Access?
===============================

No. DCS instances cannot be access at their EIPs over public networks. To ensure security, the ECS that serves as a client and the DCS instance that the client will access must belong to the same VPC.

In the application development and debugging phase, you can also use an SSH agent to access DCS instances in the local environment.
