:original_name: dcs-api-0312014.html

.. _dcs-api-0312014:

Querying Statistics of All Running Instances
============================================

Function
--------

This API is used to query the statistics of all DCS instances that are in the **Running** state.

URI
---

GET /v1.0/{project_id}/instances/statistic

:ref:`Table 1 <dcs-api-0312014__en-us_topic_0166889591_table8593726183514>` describes the parameter.

.. _dcs-api-0312014__en-us_topic_0166889591_table8593726183514:

.. table:: **Table 1** Parameter description

   +------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type   | Mandatory | Description                                                                                                                |
   +============+========+===========+============================================================================================================================+
   | project_id | String | Yes       | Project ID. For details on how to obtain the value of this parameter, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None

**Example request**

.. code-block:: text

   GET https://{dcs_endpoint}/v1.0/{project_id}/instances/statistic

Response
--------

**Response parameters**

:ref:`Table 2 <dcs-api-0312014__en-us_topic_0166889591_table254823012351>` describes the response parameter.

.. _dcs-api-0312014__en-us_topic_0166889591_table254823012351:

.. table:: **Table 2** Parameter description

   +------------+-------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Type  | Description                                                                                                                                      |
   +============+=======+==================================================================================================================================================+
   | statistics | Array | Statistics of all instances in the **Running** state. For details, see :ref:`Table 3 <dcs-api-0312014__en-us_topic_0166889591_table7914256164>`. |
   +------------+-------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0312014__en-us_topic_0166889591_table7914256164:

.. table:: **Table 3** statistics parameter description

   ============= ======= =============================================
   Parameter     Type    Description
   ============= ======= =============================================
   keys          Integer Number of cached data records
   instance_id   String  DCS instance ID
   used_memory   Integer Size of the used memory in MB
   max_memory    Integer Overall memory size in MB
   cmd_get_count Integer Number of times the GET command is run
   cmd_set_count Integer Number of times the SET command is run
   used_cpu      String  Percentage of CPU usage
   input_kbps    String  Incoming traffic (kbit/s) of the DCS instance
   output_kbps   String  Outgoing traffic (kbit/s) of the DCS instance
   ============= ======= =============================================

**Example response**

.. code-block::

   {
       "statistics" : [{
               "keys" : 0,
               "instance_id" : "e008652d-18e0-43ff-924e-072261e0372a",
               "used_memory" : 0,
               "max_memory" : 460,
               "cmd_get_count" : 0,
               "cmd_set_count" : 0,
               "used_cpu" : "0.0",
               "input_kbps" : "0.0",
               "output_kbps" : "0.0"
           }, {
               "keys" : 0,
               "instance_id" : "c577a1eb-33b7-42c7-8231-ad32358599ac",
               "used_memory" : 0,
               "max_memory" : 460,
               "cmd_get_count" : 0,
               "cmd_set_count" : 0,
               "used_cpu" : "0.0",
               "input_kbps" : "0.0",
               "output_kbps" : "0.0"
           }, {
               "keys" : 0,
               "instance_id" : "e8b98471-55d5-4695-b0bb-8f336a98e207",
               "used_memory" : 0,
               "max_memory" : 460,
               "cmd_get_count" : 0,
               "cmd_set_count" : 0,
               "used_cpu" : "0.0",
               "input_kbps" : "0.03",
               "output_kbps" : "1.19"
           }, {
               "keys" : 0,
               "instance_id" : "bc61c690-4b34-4cbe-9ce3-11246aea7aba",
               "used_memory" : 0,
               "max_memory" : 6963,
               "cmd_get_count" : 0,
               "cmd_set_count" : 0,
               "used_cpu" : "0.0",
               "input_kbps" : "0.0",
               "output_kbps" : "0.0"
           }
       ]
   }

Status Code
-----------

:ref:`Table 4 <dcs-api-0312014__en-us_topic_0166889591_table63992308123>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312014__en-us_topic_0166889591_table63992308123:

.. table:: **Table 4** Status code

   =========== =================================================
   Status Code Description
   =========== =================================================
   200         Statistics of all instances queried successfully.
   =========== =================================================
