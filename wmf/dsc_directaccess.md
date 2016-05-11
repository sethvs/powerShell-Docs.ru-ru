# Прямой доступ к методам ресурсов DSC


Добавлен командлет `Invoke-DscResource` для прямого доступа к ресурсам DSC и их методам (Get, Set или Test). Он может использоваться третьими сторонами, желающими воспользоваться преимуществами ресурсов DSC. Этот командлет обычно используется в сочетании с `refreshMode = ‘Disabled’`, однако доступен независимо от значения refreshMode. Ниже приведено несколько примеров использования нового командлета:

## Проверка наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## Тестирование наличия файла

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## Получение содержимого файла

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```


<!--HONumber=Apr16_HO4-->


