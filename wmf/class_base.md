# Объявление базового класса
Класс можно объявить Windows PowerShell в качестве базового типа для другого класса Windows PowerShell.

```PowerShell
class bar
{
   [int]foo() 
       {
           return 100500
       }
}

class baz : bar {}

[baz]::new().foo() # return 100500
```

Кроме того, можно использовать существующие типы .NET Framework в качестве базовых классов:

```PowerShell
class MyIntList : system.collections.generic.list[int]
{
    
}

$list = [MyIntList]::new()

$list.Add(100)

$list[0] # return 100
```<!--HONumber=Mar16_HO2-->
