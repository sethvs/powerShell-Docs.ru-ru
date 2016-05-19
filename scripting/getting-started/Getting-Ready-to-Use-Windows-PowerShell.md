---
title: Подготовка к использованию Windows PowerShell
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
---
# Подготовка к использованию Windows PowerShell
После установки и запуска Windows PowerShell рассмотрите следующие варианты настройки. Эти задачи можно выполнить в любое время.

-   **Установка файлов справки.** Командлеты, которые включены в Windows PowerShell 3.0, поставляются без файлов справки. Однако можно воспользоваться командлетом [Update-Help](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545), чтобы скачать и установить актуальные файлы справки. При установке файлов можно использовать командлет [Get-Help](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a), чтобы отображать их прямо в командной строке. Дополнительные сведения см. в разделе [about_Updatable_Help](https://technet.microsoft.com/en-us/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe)..

    Если вы решаете не устанавливать файлы справки, с ними можно ознакомиться в Интернете. Чтобы открыть интернет-версию раздела справки для любого командлета, введите `Get-Help <CmdletName> -Online`. Для просмотра разделов справки Windows PowerShell в библиотеке TechNet начните со страницы [http://go.microsoft.com/fwlink/?LinkID=107116](http://go.microsoft.com/fwlink/?LinkID=107116)..

-   **Запуск сценариев.** Для обеспечения безопасности Windows PowerShell политика выполнения по умолчанию в Windows PowerShell — **Ограничено**. Она позволяет выполнять командлеты, но не сценарии. Для запуска сценариев используйте командлет [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/en-us/library/5690a0e1-495b-4e63-8280-65ead7bf01ab), чтобы изменить политику выполнения на **AllSigned** или **RemoteSigned**. Этот командлет могут запускать только члены группы администраторов на компьютере. Подробнее см. в статье [about_Execution_Policies [v4]](https://technet.microsoft.com/en-us/library/347708dc-1515-4d74-978b-8334603472e6)..

-   **Включение удаленного взаимодействия.** Система уже настроена для выполнения удаленных команд на других компьютерах. В Windows Server 2012 R2 и Windows Server 2012 система также настроена для получения удаленных команд, то есть чтобы другие компьютеры могли выполнять удаленные команды на локальном компьютере. Чтобы разрешить компьютерам под управлением других версий Windows получать удаленные команды, запустите командлет [Enable-PSRemoting](https://technet.microsoft.com/en-us/library/19437c28-33b8-4ac1-9113-8439cc8beffb) на компьютере, предназначенном для удаленного управления. Этот командлет могут запускать только члены группы администраторов на компьютере. Дополнительные сведения см. в статье [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)..

    ПРИМЕЧАНИЕ. Если удаленное взаимодействие включено на компьютере, где выполняется Windows PowerShell 2.0, оно остается включенным после установки Windows Management Framework 3.0. Тем не менее в Windows Server 2008 (не Windows Server 2008 R2) после установки Windows Management Framework 3.0 удаленное взаимодействие потребуется включить повторно.

## См. также
[Установка Windows PowerShell](../setup/Installing-Windows-PowerShell.md)
[Запуск Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)



<!--HONumber=May16_HO2-->


