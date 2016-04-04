# Защита MOF-файла

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

DSC сообщает целевым узлам об их конфигурации, отправляя каждому узлу MOF-файл с этой информацией. После этого локальный диспетчер конфигураций (LCM) развертывает требуемую конфигурацию на каждом узле. Так как этот файл содержит сведения о конфигурации, его защита очень важна. Для защиты файла можно настроить проверку учетных данных пользователя в локальном диспетчере конфигураций. В этом разделе описано, как безопасно передать эти учетные данные на целевой узел путем их шифрования с помощью сертификатов.

## Необходимые компоненты

Чтобы успешно шифровать учетные данные, используемые для защиты конфигурации DSC, вам необходимо следующее:

* Какие-либо средства выпуска и распространения сертификатов. В этом разделе и примерах в нем предполагается, что вы используете центр сертификации Active Directory. Дополнительные сведения о службах сертификации Active Directory см. в статьях Общие сведения о службах сертификации Active Directory и Службы сертификации Active Directory в Windows Server 2008.
* Административный доступ к целевому узлу или узлам.
* У каждого целевого узла должен быть сертификат с поддержкой шифрования, сохраненный в личном хранилище этого узла. В Windows PowerShell путь к этому хранилищу будет таким: "Cert:\LocalMachine\My". В примерах в этом разделе используется шаблон "Проверка подлинности рабочей станции", который (вместе с другими шаблонами сертификатов) можно найти в разделе Шаблоны сертификатов по умолчанию.
* Если вы будете запускать эту конфигурацию не на целевом узле, экспортируйте открытый ключ сертификата, а затем импортируйте его на компьютер, на котором будете запускать конфигурацию. Убедитесь, что вы экспортируете только открытый ключ; закрытый ключ должен оставаться конфиденциальным.

## Общее описание процесса

 1. Настройте сертификаты, ключи и отпечатки, убедившись, что на каждом целевом узле есть копия сертификата и на компьютере конфигурации есть открытый ключ и отпечаток.
 2. Создайте блок данных конфигурации, содержащий путь и отпечаток для открытого ключа.
 3. Создайте сценарий конфигурации, который определяет нужную конфигурацию целевого узла и настраивает шифрование на целевых узлах, заставляя локальный диспетчер конфигураций расшифровывать данные конфигурации с помощью сертификата и его отпечатка.
 4. Запустите конфигурацию, которая задает параметры локального диспетчера конфигураций и запускает конфигурацию DSC.

![Diagram1](images/CredentialEncryptionDiagram1.png)

## Требования к сертификатам

Для применения шифрования учетных данных на целевом узле должен быть доступен сертификат открытого ключа, который является доверенным для компьютера, используемого для создания конфигурации DSC.
Сертификат открытого ключа имеет определенные требования, которые должны быть удовлетворены, чтобы его можно было использовать для шифрования учетных данных DSC.
 1. Использование ключа:
   - Должен содержать: "KeyEncipherment" и "DataEncipherment".
   - Не должен содержать: "Digital Signature".
 2. Расширенное использование ключа:
   - Должен содержать: "Document Encryption" (1.3.6.1.4.1.311.80.1).
   - Не должен содержать: "Client Authentication" (1.3.6.1.5.5.7.3.2) и "Server Authentication" (1.3.6.1.5.5.7.3.1).
 3. Закрытый ключ для сертификата доступен на целевом узле.
 
Рекомендация. Хотя можно использовать сертификат с использованием ключа типа "Digital Signature" или одним из вариантов расширенного использования ключа для проверки подлинности, это облегчит использование ключа не по назначению и сделает ключ более уязвимым для атаки. Поэтому рекомендуется использовать сертификат, созданный специально для защиты учетных данных DSC. В этом сертификате не применяются указанные типы использования ключа и расширенного использования ключа.
  
Для защиты учетных данных DSC можно использовать любой существующий сертификат на целевом узле, удовлетворяющий этим критериям.
 
## Создание сертификата

Сертификат закрытого ключа можно создать на целевом узле, а сертификат открытого ключа — скопировать на компьютер, используемый для компиляции конфигурации DSC в MOF-файл.

