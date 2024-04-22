:original_name: UpdatePassword.html

.. _UpdatePassword:

Changing the Password
=====================

Function
--------

This API is used to change the password of a DCS instance.

URI
---

PUT /v2/{project_id}/instances/{instance_id}/password

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

.. table:: **Table 2** Request body parameters

   ============ ========= ====== =============
   Parameter    Mandatory Type   Description
   ============ ========= ====== =============
   old_password Yes       String Old password.
   new_password Yes       String New password.
   ============ ========= ====== =============

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                            |
   +=======================+=======================+========================================================================================================================+
   | lock_time             | String                | Lock duration. If the authentication fails and the account is locked, a response is returned and is not **null**.      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+
   | result                | String                | Password change result:                                                                                                |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **success**: Password is changed successfully.                                                                      |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **passwordFailed**: Password authentication failed.                                                                 |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **locked**: The account has been locked.                                                                            |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **failed**: Password change failed.                                                                                 |
   |                       |                       |                                                                                                                        |
   |                       |                       | Enumeration values:                                                                                                    |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **success**                                                                                                         |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **passwordFailed**                                                                                                  |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **locked**                                                                                                          |
   |                       |                       |                                                                                                                        |
   |                       |                       | -  **failed**                                                                                                          |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+
   | lock_time_left        | String                | Remaining time before the account is unlocked. When the account is locked, a response is returned and is not **null**. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+
   | retry_times_left      | String                | Number of remaining password attempts. If the authentication fails, a response is returned and is not **null**.        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+
   | message               | String                | Modification result description.                                                                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------+

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

Changing the password of the DCS instance by entering the old and new passwords

.. code-block:: text

   PUT https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/password

   {
     "old_password" : "XXXXXX",
     "new_password" : "XXXXXX"
   }

Example Responses
-----------------

**Status code: 200**

Password is changed successfully.

.. code-block::

   {
     "lock_time" : "0",
     "result" : "success",
     "lock_time_left" : "0",
     "retry_times_left" : "5",
     "message" : "Modify DCSInstance password success."
   }

Status Codes
------------

=========== =================================
Status Code Description
=========== =================================
200         Password is changed successfully.
400         Invalid request.
500         Internal service error.
=========== =================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
