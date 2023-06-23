:original_name: dcs-faq-210706001.html

.. _dcs-faq-210706001:

When Will AOF Rewrites Be Triggered?
====================================

AOF rewrites involve the following concepts:

-  Rewrite window, which is currently 01:00 to 04:59
-  Disk usage threshold, which is 50%

AOF rewrites are triggered in the following scenarios:

-  If the disk usage reaches the threshold (regardless of whether the current time is within the rewrite window), rewrites will be triggered on instances whose AOF file size is larger than the memory dataset size.
-  If the disk usage is below the threshold and the current time is within the rewrite window, rewrites will be triggered on instances whose AOF file size is larger than the dataset memory multiplied by 1.5.
-  If the disk usage is below the threshold but the current time is out of the rewrite window, rewrites will be triggered on instances whose AOF file size is larger than the maximum memory multiplied by 4.5.
