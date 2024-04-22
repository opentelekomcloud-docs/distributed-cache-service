:original_name: UpdateSSLSwitch.html

.. _UpdateSSLSwitch:

Enabling or Disabling SSL
=========================

Function
--------

This API is used to enable or disable SSL. This API is only supported by DCS Redis 6.0 instances.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/ssl

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

   +-----------------+-----------------+-----------------+----------------------------+
   | Parameter       | Mandatory       | Type            | Description                |
   +=================+=================+=================+============================+
   | enabled         | Yes             | Boolean         | Enabling or disabling SSL. |
   |                 |                 |                 |                            |
   |                 |                 |                 | Enumeration values:        |
   |                 |                 |                 |                            |
   |                 |                 |                 | -  **true**                |
   |                 |                 |                 |                            |
   |                 |                 |                 | -  **false**               |
   +-----------------+-----------------+-----------------+----------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   =========== ====== =================
   Parameter   Type   Description
   =========== ====== =================
   job_id      String DCS task ID.
   instance_id String Instance ID.
   result      String Execution result.
   =========== ====== =================

**Status code: 400**

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

**Status code: 500**

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

Example Requests
----------------

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/ssl

   {
     "enabled" : true
   }

Example Responses
-----------------

**Status code: 200**

SSL enabled or disabled.

.. code-block::

   {
     "job_id" : "ff8080817fe01bb2017fe3cf68860481",
     "instance_id" : "5560df16-cebf-4473-95c4-d1b573c16e79",
     "result" : "success"
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

=========== ========================
Status Code Description
=========== ========================
200         SSL enabled or disabled.
400         Invalid request.
500         Internal service error.
=========== ========================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