Другой вариант — создать сертификат закрытого ключа на компьютере, который используется для компиляции файла конфигурации DSC, экспортировать его с закрытым ключом и затем импортировать на целевой узел. Это текущий метод шифрования учетных данных DSC на сервере Nano. 

## Данные конфигурации

Блок данных конфигурации определяет, какие целевые узлы использовать, следует ли шифровать учетные данные, какие средства шифрования использовать и т. д. Дополнительные сведения о блоке данных конфигурации см. в разделе Разделение данных конфигурации и данных среды.

Ниже перечислены элементы, связанные с учетными данными шифрования, которые можно настроить для каждого узла:
* NodeName — имя целевого узла, для которого настраивается шифрование учетных данных.
* PsDscAllowPlainTextPassword — определяет, могут ли незашифрованные учетные данные передаваться на этот узел. Это делать не рекомендуется.
* Thumbprint — отпечаток сертификата, который будет использоваться для расшифровки учетных данных в конфигурации DSC на целевом узле. **Этот сертификат должен существовать в хранилище сертификатов локального компьютера на целевом узле.**
* CertificateFile — файл сертификата (содержащий только открытый ключ), который следует использовать для шифрования учетных данных для целевого узла. Формат этого файла сертификата — двоичный стандарт X.509 в кодировке DER или Base-64.

В этом примере показан блок данных конфигурации, в котором определен целевой узел для обработки, называемый targetNode, путь к файлу сертификата открытого ключа (с именем targetNode.cer) и отпечаток открытого ключа.

```powershell
$ConfigData= @{ 
    AllNodes = @(     
            @{  
                # The name of the node we are describing 
                NodeName = "targetNode" 

                # The path to the .cer file containing the 
                # public key of the Encryption Certificate 
                # used to encrypt credentials for this node 
                CertificateFile = "C:\publicKeys\targetNode.cer" 

         
                # The thumbprint of the Encryption Certificate 
                # used to decrypt the credentials on target node 
                Thumbprint = "AC23EA3A9E291A75757A556D0B71CBBF8C4F6FD8" 
            }; 
        );    
    }
```

## Сценарий конфигурации

В самом сценарии конфигурации используйте параметр `PsCredential`, чтобы учетные данные хранились в течение минимально возможного срока. При запуске этого примера DSC запросит у вас учетные данные и затем зашифрует MOF-файл с помощью сертификата CertificateFile, который связан с этим целевым узлом в блоке данных конфигурации. В этом коде файл копируется из общей папки, которая защищена для пользователя.

```
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
    } 
}
```

## Настройка расшифровки

Перед началом работы `Start-DscConfiguration` вам необходимо сообщить локальному диспетчеру конфигураций каждого целевого узла, какой сертификат необходимо использовать для расшифровки учетных данных с помощью ресурса CertificateID для проверки отпечатка сертификата. Этот пример функции найдет соответствующий локальный сертификат (может потребоваться изменить его так, чтобы он нашел именно тот сертификат, который вы хотите использовать):

```powershell
# Get the certificate that works for encryption 
function Get-LocalEncryptionCertificateThumbprint 
{ 
    (dir Cert:\LocalMachine\my) | %{
        # Verify the certificate is for Encryption and valid 
        if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify()) 
        { 
            return $_.Thumbprint 
        } 
    } 
}
```

С сертификатом, который определяется отпечатком, можно обновить сценарий конфигурации, чтобы он использовал это значение:

```powershell
configuration CredentialEncryptionExample 
{ 
    param( 
        [Parameter(Mandatory=$true)] 
        [ValidateNotNullorEmpty()] 
        [PsCredential] $credential 
        ) 
    

    Node $AllNodes.NodeName 
    { 
        File exampleFile 
        { 
            SourcePath = "\\Server\share\path\file.ext" 
            DestinationPath = "C:\destinationPath" 
            Credential = $credential 
        } 
        
        LocalConfigurationManager 
        { 
             CertificateId = $node.Thumbprint 
        } 
    } 
}
```

## Выполнение конфигурации

