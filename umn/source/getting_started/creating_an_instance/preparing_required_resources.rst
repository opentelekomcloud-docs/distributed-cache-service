:original_name: dcs-ug-0312004.html

.. _dcs-ug-0312004:

Preparing Required Resources
============================

To access DCS instances through a Virtual Private Cloud (VPC), create a VPC and configure security groups and subnets for it before using DCS. A VPC provides an isolated virtual network environment which you can configure and manage. Using VPCs enhances cloud resource security and simplifies network deployment.

Once you have created the required resources, you can use them for all DCS instances you subsequently create.

Creating a VPC and Subnet
-------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner and select a region and a project.

#. Click **Service List**, and choose **Network** > **Virtual Private Cloud** to launch the VPC console.

#. Click **Apply for VPC**.

#. Create a VPC as prompted, retaining the default values unless otherwise required.

   For details about how to create a VPC, see `Creating a VPC <https://docs.otc.t-systems.com/usermanual/vpc/en-us_topic_0013935842.html>`__.

   After a VPC is created, a subnet is also created in the subnet. If the VPC needs more subnets, go to :ref:`6 <dcs-ug-0312004__li66581623151519>` and :ref:`7 <dcs-ug-0312004__en-us_topic_0148195347_li10954228154518>`. Otherwise, go to :ref:`Creating a Security Group <dcs-ug-0312004__section564574212010>`.

   .. note::

      -  When creating a VPC, **CIDR Block** indicates the IP address range of the VPC. If this parameter is set, the IP addresses of subnets in the VPC must be within the IP address range of the VPC.
      -  If you create a VPC to provision DCS instances, you do not need to configure the CIDR block for the VPC.

#. .. _dcs-ug-0312004__li66581623151519:

   In the navigation pane on the left, choose **Virtual Private Cloud** > **Subnets**.

#. .. _dcs-ug-0312004__en-us_topic_0148195347_li10954228154518:

   Click **Create Subnet**. Create a subnet as prompted, retaining the default values unless otherwise required.

   For details about how to create a subnet, see `Creating a Subnet for the VPC <https://docs.otc.t-systems.com/usermanual/vpc/en-us_topic_0013748726.html>`__.

.. _dcs-ug-0312004__section564574212010:

Creating a Security Group
-------------------------

.. note::

   Only DCS Redis 3.0 instances require security groups.

#. Log in to the VPC console.

#. In the navigation pane on the left, choose **Access Control** > **Security Groups** and then click **Create Security Group** in the upper right corner of the displayed page. Create a security group as prompted, retaining the default values unless otherwise required.

   For details about how to create a security group, see `Creating a Security Group <https://docs.otc.t-systems.com/usermanual/vpc/en-us_topic_0013748715.html>`__.

   -  Set **Template** to **Custom**.
   -  After a security group is created, retain the default inbound rule that allows communication among ECSs within the security group and the default outbound rule that allows all outbound traffic.
   -  To use DCS, you must add the security group rules described in the following table. You can also add other rules based on site requirements.

      .. table:: **Table 1** Security group rules

         +-----------+----------+------+-----------+-------------------------------------------------------+
         | Direction | Protocol | Port | Source    | Description                                           |
         +===========+==========+======+===========+=======================================================+
         | Inbound   | TCP      | 6379 | 0.0.0.0/0 | Access a DCS Redis 3.0 instance in a private network. |
         +-----------+----------+------+-----------+-------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001214124082.png
