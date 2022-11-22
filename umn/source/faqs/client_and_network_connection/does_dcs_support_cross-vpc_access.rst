:original_name: en-us_topic_0100698850.html

.. _en-us_topic_0100698850:

Does DCS Support Cross-VPC Access?
==================================

Cross-VPC means the client and the instance are not in the same VPC.

Generally, VPCs are isolated from each other and ECSs cannot access DCS instances that belong to a different VPC from these ECSs.

However, by establishing VPC peering connections between VPCs, ECSs can access single-node and master/standby DCS instances across VPCs.

When using VPC peering connections to access DCS instances across VPCs, adhere to the rules listed in the following table.

.. table:: **Table 1** Client CIDR block constraints

   +-----------------------------------+-------------------------------------+
   | CIDR Blocks of DCS Instances      | CIDR Blocks Not Allowed for Clients |
   +===================================+=====================================+
   | 172.16.0.0/12 to 172.16.0.0/24    | 192.168.1.0/24                      |
   |                                   |                                     |
   |                                   | 192.168.2.0/24                      |
   |                                   |                                     |
   |                                   | 192.168.3.0/24                      |
   +-----------------------------------+-------------------------------------+
   | 192.168.0.0/16 to 192.168.0.0/24  | 172.31.1.0/24                       |
   |                                   |                                     |
   | 10.0.0.0/8 to 10.0.0.0/24         | 172.31.2.0/24                       |
   |                                   |                                     |
   |                                   | 172.31.3.0/24                       |
   +-----------------------------------+-------------------------------------+

For more information about VPC peering connection, see "VPC Peering Connection" in the *Virtual Private Cloud User Guide*.

.. important::

   Cluster DCS Redis instances do not support cross-VPC access. ECSs in a VPC cannot access cluster DCS instances in another VPC by using VPC peering connections.
