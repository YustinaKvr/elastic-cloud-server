:original_name: en-us_topic_0031523135.html

.. _en-us_topic_0031523135:

Changing the OS
===============

Scenarios
---------

Changing an ECS OS will change the system disk attached to the ECS. After the change, the system disk ID of the ECS will be changed, and the original system disk will be deleted.

If the OS running on an ECS cannot meet service requirements, change the ECS OS.

The cloud platform supports changing between image types (public images, private images, and shared images) and between OSs. You can change your OS by changing your ECS image.

Constraints
-----------

-  The OS change takes about 1 to 4 minutes During this process, the ECS status is **Changing OS**.
-  Do not perform any operations on the ECS before the system injects the password or key, or the login will fail.
-  The ECS for which you want to change the OS must be in any of the following states: **Stopped**, **Reinstallation failed**, or **Failed to change the OS**.
-  The target ECS must have a system disk attached.
-  The EVS disk quota must be greater than 0.
-  The system disk type cannot be changed.
-  The system disk can be encrypted.
-  For details about the change between different OSs, see :ref:`Notes on Change Between Windows and Linux <en-us_topic_0031523135__section1852122261012>`.
-  If an ECS OS is to be changed using a full-ECS image, the ECS system disk can be encrypted.

Notes
-----

-  After the OS is changed, the original OS is not retained, and the original system disk is deleted, including the data in all partitions of the system disk.
-  Changing the OS clears the data in all partitions of the system disk, including the system partition. Back up data before changing the OS.
-  Changing the OS does not affect data in data disks.
-  After the OS is changed, your service running environment must be deployed in the new OS again.
-  After the OS is changed, the ECS will be automatically started.
-  After the OS is changed, the system disk type of the ECS cannot be changed.
-  After the OS is changed, the IP and MAC addresses of the ECS remain unchanged.
-  After the OS is changed, customized configurations, such as DNS and hostname of the original OS will be reset and require reconfiguration.
-  An OS change takes about 1 to 4 minutes to complete. During this process, the ECS is in **Changing OS** state.
-  After the OS is changed, the password for logging in to the ECS is reset. To retrieve the password, perform the following operations:

   -  For a Linux ECS, log in to it using the key and set a new password. For instructions about how to log in to an ECS using a key pair, see :ref:`Logging In to a Linux ECS Using an SSH Key Pair <en-us_topic_0017955380>`.
   -  For a Windows ECS, retrieve the password by following the instructions provided in :ref:`Obtaining the Password for Logging In to a Windows ECS <en-us_topic_0031107266>`.

-  The system disk capacity of an ECS with OS changed may change because the system disk capacity specified by the image of the changed OS may be changed.
-  You can choose to encrypt the system disk of an ECS during OS change.

.. _en-us_topic_0031523135__section1852122261012:

Notes on Change Between Windows and Linux
-----------------------------------------

When you change the OS from Windows to Linux or from Linux to Windows, note the following:

-  To change Windows to Linux, install an NTFS partition tool, such as NTFS-3G for data reads and writes on the Windows ECS.
-  To change Linux to Windows, install software, such as Ext2Read or Ext2Fsd to identify ext3 or ext4.

   .. note::

      If there are LVM partitions on the Linux ECS, these partitions may fail after the OS is changed to Windows. Therefore, a change from Linux to Windows is not recommended.

Prerequisites
-------------

-  The data is backed up.

-  If you want to change the login authentication mode from password to key pair during the OS change, create a key file in advance.

   For details, see :ref:`(Recommended) Creating a Key Pair on the Management Console <en-us_topic_0000001278350057>`.

-  If you plan to use a private image to change the OS, ensure that a private image is available. For details about how to create a private image, see *Image Management Service User Guide*.

   -  If the image of a specified ECS is required, make sure that a private image has been created using this ECS.
   -  If a local image file is required, make sure that the image file has been imported to the cloud platform and registered as a private image.
   -  If a private image from another region is required, make sure that the image has been copied.
   -  If a private image from another user account is required, make sure that the image has been shared with you.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner and select your region and project.

