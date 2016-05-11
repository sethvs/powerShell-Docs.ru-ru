# Командлеты Clipboard
Командлеты**Get-Clipboard** и **Set-Clipboard** упрощают передачу содержимого в сеанс Windows PowerShell и из него. Например, если скопировать три файла с помощью проводника Windows
в буфер обмена (скажем, выбрав их и нажав клавишу `ctrl-c`), можно затем легко получить содержимое буфера обмена в виде списка файлов:

```powershell 
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


Командлеты Clipboard поддерживают изображения, звуковые файлы, списки файлов и текст.


<!--HONumber=Apr16_HO3-->


