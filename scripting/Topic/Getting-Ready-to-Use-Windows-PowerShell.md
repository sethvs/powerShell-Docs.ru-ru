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
После установки и запуска [!INCLUDE[wps_2](../Token/wps_2_md.md)] рассмотрите следующие варианты настройки. Эти задачи можно выполнить в любое время.

-   **Установка файлов справки.** Командлеты, которые включены в [!INCLUDE[psversion3](../Token/psversion3_md.md)], поставляются без файлов справки. Однако можно воспользоваться командлетом [Update-Help](assetId:///93e1d870-ace6-432b-8778-8920291d7545), чтобы скачать и установить актуальные файлы справки. При установке файлов можно использовать командлет [Get-Help](assetId:///1f46eeb4-49d7-4bec-bb29-395d9b42f54a), чтобы отображать их прямо в командной строке. Дополнительные сведения см. в статье [about_Updatable_Help](assetId:///10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

    Если вы решаете не устанавливать файлы справки, с ними можно ознакомиться в Интернете. Чтобы открыть интернет-версию раздела справки для любого командлета, введите `Get-Help <CmdletName> -Online`. Для просмотра разделов справки [!INCLUDE[wps_2](../Token/wps_2_md.md)] в библиотеке TechNet начните с [http://go.microsoft.com/fwlink/?LinkID=107116](http://go.microsoft.com/fwlink/?LinkID=107116).

-   **Запуск сценариев.** Для обеспечения безопасности [!INCLUDE[mshshort](../Token/mshshort_md.md)] к [!INCLUDE[mshshort](../Token/mshshort_md.md)] по умолчанию применяется политика выполнения **Restricted**. Она позволяет выполнять командлеты, но не сценарии. Для запуска сценариев используйте командлет [Set-ExecutionPolicy[PSITPro5_Security]](assetId:///5690a0e1-495b-4e63-8280-65ead7bf01ab), чтобы изменить политику выполнения на **AllSigned** или **RemoteSigned**. Этот командлет могут запускать только члены группы администраторов на компьютере. Подробнее см. в статье [about_Execution_Policies [v4]](assetId:///347708dc-1515-4d74-978b-8334603472e6).

-   **Включение удаленного взаимодействия.** Система уже настроена для выполнения удаленных команд на других компьютерах. В [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] и [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] система также настроена для получения удаленных команд, то есть чтобы другие компьютеры могли выполнять удаленные команды на локальном компьютере. Чтобы разрешить компьютерам под управлением других версий Windows получать удаленные команды, запустите командлет [Enable-PSRemoting](assetId:///19437c28-33b8-4ac1-9113-8439cc8beffb) на компьютере, предназначенном для удаленного управления. Этот командлет могут запускать только члены группы администраторов на компьютере. Дополнительные сведения см. в статье [about_Remote](assetId:///9b4a5c87-9162-4adf-bdfe-fbc80b9b8970).

    ПРИМЕЧАНИЕ. Если удаленное взаимодействие включено на компьютере, где выполняется [!INCLUDE[psversion2](../Token/psversion2_md.md)], оно остается разрешенным после установки [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)]. Однако в [!INCLUDE[lserver](../Token/lserver_md.md)] (не [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)]) необходимо повторно включить удаленное взаимодействие после установки [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)].

## См. также
[Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md)
[Запуск Windows PowerShell [ps]](assetId:///8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)



<!--HONumber=Apr16_HO1-->


