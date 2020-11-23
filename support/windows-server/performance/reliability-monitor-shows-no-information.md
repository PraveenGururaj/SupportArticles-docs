---
title: Reliability Monitor shows no information
description: Describes a behavior that is by design in Windows Server 2008 and in Windows Server 2008 R2. This behavior causes no information to be displayed in Reliability Monitor.
ms.date: 09/23/2020
author: Deland-Han 
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: kaushika, subheetr
ms.prod-support-area-path: Performance monitoring tools
ms.technology: Performance
---
# Reliability Monitor displays no information in Windows Server 2008 and in Windows Server 2008 R2

This article provides a solution to an issue that Reliability Monitor displays no information when you open Reliability Monitor on a computer that is running Windows Server 2008 or Windows Server 2008 R2.

_Original product version:_ &nbsp; Windows Server 2012 R2  
_Original KB number:_ &nbsp; 983386

## Symptoms

When you open Reliability Monitor on a computer that is running Windows Server 2008 or Windows Server 2008 R2, Reliability Monitor displays no information.

> [!NOTE]
>
> - This behavior does not occur on a computer that is running Windows Vista or Windows 7.
> - Reliability Monitor displays a stability index and displays some specific event information.

## Cause

This behavior occurs because the trigger that regularly starts the RacTask task is disabled.

Information that Reliability Monitor displays is provided by the RacTask task. By default, the RacTask task runs one time that is about one hour after you install the operating system. In Windows Server 2008 and in Windows Server 2008 R2, the trigger that regularly starts the RacTask task is disabled after the RacTask task runs for the first time.

## Resolution

To resolve this issue, follow these steps:

1. Click **Start**, type Task Scheduler in the **Search** box, and then click **Task Scheduler**.
2. Enable the trigger that regularly starts the RacTask task.
    1. In Task Scheduler, expand **Task Scheduler Library**, expand **Microsoft**, and then expand **Windows**.
    2. Right-click **RAC**, click **View**, and then click to select the **Show Hidden Tasks** command.

        > [!NOTE]
        > If the **Show Hidden Tasks** command is already selected, go to step 2c.
    3. Double-click **RacTask**.
    4. In the **RacTask Properties** dialog box, click the **Triggers** tab.
    5. On the **Triggers** tab, double-click the **One time** trigger.
    6. In the **Edit Trigger** dialog box, click to select the **Enabled** option, and then click **OK**.
    7. In the **RacTask Properties** dialog box, click **OK**.
    8. Close Task Scheduler.
3. Update a registry setting.
    1. Click **Start**, type Regedit in the **Search** box, and then click **Regedit**.
    2. In Registry Editor, set the value of the following registry entry to 1:
        `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Reliability Analysis\WMI\WMIEnable`

4. Restart the computer.

## Status

This behavior is by design.

## References

For more information about how to start Reliability Monitor in Windows Server 2008 and in Windows Vista, visit the following Microsoft TechNet Web site:  
[How to start Reliability Monitor in Windows Server 2008 and in Windows Vista](https://technet.microsoft.com/library/cc748864%28ws.10%29.aspx)
For more information about how to start Reliability Monitor in Windows Server 2008 R2 and in Windows 7, visit the following Microsoft Web site:  
[How to use Reliability Monitor in Windows Server 2008 R2 and in Windows 7](https://windows.microsoft.com/windows7/how-to-use-reliability-monitor)