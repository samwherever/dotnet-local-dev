---
title: .NET Framework & Windows OS versions
description: Learn about key features in each version of .NET Framework, including underlying CLR versions and versions installed by the Windows operating system.
ms.date: 07/10/2025
helpviewer_keywords:
  - "versions, .NET Framework"
---
# .NET Framework versions and dependencies

Each version of .NET Framework contains the common language runtime (CLR), the base class libraries, and other managed libraries. This article describes the key features of .NET Framework by version, provides information about the underlying CLR versions and associated development environments, and identifies the versions that are installed by the Windows operating system (OS).

Each new version of .NET Framework adds new features but retains features from previous versions.

[!INCLUDE [net-framework-future](../../../includes/net-framework-future.md)]

The CLR is identified by its own version number. The .NET Framework version number is incremented at each release, but the CLR version is not always incremented. For example, .NET Framework 4, 4.5, and later releases include CLR 4, but .NET Framework 2.0, 3.0, and 3.5 include CLR 2.0. (There was no version 3 of the CLR.)

> [!TIP]
>
> - For a complete list of supported operating systems, see [System requirements](../get-started/system-requirements.md).
> - For downloads, see [Install .NET Framework for developers](guide-for-developers.md).
> - For information about determining which versions of .NET Framework are installed on a computer, see [How to determine which .NET Framework versions are installed](how-to-determine-which-versions-are-installed.md).

## Version information

The tables that follow summarize .NET Framework version history and correlate each version with Visual Studio, Windows, and Windows Server. Visual Studio supports multi-targeting, so you're not limited to the version of .NET Framework that's listed.

