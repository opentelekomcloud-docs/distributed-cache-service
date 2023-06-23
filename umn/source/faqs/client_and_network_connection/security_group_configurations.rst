:original_name: en-us_topic_0090662012.html

.. _en-us_topic_0090662012:

Security Group Configurations
=============================

DCS helps you control access to your DCS instances in the following ways, depending on the deployment mode:

-  To control access to DCS Redis 3.0 instances, you can use security groups. Whitelists are not supported. Security group operations are described in this section.
-  To control access to DCS Redis 4.0/5.0/6.0 instances, you can use whitelists. Security groups are not supported. Whitelist operations are described in :ref:`Managing IP Address Whitelist <dcs-ug-190812001>`.

The following describes how to configure security groups for **intra-VPC access** to DCS Redis 3.0 instances.

Intra-VPC Access to DCS Redis 3.0 Instances
-------------------------------------------

An ECS can communicate with a DCS instance if they belong to the same VPC and security group rules are configured correctly.

In addition, you must configure correct rules for the security groups of both the ECS and DCS instance so that you can access the instance through your client.

-  If the ECS and DCS instance are configured with the same security group, network access in the group is not restricted by default.
-  If the ECS and DCS instance are configured with different security groups, add security group rules to ensure that the ECS and DCS instance can access each other.

   .. note::

      -  Suppose that the ECS on which the client runs belongs to security group **sg-ECS**, and the DCS instance that the client will access belongs to security group **sg-DCS**.
      -  Suppose that the port number of the DCS service is 6379.
      -  The remote end is a security group or an IP address.

   #. Configuring security group for the ECS.

      Add the following outbound rule to allow the ECS to access the DCS instance. Skip this rule if there are no restrictions on the outbound traffic.


      .. figure:: /_static/images/en-us_image_0277697231.png
         :alt: **Figure 1** Security group rules allowing the ECS to access the DCS instance

         **Figure 1** Security group rules allowing the ECS to access the DCS instance

   #. Configuring security group for the DCS instance.

      To ensure that your client can access the DCS instance, add the following inbound rule to the security group configured for the DCS instance:


      .. figure:: /_static/images/en-us_image_0277697263.png
         :alt: **Figure 2** Security group rules making the DCS instance accessible to the ECS

         **Figure 2** Security group rules making the DCS instance accessible to the ECS

      .. important::

         For the source IP address, use the specified IP address of the DCS instance. Avoid using **0.0.0.0/0** to prevent ECSs bound with the same security group from being attacked by Redis vulnerability exploits.
