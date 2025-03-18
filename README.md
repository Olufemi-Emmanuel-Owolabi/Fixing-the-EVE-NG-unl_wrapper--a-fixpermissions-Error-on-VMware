## Fixing-the-EVE-NG-unl_wrapper--a-fixpermissions-Error-on-VMware
Fixing the EVE-NG unl_wrapper -a fixpermissions Error on VMware

## Problem Description
I installed EVE-NG on VMware and copied Switch/Router images. While following a tutorial on YouTube, I successfully transferred files using WinSCP to EVE-NG. However, when I attempted to run the following command:
/opt/unetlab/wrappers/unl_wrapper -a fixpermissions

I encountered the following error: PHP Warning: file_get_contents(/opt/unetlab/platform/): failed to open stream: No such file or directory in /opt/unetlab/html/includes/init.php on line 71

![permissions error](https://github.com/user-attachments/assets/fc211d59-f703-4eb0-b22b-365249ac7197)

## Solution

To resolve this issue, follow the steps below:

1. Verify Line 71 in the init.php File
Open the file /opt/unetlab/html/includes/init.php and navigate to line 71.

Ensure that the line is exactly as follows:
$kvm_family = file_get_contents("/opt/unetlab/platform");

Note: If the line is missing or incorrect, edit the file to match the line above.

2.  Identify CPU Type
Run the following command to check your CPU type: dmesg | grep -i cpu | grep -i -e intel -e amd
If the output contains "Intel", run: echo "intel" > /opt/unetlab/platform
If the output contains "AMD", run: echo "amd" > /opt/unetlab/platform

3. Verify the Fix
   After applying the fix, try running the fixpermissions command again: /opt/unetlab/wrappers/unl_wrapper -a fixpermissions

If the command runs successfully without errors, the issue has been resolved.

