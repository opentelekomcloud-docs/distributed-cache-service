:original_name: CreateRedislogDownloadLink.html

.. _CreateRedislogDownloadLink:

Obtaining the Log Download Link
===============================

Function
--------

This API is used to obtain the link for downloading logs.

URI
---

POST /v2/{project_id}/instances/{instance_id}/redislog/{id}/links

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | id          | Yes       | String | Unique ID of a log, which is obtained from the API used to query run logs.    |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------+--------+-------------------------------------------------------------+
   | Parameter | Type   | Description                                                 |
   +===========+========+=============================================================+
   | id        | String | Log ID.                                                     |
   +-----------+--------+-------------------------------------------------------------+
   | backup_id | String | Background task ID.                                         |
   +-----------+--------+-------------------------------------------------------------+
   | link      | String | Log download link. The default validity period is 24 hours. |
   +-----------+--------+-------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 3** Response body parameters

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

**Status code: 403**

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

**Status code: 404**

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

**Status code: 500**

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

Example Requests
----------------

.. code-block:: text

   POST https://{dcs_endpoint}/v2/0524e839a54847039e9b2b46e8aa788a/instances/5c597ce5-9823-48aa-bf4d-2defb9385b4a/redislog/3ea6ce21-048e-447a-83c3-3fb004b88439/links

Example Responses
-----------------

**Status code: 200**

Log download link obtained successfully.

.. code-block::

   {
     "id" : "3ea6ce21-048e-447a-83c3-3fb004b88439",
     "backup_id" : "3ea6ce21-048e-447a-83c3-3fb004b88439",
     "link" : "https://bucketxxxxx.{obs_endpoint}:443/xxxxx/redis_192.168.x.x_2021-04-16.log?AWSAccessKeyId=xxxxx"
   }

Status Codes
------------

=========== ========================================
Status Code Description
=========== ========================================
200         Log download link obtained successfully.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== ========================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
