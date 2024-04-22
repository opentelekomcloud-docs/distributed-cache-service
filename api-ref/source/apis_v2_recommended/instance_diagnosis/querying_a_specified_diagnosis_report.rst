:original_name: ShowDiagnosisTaskDetails.html

.. _ShowDiagnosisTaskDetails:

Querying a Specified Diagnosis Report
=====================================

Function
--------

This API is used to query details about a diagnosis report based on the report ID.

URI
---

GET /v2/{project_id}/diagnosis/{report_id}

.. table:: **Table 1** Path Parameters

   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                   |
   +============+===========+========+===============================================================================+
   | project_id | Yes       | String | Project ID. For details, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +------------+-----------+--------+-------------------------------------------------------------------------------+
   | report_id  | Yes       | String | Diagnosis report ID.                                                          |
   +------------+-----------+--------+-------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameters

   +----------------------------+------------------------------------------------------------------------------------------------------+-------------------------------------------+
   | Parameter                  | Type                                                                                                 | Description                               |
   +============================+======================================================================================================+===========================================+
   | abnormal_item_sum          | Integer                                                                                              | Total number of abnormal diagnosis items. |
   +----------------------------+------------------------------------------------------------------------------------------------------+-------------------------------------------+
   | failed_item_sum            | Integer                                                                                              | Total number of failed diagnosis items.   |
   +----------------------------+------------------------------------------------------------------------------------------------------+-------------------------------------------+
   | diagnosis_node_report_list | Array of :ref:`DiagnosisNodeReport <showdiagnosistaskdetails__response_diagnosisnodereport>` objects | Node diagnosis report list.               |
   +----------------------------+------------------------------------------------------------------------------------------------------+-------------------------------------------+

.. _showdiagnosistaskdetails__response_diagnosisnodereport:

.. table:: **Table 3** DiagnosisNodeReport

   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | Parameter                | Type                                                                                               | Description                                       |
   +==========================+====================================================================================================+===================================================+
   | node_ip                  | String                                                                                             | Node IP address, for example, 192.168.0.234:6379. |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | az_code                  | String                                                                                             | Code of the AZ where the node is.                 |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | group_name               | String                                                                                             | Name of the shard where the node is.              |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | abnormal_sum             | Integer                                                                                            | Total number of abnormal diagnosis items.         |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | failed_sum               | Integer                                                                                            | Total number of failed diagnosis items.           |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | role                     | String                                                                                             | Node role.                                        |
   |                          |                                                                                                    |                                                   |
   |                          |                                                                                                    | Enumeration values:                               |
   |                          |                                                                                                    |                                                   |
   |                          |                                                                                                    | -  **master**                                     |
   |                          |                                                                                                    |                                                   |
   |                          |                                                                                                    | -  **slave**                                      |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | diagnosis_dimension_list | Array of :ref:`DiagnosisDimension <showdiagnosistaskdetails__response_diagnosisdimension>` objects | Diagnosis dimension list.                         |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | command_time_taken_list  | :ref:`CommandTimeTakenList <showdiagnosistaskdetails__response_commandtimetakenlist>` object       | Command execution duration list.                  |
   +--------------------------+----------------------------------------------------------------------------------------------------+---------------------------------------------------+

.. _showdiagnosistaskdetails__response_diagnosisdimension:

