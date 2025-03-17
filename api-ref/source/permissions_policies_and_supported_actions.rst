:original_name: api-grant-policy.html

.. _api-grant-policy:

Permissions Policies and Supported Actions
==========================================

This chapter describes fine-grained permissions management for your DCS. If your account does not need individual IAM users, you can skip the configurations described in this chapter.

By default, new IAM users do not have any permissions assigned. You need to add a user to one or more groups, and assign policies or roles to these groups. The user then inherits permissions from the groups it is a member of. This process is called authorization. After authorization, the user can perform specified operations on cloud services based on the permissions.

You can grant users permissions by using roles and policies. Roles are a type of coarse-grained authorization mechanism that defines permissions related to user responsibilities. Policies define API-based permissions for operations on specific resources under certain conditions, allowing for more fine-grained, secure access control of cloud resources.

.. note::

   You can use policies to allow or deny access to specific APIs.

An account has all of the permissions required to call all APIs, but IAM users must have the required permissions specifically assigned. The permissions required for calling an API are determined by the actions supported by the API. Only users who have been granted permissions allowing the actions can call the API successfully. For example, if an IAM user wants to query ECSs using an API, the user must have been granted permissions that allow the **dcs:servers:list** action.

Supported Actions
-----------------

DCS provides system-defined policies, which can be directly used in IAM. You can also create custom policies to supplement system-defined policies for more refined access control. Actions supported by policies are specific to APIs. Common concepts related to policies include:

-  Permissions: Allow or deny certain operations.
-  APIs: REST APIs that can be called in a custom policy.
-  Actions: Added to a custom policy to control permissions for specific operations.
-  Dependent actions: When assigning permissions for an action, you also need to assign permissions for the dependent actions.
-  IAM and enterprise projects: Type of projects for which an action will take effect. Policies that contain actions supporting both IAM and enterprise projects can be assigned to user groups and take effect in both IAM and Enterprise Management. Policies that only contain actions supporting IAM projects can be assigned to user groups and only take effect for IAM. Such policies will not take effect if they are assigned to user groups in Enterprise Project. Administrators can check whether an action supports IAM projects or enterprise projects in the action list. The check mark (Y) indicates that the action supports the project and the cross symbol (x) indicates that the action does not support the project.

The following table lists the API actions supported by DCS.

