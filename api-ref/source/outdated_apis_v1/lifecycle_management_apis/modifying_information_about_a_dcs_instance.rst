:original_name: dcs-api-0312007.html

.. _dcs-api-0312007:

Modifying Information About a DCS Instance
==========================================

Function
--------

This API is used to modify the information about a DCS instance, including the instance name, description, backup policy, start and end time of the maintenance window, and security group.

URI
---

PUT /v1.0/{project_id}/instances/{instance_id}

:ref:`Table 1 <dcs-api-0312007__en-us_topic_0166889612_table938420556341>` describes the parameters.

.. _dcs-api-0312007__en-us_topic_0166889612_table938420556341:

.. table:: **Table 1** Parameter description

   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Type   | Mandatory | Description                                                                                                                |
   +=============+========+===========+============================================================================================================================+
   | project_id  | String | Yes       | Project ID. For details on how to obtain the value of this parameter, see :ref:`Obtaining a Project ID <dcs-api-0312045>`. |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+
   | instance_id | String | Yes       | DCS instance ID.                                                                                                           |
   +-------------+--------+-----------+----------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312007__en-us_topic_0166889612_table785213273513>` describes the request parameters.

.. _dcs-api-0312007__en-us_topic_0166889612_table785213273513:

.. table:: **Table 2** Parameter description

   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Type            | Mandatory       | Description                                                                                                                                                                                                                                                                              |
   +========================+=================+=================+==========================================================================================================================================================================================================================================================================================+
   | name                   | String          | No              | DCS instance name.                                                                                                                                                                                                                                                                       |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | An instance name can contain 4 to 64 characters, including letters, digits, underscores (_), and hyphens (-), and must start with a letter.                                                                                                                                              |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description            | String          | No              | Brief description of the DCS instance.                                                                                                                                                                                                                                                   |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | A brief description supports up to 1024 characters.                                                                                                                                                                                                                                      |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | .. note::                                                                                                                                                                                                                                                                                |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 |    "\\" is defined as an escape character in the queue description. If you need to enter a backward slash (\\) or a double quotation mark (") in the queue description, enter **\\\\** or **\\"**.                                                                                       |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instance_backup_policy | Object          | No              | Backup policy.                                                                                                                                                                                                                                                                           |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | This parameter is available for master/standby and cluster DCS instances. For details, see :ref:`Table 3 <dcs-api-0312004__en-us_topic_0166889598_table12803218151513>` and :ref:`Table 4 <dcs-api-0312004__en-us_topic_0166889598_table187492037201518>`.                               |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_begin         | String          | No              | Time at which the maintenance time window starts.                                                                                                                                                                                                                                        |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | Format: hh:mm:ss.                                                                                                                                                                                                                                                                        |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | -  The start time and end time of the maintenance time window must indicate the time segment of a supported maintenance time window. For details on how to query the time segments of supported maintenance time windows, see :ref:`Querying Maintenance Time Window <dcs-api-0312041>`. |
   |                        |                 |                 | -  The start time must be set to 22:00:00, 02:00:00, 06:00:00, 10:00:00, 14:00:00, or 18:00: 00.                                                                                                                                                                                         |
   |                        |                 |                 | -  Parameters **maintain_begin** and **maintain_end** must be set in pairs. If parameter **maintain_begin** is left blank, parameter **maintain_end** is also blank.                                                                                                                     |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | maintain_end           | String          | No              | Time at which the maintenance time window ends.                                                                                                                                                                                                                                          |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | Format: hh:mm:ss.                                                                                                                                                                                                                                                                        |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | -  The start time and end time of the maintenance time window must indicate the time segment of a supported maintenance time window. For details on how to query the time segments of supported maintenance time windows, see :ref:`Querying Maintenance Time Window <dcs-api-0312041>`. |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | -  The end time is four hours later than the start time. For example, if the start time is 22:00:00, the end time is 02:00:00.                                                                                                                                                           |
   |                        |                 |                 | -  Parameters **maintain_begin** and **maintain_end** must be set in pairs. If parameter **maintain_end** is left blank, parameter **maintain_start** is also blank.                                                                                                                     |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_group_id      | String          | No              | Security group ID.                                                                                                                                                                                                                                                                       |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The value can be obtained from the VPC console or the API.                                                                                                                                                                                                                               |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | This parameter is supported only by DCS Redis 3.0 instances.                                                                                                                                                                                                                             |
   +------------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Example request**

Request URL:

.. code-block:: text

   PUT https://{dcs_endpoint}/v1.0/{project_id}/instances/{instance_id}

-  Example 1

   .. code-block::

      {
          "description": "instance description"
      }

-  Example 2

   .. code-block::

      {
          "name": "dcs002",
          "description": "instance description",
          "instance_backup_policy": {
              "backup_type": "auto",
              "save_days": 1,
              "periodical_backup_plan": {
                  "begin_at": "00:00-01:00",
                  "period_type": "weekly",
                  "backup_at": [
                      "1",
                      "2",
                      "3",
                      "4",
                      "6",
                      "7"
                  ]
              }
          },
          "security_group_id": "18e9309f-f81a-4749-bb21-f74576292162",
          "maintain_begin": "02:00:00",
          "maintain_end": "06:00:00"
      }

Response
--------

**Response parameters**

None

**Example response**

None

Status Code
-----------

:ref:`Table 3 <dcs-api-0312007__en-us_topic_0166889612_table1475915181216>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312007__en-us_topic_0166889612_table1475915181216:

.. table:: **Table 3** Status code

   =========== ===================================
   Status Code Description
   =========== ===================================
   204         DCS instance modified successfully.
   =========== ===================================
