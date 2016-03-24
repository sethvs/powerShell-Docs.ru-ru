# Командлеты Clipboard
Командлеты**Get-Clipboard** и **Set-Clipboard** упрощают передачу содержимого в сеанс Windows PowerShell и из него. В следующем примере для копирования трех файлов используется проводник:

Теперь можно легко получить доступ к содержимому буфера обмена в виде списка файлов:

PS C:\\&gt; Get-Clipboard -Format FileDropList

Каталог: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt

Командлеты Clipboard поддерживают изображения, звуковые файлы, списки файлов и текст.
<!--HONumber=Mar16_HO2-->
