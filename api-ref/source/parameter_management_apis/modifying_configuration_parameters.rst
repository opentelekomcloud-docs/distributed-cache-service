:original_name: dcs-api-0312017.html

.. _dcs-api-0312017:

Modifying Configuration Parameters
==================================

Function
--------

You can modify the configuration parameters of your DCS instance to optimize DCS performance based on your requirements.

URI
---

PUT /v1.0/{project_id}/instances/{instance_id}/configs

:ref:`Table 1 <dcs-api-0312017__table139152015133712>` describes the parameters.

.. _dcs-api-0312017__table139152015133712:

.. table:: **Table 1** Parameter description

   =========== ====== ========= ==================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ==================================
   project_id  String Yes       Project ID.
   instance_id String Yes       ID of the instance to be modified.
   =========== ====== ========= ==================================

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312017__table16620132063713>` describes the request parameters.

.. _dcs-api-0312017__table16620132063713:

.. table:: **Table 2** Parameter description

   +--------------+-------+-----------+---------------------------------------------------+
   | Parameter    | Type  | Mandatory | Description                                       |
   +==============+=======+===========+===================================================+
   | redis_config | Array | Yes       | Array of configuration items of the DCS instance. |
   +--------------+-------+-----------+---------------------------------------------------+

.. _dcs-api-0312017__table35215230340:

.. table:: **Table 3** redis_config parameter description

   =========== ====== ========= ================================
   Parameter   Type   Mandatory Description
   =========== ====== ========= ================================
   param_id    String Yes       Configuration item ID.
   param_name  String Yes       Configuration item name.
   param_value String Yes       Value of the configuration item.
   =========== ====== ========= ================================

For possible values of parameters in :ref:`Table 3 <dcs-api-0312017__table35215230340>`, see :ref:`Table 4 <dcs-api-0312015__table1439111281351>`.

**Example request**

-  Request URL:

   .. code-block:: text

      PUT https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}/configs

-  Example:

   .. code-block::

      {
          "redis_config": [
              {
                  "param_id": "1",
                  "param_name": "timeout",
                  "param_value": "100"
              }
          ]
      }

Response
--------

**Response parameters**

None

**Example response**

None

Status Code
-----------

:ref:`Table 4 <dcs-api-0312017__table17459195018122>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312017__table17459195018122:

.. table:: **Table 4** Status code

   =========== ==================================================
   Status Code Description
   =========== ==================================================
   204         DCS instance configurations modified successfully.
   =========== ==================================================
