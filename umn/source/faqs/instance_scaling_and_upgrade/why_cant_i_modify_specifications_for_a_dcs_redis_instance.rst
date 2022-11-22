:original_name: dcs-faq-0730048.html

.. _dcs-faq-0730048:

Why Can't I Modify Specifications for a DCS Redis Instance?
===========================================================

Specifications of a DCS instance cannot be modified if another task of the instance is still running. For example, you cannot delete or scale up an instance while it is being restarted. Likewise, you cannot delete an instance while it is being scaled up.

If the specification modification fails, try again later. If it fails again, contact technical support.
