:original_name: CreateOnlineMigrationTask.html

.. _CreateOnlineMigrationTask:

Creating an Online Data Migration Task
======================================

Function
--------

This API is used to create an online data migration task.

URI
---

POST /v2/{project_id}/migration/instance

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                                                                                                                                                                             |
   +===================+=================+=================+=========================================================================================================================================================================================================================================================+
   | name              | Yes             | String          | Name of the online migration task.                                                                                                                                                                                                                      |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description       | No              | String          | Description of the online migration task.                                                                                                                                                                                                               |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vpc_id            | Yes             | String          | VPC ID.                                                                                                                                                                                                                                                 |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | To obtain it, do as follows:                                                                                                                                                                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 1: Log in to the VPC console and view the VPC ID in the VPC details.                                                                                                                                                                          |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 2: Call the VPC API. For details, see the API for querying VPCs.                                                                                                                                                                              |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_id         | Yes             | String          | Network ID of the subnet.                                                                                                                                                                                                                               |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | To obtain it, do as follows:                                                                                                                                                                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 1: Log in to VPC console and click the target subnet on the **Subnets** tab page. You can view the network ID on the displayed page.                                                                                                          |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 2: Call the VPC API. For details, see the API for querying subnets.                                                                                                                                                                           |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_group_id | Yes             | String          | Security group which the instance belongs to.                                                                                                                                                                                                           |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | A security group implements access control for VMs within a security group or in different security groups, enhancing VM security. You can define different access rules for a security group to protect the VMs that are added to this security group. |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | To obtain it, do as follows:                                                                                                                                                                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 1: Log in to the VPC console and choose **Access Control** > **Security Groups**. You can create and configure a security group, and obtain the security group ID.                                                                            |
   |                   |                 |                 |                                                                                                                                                                                                                                                         |
   |                   |                 |                 | -  Method 2: Call the API used to query security group details. For details, see the API for querying security group details.                                                                                                                           |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   =========== ====== =========================
   Parameter   Type   Description
   =========== ====== =========================
   instance_id String Online migration task ID.
   =========== ====== =========================

**Status code: 400**

.. table:: **Table 4** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 401**

.. table:: **Table 5** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 403**

.. table:: **Table 6** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 404**

.. table:: **Table 7** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 8** Response body parameters

   +---------------+--------+------------------------------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                                              |
   +===============+========+==========================================================================================+
   | error_msg     | String | Error message.                                                                           |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_code    | String | Error code.                                                                              |
   +---------------+--------+------------------------------------------------------------------------------------------+
   | error_ext_msg | String | Extended error information. This parameter is not used currently and is set to **null**. |
   +---------------+--------+------------------------------------------------------------------------------------------+

Example Requests
----------------

Creating an online migration task and configuring the VPC, subnet, and security group for the migration ECS

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/migration/instance

   {
     "name" : "dcs-migration-thrc",
     "description" : "Creating an online data migration task",
     "vpc_id" : "5e37b3be-950a-48e1-b498-65b63d336481",
     "subnet_id" : "40f15ed6-7f85-49d5-ba0e-65b940d4812c",
     "security_group_id" : "9df96622-24b7-4813-84b8-ab74552a21d7"
   }

Example Responses
-----------------

**Status code: 200**

Online data migration task created.

.. code-block::

   {
     "instance_id" : "b21989ec-2889-4b8e-99db-19c073425ec2"
   }

Status Codes
------------

=========== ====================================
Status Code Description
=========== ====================================
200         Online data migration task created.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ====================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
