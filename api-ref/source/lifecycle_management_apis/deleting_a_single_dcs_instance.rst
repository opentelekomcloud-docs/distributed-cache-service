:original_name: dcs-api-0312008.html

.. _dcs-api-0312008:

Deleting a Single DCS Instance
==============================

Function
--------

This API is used to delete a specified DCS instance to free up all resources occupied by the DCS instance.

URI
---

DELETE /v1.0/{project_id}/instances/{instance_id}

:ref:`Table 1 <dcs-api-0312008__table4154121820350>` describes the parameter.

.. _dcs-api-0312008__table4154121820350:

.. table:: **Table 1** Parameter description

   =========== ====== ========= ============
   Parameter   Type   Mandatory Description
   =========== ====== ========= ============
   project_id  String Yes       Project ID.
   instance_id String Yes       Instance ID.
   =========== ====== ========= ============

Request
-------

**Request parameters**

None

**Example request**

Request URL:

.. code-block:: text

   DELETE https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}

Response
--------

**Response parameters**

None

**Example response**

None

Status Code
-----------

:ref:`Table 2 <dcs-api-0312008__table8301101911215>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312008__table8301101911215:

.. table:: **Table 2** Status code

   =========== ===================================
   Status Code Description
   =========== ===================================
   204         DCS instances deleted successfully.
   =========== ===================================
