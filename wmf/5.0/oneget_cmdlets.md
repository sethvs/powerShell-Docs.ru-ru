# Командлеты PackageManagement
Это основная составляющая PackageManagement, отвечающая за поддержку обнаружения, установки и инвентаризации программного обеспечения. Попробуйте использовать для выполнения этих операций следующие командлеты:
-   Find-Package
-   Find-PackageProvider
-   Get-Package
-   Get-PackageProvider
-   Get-PackageSource
-   Import-PackageProvider
-   Install-Package
-   Install-PackageProvider
-   Register-PackageSource
-   Save-Package
-   Set-PackageSource
-   Uninstall-Package
-   Unregister-PackageSource

Поскольку PackageManagement является модулем PowerShell, можно обновить сам PackageManagement следующим образом:
```powershell
PS C:\> Install-Module PackageManagement –Force
```
В этом случае потребуется повторно войти в сеанс PowerShell, чтобы переключиться на новую версию PackageManagement.

## [Командлет Find-Package](https://technet.microsoft.com/en-us/library/dn890709.aspx)
Этот командлет обеспечивает обнаружения пакетов программного обеспечения в доступных источниках с помощью загруженных поставщиков пакетов.
```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -Provider PowerShellGet -Source PSGallery

# Find a package from a provider that is not yet installed
# This will bootstrap NuGet provider and then search for jquery package using NuGet
# with <http://www.nuget.org/api/v2/> as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## [Командлет Find-PackageProvider](https://technet.microsoft.com/en-us/library/mt676544.aspx)
Командлет Find-PackageProvider находит подходящие поставщики PackageManagement, которые доступны в зарегистрированных источниках пакетов PowerShellGet. Эти поставщики пакетов можно установить с помощью командлета Install-PackageProvider. По умолчанию сюда относятся модули, доступные в коллекции PowerShell с тегами PackageManagement и Provider. 

Кроме того, Find-PackageProvider находит совпадающие поставщики PackageManagement, доступные в хранилище BLOB-объектов Azure PackageManagement, где для их поиска и установки используется поставщик начального загрузчика PackageManagement.
```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## [Командлет Get-Package](https://technet.microsoft.com/en-us/library/dn890704.aspx)
Этот командлет возвращает список всех пакетов программного обеспечения, установленных с помощью PackageManagement.
```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## [Командлет Get-PackageProvider](https://technet.microsoft.com/en-us/library/dn890703.aspx)
С помощью этого командлета можно выполнить инвентаризацию поставщиков пакетов, которые уже загружены и готовы к использованию на локальном компьютере.
```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## [Командлет Get-PackageSource](https://technet.microsoft.com/en-us/library/dn890705.aspx)
Этот командлет возвращает список источников пакетов, зарегистрированных для поставщика пакетов.
```powershelll
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## [Командлет Import-PackageProvider](https://technet.microsoft.com/en-us/library/mt676545.aspx)
Этот командлет добавляет поставщиков пакетов для управления пакетами в текущий сеанс.
```powershell
# Import a package provider from the local machine
Import-PackageProvider –Name MyProvider

#The -Name parameter can be either the name of the provider or the full path to the provider. Currently, we support .dll, .exe and.psm1 for the full path case. If the name of the provider is used for the -Name parameter, then additional version parameters such as -RequiredVersion, -MinimumVersion and -MaximumVersion may be specified. Otherwise, the latest version of the provider will be imported.

#If a package provider is not yet loaded to your system, we can discover and install on-demand. You can use explicit discovery and install cmdlets to do so:
 Find-PackageProvider
 Install-PackageProvider –Name MyProvider

#After installed, follow the Import-PackageProvider to load it to your system.

# Import a specific version of a package provider. PackageManagement supports installations of multiple versions of a package provider using PackageProvider cmdlets (not by bootstrapper provider). You can install another version of a package provider given that you already have one up running by:
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force
Get-PackageProvider –ListAvailable
Import-PackageProvider –Name "Nuget" -RequiredVersion "2.8.5.201" -Verbose
Import-PackageProvider –Name MyProvider –RequiredVersion xxxx -force
```

##[ Командлет Install-Package](https://technet.microsoft.com/en-us/library/dn890711.aspx)

Этот командлет обеспечивает установку пакетов программного обеспечения в доступных источниках с помощью загруженных поставщиков пакетов.
```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## [Командлет Install-PackageProvider](https://technet.microsoft.com/en-us/library/mt676543.aspx)
Этот командлет устанавливает один или несколько поставщиков пакетов для управления пакетами.
```powershell
# Install a package provider from the PowerShell Gallery
Install-PackageProvider –Name "Gistprovider" -Verbose

# Install a specified version of a package provider
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force

# Find a provider and install it
Find-PackageProvider –Name "Gistprovider" | Install-PackageProvider -Verbose

# Install a provider to the current user’s module folder
Install-PackageProvider –Name Gistprovider –Verbose –Scope CurrentUser
```

## [Командлет Register-PackageSource](https://technet.microsoft.com/en-us/library/dn890701.aspx)
Этот командлет добавляет источник пакетов для указанного поставщика пакетов.
Каждый поставщик PackageManagement может иметь один или несколько источников программного обеспечения или репозиториев. PackageManagement предоставляет командлеты PowerShell для добавления, удаления и запроса источника. Например, можно зарегистрировать источник пакетов для поставщика NuGet:
```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## [Командлет Save-Package](https://technet.microsoft.com/en-us/library/dn890708.aspx)
Этот командлет сохраняет пакеты на локальном компьютере без установки.
```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -source c:\test
```

## [Командлет Set-PackageSource](https://technet.microsoft.com/en-us/library/dn890710.aspx)
Этот командлет изменяет сведения о существующем источнике пакетов. 
```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2 
```

## [Командлет Uninstall-Package](https://technet.microsoft.com/en-us/library/dn890702.aspx)
Этот командлет удаляет пакеты, установленные на локальном компьютере.
```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## [Командлет Unregister-PackageSource](https://technet.microsoft.com/en-us/library/dn890707.aspx)
```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```


<!--HONumber=Jun16_HO4-->


