:original_name: en-us_topic_0167429328.html

.. _en-us_topic_0167429328:

Why Is My Windows ECS Running Slowly?
=====================================

If your ECS runs slowly or is inaccessible unexpectedly, the bandwidth or vCPU usage of the ECS may be excessively high. If you have created an alarm rule in Cloud Eye, the system automatically sends an alarm to you when the bandwidth or CPU usage reaches the threshold specified in the rule.

To handle this issue, perform the following operations:

#. Fault locating:

   Identify the drivers from unknown sources and processes leading to high bandwidth or CPU usage.

   Windows offer multiple tools to locate faults, including Task Manager, Performance Monitor, Resource Monitor, Process Explorer, Xperf (supported by versions later than Windows Server 2008), and full memory dump.

2. Check whether the processes and drivers are malicious and handle the issue accordingly.

   -  If the processes are not malicious, optimize their programs or modify ECS specifications.
   -  If the processes are malicious, stop these processes manually or use a third-party tool to stop them automatically.
   -  If the drivers are from official sources, there is no need to deal with system built-in drivers. Determine whether to uninstall the third-party software based on your requirements.
   -  If the drivers are from unknown sources, you are advised to uninstall them by using commercial antivirus software or third-party security management tools.

Fault Locating
--------------

#. Log in to the ECS using VNC available on the management console.

#. Start the **Run** dialog box, and then enter **perfmon -res**.


   .. figure:: /_static/images/en-us_image_0281771106.png
      :alt: **Figure 1** Starting the Resource Monitor

      **Figure 1** Starting the Resource Monitor

#. On the **Resource Monitor** page, click the **CPU** or **Network** tab to view the CPU or bandwidth usage.


   .. figure:: /_static/images/en-us_image_0281773972.png
      :alt: **Figure 2** Resource Monitor

      **Figure 2** Resource Monitor

#. Obtain the IDs and names of the processes with high CPU or bandwidth usage.

#. On the remote login page, click **Ctrl+Alt+Del** to start the **Windows Task Manager**.

   Alternatively, start the **Run** dialog box and enter **taskmgr** to start the **Windows Task Manager**.

   The following describes how to display PIDs in **Windows Task Manager**, locate a process, and check whether it is malicious.

   a. Click the **Processes** tab.

   b. Click **PID** to sort the data.

   c. Right-click the process with high CPU or bandwidth usage and choose **Open File Location** from the shortcut menu.

   d. Check whether the process is malicious.


      .. figure:: /_static/images/en-us_image_0000001695612925.png
         :alt: **Figure 3** Checking the process

         **Figure 3** Checking the process

#. Open the **Run** dialog box and enter **fltmc** to view the filter drivers of the system.

   The following figure uses Windows 10 as an example. Different OSs have different built-in drivers. For details, see their official websites. If a third-party driver is installed, it is also displayed in this figure.


   .. figure:: /_static/images/en-us_image_0000001714627664.png
      :alt: **Figure 4** Viewing the system drivers

      **Figure 4** Viewing the system drivers

   The following describes how to view a driver source and check whether the source is unknown.

   a. Go to the **C:\\Windows\\System32\\drivers** directory on the local PC.

   b. Click the name of the unknown driver and choose **Properties** to view its details.

   c. Click the **Digital Signatures** tab to view the driver source.


      .. figure:: /_static/images/en-us_image_0000001762549449.png
         :alt: **Figure 5** Viewing the driver source

         **Figure 5** Viewing the driver source

Troubleshooting
---------------

Before the troubleshooting, check whether the processes or drivers leading to the high CPU or bandwidth usage are normal, and handle the issue accordingly.

**Suggestions for non-malicious processes**

#. If your ECS runs Windows Server 2008 or 2012, ensure that the available memory is 2 GiB or larger.
#. Check whether Windows Update is running.
#. Check whether the antivirus software is scanning files and programs on the backend.
#. Check whether any applications requiring high CPU or bandwidth resources are running on the ECS. If yes, modify ECS specifications or increase bandwidth.
#. If the ECS configuration meets the application requirements, deploy applications separately. For example, deploy the database and applications separately.

**Suggestions for malicious processes**

If the high CPU or bandwidth usage is caused by viruses or Trojan horses, manually stop the affected processes. You are advised to troubleshoot the issue as follows:

#. Use the commercial-edition antivirus software or install `Microsoft Safety Scanner <https://learn.microsoft.com/en-us/microsoft-365/security/intelligence/safety-scanner-download?view=o365-worldwide&spm=a2c4g.11186623.2.22.3fe9671c4mJYXV>`__ to scan for viruses in security mode.
#. Install the latest patches for Windows.
#. Run **MSconfig** to disable all drivers that are not delivered with Microsoft and check whether the fault is rectified. For details, see the official Microsoft document *How to perform a clean boot in Windows*.

**Suggestions for drivers from unknown sources**

Some viruses and Trojan horses are loaded through the filter drivers of the system. If you find a driver from an unknown source, you are advised to uninstall it. You can also use commercial antivirus software or third-party security management tools to delete it.

If an unknown driver cannot be deleted, or will appear again after being deleted, it is usually a virus or Trojan horse driver. If the driver cannot be completely deleted using commercial antivirus software or third-party security management tools, you are advised to reinstall the OS and back up data before the reinstallation.
