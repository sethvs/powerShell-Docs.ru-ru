# Изменения объекта FileInfo
Сведения о версии файла могут вводить пользователя в заблуждение, особенно в случаях, когда файл был исправлен. В этом выпуске WMF 5.0 новые свойства сценариев **FileVersionRaw** и **ProductVersionRaw** 
добавлены в объекты FileInfo. Ниже приведены свойства, отображаемые для powershell.exe (при условии, что $pid является идентификатором процесса PowerShell).

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117


<!--HONumber=Apr16_HO3-->


