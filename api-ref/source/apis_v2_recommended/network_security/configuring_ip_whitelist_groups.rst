:original_name: UpdateIpWhitelist.html

.. _UpdateIpWhitelist:

Configuring IP Whitelist Groups
===============================

Function
--------

This API is used to configure IP address whitelist groups for a specific instance, including creating, disabling, editing, and deleting a whitelist. New whitelist settings will overwrite the existing setting. Therefore, save the existing whitelist before you add a new one.

IP whitelist groups are supported only by DCS Redis 4.0 and later instances.

URI
---

PUT /v2/{project_id}/instance/{instance_id}/whitelist

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameters

   +------------------+-----------+--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Mandatory | Type                                                                     | Description                                                                                                                                      |
   +==================+===========+==========================================================================+==================================================================================================================================================+
   | instance_id      | No        | String                                                                   | Instance ID.                                                                                                                                     |
   +------------------+-----------+--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable_whitelist | Yes       | Boolean                                                                  | Whether to enable the whitelist. The options are **true** and **false**.                                                                         |
   +------------------+-----------+--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | whitelist        | Yes       | Array of :ref:`Whitelist <updateipwhitelist__request_whitelist>` objects | IP whitelist group. New whitelist settings will overwrite the existing setting. Therefore, save the existing whitelist before you add a new one. |
   +------------------+-----------+--------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. _updateipwhitelist__request_whitelist:

.. table:: **Table 3** Whitelist

   +------------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type             | Description                                                                                                                                                                                                                                                         |
   +============+===========+==================+=====================================================================================================================================================================================================================================================================+
   | group_name | Yes       | String           | Whitelist group name. A maximum of four groups can be created for each instance.                                                                                                                                                                                    |
   +------------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ip_list    | Yes       | Array of strings | List of IP addresses in the whitelist group. A maximum of 20 IP addresses or IP address ranges can be added to an instance. Separate multiple IP addresses or IP address ranges with commas (,). IP address 0.0.0.0 and IP address range 0.0.0/0 are not supported. |
   +------------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

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

-  Enabling the whitelist and configuring IP addresses allowed to access the instance

   .. code-block:: text

      PUT https://{dcs_endpoint}/v2/{project_id}/instance/{instance_id}/whitelist

      {
        "enable_whitelist" : true,
        "whitelist" : [ {
          "group_name" : "test001",
          "ip_list" : [ "10.10.10.1", "10.10.10.2" ]
        } ]
      }

-  Enabling the whitelist and configuring subnet mask allowed to access the instance.

   .. code-block:: text

      PUT https://{dcs_endpoint}/v2/{project_id}/instance/{instance_id}/whitelist

Example Responses
-----------------

None

Status Codes
------------

=========== ============================================
Status Code Description
=========== ============================================
204         IP whitelist groups configured successfully.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
