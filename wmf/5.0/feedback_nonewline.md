# Параметр NoNewLine
**Out-File**, **Add-Content** и **Set-Content** теперь имеют новый параметр **–NoNewline**, который просто пропускает перевод на новую строку после выходных данных.
```PowerShell
PS C:\> "This is " | Out-File -FilePath Example.txt -NoNewline

PS C:\>; "a single " | Add-Content -Path Example.txt -NoNewline

PS C:\> "sentence." | Add-Content -Path Example.txt -NoNewline

PS C:\> Get-Content .\Example.txt

This is a single sentence.
```
Без параметра **–NoNewline** каждый фрагмент будет находиться на отдельной строке:
```PowerShell
PS C:\> "This is " | Out-File -FilePath Example.txt

PS C:\> "a single " | Add-Content -Path Example.txt

PS C:\> "sentence." | Add-Content -Path Example.txt

PS C:\> Get-Content .\Example.txt

This is

a single

sentence.
```


<!--HONumber=Jun16_HO4-->


