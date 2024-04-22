:original_name: BatchCreateOrDeleteTags.html

.. _BatchCreateOrDeleteTags:

Batch Adding or Deleting Tags
=============================

Function
--------

This API is used to add or delete tags in batches for a DCS instance.

URI
---

POST /v2/{project_id}/dcs/{instance_id}/tags/action

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

.. table:: **Table 2** Request body parameters

   +-----------+-----------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                               | Description                                                           |
   +===========+===========+====================================================================================+=======================================================================+
   | action    | Yes       | String                                                                             | Operation to be performed. The value can be **create** or **delete**. |
   +-----------+-----------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | tags      | Yes       | Array of :ref:`ResourceTag <batchcreateordeletetags__request_resourcetag>` objects | Tag list.                                                             |
   +-----------+-----------+------------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. _batchcreateordeletetags__request_resourcetag:

.. table:: **Table 3** ResourceTag

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                               |
   +=================+=================+=================+===========================================================================================================================+
   | key             | Yes             | String          | Tag key.                                                                                                                  |
   |                 |                 |                 |                                                                                                                           |
   |                 |                 |                 | -  Must be unique for each resource.                                                                                      |
   |                 |                 |                 |                                                                                                                           |
   |                 |                 |                 | -  Contains up to 128 characters.                                                                                         |
   |                 |                 |                 |                                                                                                                           |
   |                 |                 |                 | -  Must be unique and cannot be empty.                                                                                    |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------+
   | value           | No              | String          | Tag value.                                                                                                                |
   |                 |                 |                 |                                                                                                                           |
   |                 |                 |                 | -  This parameter is mandatory when **action** is set to **create** and is optional when **action** is set to **delete**. |
   |                 |                 |                 |                                                                                                                           |
   |                 |                 |                 | -  It can contain a maximum of 255 characters.                                                                            |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

None

Example Requests
----------------

-  Adding tags to a specified resource in batches

   .. code-block:: text

      POST https://{dcs_endpoint}/v2/7dddae81f0e34f62adb9618bc8c8b1fe/dcs/01928d55-7020-4500-9c29-774caabe4bc4/tags/action

      {
        "action" : "create",
        "tags" : [ {
          "value" : "2",
          "key" : "dcs001"
        }, {
          "value" : "4",
          "key" : "dcs003"
        } ]
      }

-  Deleting tags from a specified instance in batches

   .. code-block:: text

      POST https://{dcs_endpoint}/v2/7dddae81f0e34f62adb9618bc8c8b1fe/dcs/01928d55-7020-4500-9c29-774caabe4bc4/tags/action

      {
        "action" : "delete",
        "tags" : [ {
          "key" : "key1",
          "value" : "11"
        } ]
      }

Example Responses
-----------------

None

Status Codes
------------

=========== ===================================
Status Code Description
=========== ===================================
204         Tags added or deleted successfully.
=========== ===================================

Error Codes
-----------

See :ref:`Error Codes <errorcode>`.
