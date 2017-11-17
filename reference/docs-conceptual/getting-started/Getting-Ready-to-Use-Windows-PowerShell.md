---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Подготовка к использованию Windows PowerShell"
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
ms.openlocfilehash: de09c74e938f11a130864b1620d6c169006a27be
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2017
---
# <a name="getting-ready-to-use-windows-powershell"></a>Подготовка к использованию Windows PowerShell
После установки и запуска Windows PowerShell рассмотрите следующие варианты настройки. Эти задачи можно выполнить в любое время.

- **Установка файлов справки.** Командлеты, которые включены в Windows PowerShell 3.0, поставляются без файлов справки. Однако можно воспользоваться командлетом [Update-Help](/powershell/module/microsoft.powershell.core/update-help), чтобы скачать и установить актуальные файлы справки. При установке файлов можно использовать командлет [Get-Help](/powershell/module/microsoft.powershell.core/get-help), чтобы отображать их прямо в командной строке. Дополнительные сведения см. в статье [about_Updatable_Help](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

    Если вы решаете не устанавливать файлы справки, с ними можно ознакомиться в Интернете. Чтобы открыть интернет-версию раздела справки для любого командлета, введите `Get-Help <CmdletName> -Online`. Для ознакомления с разделами справки Windows PowerShell см. [документацию по PowerShell](/powershell/scripting).

- **Запуск сценариев.** Для обеспечения безопасности Windows PowerShell политика выполнения по умолчанию в Windows PowerShell — **Ограничено**. Она позволяет выполнять командлеты, но не сценарии. Для запуска сценариев используйте командлет [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy), чтобы изменить политику выполнения на **AllSigned** или **RemoteSigned**. Этот командлет могут запускать только члены группы администраторов на компьютере. Подробнее см. в разделе [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

- **Включение удаленного взаимодействия.** Система уже настроена для выполнения удаленных команд на других компьютерах. В Windows Server 2012 R2 и Windows Server 2012 система также настроена для получения удаленных команд, то есть чтобы другие компьютеры могли выполнять удаленные команды на локальном компьютере. Чтобы разрешить компьютерам под управлением других версий Windows получать удаленные команды, запустите командлет [Enable-PSRemoting](/powershell/module/microsoft.powershell.core/enable-psremoting) на компьютере, предназначенном для удаленного управления. Этот командлет могут запускать только члены группы администраторов на компьютере. Дополнительные сведения см. в статье [about_Remote](/powershell/module/microsoft.powershell.core/about/about_remote).

    ПРИМЕЧАНИЕ. Если удаленное взаимодействие включено на компьютере, где выполняется Windows PowerShell 2.0, оно остается включенным после установки Windows Management Framework 3.0. Тем не менее в Windows Server 2008 (не Windows Server 2008 R2) после установки Windows Management Framework 3.0 удаленное взаимодействие потребуется включить повторно.

## <a name="see-also"></a>См. также
- [Установка Windows PowerShell](../setup/Installing-Windows-PowerShell.md)
- [Запуск Windows PowerShell](/powershell/scripting/setup/starting-windows-powershell)

