:original_name: dcs-api-0312010.html

.. _dcs-api-0312010:

Scaling Up a DCS Instance
=========================

Function
--------

This API is used to scale up a DCS Redis instance in the **Running** state.

URI
---

POST /v1.0/{project_id}/instances/{instance_id}/extend

:ref:`Table 1 <dcs-api-0312010__en-us_topic_0166889656_table4154121820350>` describes the parameters.

.. _dcs-api-0312010__en-us_topic_0166889656_table4154121820350:

.. table:: **Table 1** Parameter description

   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Mandatory | Description                                                                                                                |
   +=============+========+===========+============================================================================================================================+
   | project_id  | String | Yes       | Project ID. For details on how to obtain the value of this parameter, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+
   | instance_id | String | Yes       | Instance ID.                                                                                                               |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312010__en-us_topic_0166889656_table166993107405>` describes the request parameters.

.. _dcs-api-0312010__en-us_topic_0166889656_table166993107405:

.. table:: **Table 2** Parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                                                                                                                                       |
   +=================+=================+=================+===================================================================================================================================================================================+
   | new_capacity    | Integer         | Yes             | New specification (memory space) of the DCS instance. The new specification to which the DCS instance will be scaled up must be greater than the current specification. Unit: GB. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | spec_code       | String          | Yes             | DCS instance specification code.                                                                                                                                                  |
   |                 |                 |                 |                                                                                                                                                                                   |
   |                 |                 |                 | This parameter is optional for DCS Redis 3.0 instances.                                                                                                                           |
   |                 |                 |                 |                                                                                                                                                                                   |
   |                 |                 |                 | This parameter is mandatory for DCS Redis 4.0 and later instances.                                                                                                                |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Example request**

-  Request URL:

   .. code-block:: text

      POST https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/extend

-  Example:

   .. code-block::

      {
          "spec_code":"redis.single.au1.large.4",
          "new_capacity":4,

      }

Response
--------

**Response parameters**

None

**Example response**

None

Status Code
-----------

:ref:`Table 3 <dcs-api-0312010__en-us_topic_0166889656_table8301101911215>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312010__en-us_topic_0166889656_table8301101911215:

.. table:: **Table 3** Status code

   =========== =====================================
   Status Code Description
   =========== =====================================
   204         Scale-up task submitted successfully.
   =========== =====================================
