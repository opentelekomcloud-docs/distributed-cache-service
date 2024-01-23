:original_name: dcs-faq-0730048.html

.. _dcs-faq-0730048:

Why Can't I Modify Specifications for a DCS Redis Instance?
===========================================================

-  Check whether other tasks are running.

   Specifications of a DCS instance cannot be modified if another task of the instance is still running. For example, you cannot delete or scale up an instance while it is being restarted. Likewise, you cannot delete an instance while it is being scaled up.

   If the specification modification fails, try again later. If it fails again, contact technical support.

-  Modify instance specifications during off-peak hours. If the modification failed in peak hours (for example, when memory or CPU usage is over 90% or write traffic surges), try again during off-peak hours.
