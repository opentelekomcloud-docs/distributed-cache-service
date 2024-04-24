:original_name: ShowInstanceSSLDetail.html

.. _ShowInstanceSSLDetail:

Querying SSL Encryption of an Instance
======================================

Function
--------

This API is used to query SSL encryption of an instance. This API is only supported by DCS Redis 6.0 instances.

URI
---

GET /v2/{project_id}/instances/{instance_id}/ssl

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

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+-----------------------+---------------------------------------------+
   | Parameter             | Type                  | Description                                 |
   +=======================+=======================+=============================================+
   | enabled               | Boolean               | Enabling or disabling SSL.                  |
   |                       |                       |                                             |
   |                       |                       | Enumeration values:                         |
   |                       |                       |                                             |
   |                       |                       | -  **true**                                 |
   |                       |                       |                                             |
   |                       |                       | -  **false**                                |
   +-----------------------+-----------------------+---------------------------------------------+
   | ip                    | String                | IP address used when SSL is enabled.        |
   +-----------------------+-----------------------+---------------------------------------------+
   | port                  | String                | Port used when SSL is enabled.              |
   +-----------------------+-----------------------+---------------------------------------------+
   | domain_name           | String                | Domain name used when SSL is enabled.       |
   +-----------------------+-----------------------+---------------------------------------------+
   | ssl_expired_at        | String                | SSL certificate validity period (UTC time). |
   +-----------------------+-----------------------+---------------------------------------------+
   | ssl_validated         | Boolean               | Whether the SSL certificate is valid.       |
   +-----------------------+-----------------------+---------------------------------------------+

**Status code: 400**

.. table:: **Table 3** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | error_msg             | String                | Error message.                                                                           |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code.                                                                              |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **9**                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_ext_msg         | String                | Extended error information. This parameter is not used currently and is set to **null**. |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

**Status code: 500**

.. table:: **Table 4** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | error_msg             | String                | Error message.                                                                           |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code.                                                                              |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **9**                                                                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_ext_msg         | String                | Extended error information. This parameter is not used currently and is set to **null**. |
   |                       |                       |                                                                                          |
   |                       |                       | Maximum: **1024**                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

Example Requests
----------------

.. code-block:: text

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/ssl

Example Responses
-----------------

**Status code: 200**

Instance SSL queried successfully.

.. code-block::

   {
     "enabled" : true,
     "ip" : "192.168.0.5",
     "port" : "6379",
     "domain_name" : "redis-553a2516-b865-4159-b774-204dc0a36e37.dcs.example.com:6379",
     "ssl_expired_at" : "2022-06-15T02:21:18.669Z",
     "ssl_validated" : true
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "DCS.4201",
     "error_msg" : "Do not support SSL."
   }

**Status code: 500**

Internal service error.

.. code-block::

   {
     "error_code" : "DCS.5010",
     "error_msg" : "Failed to operate SSL in database."
   }

Status Codes
------------

=========== ==================================
Status Code Description
=========== ==================================
200         Instance SSL queried successfully.
400         Invalid request.
500         Internal service error.
=========== ==================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
