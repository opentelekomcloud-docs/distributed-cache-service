:original_name: BatchDeleteInstances.html

.. _BatchDeleteInstances:

Batch Deleting DCS Instances
============================

Function
--------

This API is used to delete multiple DCS instances at a time.

URI
---

DELETE /v2/{project_id}/instances

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                            |
   +=================+=================+=================+========================================================================================================================================+
   | all_failure     | No              | Boolean         | Whether to delete all DCS instances that failed to be created. Values:                                                                 |
   |                 |                 |                 |                                                                                                                                        |
   |                 |                 |                 | -  **true**: all instances that fail to be created are deleted. In this case, the **instances** parameter in the request can be empty. |
   |                 |                 |                 |                                                                                                                                        |
   |                 |                 |                 | -  **false** or other values: The DCS instances specified by the **instances** parameter will be deleted.                              |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 3** Request body parameters

   +-----------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type             | Description                                                                                                    |
   +=================+=================+==================+================================================================================================================+
   | instances       | No              | Array of strings | List of instance IDs.                                                                                          |
   |                 |                 |                  |                                                                                                                |
   |                 |                 |                  | This parameter is set only when the **all_failure** parameter in the URI is set to **false** or another value. |
   +-----------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------+----------------------------------------------------------------------------------------+------------------------------------------------------------------+
   | Parameter | Type                                                                                   | Description                                                      |
   +===========+========================================================================================+==================================================================+
   | results   | Array of :ref:`BatchOpsResult <batchdeleteinstances__response_batchopsresult>` objects | Result of deleting, restarting, or clearing data of an instance. |
   +-----------+----------------------------------------------------------------------------------------+------------------------------------------------------------------+

.. _batchdeleteinstances__response_batchopsresult:

.. table:: **Table 5** BatchOpsResult

   +-----------+--------+----------------------------------------------------------------+
   | Parameter | Type   | Description                                                    |
   +===========+========+================================================================+
   | result    | String | Instance deletion result. Options: **success** and **failed**. |
   +-----------+--------+----------------------------------------------------------------+
   | instance  | String | DCS instance ID.                                               |
   +-----------+--------+----------------------------------------------------------------+

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

**Status code: 400**

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

Batch deleting DCS instances

.. code-block:: text

   DELETE https://{dcs_endpoint}/v2/{project_id}/instances?all_failure={all_failure}

   {
     "instances" : [ "54602a9d-5e22-4239-9123-77e350df4a34", "7166cdea-dbad-4d79-9610-7163e6f8b640" ]
   }

Example Responses
-----------------

**Status code: 200**

DCS instances deleted successfully.

.. code-block::

   {
     "results" : [ {
       "result" : "success",
       "instance" : "54602a9d-5e22-4239-9123-77e350df4a34"
     }, {
       "result" : "success",
       "instance" : "7166cdea-dbad-4d79-9610-7163e6f8b640"
     } ]
   }

Status Codes
------------

=========== ===================================
Status Code Description
=========== ===================================
200         DCS instances deleted successfully.
500         Internal service error.
400         Invalid request.
=========== ===================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
