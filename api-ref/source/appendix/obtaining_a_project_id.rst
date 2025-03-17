:original_name: dcs-api-0312045.html

.. _dcs-api-0312045:

Obtaining a Project ID
======================

Obtaining a Project ID by Calling an API
----------------------------------------

You can obtain a project ID by calling the API used to query project information based on the specified criteria.

The API used to obtain a project ID is **GET https://{Endpoint}/v3/projects**. {Endpoint} is the IAM endpoint and can be obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/regions-and-endpoints/index.html>`__.

The following is an example response. The value of **id** in the **projects** section is the project ID.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "project_name",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }

Obtaining a Project ID from the Console
---------------------------------------

A project ID is required for some URLs when an API is called.

To obtain a project ID, perform the following operations:

#. Sign up and log in to the management console.

#. Click the username in the upper right corner and choose **My Credentials** from the drop-down list.

#. On the **My Credentials** page, view project IDs in the project list.


   .. figure:: /_static/images/en-us_image_0216824199.jpg
      :alt: **Figure 1** Viewing project IDs

      **Figure 1** Viewing project IDs
