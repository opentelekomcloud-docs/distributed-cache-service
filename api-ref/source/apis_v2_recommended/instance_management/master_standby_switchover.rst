:original_name: ChangeMasterStandby.html

.. _ChangeMasterStandby:

Master/Standby Switchover
=========================

Function
--------

This API is used to perform a master/standby switchover. Only master/standby instances support this operation.

URI
---

POST /v2/{project_id}/instances/{instance_id}/swap

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 400**

.. table:: **Table 2** Response body parameters

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

**Status code: 403**

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

**Status code: 404**

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

**Status code: 500**

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

Example Requests
----------------

.. code-block:: text

   POST https://{dcs_endpoint}/v2/a4d31cb6-3d72-4fdc-8ec9-6e3a41e47f71/instances/5560df16-cebf-4473-95c4-d1b573c16e79/swap

Example Responses
-----------------

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_msg" : "Master standby swap is not supported.",
     "error_code" : "DCS.4855",
     "error_ext_msg" : null
   }

Status Codes
------------

=========== =================================================
Status Code Description
=========== =================================================
204         Master/standby switchover performed successfully.
400         Invalid request.
401         Invalid authentication information.
403         The request is rejected.
404         The requested resource is not found.
500         Internal service error.
=========== =================================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
