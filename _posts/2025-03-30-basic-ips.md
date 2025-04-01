---
title: Azure Update Manager - Set Patch Orchestration Mode to AutomaticByPlatform
date: 2024-10-23 11:06:05 +/-TTTT
categories: [Azure, Update Manager]
tags: [azure, aum, update, manager, prerequisites, automaticbyplatform] # TAG names should always be lowercase
---

One of the prerequisites to patch VMs using Azure Update Manager is to set the orchestration mode to "AutomaticByPlatform". If this is not set, when you deploy a new Update Schedule, you may receive the following error in your deploytment:

> Error
> "code": "UnsupportedResourceOperation",
> "message": "\"Patch orchestration mode is not set to AutomaticByPlatform",The prerequisites to patch your machine were not met. Please set the patchMode to AutomaticByPlatform and bypassPlatformChecksOnUserSchedule as true.
{: .prompt-warning }

## Resolution

To fix this, you need to set the orchestration mode to "AutomaticByPlatform" for all the vms in your scope.

### Portal Method - Enable for existing VMs

You can update the patch orchestration option for existing VMs that either already have schedules associated or will be newly associated with a schedule.

If Patch orchestration is set as Azure-orchestrated or Azure Managed - Safe Deployment (AutomaticByPlatform), BypassPlatformSafetyChecksOnUserSchedule is set to false, and there's no schedule associated, the VMs will be autopatched.

To update the patch mode:

1. Sign in to the Azure portal.
2. Go to Azure Update Manager and select Update Settings.
3. In Change update settings, select Add machine.
4. In Select resources, select your VMs and then select Add.
5. On the Change update settings pane, under Patch orchestration, select Customer Managed Schedules and then select Save.

Attach a schedule after you finish the preceding steps.

To check if _BypassPlatformSafetyChecksOnUserSchedule_ is enabled, go to the Virtual machine home page and select Overview > JSON View.

### Powershell Method

#### Enable on Windows VMs

``` powershell
$VirtualMachine = Get-AzVM -ResourceGroupName "<resourceGroup>" -Name "<vmName>"
Set-AzVMOperatingSystem -VM $VirtualMachine -Windows -PatchMode "AutomaticByPlatform"
$AutomaticByPlatformSettings = $VirtualMachine.OSProfile.WindowsConfiguration.PatchSettings.AutomaticByPlatformSettings

if ($null -eq $AutomaticByPlatformSettings) {
   $VirtualMachine.OSProfile.WindowsConfiguration.PatchSettings.AutomaticByPlatformSettings = New-Object -TypeName Microsoft.Azure.Management.Compute.Models.WindowsVMGuestPatchAutomaticByPlatformSettings -Property @{BypassPlatformSafetyChecksOnUserSchedule = $true}
} else {
   $AutomaticByPlatformSettings.BypassPlatformSafetyChecksOnUserSchedule = $true
}

Update-AzVM -VM $VirtualMachine -ResourceGroupName "<resourceGroup>"
```

#### Enable on Linux VMs

``` powershell
$VirtualMachine = Get-AzVM -ResourceGroupName "<resourceGroup>" -Name "<vmName>"
Set-AzVMOperatingSystem -VM $VirtualMachine -Linux -PatchMode "AutomaticByPlatform"
$AutomaticByPlatformSettings = $VirtualMachine.OSProfile.LinuxConfiguration.PatchSettings.AutomaticByPlatformSettings

if ($null -eq $AutomaticByPlatformSettings) {
   $VirtualMachine.OSProfile.LinuxConfiguration.PatchSettings.AutomaticByPlatformSettings = New-Object -TypeName Microsoft.Azure.Management.Compute.Models.LinuxVMGuestPatchAutomaticByPlatformSettings -Property @{BypassPlatformSafetyChecksOnUserSchedule = $true}
} else {
   $AutomaticByPlatformSettings.BypassPlatformSafetyChecksOnUserSchedule = $true
}

Update-AzVM -VM $VirtualMachine -ResourceGroupName "<resourceGroup>"
```
## Related Links

<a href="https://learn.microsoft.com/en-us/azure/update-manager/prerequsite-for-schedule-patching?tabs=new-prereq-portal,auto-portal#enable-schedule-patching-on-azure-vms" target="_blank">Enable schedule patching on Azure VMs</a>
