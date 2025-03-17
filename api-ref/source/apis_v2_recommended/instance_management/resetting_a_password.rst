:original_name: ResetPassword.html

.. _ResetPassword:

Resetting a Password
====================

Function
--------

This API is used to reset the password of a DCS instance.

URI
---

POST /v2/{project_id}/instances/{instance_id}/password/reset

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

   +--------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                                                                                  |
   +====================+=================+=================+==============================================================================================================================+
   | new_password       | No              | String          | New password. When **no_password_access** is set to false or not specified, the request must contain the password parameter. |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 | The password of a DCS Redis instance must meet the following complexity requirements:                                        |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 | -  Can contain 8 to 32 characters.                                                                                           |
   |                    |                 |                 | -  Must contain at least three of the following character types:                                                             |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 |    -  Lowercase letters                                                                                                      |
   |                    |                 |                 |    -  Uppercase letters                                                                                                      |
   |                    |                 |                 |    -  Digits                                                                                                                 |
   |                    |                 |                 |    -  Special characters :literal:`\`~!@#$^&*()-_=+\\|{},<.>/?`                                                              |
   +--------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | no_password_access | No              | Boolean         | Whether to change the DCS instance to password-free.                                                                         |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 | -  **true**: The instance can be accessed without a password.                                                                |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 | -  **false**: The instance can be accessed only after password authentication.                                               |
   |                    |                 |                 |                                                                                                                              |
   |                    |                 |                 |    If this parameter is not set, the default value **false** is used.                                                        |
   +--------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                            |
   +=======================+=======================+========================================================================================================================================================================+
   | retry_times_left      | String                | Number of remaining password attempts. Resetting a password does not verify passwords. This parameter is deprecated and **5** is returned by default.                  |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | lock_time             | String                | Lock duration, in minutes. Resetting a password does not involve locks. This parameter is deprecated and **0** is returned by default.                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | lock_time_left        | String                | Remaining time before the account is unlocked, in minutes. Resetting a password does not involve locks. This parameter is deprecated and **0** is returned by default. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | code                  | String                | Code of a password reset result.                                                                                                                                       |
   |                       |                       |                                                                                                                                                                        |
   |                       |                       | **1**: Successful                                                                                                                                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | message               | String                | Password reset result.                                                                                                                                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ext_message           | String                | Password reset error message. The value is **null** when the reset is successful.                                                                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

**Status code: 500**

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

Example Requests
----------------

Resetting the password of the DCS instance by entering a new password

.. code-block:: text

   POST https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}/password/reset

   {
     "new_password" : "xxxxxx",
     "no_password_access" : false
   }

Example Responses
-----------------

**Status code: 200**

The password is changed successfully.

.. code-block::

   {
     "lock_time" : "0",
     "lock_time_left" : "0",
     "retry_times_left" : "5"
     "code" : "1",
     "message" : "success",
     "ext_message" : null
   }

**Status code: 400**

Invalid request.

.. code-block::

   {
     "error_code" : "DCS.4839",
     "error_msg" : "is not support reset instance password."
   }

Status Codes
------------

=========== =====================================
Status Code Description
=========== =====================================
200         The password is changed successfully.
400         Invalid request.
500         Internal service error.
=========== =====================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