#. .. _en-us_topic_0031523135__en-us_topic_0031523135_en-us_topic_0024911405_li45082966143628:

   Under **Computing**, choose **Elastic Cloud Server**.

#. Locate the row containing the target ECS and choose **More** > **Manage Image/Backup** > **Change OS** in the **Operation** column.

   Only stopped ECSs support OS change. If the ECS is not stopped, stop it before proceeding with changing.

#. Select the target image.

   For details, see :ref:`Creating an ECS <en-us_topic_0021831611>`.


   .. figure:: /_static/images/en-us_image_0000001658474496.png
      :alt: **Figure 1** Changing an OS

      **Figure 1** Changing an OS

#. (Optional) Select the **Encryption** option to encrypt the system disk during OS change.

   To enable encryption, click **Create Xrole** to grant KMS access permissions to EVS. If you have the granting permission, grant KMS access permissions to EVS. If you do not have the granting permission, contact the user who has the Security Administrator permissions to grant KMS access permissions. For details, see :ref:`Can All Users Use the Encryption Feature? <en-us_topic_0047272493>`

   Encryption parameters are as follows:

   -  **Encryption**: indicates that the EVS disk has been encrypted.
   -  **Create Xrole**: assigns KMS access permissions to EVS to obtain KMS keys. After the permissions are assigned, follow-up operations do not require assigning permissions again.
   -  **Xrole Name**: set to **EVSAccessKMS**, which means that permissions have been assigned to EVS to obtain KMS keys for encrypting or decrypting EVS disks.
   -  **KMS Key Name**: specifies the name of the key used by the encrypted EVS disk. You can select an existing key, or click **Create KMS Key** and create a new one on the KMS console. The default value is **evs/default**.
   -  **KMS Key ID**: specifies the ID of the key used by the encrypted data disk.

#. (Optional) Select a **License Type** (**Use license from the system** or **Bring your own license (BYOL)**) if the changed OS running on your ECS is billed. For more details, see :ref:`License Types <en-us_topic_0046566932>`.

   The following OSs are billed:

   -  SUSE Linux Enterprise Server
   -  Oracle Enterprise Linux
   -  Red Hat Enterprise Linux

#. Configure the login mode.

   If the target ECS uses key pair authentication, you can replace the original key pair.

#. Click **OK**.

#. .. _en-us_topic_0031523135__en-us_topic_0031523135_en-us_topic_0024911405_li45992498111556:

   In the **Change ECS OS** dialog box, confirm the specifications, and click **Submit**.

   After the application is submitted, the ECS status changes to **Changing OS**. When this status disappears, the OS change is complete.

   .. note::

      During the OS change process, a temporary ECS is created. After the OS change is complete, this ECS will be automatically deleted.

Follow-up Procedure
-------------------

-  If the OSs before and after the OS change are both Linux, and automatic mounting upon system startup has been enabled for data disks, the data disk partition mounting information will be lost after the OS is changed. In such a case, you need to update the **/etc/fstab** configuration.

   #. Write the new partition information into **/etc/fstab**.

      It is a good practice to back up the **/etc/fstab** file before writing data into it.

      To enable automatic partition mounting upon system startup, see :ref:`Initializing a Linux Data Disk (fdisk) <en-us_topic_0085634797>`.

   #. Mount the partition so that you can use the data disk.

      **mount** *Disk partition* *Device name*

   #. Check the mount result.

      **df -TH**

-  If the OS change is unsuccessful, perform steps :ref:`3 <en-us_topic_0031523135__en-us_topic_0031523135_en-us_topic_0024911405_li45082966143628>` to :ref:`10 <en-us_topic_0031523135__en-us_topic_0031523135_en-us_topic_0024911405_li45992498111556>` again to retry the OS change.
-  If the second OS change attempt is unsuccessful, contact customer service for manual recovery at the backend.

.. |image1| image:: /_static/images/en-us_image_0210779229.png
