:original_name: ListConfigHistories.html

.. _ListConfigHistories:

Querying the List of Instance Parameter Modification Records
============================================================

Function
--------

This API is used to query the parameter modification record list of an instance by keyword.

URI
---

GET /v2/{project_id}/instances/{instance_id}/config-histories

.. table:: **Table 1** Path Parameters

   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type   | Description                                                                   |
   +=============+===========+========+===============================================================================+
   | project_id  | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+
   | instance_id | Yes       | String | Instance ID.                                                                  |
   +-------------+-----------+--------+-------------------------------------------------------------------------------+

.. table:: **Table 2** Query Parameters

   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                                                                                                                                                    |
   +===========+===========+=========+================================================================================================================================================================================================+
   | offset    | No        | Integer | Offset, which is the position where the query starts. The value must be no less than 0.                                                                                                        |
   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit     | No        | Integer | Number of records displayed on each page. The minimum value is **1**. The maximum value is **1000**\ \*. If this parameter is not specified, 10 records are displayed on each page by default. |
   +-----------+-----------+---------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-------------+---------------------------------------------------------------------------------+-----------------------------------------------------+
   | Parameter   | Type                                                                            | Description                                         |
   +=============+=================================================================================+=====================================================+
   | history_num | Integer                                                                         | Number of instance parameter modification records.  |
   +-------------+---------------------------------------------------------------------------------+-----------------------------------------------------+
   | histories   | Array of :ref:`HistoryInfo <listconfighistories__response_historyinfo>` objects | Details of instance parameter modification records. |
   +-------------+---------------------------------------------------------------------------------+-----------------------------------------------------+

.. _listconfighistories__response_historyinfo:

.. table:: **Table 4** HistoryInfo

   ========== ====== =======================
   Parameter  Type   Description
   ========== ====== =======================
   history_id String Modification record ID.
   type       String Modification type.
   created_at String Modification time.
   status     String Modification status.
   ========== ====== =======================

**Status code: 400**

.. table:: **Table 5** Response body parameters

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

.. table:: **Table 6** Response body parameters

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

   GET https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/config-histories?offset=0&limit=10

Example Responses
-----------------

**Status code: 200**

List of instance parameter modification records queried successfully.

.. code-block::

   {
     "history_num" : 1,
     "histories" : [ {
       "history_id" : "4ae8507f-7992-40e2-9928-41ccf1db4bdc",
       "type" : "config_param",
       "created_at" : "2022-10-20T03:37:44.636Z",
       "status" : "SUCCESS"
     } ]
   }

Status Codes
------------

+-------------+-----------------------------------------------------------------------+
| Status Code | Description                                                           |
+=============+=======================================================================+
| 200         | List of instance parameter modification records queried successfully. |
+-------------+-----------------------------------------------------------------------+
| 400         | Invalid request.                                                      |
+-------------+-----------------------------------------------------------------------+
| 500         | Internal service error.                                               |
+-------------+-----------------------------------------------------------------------+

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
