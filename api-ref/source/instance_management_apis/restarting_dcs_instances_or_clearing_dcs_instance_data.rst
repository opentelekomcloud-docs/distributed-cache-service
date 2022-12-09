:original_name: dcs-api-0312018.html

.. _dcs-api-0312018:

Restarting DCS Instances or Clearing DCS Instance Data
======================================================

Function
--------

This API is used to restart a running DCS instance.

Data clearance operations cannot be undone on DCS Redis 4.0 and 5.0 instances.

URI
---

PUT /v1.0/{project_id}/instances/status

:ref:`Table 1 <dcs-api-0312018__table344154216371>` describes the parameter.

.. _dcs-api-0312018__table344154216371:

.. table:: **Table 1** Parameter description

   ========== ====== ========= ===========
   Parameter  Type   Mandatory Description
   ========== ====== ========= ===========
   project_id String Yes       Project ID.
   ========== ====== ========= ===========

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312018__table103786452372>` describes the request parameters.

.. _dcs-api-0312018__table103786452372:

.. table:: **Table 2** Parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                             |
   +=================+=================+=================+=========================================================================+
   | action          | String          | Yes             | Action performed on DCS instances. Options: **restart**, and **flush**. |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 | .. note::                                                               |
   |                 |                 |                 |                                                                         |
   |                 |                 |                 |    Only DCS Redis 4.0 and 5.0 instances can be flushed.                 |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+
   | instances       | Array           | Yes             | List of DCS instance IDs.                                               |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------+

**Example request**

-  Request URL:

   .. code-block:: text

      PUT https://{dcs_endpoint}/v1.0/{project_id}/instances/status

-  Example:

   .. code-block::

      {
          "action": "restart",
          "instances": [
              "2e803f66-fbb0-47ad-b6cb-fb87f5bed4ef"
          ]
      }

Response
--------

**Response parameters**

:ref:`Table 3 <dcs-api-0312018__table52851943388>` describes the response parameter.

.. _dcs-api-0312018__table52851943388:

.. table:: **Table 3** Parameter description

   ========= ===== ==============================================
   Parameter Type  Description
   ========= ===== ==============================================
   results   Array Indicates the result of instance modification.
   ========= ===== ==============================================

.. table:: **Table 4** results parameter description

   +-----------+--------+------------------------------------------------------------------+
   | Parameter | Type   | Description                                                      |
   +===========+========+==================================================================+
   | instance  | String | DCS instance ID.                                                 |
   +-----------+--------+------------------------------------------------------------------+
   | result    | String | Instance modification result. Options: **success** or **failed** |
   +-----------+--------+------------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "results": [
           {
               "result": "success",
               "instance": "2e803f66-fbb0-47ad-b6cb-fb87f5bed4ef"
           }
       ]
   }

Status Code
-----------

:ref:`Table 5 <dcs-api-0312018__table1357115714126>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312018__table1357115714126:

.. table:: **Table 5** Status code

   +-------------+-------------------------------------------------------------------+
   | Status Code | Description                                                       |
   +=============+===================================================================+
   | 200         | Successfully restarted DCS instance or cleared DCS instance data. |
   +-------------+-------------------------------------------------------------------+
