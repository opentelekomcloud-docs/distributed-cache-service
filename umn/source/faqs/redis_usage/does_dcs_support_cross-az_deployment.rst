:original_name: dcs-faq-0730029.html

.. _dcs-faq-0730029:

Does DCS Support Cross-AZ Deployment?
=====================================

Master/Standby and cluster DCS Redis instances can be deployed across availability zones (AZs).

-  If instances nodes in an AZ are faulty, nodes in other AZs will not be affected. The standby node automatically becomes the master node to continue to operate, ensuring disaster recovery (DR).
-  Cross-AZ deployment does not compromise the speed of data synchronization between the master and standby nodes.
