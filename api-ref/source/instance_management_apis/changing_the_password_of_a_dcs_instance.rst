:original_name: dcs-api-0312019.html

.. _dcs-api-0312019:

Changing the Password of a DCS Instance
=======================================

Function
--------

This API is used to change the password of a DCS instance.

URI
---

PUT /v1.0/{project_id}/instances/{instance_id}/password

:ref:`Table 1 <dcs-api-0312019__table1899262913382>` describes the parameters.

.. _dcs-api-0312019__table1899262913382:

.. table:: **Table 1** Parameter description

   =========== ====== ========= ================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ================
   project_id  String Yes       Project ID.
   instance_id String Yes       DCS instance ID.
   =========== ====== ========= ================

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312019__table153111335113816>` describes the request parameters.

.. _dcs-api-0312019__table153111335113816:

.. table:: **Table 2** Parameter description

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                        |
   +=================+=================+=================+====================================================================+
   | old_password    | String          | Yes             | Old password.                                                      |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+
   | new_password    | String          | Yes             | New password.                                                      |
   |                 |                 |                 |                                                                    |
   |                 |                 |                 | Password complexity requirements:                                  |
   |                 |                 |                 |                                                                    |
   |                 |                 |                 | -  Cannot be empty.                                                |
   |                 |                 |                 | -  Cannot be the username or the username spelled backwards.       |
   |                 |                 |                 | -  Can be 8 to 32 characters long.                                 |
   |                 |                 |                 | -  Contain at least three of the following character types:        |
   |                 |                 |                 |                                                                    |
   |                 |                 |                 |    -  Lowercase letters                                            |
   |                 |                 |                 |    -  Uppercase letters                                            |
   |                 |                 |                 |    -  Digits                                                       |
   |                 |                 |                 |    -  Special characters (:literal:`\`~!@#$^&*()-_=+\\|{}:,<.>/?`) |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+

**Example request**

-  Request URL:

   .. code-block:: text

      PUT https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/password

-  Example:

   .. code-block::

      {
          "old_password": "XXXXXX",
          "new_password": "XXXXXX"
      }

Response
--------

**Response parameters**

:ref:`Table 3 <dcs-api-0312019__table1861319576383>` describes the response parameters.

.. _dcs-api-0312019__table1861319576383:

.. table:: **Table 3** Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                       |
   +=======================+=======================+===================================================================================================================================+
   | result                | String                | An indicator of whether the password is successfully changed: Options:                                                            |
   |                       |                       |                                                                                                                                   |
   |                       |                       | -  **Success**: Password changed successfully.                                                                                    |
   |                       |                       | -  **passwordFailed**: The old password is incorrect.                                                                             |
   |                       |                       | -  **Locked**: This account has been locked.                                                                                      |
   |                       |                       | -  **Failed**: Failed to change the password.                                                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | message               | String                | Result of password change.                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | retry_times_left      | String                | Number of remaining password attempts. If the old password is incorrect, the value of this parameter is not **null**.             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | lock_time             | String                | Account lockout duration. If the old password is incorrect or the account is locked, the value of this parameter is not **null**. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | lock_time_left        | String                | Remaining time before the account is unlocked. If the account is locked, the value of this parameter is not **null**.             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------+

**Example response**

.. code-block::

   //Change password success.
   {
       "result" : "Success",
       "message" : "Modify DCSInstance password success.",
       "retry_times_left" : "5",
       "lock_time" : "0",
       "lock_time_left" : "0"
   }
   //Change password failed.
   {
       "result" : "passwordFailed",
       "message" : "verify password failed.",
       "retry_times_left" : "4",
       "lock_time" : "5",
       "lock_time_left" : "5"
   }

Status Code
-----------

:ref:`Table 4 <dcs-api-0312019__table486141410130>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312019__table486141410130:

.. table:: **Table 4** Status code

   =========== ==============================
   Status Code Description
   =========== ==============================
   200         Password changed successfully.
   =========== ==============================
