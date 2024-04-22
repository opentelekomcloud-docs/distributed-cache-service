:original_name: dcs-api-0312009.html

.. _dcs-api-0312009:

Batch Deleting DCS Instances
============================

Function
--------

This API is used to delete multiple DCS instances at a time.

URI
---

DELETE /v1.0/{project_id}/instances?allFailure={allFailure}

:ref:`Table 1 <dcs-api-0312009__en-us_topic_0166889613_table4154121820350>` describes the parameters.

.. _dcs-api-0312009__en-us_topic_0166889613_table4154121820350:

.. table:: **Table 1** Parameter description

   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                                                                                            |
   +=================+=================+=================+========================================================================================================================================+
   | project_id      | String          | Yes             | Project ID. For details on how to obtain the value of this parameter, see :ref:`Obtaining a Project ID <dcs-api-0312045>`.             |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------+
   | allFailure      | String          | No              | An indicator of whether all DCS instances failed to be created will be deleted. Options:                                               |
   |                 |                 |                 |                                                                                                                                        |
   |                 |                 |                 | Options:                                                                                                                               |
   |                 |                 |                 |                                                                                                                                        |
   |                 |                 |                 | -  **true**: all instances that fail to be created are deleted. In this case, the **instances** parameter in the request can be empty. |
   |                 |                 |                 | -  **false** or other values: The DCS instances specified by the instances parameter in the API request will be deleted.               |
   +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

:ref:`Table 2 <dcs-api-0312009__en-us_topic_0166889613_table166993107405>` describes the request parameters.

.. _dcs-api-0312009__en-us_topic_0166889613_table166993107405:

.. table:: **Table 2** Parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type            | Mandatory       | Description                                                                                                   |
   +=================+=================+=================+===============================================================================================================+
   | instances       | Array           | No              | IDs of DCS instances to be deleted.                                                                           |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | This parameter is set only when the **allFailure** parameter in the URI is set to **false** or another value. |
   |                 |                 |                 |                                                                                                               |
   |                 |                 |                 | A maximum of 50 instances can be deleted at a time.                                                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

**Request URL:**

.. code-block:: text

   DELETE https://{dcs_endpoint}/v1.0/{project_id}/instances?allFailure={allFailure}

Example request with **allFailure** set to **false**:

.. code-block::

   {
       "instances": [
           "54602a9d-5e22-4239-9123-77e350df4a34",
           "7166cdea-dbad-4d79-9610-7163e6f8b640"
       ]
   }

Response
--------

**Response parameters**

If the value of the **allFailure** parameter in the URI is **false**, an empty response is then returned. If the value of the **allFailure** parameter in the URI is **true**, a response containing the parameter in :ref:`Table 3 <dcs-api-0312009__en-us_topic_0166889613_table18935105020414>` is returned.

.. _dcs-api-0312009__en-us_topic_0166889613_table18935105020414:

.. table:: **Table 3** Parameter description

   +-----------+-------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type  | Description                                                                                                                    |
   +===========+=======+================================================================================================================================+
   | results   | Array | For details about how to delete an instance, see :ref:`Table 4 <dcs-api-0312009__en-us_topic_0166889613_table69371750154117>`. |
   +-----------+-------+--------------------------------------------------------------------------------------------------------------------------------+

.. _dcs-api-0312009__en-us_topic_0166889613_table69371750154117:

.. table:: **Table 4** results parameter description

   +-----------+--------+---------------------------------------------------------------+
   | Parameter | Type   | Description                                                   |
   +===========+========+===============================================================+
   | instance  | String | DCS instance ID.                                              |
   +-----------+--------+---------------------------------------------------------------+
   | result    | String | Instance deletion result. Options: **success** and **failed** |
   +-----------+--------+---------------------------------------------------------------+

**Example response**

.. code-block::

   {
       "results": [
           {
               "instance": "54602a9d-5e22-4239-9123-77e350df4a34",
               "result": "success"
           },
           {
               "instance": "7166cdea-dbad-4d79-9610-7163e6f8b640",
               "result": "success"
           }
       ]
   }

Status Code
-----------

:ref:`Table 5 <dcs-api-0312009__en-us_topic_0166889613_table8301101911215>` describes the status code of successful operations. For details about other status codes, see :ref:`Table 1 <dcs-api-0312043__table5210141351517>`.

.. _dcs-api-0312009__en-us_topic_0166889613_table8301101911215:

.. table:: **Table 5** Status codes

   +-------------+-------------------------------------------------------------------+
   | Status Code | Description                                                       |
   +=============+===================================================================+
   | 200         | DCS instances deleted successfully.                               |
   +-------------+-------------------------------------------------------------------+
   | 204         | DCS instances that failed to be created are cleared successfully. |
   +-------------+-------------------------------------------------------------------+
