---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: e8620cdeb90792e86d091d3e19a169f9dfa690f9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="known-issues-and-limitations" class="xliff"></a>
# Известные проблемы и ограничения

<a id="powershell-shortcuts-are-broken-when-used-for-the-first-time" class="xliff"></a>
PowerShell ярлыки перестают работать при первом использовании
------------------------------------------------------------

**Решение.** Выполните одно из следующих действий:

1.  Щелкните ярлык PowerShell правой кнопкой мыши. Выберите Windows PowerShell для запуска в режиме без повышенных прав.
2.  Щелкните ярлык PowerShell правой кнопкой мыши. Щелкните Windows PowerShell правой кнопкой мыши и выберите пункт "Запуск от имени администратора" для запуска в режиме с повышенными правами.

После выполнения любого из указанных действий ярлыки PowerShell будут работать. Эти действия требуется выполнить всего один раз.


<a id="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7" class="xliff"></a>
Модули PowerShell и ресурсы DSC выдает ошибки для ExecutionPolicy в Windows 7
-------------------------------------------------------------------------------------
В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.

**Решение.** Задайте для ExecutionPolicy значение RemoteSigned, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a id="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash" class="xliff"></a>
Подключение к старой удаленной конечной точки Exchange вызывает сбой
------------------------------------------------------------

Старая конечная точка Exchange выполняет перенаправление на новую конечную точку. В логике перенаправления имеется ошибка, которая вызывает сбой.

**Решение.** Подключитесь непосредственно к новой конечной точке.


<a id="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2" class="xliff"></a>
Функция инвентаризации программного обеспечения ошибочно остановлена после установки WMF 5.0 в Windows Server 2012 R2
-------------------------------------------------------------------------------------------------------------

При установке WMF 5.0 в Windows Server 2012 R2, где уже выполняется инвентаризации программного обеспечения, эта функция ошибочно останавливается после установки.

**Решение.** Запустите командлет Start-SilLogging один раз после установки WMF, так как процесс его установки ошибочно останавливает функцию инвентаризации программного обеспечения.

<a id="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together" class="xliff"></a>
Get-ChildItem не работает, если -LiteralPath и -Recurse используются совместно
--------------------------------------------------------------------------

Если имя каталога содержит недопустимый подстановочный знак, то Get-ChildItem не дает ожидаемые результаты при совместном использовании -LiteralPath и -Recurse.

**Решение.** В настоящее время обходной путь, хотя он и не является оптимальным, заключается в реализации рекурсии в скрипте вместо использования командлета.


<a id="sysprep-fails-after-wmf-50-installation" class="xliff"></a>
Sysprep не работает после установки WMF 5.0
----------------------------------------

Существует два способа решения этой проблемы в зависимости от используемой версии Windows Server.

**Решение**
- Для систем под управлением **Windows Server 2008 R2**
  1. Откройте PowerShell от имени администратора.
  2. Выполните следующую команду. 
  
  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. Выполните команду и пропустите ошибку, так как она ожидалась.
  
  ```powershell
    Publish-SilData
   ```
  4. Удалите файлы в каталоге \Windows\System32\Logfiles\SIL\.
  
  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. Установите все доступные важные обновления Windows и запустите Sysyprep в обычном режиме.
  
- Для систем под управлением **Windows Server 2012**
  1.    После установки WMF 5.0 на сервере, где предполагается выполнить Sysprep, войдите в систему как администратор.
  2.    Скопируйте файл Generize.xml из папки \Windows\System32\Sysprep\ActionFiles\ в расположение за пределами каталога Windows, например C:\.
  3.    Откройте копию Generalize.xml в блокноте.
  4.    Найдите и удалите следующий текст: нужно удалить по одному экземпляру каждой строки (они находятся ближе к концу документа).

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    Сохраните измененную копию Generalize.xml и закройте файл.
  6.    Откройте командную строку от имени администратора.
  7.    Выполните следующую команду, чтобы стать владельцем файла Generalize.xml в папке system32:

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```

  8.    Выполните следующую команду, чтобы установить соответствующее разрешение для доступа к файлу:

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F 
    ```
      * Ответьте "Да" в запросе на подтверждение. 
      * Обратите внимание, что `<AdministratorUserName>` следует заменить именем пользователя, который является администратором на данном компьютере. Например, "Administrator".
      
  9.    Скопируйте измененный и сохраненный файл в каталог Sysprep, используя следующую команду:

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```
      * В запросе ответьте "Да", чтобы перезаписать файл (если запрос на перезапись не появится, перепроверьте введенный путь).
      * Предполагается, что измененная копия Generalize.xml скопирована в каталог C:\.

  10.   Теперь файл Generalize.xml изменен. Запустите программу Sysprep с включенным параметром generalize.