.. table:: **Table 4** DiagnosisDimension

   +-----------------------+------------------------------------------------------------------------------------------+-------------------------------------------+
   | Parameter             | Type                                                                                     | Description                               |
   +=======================+==========================================================================================+===========================================+
   | name                  | String                                                                                   | Diagnosis dimension name.                 |
   |                       |                                                                                          |                                           |
   |                       |                                                                                          | Enumeration values:                       |
   |                       |                                                                                          |                                           |
   |                       |                                                                                          | -  **network**                            |
   |                       |                                                                                          |                                           |
   |                       |                                                                                          | -  **storage**                            |
   |                       |                                                                                          |                                           |
   |                       |                                                                                          | -  **load**                               |
   +-----------------------+------------------------------------------------------------------------------------------+-------------------------------------------+
   | abnormal_num          | Integer                                                                                  | Total number of abnormal diagnosis items. |
   +-----------------------+------------------------------------------------------------------------------------------+-------------------------------------------+
   | failed_num            | Integer                                                                                  | Total number of failed diagnosis items.   |
   +-----------------------+------------------------------------------------------------------------------------------+-------------------------------------------+
   | diagnosis_item_list   | Array of :ref:`DiagnosisItem <showdiagnosistaskdetails__response_diagnosisitem>` objects | Diagnosis items.                          |
   +-----------------------+------------------------------------------------------------------------------------------+-------------------------------------------+

.. _showdiagnosistaskdetails__response_diagnosisitem:

.. table:: **Table 5** DiagnosisItem

   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                                       | Description                                                                                      |
   +=======================+============================================================================================+==================================================================================================+
   | name                  | String                                                                                     | Diagnosis item name.                                                                             |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | Enumeration values:                                                                              |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **connection_num**                                                                            |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **rx_controlled**                                                                             |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **persistence**                                                                               |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **centralized_expiration**                                                                    |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **inner_memory_fragmentation**                                                                |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **time_consuming_commands**                                                                   |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **hit_ratio**                                                                                 |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **memory_usage**                                                                              |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **cpu_usage**                                                                                 |
   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
   | cause_ids             | Array of :ref:`ConclusionItem <showdiagnosistaskdetails__response_conclusionitem>` objects | List of cause IDs. For details about the IDs, see "Instance Diagnosis IDs" in the appendix.      |
   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
   | impact_ids            | Array of :ref:`ConclusionItem <showdiagnosistaskdetails__response_conclusionitem>` objects | List of impact IDs. For details about the IDs, see "Instance Diagnosis IDs" in the appendix.     |
   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
   | advice_ids            | Array of :ref:`ConclusionItem <showdiagnosistaskdetails__response_conclusionitem>` objects | List of suggestion IDs. For details about the IDs, see "Instance Diagnosis IDs" in the appendix. |
   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+
   | result                | String                                                                                     | Diagnosis result.                                                                                |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | Enumeration values:                                                                              |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **failed**                                                                                    |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **abnormal**                                                                                  |
   |                       |                                                                                            |                                                                                                  |
   |                       |                                                                                            | -  **normal**                                                                                    |
   +-----------------------+--------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------+

.. _showdiagnosistaskdetails__response_conclusionitem:

.. table:: **Table 6** ConclusionItem

   ========= ================== ======================
   Parameter Type               Description
   ========= ================== ======================
   id        Integer            Conclusion ID.
   params    Map<String,String> Conclusion parameters.
   ========= ================== ======================

.. _showdiagnosistaskdetails__response_commandtimetakenlist:

.. table:: **Table 7** CommandTimeTakenList

   +-----------------------+------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | Parameter             | Type                                                                                           | Description                                       |
   +=======================+================================================================================================+===================================================+
   | total_num             | Integer                                                                                        | Total number of times that commands are executed. |
   +-----------------------+------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | total_usec_sum        | Double                                                                                         | Total duration of command execution.              |
   +-----------------------+------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | result                | String                                                                                         | Command execution latency result.                 |
   |                       |                                                                                                |                                                   |
   |                       |                                                                                                | Enumeration values:                               |
   |                       |                                                                                                |                                                   |
   |                       |                                                                                                | -  **succeed**                                    |
   |                       |                                                                                                |                                                   |
   |                       |                                                                                                | -  **failed**                                     |
   +-----------------------+------------------------------------------------------------------------------------------------+---------------------------------------------------+
   | command_list          | Array of :ref:`CommandTimeTaken <showdiagnosistaskdetails__response_commandtimetaken>` objects | Command execution latency statistics.             |
   +-----------------------+------------------------------------------------------------------------------------------------+---------------------------------------------------+

