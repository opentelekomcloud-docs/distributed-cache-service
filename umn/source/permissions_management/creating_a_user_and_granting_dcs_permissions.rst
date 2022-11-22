:original_name: dcs-ug-210626004.html

.. _dcs-ug-210626004:

Creating a User and Granting DCS Permissions
============================================

This chapter describes how to use IAM to implement fine-grained permissions control for your DCS resources. With IAM, you can:

-  Create IAM users for employees based on your enterprise's organizational structure. Each IAM user will have their own security credentials for accessing DCS resources.
-  Grant only the permissions required for users to perform a specific task.
-  Entrust an account or cloud service to perform efficient O&M on your DCS resources.

If your account does not need individual IAM users, you may skip over this chapter.

This section describes the procedure for granting the **DCS ReadOnlyAccess** permission (see :ref:`Figure 1 <dcs-ug-210626004__fig17581732820>`) as an example.

Prerequisites
-------------

You are familiar with the permissions (see :ref:`Permissions Management <dcs-pd-210626001>`) supported by DCS and choose policies or roles according to your requirements. For the permissions of other services, see Permissions Policies.

Process Flow
------------

.. _dcs-ug-210626004__fig17581732820:

.. figure:: /_static/images/en-us_image_0000001196623620.png
   :alt: **Figure 1** Process of granting DCS permissions

   **Figure 1** Process of granting DCS permissions

#. .. _dcs-ug-210626004__en-us_topic_0170877287_en-us_topic_0170877287_li10176121316284:

   Create a user group and grant permissions.

   Create a user group on the IAM console, and attach the **DCS ReadOnlyAccess** policy to the group.

#. Create an IAM user.

   Create a user on the IAM console and add the user to the group created in :ref:`1 <dcs-ug-210626004__en-us_topic_0170877287_en-us_topic_0170877287_li10176121316284>`.

#. Log in and verify permissions.

   Log in to the DCS console by using the newly created user, and verify that the user only has read permissions for DCS.
