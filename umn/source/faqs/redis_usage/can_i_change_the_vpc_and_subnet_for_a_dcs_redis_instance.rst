:original_name: dcs-faq-0730013.html

.. _dcs-faq-0730013:

Can I Change the VPC and Subnet for a DCS Redis Instance?
=========================================================

No. Once an instance is created, its VPC and subnet cannot be changed. If you want to use a different set of VPC and subnet, create a same instance and specify a desired set of VPC and subnet. After the new instance is created, you can migrate data from the old instance to the new instance by following the :ref:`data migration instructions <dcs-ug-0312035>`.
