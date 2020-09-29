---
title: Stop error 0x109:CRITICAL_STRUCTURE_CORRUPTION on a VMWare virtual machine
description: describes how to fix Stop error 0x109:CRITICAL_STRUCTURE_CORRUPTION on a VMWare virtual machine
ms.date: 09/10/2020
author: Deland-Han
ms.author: delhan 
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika
ms.prod-support-area-path: Blue Screen/Bugcheck
ms.technology: Performance
---
# Stop error 0x109: CRITICAL_STRUCTURE_CORRUPTION on a VMWare virtual machine

This article provides the resolution of fixing the Stop error 0x109: CRITICAL_STRUCTURE_CORRUPTION on a VMWare virtual machine.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 2902739

## Symptoms

On a Windows Server Virtual Machine that is running VMWare ESXi 5.0.x, you receive a "CRITICAL_STRUCTURE_CORRUPTION" Stop error code that begins as follows:
>Bug check code 00000109  
Arguments a3a01f58 \`92797517 b3b72bde \`e4f976b6 00000000 \`c0000103 00000000` 00000007

## Cause

This problem occurs because the system detects a Critical MSR modification, and then it crashes.

## Resolution

To resolve this problem, go to the following VMWare website: [Windows 8.1/Windows Server 2012 virtual machines fail with a blue screen and report the error: CRITICAL_STRUCTURE_CORRUPTION (2060019)](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2060019&sliceId=1&docTypeID=DT_KB_1_1&dialogID=158133794&stateId=0%200%20158145165) 

This is a known issue that affects ESXi 5.0.x. For more information, contact VMWare.

To work around this issue, manually create a CPUID mask for the affected virtual machines. To do this, follow these steps:

1. Turn off the virtual machine.
2. Right-click the virtual machine, and then click **Edit Settings**.
3. Click the **Options** tab.
4. Under **Advanced**, click **CPUID Mask**.
5. Click **Advanced**.
6. In the Register column, locate the **edx**  register under **Level 80000001**.
7. In the **Value** field, enter the following character string exactly:

   ----:0---:----:----:----:----:----:---- 

8. Click **OK** two times. The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.

## More information

0: kd>. bugcheck
Bugcheck code 00000109
Arguments a3a01f58`92797517 b3b72bde`e4f976b6 00000000`c0000103 00000000`00000007
0: kd> !sysinfo machineid
Machine ID Information [From Smbios 2.4, DMIVersion 0, Size=10150]
BiosMajorRelease = 4
BiosMinorRelease = 6
FirmwareMajorRelease = 0
FirmwareMinorRelease = 0
BiosVendor = Phoenix Technologies LTD
BiosVersion = 6.00
BiosReleaseDate = 07/09/2012
SystemManufacturer = VMware, Inc.
SystemProductName = VMware Virtual Platform
SystemVersion = None
BaseBoardManufacturer = Intel Corporation
BaseBoardProduct = 440BX Desktop Reference Platform
BaseBoardVersion = None

CRITICAL_STRUCTURE_CORRUPTION (109)

This Stop error is generated when the kernel detects that critical kernel code or data has been corrupted. Typically, any of the following situations can cause this corruption:
- A driver inadvertently or deliberately modified critical kernel code or data. For more information, see [Kernel patch protection for x64-based operating systems](https://www.microsoft.com/whdc/driver/kernel/64bitPatching.mspx).

- A developer tried to set a standard kernel breakpoint by using a kernel debugger that was not attached when the system was started. Standard breakpoints (bp) can be set only if the debugger is attached at startup. Processor breakpoints (ba) can be set at any time.

- A hardware corruption occurred. For example, the kernel code or data might have been stored in memory that failed.

Arguments:
Arg1: a3a01f5892797517, Reserved
Arg2: b3b72bdee4f976b6, Reserved
Arg3: 00000000c0000103, Failure type-dependent information
Arg4: 0000000000000007, Type of corrupted region, can be 7: Critical MSR modification