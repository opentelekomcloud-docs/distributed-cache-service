:original_name: dcs-ug-210626005.html

.. _dcs-ug-210626005:

DCS Custom Policies
===================

Custom policies can be created to supplement the system-defined policies of DCS. For the actions that can be added to custom policies, see section "Permissions Policies and Supported Actions" in the *Distributed Cache Service API Reference*.

You can create custom policies in either of the following ways:

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy syntax.
-  JSON: Edit JSON policies from scratch or based on an existing policy.

For details, see section "Creating a Custom Policy" in the *Identity and Access Management API Reference*. The following section contains examples of common DCS custom policies.

.. note::

   Due to data caching, a policy involving OBS actions will take effect five minutes after it is attached to a user, user group, or project.

Example Custom Policies
-----------------------

-  Example 1: Allowing users to delete and restart DCS instances and clear data of an instance

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "
                           dcs:instance:delete
                           dcs:instance:modifyStatus
                       "
                  ]
              }
          ]
      }

-  Example 2: Denying DCS instance deletion

   A policy with only "Deny" permissions must be used in conjunction with other policies to take effect. If the permissions assigned to a user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   The following method can be used if you need to assign permissions of the **DCS FullAccess** policy to a user but you want to prevent the user from deleting DCS instances. Create a custom policy for denying DCS instance deletion, and attach both policies to the group to which the user belongs. Then, the user can perform all operations on DCS instances except deleting DCS instances. The following is an example of a deny policy:

   .. code-block::

      {
              "Version": "1.1",
              "Statement": [
                      {
                              "Effect": "Deny",
                              "Action": [
                                      "dcs:instance:delete"
                              ]
                      }
              ]
      }
