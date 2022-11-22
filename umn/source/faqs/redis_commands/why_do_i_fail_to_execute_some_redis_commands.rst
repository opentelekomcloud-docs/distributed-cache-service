:original_name: dcs-faq-0730040.html

.. _dcs-faq-0730040:

Why Do I Fail to Execute Some Redis Commands?
=============================================

Possible causes include the following:

-  The command is incorrect.

-  The command is disabled in DCS.

   For security purposes, some Redis commands are disabled in DCS. For details about disabled and restricted Redis commands, see :ref:`Command Compatibility <dcs-pd-200312003>`.

-  The LUA script fails to be executed.

   For example, the error message "ERR unknown command 'EVAL'" indicates that your DCS Redis instance is of a lower version that does not support the LUA script. In this case, contact technical support for the instance to be upgraded.

-  The **CLIENT SETNAME** and **CLIENT GETNAME** commands fail to be executed.

   This is because the DCS Redis instance is of a lower version that does not support these commands. In this case, contact technical support for the instance to be upgraded.