.. _showdiagnosistaskdetails__response_commandtimetaken:

.. table:: **Table 8** CommandTimeTaken

   ============ ======= ==========================
   Parameter    Type    Description
   ============ ======= ==========================
   calls_sum    Integer Number of calls.
   usec_sum     Double  Total time consumed.
   command_name String  Command name.
   per_usec     String  Duration percentage.
   average_usec Double  Average duration of calls.
   ============ ======= ==========================

**Status code: 400**

.. table:: **Table 9** Response body parameters

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

.. table:: **Table 10** Response body parameters

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

None

Example Responses
-----------------

**Status code: 200**

The specified report is queried successfully.

.. code-block::

   {
     "abnormal_item_sum" : 1,
     "failed_item_sum" : 0,
     "diagnosis_node_report_list" : [ {
       "group_name" : "group-0",
       "az_code" : "region01",
       "node_ip" : "192.168.0.170:6379",
       "abnormal_sum" : 1,
       "failed_sum" : 0,
       "role" : "master",
       "command_time_taken_list" : {
         "command_list" : [ {
           "calls_sum" : 329,
           "usec_sum" : 20.732,
           "command_name" : "info",
           "per_usec" : "68.61%",
           "average_usec" : 0.063
         }, {
           "calls_sum" : 1788,
           "usec_sum" : 1.787,
           "command_name" : "ping",
           "per_usec" : "5.91%",
           "average_usec" : 0.001
         }, {
           "calls_sum" : 2,
           "usec_sum" : 0.025,
           "command_name" : "config",
           "per_usec" : "0.08%",
           "average_usec" : 0.013
         }, {
           "calls_sum" : 60,
           "usec_sum" : 0.186,
           "command_name" : "slowlog",
           "per_usec" : "0.62%",
           "average_usec" : 0.003
         }, {
           "calls_sum" : 1764,
           "usec_sum" : 7.485,
           "command_name" : "publish",
           "per_usec" : "24.77%",
           "average_usec" : 0.004
         } ],
         "result" : "succeed",
         "error_code" : null,
         "total_num" : 5,
         "total_usec_sum" : 30.215
       },
       "diagnosis_dimension_list" : [ {
         "name" : "load",
         "abnormal_num" : 0,
         "failed_num" : 0,
         "diagnosis_item_list" : [ {
           "name" : "cpu_usage",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         }, {
           "name" : "time_consuming_commands",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         } ]
       }, {
         "name" : "storage",
         "abnormal_num" : 1,
         "failed_num" : 0,
         "diagnosis_item_list" : [ {
           "name" : "inner_memory_fragmentation",
           "result" : "normal",
           "cause_ids" : [ {
             "id" : 7,
             "params" : null
           } ],
           "impact_ids" : [ {
             "id" : 3,
             "params" : null
           } ],
           "advice_ids" : [ {
             "id" : 4,
             "params" : null
           } ],
           "error_code" : null
         }, {
           "name" : "persistence",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         }, {
           "name" : "centralized_expiration",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         }, {
           "name" : "memory_usage",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         }, {
           "name" : "hit_ratio",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         } ]
       }, {
         "name" : "network",
         "abnormal_num" : 0,
         "failed_num" : 0,
         "diagnosis_item_list" : [ {
           "name" : "connection_num",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         }, {
           "name" : "rx_controlled",
           "result" : "normal",
           "cause_ids" : null,
           "impact_ids" : null,
           "advice_ids" : null,
           "error_code" : null
         } ]
       } ]
     } ]
   }

Status Codes
------------

=========== =============================================
Status Code Description
=========== =============================================
200         The specified report is queried successfully.
400         Invalid request.
500         Internal service error.
=========== =============================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