.. table:: **Table 1** DCS actions

   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Permission                                                           | Action                            | API                                                                     | IAM Projects | Enterprise Project |
   +======================================================================+===================================+=========================================================================+==============+====================+
   | Creating a DCS instance                                              | dcs:instance:create               | POST /v2/{project_id}/instances                                         | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying an instance                                                 | dcs:instance:get                  | GET /v2/{project_id}/instances/{instance_id}                            | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying the information about an instance                          | dcs:instance:modify               | PUT /v2/{project_id}/instances/{instance_id}                            | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting an instance                                                 | dcs:instance:delete               | DELETE /v2/{project_id}/instances/{instance_id}                         | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Expanding instance capacity                                          | dcs:instance:scale                | POST /v2/{project_id}/instances/{instance_id}/resize                    | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying all instances                                               | dcs:instance:list                 | GET /v2/{project_id}/instances                                          | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying instance configuration parameters                           | dcs:instance:getConfiguration     | GET /v2/{project_id}/instances/{instance_id}/configs                    | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying instance configuration parameters                          | dcs:instance:modifyConfigureation | PUT /v2/{project_id}/instances/{instance_id}/configs                    | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Restarting an instance or clearing instance data                     | dcs:instance:modifyStatus         | PUT /v2/{project_id}/instances/status                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Changing the instance password                                       | dcs:instance:modifyAuthInfo       | PUT /v2/{project_id}/instances/{instance_id}/password                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Backing up an instance                                               | dcs:instance:backupData           | POST /v2/{project_id}/instances/{instance_id}/backups                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Restoring an instance                                                | dcs:instance:restoreData          | POST /v2/{project_id}/instances/{instance_id}/restores                  | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying backup records                                              | dcs:instance:getDataBackupLog     | GET /v2/{project_id}/instances/{instance_id}/backups                    | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying restoration records                                         | dcs:instance:getDataRestoreLog    | GET /v2/{project_id}/instances/{instance_id}/restores                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting backup files                                                | dcs:instance:deleteDataBackupFile | DELETE /v2/{project_id}/instances/{instance_id}/backups/{backup_id}     | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Listing background tasks                                             | dcs:instance:getBackgroundTask    | GET /v2/{project_id}/instances/{instance_id}/tasks                      | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting a background task                                           | dcs:instance:deleteBackgroundTask | DELETE /v2/{project_id}/instances/{instance_id}/tasks/{task_id}         | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Resetting the instance password                                      | dcs:instance:resetAuthInfo        | POST /v2/{project_id}/instances/{instance_id}/password/reset            | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Downloading backup files                                             | dcs:instance:downloadBackupData   | POST /v2/{project_id}/instances/{instance_id}/backups/{backup_id}/links | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Web CLI                                                              | dcs:instance:webcli               | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Creating a migration task                                            | dcs:migrationTask:create          | POST /v2/{project_id}/migration-task                                    | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying migration task configurations or stopping a migration task | dcs:migrationTask:modify          | POST /v2/{project_id}/migration-task/{task_id}/stop                     | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting a migration task                                            | dcs:migrationTask:delete          | DELETE /v2/{project_id}/migration-tasks/delete                          | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Listing migration tasks                                              | dcs:migrationTask:list            | GET /v2/{project_id}/migration-tasks                                    | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying details of a data migration task                            | dcs:migrationTask:get             | GET /v2/{project_id}/migration-task/{task_id}                           | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Diagnosing an instance                                               | dcs:instance:diagnosis            | POST /v2/{project_id}/instances/{instance_id}/diagnosis                 | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Viewing parameter templates                                          | dcs:template:list                 | GET /v2/{project_id}/config-templates                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Creating a parameter template                                        | dcs:template:create               | POST /v2/{project_id}/config-templates                                  | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Performing a master/standby switchover                               | dcs:instance:swap                 | POST /v2/{project_id}/instances/{instance_id}/swap                      | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying the whitelist of an instance                               | dcs:whitelist:modify              | PUT /v2/{project_id}/instance/{instance_id}/whitelist                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Obtaining the whitelist of an instance                               | dcs:whitelist:list                | GET /v2/{project_id}/instance/{instance_id}/whitelist                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Creating a user for accessing an instance                            | dcs:aclaccount:create             | POST /v2/{project_id}/instances/{instance_id}/accounts                  | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting an instance user                                            | dcs:aclaccount:delete             | DELETE /v2/{project_id}/instances/{instance_id}/accounts/{account_id}   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying the information about an instance user                     | dcs:aclaccount:modify             | PUT /v2/{project_id}/instances/{instance_id}/accounts/{account_id}      | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Obtaining the list of instance users                                 | dcs:aclaccount:list               | GET /v2/{project_id}/instances/{instance_id}/accounts                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying slow logs                                                   | dcs:slowlog:list                  | GET /v2/{project_id}/instances/{instance_id}/slowlog                    | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Viewing parameter templates                                          | dcs:template:get                  | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Viewing the task progress                                            | dcs:job:get                       | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Viewing audit logs                                                   | dcs:auditlog:get                  | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying instance upgrade information                                | dcs:instance:getUpgradeInfo       | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying SSL encryption of an instance                               | dcs:ssl:get                       | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Updating domain names                                                | dcs:domainname:rebuild            | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Switching IP addresses                                               | dcs:migrationTask:exchangeIp      | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Rolling back IP address switching                                    | dcs:migrationTask:rollbackIp      | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Killing Redis sessions                                               | dcs:clients:kill                  | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying a parameter template                                       | dcs:template:modify               | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Enabling or disabling public domain name resolution                  | dcs:publicdomainname:update       | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Deleting a parameter template                                        | dcs:template:delete               | ``-``                                                                   | Y            | X                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Releasing historical domain names                                    | dcs:histroydomainname:release     | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Analyzing big or hot keys                                            | dcs:instance:analyze              | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Enabling or disabling audit logging                                  | dcs:auditlog:modify               | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Enabling or disabling client IP pass-through                         | dcs:clientiptrans:modify          | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Modifying SSL encryption for an instance                             | dcs:ssl:modify                    | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
   | Querying the Redis session list                                      | dcs:clients:list                  | ``-``                                                                   | Y            | Y                  |
   +----------------------------------------------------------------------+-----------------------------------+-------------------------------------------------------------------------+--------------+--------------------+
