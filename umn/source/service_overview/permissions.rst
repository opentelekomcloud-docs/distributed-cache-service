:original_name: dcs-pd-210626001.html

.. _dcs-pd-210626001:

Permissions
===========

If you need to assign different permissions to employees in your enterprise to access your DCS resources, Identity and Access Management (IAM) is a good choice for fine-grained permissions management. IAM provides identity authentication, permissions management, and access control, helping you secure access to your resources.

With IAM, you can use your account to create IAM users, and assign permissions to the users to control their access to specific resources. For example, some software developers in your enterprise need to use DCS resources but should not be allowed to delete DCS instances or perform any other high-risk operations. In this scenario, you can create IAM users for the software developers and grant them only the permissions required for using DCS resources.

If your account does not require individual IAM users for permissions management, skip this section.

DCS Permissions
---------------

By default, new IAM users do not have permissions assigned. You need to add a user to one or more groups, and attach permissions policies or roles to these groups. Users inherit permissions from the groups to which they are added and can perform specified operations on cloud services based on the permissions.

DCS is a project-level service deployed and accessed in specific physical regions. To assign DCS permissions to a user group, specify the scope as region-specific projects and select regions for the permissions to take effect. If **All projects** is selected, the permissions will take effect for the user group in all region-specific projects. When accessing DCS, the users need to switch to a region where they have been authorized to use this service.

You can grant users permissions by using roles and policies.

-  Roles: A type of coarse-grained authorization mechanism that defines permissions related to user responsibilities. This mechanism provides only a limited number of service-level roles for authorization. When using roles to grant permissions, you must also assign other roles on which the permissions depend to take effect. However, roles are not an ideal choice for fine-grained authorization and secure access control.
-  Policies: A type of fine-grained authorization mechanism that defines permissions required to perform operations on specific cloud resources under certain conditions. This mechanism allows for more flexible policy-based authorization, meeting requirements for secure access control. For example, you can grant DCS users only the permissions for operating DCS instances. Fine-grained policies are based on APIs. The minimum granularity of a policy is API actions. For the API actions supported by DCS, see section "Permissions Policies and Supported Actions" in the *Distributed Cache Service API Reference*.

:ref:`Table 1 <dcs-pd-210626001__en-us_topic_0170871404_table8486434381>` lists all the system permissions supported by DCS.

.. _dcs-pd-210626001__en-us_topic_0170871404_table8486434381:

.. table:: **Table 1** System-defined roles and policies supported by DCS

   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | Role/Policy Name   | Description                                                                                                                                   | Type                  | Dependency |
   +====================+===============================================================================================================================================+=======================+============+
   | DCS FullAccess     | All permissions for DCS. Users granted these permissions can operate and use all DCS instances.                                               | System-defined policy | None       |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DCS UserAccess     | Common user permissions for DCS, excluding permissions for creating, modifying, deleting DCS instances and modifying instance specifications. | System-defined policy | None       |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+------------+
   | DCS ReadOnlyAccess | Read-only permissions for DCS. Users granted these permissions can only view DCS instance data.                                               | System-defined policy | None       |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+------------+

.. note::

   The **DCS UserAccess** policy is different from the **DCS FullAccess** policy. If you configure both of them, you cannot create, modify, delete, or scale DCS instances because deny statements will take precedence over allowed statements.

:ref:`Table 2 <dcs-pd-210626001__en-us_topic_0170871404_table12985122891519>` lists the common operations supported by system-defined policies for DCS.

.. _dcs-pd-210626001__en-us_topic_0170871404_table12985122891519:

.. table:: **Table 2** Common operations supported by each system policy

   +---------------------------------------------+----------------+----------------+--------------------+
   | Operation                                   | DCS FullAccess | DCS UserAccess | DCS ReadOnlyAccess |
   +=============================================+================+================+====================+
   | Modifying instance configuration parameters | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Deleting background tasks                   | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Accessing instances using Web CLI           | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Modifying instance running status           | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Expanding instance capacity                 | Y              | x              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Changing instance passwords                 | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Modifying DCS instances                     | Y              | x              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Performing a master/standby switchover      | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Backing up instance data                    | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Analyzing big keys or hot keys              | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Creating DCS instances                      | Y              | x              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Deleting instance backup files              | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Restoring instance data                     | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Resetting instance passwords                | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Migrating instance data                     | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Downloading instance backup data            | Y              | Y              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Deleting DCS instances                      | Y              | x              | x                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying instance configuration parameters  | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying instance restoration logs          | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying instance backup logs               | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying DCS instances                      | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying instance background tasks          | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Querying all instances                      | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
   | Viewing instance performance metrics        | Y              | Y              | Y                  |
   +---------------------------------------------+----------------+----------------+--------------------+
