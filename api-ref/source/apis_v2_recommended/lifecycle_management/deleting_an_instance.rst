:original_name: DeleteSingleInstance.html

.. _DeleteSingleInstance:

Deleting an Instance
====================

Function
--------

This API is used to delete a specified DCS instance to free up all resources occupied by it.

.. note::

   To delete pay-per-use resources, perform operations in this section..

URI
---

DELETE /v2/{project_id}/instances/{instance_id}

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

None

Response Parameters
-------------------

None

Example Requests
----------------

Deleting a specified instance

.. code-block:: text

   DELETE https://{dcs_endpoint}/v2/{project_id}/instances/{instance_id}

Example Responses
-----------------

None

Status Codes
------------

=========== ==============================
Status Code Description
=========== ==============================
204         Instance deleted successfully.
400         Invalid request.
500         Internal service error.
=========== ==============================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
