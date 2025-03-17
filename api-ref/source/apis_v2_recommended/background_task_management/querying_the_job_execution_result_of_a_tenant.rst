:original_name: ShowJobInfo.html

.. _ShowJobInfo:

Querying the Job Execution Result of a Tenant
=============================================

Function
--------

This API is used to query the task execution result.

URI
---

GET /v2/{project_id}/jobs/{job_id}

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | job_id     | Yes       | String | Task ID.                                                                      |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                     |
   +=======================+=======================+=================================================================+
   | job_id                | String                | Task ID.                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | job_type              | String                | Job type. Options:                                              |
   |                       |                       |                                                                 |
   |                       |                       | -  **masterStandbySwapJob**: switching master and standby nodes |
   |                       |                       | -  **modifyClientIpTransJob**: modifying source IP pass-through |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | status                | String                | Job status. Enumeration values:                                 |
   |                       |                       |                                                                 |
   |                       |                       | -  **INIT**                                                     |
   |                       |                       | -  **RUNNING**                                                  |
   |                       |                       | -  **SUCCESS**                                                  |
   |                       |                       | -  **FAIL**                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | begin_time            | String                | Job start timestamp, in ms. The format is 1684191545379.        |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | end_time              | String                | Job start timestamp, in ms. The format is 1684191548248.        |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | fail_reason           | String                | Failure cause.                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------+

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

   GET https://{dcs_endpoint}/v2/a4d31cb6-3d72-4fdc-8ec9-6e3a41e47f71/instances/5560df16-cebf-4473-95c4-d1b573c16e79/tasks/8abf6e1e72c12e7c0172c15b508500aa/progress

Example Responses
-----------------

**Status code: 200**

Details of the background task queried successfully.

.. code-block::

   {
     "job_id" : "ff8080818822bbf70188235afc24141a",
     "job_type" : "masterStandbySwapJob",
     "status" : "SUCCESS",
     "begin_time" : "1684191545379",
     "end_time" : "1684191548248",
     "fail_reason" : null
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "111400063",
     "error_msg" : "Invalid {0} parameter in the request."
   }

Status Codes
------------

=========== ====================================================
Status Code Description
=========== ====================================================
200         Details of the background task queried successfully.
400         Invalid request.
401         Invalid authentication information.
403         Request rejected.
404         The requested resource could not be found.
500         Internal service error.
=========== ====================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