- The check mark icon ✔️ denotes OS versions on which .NET Framework is installed by default.
- The plus sign icon ➕ denotes OS versions on which .NET Framework doesn't come installed but can be installed.
- The asterisk **\*** denotes OS versions on which .NET Framework (whether preinstalled or not) must be enabled [in Control Panel](dotnet-35-windows.md#enable-net-framework-35-on-windows) or, for Windows Server, through the [Server Manager](dotnet-35-windows.md#enable-net-framework-35-on-windows-server).

Jump to:

- [.NET Framework 4.8.1](#net-framework-481)
- [.NET Framework 4.8](#net-framework-48)
- [.NET Framework 4.7.2](#net-framework-472)
- [.NET Framework 4.7.1](#net-framework-471)
- [.NET Framework 4.7](#net-framework-47)
- [.NET Framework 4.6.2](#net-framework-462)
- [.NET Framework 4.6.1](#net-framework-461)
- [.NET Framework 4.6](#net-framework-46)
- [.NET Framework 4.5.2](#net-framework-452)
- [.NET Framework 4.5.1](#net-framework-451)
- [.NET Framework 4.5](#net-framework-45)
- [.NET Framework 4](#net-framework-4)
- [.NET Framework 3.5](#net-framework-35)
- [.NET Framework 3.0](#net-framework-30)
- [.NET Framework 2.0](#net-framework-20)
- [.NET Framework 1.1](#net-framework-11)
- [.NET Framework 1.0](#net-framework-10)

### .NET Framework 4.8.1

- [New features](../whats-new/index.md#whats-new-in-net-framework-481)
- New accessibility features
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net481/README.md)

|                    | Versions              |
|--------------------|-----------------------|
| **CLR**            | 4                     |
| **Windows**        | ✔️ 11 version 24H2 (version 26100)<br/>✔️ 11 October 2023 Release (version 22631)<br/>✔️ 11 September 2022 Release (version 22621)<br/>➕ 11 October 2021 Release (version 22000)<br/>➕ 10 October 2022 Update (22H2)<br/>➕ 10 November 2021 Update<br/>➕ 10 May 2021 Update<br/>➕ 10 October 2020 Update<br/>|
| **Windows Server** | ✔️ Windows Server 2025<br/>➕ Windows Server 2022 |

To determine the installed .NET version, use the following `Release` DWORD:

- 533320 (Windows 11 September 2022 Release and Windows 11 October 2023 Release)
- 533325 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.8

- [New features](../whats-new/index.md#whats-new-in-net-framework-48)
- [New in accessibility](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-48)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net48/README.md)

|         | Versions |
|---------|----------|
| **CLR** | 4        |
|**Windows**|✔️ 11 October 2021 Release (Version 22000)<br/>✔️ 10 October 2022 Update (22H2)<br/>✔️ 10 November 2021 Update<br/>✔️ 10 May 2021 Update<br/>✔️ 10 October 2020 Update<br/>✔️ 10 May 2020 Update<br/>✔️ 10 November 2019 Update<br/>✔️ 10 May 2019 Update<br/>➕ 10 October 2018 Update (Version 1809)<br/>➕ 10 April 2018 Update (Version 1803)<br/>➕ 10 Fall Creators Update (Version 1709)<br/>➕ 10 Creators Update (Version 1703)<br/>➕ 10 Anniversary Update (Version 1607)<br/>➕ 8.1<br/>➕7|
|**Windows Server**|✔️ Windows Server 2022<br/>➕ Windows Server 2019<br/>➕ Windows Server, version 1809<br/>➕ Windows Server, version 1803<br/>➕ 2016<br/>➕ 2012 R2<br/>➕ 2012<br/>➕ 2008 R2 SP1|

To determine the installed .NET version, use the following `Release` DWORD:

- 528449 (Windows 11 and Windows Server 2022)
- 528372 (Windows 10 May 2020 Update and Windows 10 October 2020 Update and Windows 10 May 2021 Update)
- 528040 (Windows 10 May 2019 Update and Windows 10 November 2019 Update)
- 528049 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.7.2

- [New features](../whats-new/index.md#whats-new-in-net-framework-472)
- [New in accessibility](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-472)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net472/README.md)

|                               | Versions |
|-------------------------------|----------|
| **CLR**                       | 4        |
| **Included in Visual Studio** | 2019†    |
|**Windows**|✔️ 10 October 2018 Update (Version 1809)<br/>✔️ 10 April 2018 Update (Version 1803)<br/>➕ 10 Fall Creators Update (Version 1709)<br/>➕ 10 Creators Update (Version 1703)<br/>➕ 10 Anniversary Update (Version 1607)<br/>➕ 8.1<br/>➕7|
|**Windows Server**|✔️ Windows Server 2019<br/>✔️ Windows Server, version 1809<br/>✔️ Windows Server, version 1803<br/>➕ Windows Server, version 1709<br/>➕ 2016<br/>➕ 2012 R2<br/>➕ 2012<br/>➕ 2008 R2 SP1|

†Requires installing the **.NET desktop development**, **ASP.NET and web development**, **Azure development**, **Office/SharePoint development**, **Mobile development with .NET**, or **.NET Core cross-platform development** workloads.

To determine the installed .NET version, use the following `Release` DWORD:

- 461814 (Windows 10 October 2018 Update)
- 461808 (Windows 10 April 2018 Update and Windows Server, version 1803)
- 461814 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.7.1

- [New features](../whats-new/index.md#whats-new-in-net-framework-471)
- [New in accessibility](../whats-new/whats-new-in-accessibility.md#whats-new-in-accessibility-in-net-framework-471)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net471/README.md)

|         | Versions |
|---------|----------|
| **CLR** | 4        |
|**Windows**|✔️ 10 Fall Creators Update (Version 1709)<br/>➕ 10 Creators Update (Version 1703)<br/>➕ 10 Anniversary Update (Version 1607)<br/>➕ 8.1<br/>➕7|
|**Windows Server**|➕ Windows Server, version 1803<br/>✔️ Windows Server, version 1709<br/>➕ 2016<br/>➕ 2012 R2<br/>➕ 2012<br/>➕ 2008 R2 SP1|

To determine the installed .NET version, use the following `Release` DWORD:

- 461308 (Windows 10 Creators Update and Windows Server, version 1709)
- 461310 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.7

- [New features](../whats-new/index.md#whats-new-in-net-framework-47)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net47/README.md)

|                    | Versions                                                                                              |
|--------------------|-------------------------------------------------------------------------------------------------------|
| **CLR**            | 4                                                                                                     |
| **Windows**        | ✔️ 10 Creators Update (Version 1703)<br/>➕ 10 Anniversary Update (Version 1607)<br/>➕ 8.1<br/>➕7 |
| **Windows Server** | ➕ 2016<br/>➕ 2012 R2<br/>➕ 2012<br/>➕ 2008 R2 SP1                                               |

To determine the installed .NET version, use the following `Release` DWORD:

- 460798 (Windows 10 Creators Update)
- 460805 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.6.2

- [New features](../whats-new/index.md#whats-new-in-net-framework-462)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net462/README.md)

|                    | Versions                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------|
| **CLR**            | 4                                                                                                          |
| **Windows**        | ✔️ 10 Anniversary Update (Version 1607)<br/>➕ 10 November Update (Version 1511)<br/>➕ 10<br/>➕ 8.1<br />➕ 7 |
| **Windows Server** | ✔️ 2016<br /><br/>➕ 2012 R2<br />➕ 2012<br />➕ 2008 R2 SP1<br />➕ 2008 SP2                           |

To determine the installed .NET version, use the following `Release` DWORD:

- 394802 (Windows 10 Anniversary Update and Windows Server 2016)
- 394806 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.6.1

- [New features](../whats-new/index.md#whats-new-in-net-framework-461)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net461/README.md)

|                                       | Versions                                                                  |
|---------------------------------------|---------------------------------------------------------------------------|
| **CLR**                               | 4                                                                         |
| **Included in Visual Studio** | 2017<sup>1</sup>                                                          |
| **Windows**                           | ✔️ 10 November Update (Version 1511)<br/>➕ 10<br />➕ 8.1<br />➕ 8<br />➕ 7 |
| **Windows Server**                    | ➕ 2012 R2<br />➕ 2012<br />➕ 2008 R2 SP1                                 |

<sup>1</sup> Requires installing the **.NET desktop development**, **ASP.NET and web development**, **Azure development**, **Office/SharePoint development**, **Mobile development with .NET**, or **.NET Core cross-platform development** workloads.

To determine the installed .NET version, use the following `Release` DWORD:

- 394254 (Windows 10 November Update)
- 394271 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.6

- [New features](../whats-new/index.md#whats-new-in-net-2015)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net46/README.md)

|                                       | Versions                                                 |
|---------------------------------------|----------------------------------------------------------|
| **CLR**                               | 4                                                        |
| **Included in Visual Studio**         | 2015                                                     |
| **Windows**                           | ✔️ 10<br /><br />➕ 8.1<br />➕ 8<br />➕ 7<br />➕ Vista   |
| **Windows Server**                    | ➕ 2012 R2<br />➕ 2012<br />➕ 2008 R2 SP1<br />➕ 2008 SP2 |

To determine the installed .NET version, use the following `Release` DWORD:

- 393295 (Windows 10)
- 393297 (all other OS versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.5.2

- [New features](../whats-new/index.md#whats-new-in-net-framework-452)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net452/README.md)

|                    | Versions                                                 |
|--------------------|----------------------------------------------------------|
| **CLR**            | 4                                                        |
| **Windows**        | ➕ 8.1<br />➕ 8<br />➕ 7<br />➕ Vista                    |
| **Windows Server** | ➕ 2012 R2<br />➕ 2012<br />➕ 2008 R2 SP1<br />➕ 2008 SP2 |

To determine the installed .NET version, use `Release` DWORD 379893. For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 4.5.1

- [New features](../whats-new/index.md#whats-new-in-net-framework-451)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net451/README.md)

|                                       | Versions                                                       |
|---------------------------------------|----------------------------------------------------------------|
| **CLR**                               | 4                                                              |
| **Included in Visual Studio**         | 2013                                                           |
| **Windows**                           | ✔️ 8.1<br /><br />➕ 8<br />➕ 7<br />➕ Vista                   |
| **Windows Server**                    | ✔️ 2012 R2<br /><br />➕ 2012<br />➕ 2008 R2 SP1<br />➕ 2008 SP2 |

To determine the installed .NET version, use the following `Release` DWORD:

- 378675 (Windows 8.1)
- 378758 (all other Windows versions)

For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

[!INCLUDE [net-framework-vs](../../../includes/net-framework-vs.md)]

### .NET Framework 4.5

- [New features](../whats-new/index.md#whats-new-in-net-framework-45)
- [Release notes](https://github.com/Microsoft/dotnet/tree/main/releases/net45/README.md)

|                                       | Versions                                  |
|---------------------------------------|-------------------------------------------|
| **CLR**                               | 4                                         |
| **Included in Visual Studio**         | 2012                                      |
| **Windows**                           | ✔️ 8<br />➕ 7<br />➕ Vista               |
| **Windows Server**                    | ✔️ 2012<br />➕ 2008 R2 SP1<br />➕ 2008 SP2 |

To determine the installed .NET version, use `Release` DWORD 378389. For more information, see [instructions](how-to-determine-which-versions-are-installed.md).

[!INCLUDE [net-framework-vs](../../../includes/net-framework-vs.md)]

### .NET Framework 4

[New features](/previous-versions/dotnet/netframework-4.0/ms171868(v=vs.100))

|                               | Versions                                  |
|-------------------------------|-------------------------------------------|
| **CLR**                       | 4                                         |
| **Included in Visual Studio** | 2010                                      |
| **Windows**                   | ➕ 7<br />➕ Vista                         |
| **Windows Server**            | ➕ 2008 R2 SP1<br />➕ 2008 SP2<br />➕ 2003 |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

[!INCLUDE [net-framework-vs](../../../includes/net-framework-vs.md)]

### .NET Framework 3.5

[New features](/previous-versions/visualstudio/visual-studio-2008/ms171868\(v=vs.90\)):

- LINQ
- Expression trees
- Improved ASP.NET support for AJAX development
- HashSet collections
- DateTimeOffset
- WCF and WF integration
- Peer-to-Peer networking
- Add-ins for extensibility

|                               | Versions                                                                                                                                                                    |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **CLR**                       | 2.0                                                                                                                                                                         |
| **Included in Visual Studio** | 2008                                                                                                                                                                        |
| **Windows**                   | ✔️ 10\*<br/>✔️ 8.1\*<br />✔️ 8\*<br />✔️ 7<br /><br />➕ Vista                                                                                                              |
| **Windows Server**            | ➕ Windows Server, version 1803\*<br/>➕ Windows Server, version 1709\*<br/>➕ 2016\*<br/>➕ 2012 R2\*<br />➕ 2012\*<br /><br />✔️2008 R2 SP1\*<br /><br/>➕ 2008 SP2<br />➕ 2003 |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 3.0

[New features](/previous-versions/visualstudio/visual-studio-2008/bb822048(v=vs.90)):

- Windows Presentation Foundation
- Windows Communication Foundation
- Windows Workflow Foundation
- Windows CardSpace

|                    | Versions                                           |
|--------------------|----------------------------------------------------|
| **CLR**            | 2.0                                                |
| **Windows**        | ✔️ Vista                                          |
| **Windows Server** | ✔️ 2008 R2 SP1*<br />✔️ 2008 SP2\*<br /><br />➕ 2003 |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 2.0

[New features](/previous-versions/visualstudio/visual-studio-2008/t357fb32(v=vs.90)):

- Generics
- Debugger edit and continue
- Improved scalability and performance
- ClickOnce deployment
- In ASP.NET 2.0, new controls and support for a broad array of browsers
- 64-bit support

|                               | Versions                                  |
|-------------------------------|-------------------------------------------|
| **CLR**                       | 2.0                                       |
| **Included in Visual Studio** | 2005                                      |
| **Windows**                   | N/A                                       |
| **Windows Server**            | ✔️ 2008 R2 SP1<br />✔️ 2008 SP2<br />✔️ 2003 |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 1.1

[New features](/previous-versions/visualstudio/visual-studio-2008/h88tthh0(v=vs.90)):

- ASP.NET mobile controls
- Side-by-side execution
- IPv6 support

|                               | Versions |
|-------------------------------|----------|
| **CLR**                       | 1.1      |
| **Included in Visual Studio** | 2003     |
| **Windows**                   | N/A      |
| **Windows Server**            | ✔️ 2003 |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

### .NET Framework 1.0

|                               | Versions           |
|-------------------------------|--------------------|
| **CLR**                       | 1.0                |
| **Included in Visual Studio** | Visual Studio .NET |
| **Windows**                   | N/A                |
| **Windows Server**            | N/A                |

**To determine installed .NET version**: See [instructions](how-to-determine-which-versions-are-installed.md).

> [!NOTE]
>
> - .NET Framework must be enabled on this operating system through [Control Panel (for Windows)](dotnet-35-windows.md#enable-net-framework-35-on-windows) or the [Server Manager (for Windows Server)](dotnet-35-windows.md#enable-net-framework-35-on-windows-server).
> - In general, you should not uninstall any versions of .NET Framework that are installed on your computer, because an application you use may depend on a specific version and may break if that version is removed. You can load multiple versions of .NET Framework on a single computer at the same time. This means that you can install .NET Framework without having to uninstall previous versions. For more information, see [Getting Started](../get-started/index.md).

## Remarks for version 4.5 and later

.NET Framework 4.5 is an in-place update that replaces .NET Framework 4 on your computer, and similarly, .NET Framework 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, and 4.8 are in-place updates to .NET Framework 4.5. In-place update means that they use the same runtime version, but the assembly versions are updated and include new types and members. After you install one of these updates, your .NET Framework 4, .NET Framework 4.5, .NET Framework 4.6, or .NET Framework 4.7 apps should continue to run without requiring recompilation. However, the reverse is not true. We do not recommend running apps that target a later version of .NET Framework on an earlier version. For example, we do not recommend that you run an app the targets .NET Framework 4.6 on .NET Framework 4.5.

The following guidelines apply:

- In Visual Studio, you can choose .NET Framework 4.5 as the target framework for a project (this sets the <xref:Microsoft.Build.Tasks.GetReferenceAssemblyPaths.TargetFrameworkMoniker%2A?displayProperty=nameWithType> property) to compile the project as a .NET Framework 4.5 assembly or executable. This assembly or executable can then be used on any computer that has .NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, or 4.8 installed.

- In Visual Studio, you can choose .NET Framework 4.5.1 as the target framework for a project to compile it as a .NET Framework 4.5.1 assembly or executable. Only run this assembly or executable on computers that have .NET Framework 4.5.1 or later installed. An executable that targets .NET Framework 4.5.1 will be blocked from running on a computer that only has an earlier version of .NET Framework, such as .NET Framework 4.5, installed. The user will be prompted to install .NET Framework 4.5.1. In addition, .NET Framework 4.5.1 assemblies should not be called from an app that targets an earlier version of .NET Framework, such as .NET Framework 4.5.

  > [!NOTE]
  > .NET Framework 4.5.1 and .NET Framework 4.5 are used here only as examples. The principle described applies to any app that targets a later version of .NET Framework than the one installed on the system on which it's running.

Some changes in .NET Framework may require changes to your app code; see [Application Compatibility](../migration-guide/application-compatibility.md) before you run your existing apps with .NET Framework 4.5 or later versions. For more information about installing the current version, see [Install the .NET Framework for developers](guide-for-developers.md). For information about support for the .NET Framework, see [.NET Framework official support policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework) on the .NET website.

## Remarks for older versions

.NET Framework versions 2.0, 3.0, and 3.5 are built with the same version of the CLR (CLR 2.0). These versions represent successive layers of a single installation. Each version is built incrementally on top of the earlier versions. It's not possible to run versions 2.0, 3.0, and 3.5 side by side on a computer. When you install version 3.5, you get the 2.0 and 3.0 layers automatically, and apps that were built for versions 2.0, 3.0, and 3.5 can all run on version 3.5. However, .NET Framework 4 ends this layering approach, and it and later releases (.NET Framework 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, and 4.8) also represent successive layers of a single installation. Starting with .NET Framework 4, you can use in-process, side by side hosting to run multiple versions of the CLR in a single process. For more information, see [Assemblies and Side-by-Side Execution](../../standard/assembly/side-by-side-execution.md).

In addition, if your app targets version 2.0, 3.0, or 3.5, your users may be required to enable .NET Framework 3.5 on a Windows 8, Windows 8.1, or Windows 10 computer before they can run your app. For more information, see [Install the .NET Framework 3.5 on Windows 11, Windows 10, Windows 8.1, and Windows 8](dotnet-35-windows.md).

[!INCLUDE [net-framework-vs](../../../includes/net-framework-vs.md)]

## Next steps

- If you're new to the .NET Framework, see the [overview](../get-started/overview.md) for an introduction to key concepts and features.

- For new features and improvements in the .NET Framework 4.5 and its point releases, see [What's new in the .NET Framework](../whats-new/index.md).

- For information about migrating your app to a newer version of the .NET Framework, see the [migration guide](index.md).

- For information about determining which versions or updates are installed on a computer, see [How to: Determine Which .NET Framework Versions Are Installed](how-to-determine-which-versions-are-installed.md) and [How to: Determine Which .NET Framework Updates Are Installed](how-to-determine-which-net-framework-updates-are-installed.md).

## See also

- [Version compatibility](../migration-guide/version-compatibility.md)
- [.NET Framework official support policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)
- [Troubleshoot blocked .NET Framework installations and uninstallations](troubleshoot-blocked-installations-and-uninstallations.md)