На этом этапе можно запустить конфигурацию, в результате чего вы получите два выходных файла:

 * Файл *. meta.mof, настраивающий расшифровку учетных данных в локальном диспетчере конфигураций с помощью сертификата, который хранится в хранилище локального компьютера и определяется его отпечатком. `Set-DscLocalConfigurationManager` применяет файл *.meta.mof.
 * MOF-файл, который фактически применяет конфигурацию. Командлет Start-DscConfiguration применяет конфигурацию.

Эти команды выполнят следующие действия:

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

В этом примере конфигурация DSC будет принудительно отправляться на целевой узел.
Конфигурацию DSC также можно применить с помощью опрашивающего сервера DSC, если он доступен.

Дополнительные сведения о применении конфигурации DSC с помощью опрашивающего сервера DSC приведены на этой странице.

## Пример модуля шифрования учетных данных

Ниже приведен полный пример, включающий все эти действия, а также вспомогательный командлет, который экспортирует и копирует открытые ключи:

```powershell
# A simple example of using credentials
configuration CredentialEncryptionExample
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $credential
        )
    

    Node $AllNodes.NodeName
    {
        File exampleFile
        {
            SourcePath = "\\server\share\file.txt"
            DestinationPath = "C:\Users\user"
            Credential = $credential
        }
        
        LocalConfigurationManager
        {
            CertificateId = $node.Thumbprint
        }
    }
}

# A Helper to invoke the configuration, with the correct public key 
# To encrypt the configuration credentials
function Start-CredentialEncryptionExample
{
    [CmdletBinding()]
    param ($computerName)


    [string] $thumbprint = Get-EncryptionCertificate -computerName $computerName -Verbose
    Write-Verbose "using cert: $thumbprint"

    $certificatePath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"         

    $ConfigData=    @{
        AllNodes = @(     
                        @{  
                            # The name of the node we are describing
                            NodeName = "$computerName"

                            # The path to the .cer file containing the
                            # public key of the Encryption Certificate
                            CertificateFile = "$certificatePath"

                            # The thumbprint of the Encryption Certificate
                            # used to decrypt the credentials
                            Thumbprint = $thumbprint
                        };
                    );    
    }

    Write-Verbose "Generate DSC Configuration..."
    CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample `
        -credential (Get-Credential -UserName "$env:USERDOMAIN\$env:USERNAME" -Message "Enter credentials for configuration") 

    Write-Verbose "Setting up LCM to decrypt credentials..."
    Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 

    Write-Verbose "Starting Configuration..."
    Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose

}


#region HelperFunctions

# The folder name for the exported public keys
$script:publicKeyFolder = "publicKeys"

# Get the certificate that works for encryptions
function Get-EncryptionCertificate
{
    [CmdletBinding()]
    param ($computerName)
    $returnValue= Invoke-Command -ComputerName $computerName -ScriptBlock {
            $certificates = dir Cert:\LocalMachine\my

            $certificates | %{
                    # Verify the certificate is for Encryption and valid
                    if ($_.PrivateKey.KeyExchangeAlgorithm -and $_.Verify())
                    {
                        # Create the folder to hold the exported public key
                        $folder= Join-Path -Path $env:SystemDrive\ -ChildPath $using:publicKeyFolder
                        if (! (Test-Path $folder))
                        {
                            md $folder | Out-Null
                        }

                        # Export the public key to a well known location
                        $certPath = Export-Certificate -Cert $_ -FilePath (Join-Path -path $folder -childPath "EncryptionCertificate.cer") 

                        # Return the thumbprint, and exported certificate path
                        return @($_.Thumbprint,$certPath);
                    }
                  }
        }
    Write-Verbose "Identified and exported cert..."
    # Copy the exported certificate locally
    $destinationPath = join-path -Path "$env:SystemDrive\$script:publicKeyFolder" -childPath "$computername.EncryptionCertificate.cer"
    Copy-Item -Path (join-path -path \\$computername -childPath $returnValue[1].FullName.Replace(":","$"))  $destinationPath | Out-Null

    # Return the thumbprint
    return $returnValue[0]
}

Start-CredentialEncryptionExample
```

<!--HONumber=Mar16_HO4-->


