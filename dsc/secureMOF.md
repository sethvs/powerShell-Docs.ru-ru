---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Защита MOF-файла"
ms.openlocfilehash: dc900f53c954637a407fbd026d24d20c2fdabf6e
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2017
---
# <a name="securing-the-mof-file"></a><span data-ttu-id="9b5e3-103">Защита MOF-файла</span><span class="sxs-lookup"><span data-stu-id="9b5e3-103">Securing the MOF File</span></span>

><span data-ttu-id="9b5e3-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9b5e3-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="9b5e3-105">DSC сообщает целевым узлам об их конфигурации, отправляя каждому узлу MOF-файл с этой информацией. После этого локальный диспетчер конфигураций (LCM) развертывает требуемую конфигурацию на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-105">DSC tells the target nodes what configuration they should have by sending a MOF file with that information to each node, where the Local Configuration Manager (LCM) implements the desired configuration.</span></span> <span data-ttu-id="9b5e3-106">Так как этот файл содержит сведения о конфигурации, его защита очень важна.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-106">Because this file contains the details of the configuration, it’s important to keep it secure.</span></span> <span data-ttu-id="9b5e3-107">Для этого можно настроить LCM для проверки учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-107">To do this, you can set the LCM to check the credentials of a user.</span></span> <span data-ttu-id="9b5e3-108">В этом разделе описано, как безопасно передать эти учетные данные на целевой узел путем их шифрования с помощью сертификатов.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-108">This topic describes how to transmit those credentials securely to the target node by encrypting them with certificates.</span></span>

><span data-ttu-id="9b5e3-109">**Примечание.** В этой статье описаны сертификаты, используемые для шифрования.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-109">**Note:** This topic discusses certificates used for encryption.</span></span> <span data-ttu-id="9b5e3-110">Самозаверяющего сертификата достаточно для шифрования, так как закрытый ключ всегда хранится в тайне, а шифрование не подразумевает доверие документа.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-110">For encryption, a self-signed certificate is sufficient, because the private key is always kept secret and encryption does not imply trust of the document.</span></span> <span data-ttu-id="9b5e3-111">Самозаверяющие сертификаты *не* следует использовать для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-111">Self-signed certificates should *not* be used for authentication purposes.</span></span> <span data-ttu-id="9b5e3-112">Для этого нужен сертификат из доверенного центра сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-112">You should use a certificate from a trusted Certification Authority (CA) for any authentication purposes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b5e3-113">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="9b5e3-113">Prerequisites</span></span>

<span data-ttu-id="9b5e3-114">Чтобы успешно шифровать учетные данные, используемые для защиты конфигурации DSC, вам необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-114">To successfully encrypt the credentials used to secure a DSC configuration, make sure you have the following:</span></span>

* <span data-ttu-id="9b5e3-115">**Какие-либо средства выпуска и распространения сертификатов**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-115">**Some means of issuing and distributing certificates**.</span></span> <span data-ttu-id="9b5e3-116">В этом разделе и примерах в нем предполагается, что вы используете центр сертификации Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-116">This topic and its examples assume you are using Active Directory Certification Authority.</span></span> <span data-ttu-id="9b5e3-117">Дополнительные сведения о службах сертификации Active Directory см. в статьях [Общие сведения о службах сертификации Active Directory](https://technet.microsoft.com/library/hh831740.aspx) и [Службы сертификации Active Directory в Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-117">For more background information on Active Directory Certificate Services, see [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) and [Active Directory Certificate Services in Windows Server 2008](https://technet.microsoft.com/windowsserver/dd448615.aspx).</span></span>
* <span data-ttu-id="9b5e3-118">**Административный доступ к целевому узлу или узлам**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-118">**Administrative access to the target node or nodes**.</span></span>
* <span data-ttu-id="9b5e3-119">**У каждого целевого узла должен быть сертификат с поддержкой шифрования, сохраненный в личном хранилище этого узла**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-119">**Each target node has an encryption-capable certificate saved its Personal Store**.</span></span> <span data-ttu-id="9b5e3-120">В Windows PowerShell путь к этому хранилищу будет таким: "Cert:\LocalMachine\My".</span><span class="sxs-lookup"><span data-stu-id="9b5e3-120">In Windows PowerShell, the path to the store is Cert:\LocalMachine\My.</span></span> <span data-ttu-id="9b5e3-121">В примерах в этом разделе используется шаблон "Проверка подлинности рабочей станции", который (вместе с другими шаблонами сертификатов) можно найти в разделе [Шаблоны сертификатов по умолчанию](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-121">The examples in this topic use the “workstation authentication” template, which you can find (along with other certificate templates) at [Default Certificate Templates](https://technet.microsoft.com/library/cc740061(v=WS.10).aspx).</span></span>
* <span data-ttu-id="9b5e3-122">Если вы будете запускать эту конфигурацию не на целевом узле, **экспортируйте открытый ключ сертификата**, а затем импортируйте его на компьютер, на котором будете запускать конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-122">If you will be running this configuration on a computer other than the target node, **export the public key of the certificate**, and then import it to the computer you will run the configuration from.</span></span> <span data-ttu-id="9b5e3-123">Убедитесь, что вы экспортируете только **открытый** ключ; закрытый ключ должен оставаться конфиденциальным.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-123">Make sure that you export only the **public** key; keep the private key secure.</span></span>

## <a name="overall-process"></a><span data-ttu-id="9b5e3-124">Общее описание процесса</span><span class="sxs-lookup"><span data-stu-id="9b5e3-124">Overall process</span></span>

 1. <span data-ttu-id="9b5e3-125">Настройте сертификаты, ключи и отпечатки, убедившись, что на каждом целевом узле есть копия сертификата и на компьютере конфигурации есть открытый ключ и отпечаток.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-125">Set up the certificates, keys, and thumbprints, making sure that each target node has copies of the certificate and the configuration computer has the public key and thumbprint.</span></span>
 2. <span data-ttu-id="9b5e3-126">Создайте блок данных конфигурации, содержащий путь и отпечаток для открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-126">Create a configuration data block that contains the path and thumbprint of the public key.</span></span>
 3. <span data-ttu-id="9b5e3-127">Создайте сценарий конфигурации, который определяет нужную конфигурацию целевого узла и настраивает шифрование на целевых узлах, заставляя локальный диспетчер конфигураций расшифровывать данные конфигурации с помощью сертификата и его отпечатка.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-127">Create a configuration script that defines your desired configuration for the target node and sets up decryption on the target nodes by commanding the Local Configuration manager to decrypt the configuration data using the certificate and its thumbprint.</span></span>
 4. <span data-ttu-id="9b5e3-128">Запустите конфигурацию, которая задает параметры локального диспетчера конфигураций и запускает конфигурацию DSC.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-128">Run the configuration, which will set the Local Configuration Manager settings and start the DSC configuration.</span></span>

![Diagram1](images/CredentialEncryptionDiagram1.png)

## <a name="certificate-requirements"></a><span data-ttu-id="9b5e3-130">Требования к сертификатам</span><span class="sxs-lookup"><span data-stu-id="9b5e3-130">Certificate Requirements</span></span>

<span data-ttu-id="9b5e3-131">Для применения шифрования учетных данных на _целевом узле_ должен быть доступен сертификат открытого ключа, который является **доверенным** для компьютера, используемого для создания конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-131">To enact credential encryption, a public key certificate must be available on the _Target Node_ that is **trusted** by the computer being used to author the DSC configuration.</span></span>
<span data-ttu-id="9b5e3-132">Чтобы сертификат открытого ключа можно было использовать для шифрования учетных данных DSC, он должен соответствовать определенным требованиям.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-132">This public key certificate has specific requirements for it to be used for DSC credential encryption:</span></span>
 1. <span data-ttu-id="9b5e3-133">**Использование ключа**:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-133">**Key Usage**:</span></span>
   - <span data-ttu-id="9b5e3-134">Должен содержать: "KeyEncipherment" и "DataEncipherment".</span><span class="sxs-lookup"><span data-stu-id="9b5e3-134">Must contain: 'KeyEncipherment' and 'DataEncipherment'.</span></span>
   - <span data-ttu-id="9b5e3-135">_Не_ должен содержать: "Digital Signature".</span><span class="sxs-lookup"><span data-stu-id="9b5e3-135">Should _not_ contain: 'Digital Signature'.</span></span>
 2. <span data-ttu-id="9b5e3-136">**Расширенное использование ключа**:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-136">**Enhanced Key Usage**:</span></span>
   - <span data-ttu-id="9b5e3-137">Должен содержать: "Document Encryption" (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-137">Must contain: Document Encryption (1.3.6.1.4.1.311.80.1).</span></span>
   - <span data-ttu-id="9b5e3-138">_Не_ должен содержать: "Client Authentication" (1.3.6.1.5.5.7.3.2) и "Server Authentication" (1.3.6.1.5.5.7.3.1).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-138">Should _not_ contain: Client Authentication (1.3.6.1.5.5.7.3.2) and Server Authentication (1.3.6.1.5.5.7.3.1).</span></span>
 3. <span data-ttu-id="9b5e3-139">Закрытый ключ для сертификата доступен на *целевом узле_.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-139">The Private Key for the certificate is available on the *Target Node_.</span></span>
 4. <span data-ttu-id="9b5e3-140">**Поставщиком** для сертификата должен быть "Microsoft RSA SChannel Cryptographic Provider".</span><span class="sxs-lookup"><span data-stu-id="9b5e3-140">The **Provider** for the certificate must be "Microsoft RSA SChannel Cryptographic Provider".</span></span>
 
><span data-ttu-id="9b5e3-141">**Рекомендация**. Хотя можно использовать сертификат с ключом типа "Digital Signature" или одним из вариантов расширенного использования ключа для аутентификации, это упростит использование ключа не по назначению и сделает ключ более уязвимым для атаки.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-141">**Recommended Best Practice:** Although you can use a certificate with containing a Key Usage of 'Digital Signature' or one of the Authentication EKU's, this will enable the encryption key to be more easily misused and vulnerable to attack.</span></span> <span data-ttu-id="9b5e3-142">Поэтому рекомендуется использовать сертификат, созданный специально для защиты учетных данных DSC. В этом сертификате не применяются указанные типы использования ключа и расширенного использования ключа.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-142">So it is best practice to use a certificate created specifically for the purpose of securing DSC credentials that omits these Key Usage and EKUs.</span></span>
  
<span data-ttu-id="9b5e3-143">Для защиты учетных данных DSC можно использовать любой существующий сертификат на _целевом узле_, удовлетворяющий этим критериям.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-143">Any existing certificate on the _Target Node_ that meets these criteria can be used to secure DSC credentials.</span></span>

## <a name="certificate-creation"></a><span data-ttu-id="9b5e3-144">Создание сертификата</span><span class="sxs-lookup"><span data-stu-id="9b5e3-144">Certificate creation</span></span>

<span data-ttu-id="9b5e3-145">Существует два способа создания и использования обязательного сертификата шифрования (пары открытого и закрытого ключей).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-145">There are two approaches you can take to create and use the required Encryption Certificate (public-private key pair).</span></span>

1. <span data-ttu-id="9b5e3-146">Создание сертификата на **целевом узле** и экспорт только открытого ключа на **узел разработки**</span><span class="sxs-lookup"><span data-stu-id="9b5e3-146">Create it on the **Target Node** and export just the public key to the **Authoring Node**</span></span>
2. <span data-ttu-id="9b5e3-147">Создание сертификата на **узле разработки** и экспорт всей пары ключей на **целевой узел**</span><span class="sxs-lookup"><span data-stu-id="9b5e3-147">Create it on the **Authoring Node** and export the entire key pair to the **Target Node**</span></span>

<span data-ttu-id="9b5e3-148">Рекомендуется первый способ, поскольку закрытый ключ, используемый для расшифровки учетных данных в MOF-файле, не покидает целевой узел.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-148">Method 1 is recommended because the private key used to decrypt credentials in the MOF stays on the Target Node at all times.</span></span>


### <a name="creating-the-certificate-on-the-target-node"></a><span data-ttu-id="9b5e3-149">Создание сертификата на целевом узле</span><span class="sxs-lookup"><span data-stu-id="9b5e3-149">Creating the Certificate on the Target Node</span></span>

<span data-ttu-id="9b5e3-150">Закрытый ключ следует хранить в тайне, так как он используется для расшифровки MOF-файла на **целевом узле**. Проще всего это сделать, создав сертификат закрытого ключа на **целевом узле** и скопировав **сертификат открытого ключа** на компьютер, используемый для разработки конфигурации DSC в MOF-файле.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-150">The private key must be kept secret, because is used to decrypt the MOF on the **Target Node** The easiest way to do that is to create the private key certificate on the **Target Node**, and copy the **public key certificate** to the computer being used to author the DSC configuration into a MOF file.</span></span>
<span data-ttu-id="9b5e3-151">В следующем примере</span><span class="sxs-lookup"><span data-stu-id="9b5e3-151">The following example:</span></span>
 1. <span data-ttu-id="9b5e3-152">сертификат создается на **целевом узле**;</span><span class="sxs-lookup"><span data-stu-id="9b5e3-152">creates a certificate on the **Target node**</span></span>
 2. <span data-ttu-id="9b5e3-153">сертификат открытого ключа экспортируется на **целевой узел**;</span><span class="sxs-lookup"><span data-stu-id="9b5e3-153">exports the public key certificate on the **Target node**.</span></span>
 3. <span data-ttu-id="9b5e3-154">сертификат открытого ключа импортируется в хранилище сертификатов **my** на **узле разработки**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-154">imports the public key certificate into the **my** certificate store on the **Authoring node**.</span></span>

#### <a name="on-the-target-node-create-and-export-the-certificate"></a><span data-ttu-id="9b5e3-155">На целевом узле: создание и экспорт сертификата</span><span class="sxs-lookup"><span data-stu-id="9b5e3-155">On the Target Node: create and export the certificate</span></span>
><span data-ttu-id="9b5e3-156">Узел разработки: Windows Server 2016 и Windows 10</span><span class="sxs-lookup"><span data-stu-id="9b5e3-156">Authoring Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
<span data-ttu-id="9b5e3-157">После экспорта файл ```DscPublicKey.cer``` потребуется скопировать на **узел разработки**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-157">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

><span data-ttu-id="9b5e3-158">Узел разработки: Windows Server 2012 R2 или Windows 8.1 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="9b5e3-158">Authoring Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="9b5e3-159">Поскольку командлет New-SelfSignedCertificate в операционных системах Windows, предшествующих Windows 10 и Windows Server 2016, не поддерживает параметр **Type**, для таких операционных систем необходим альтернативный способ создания этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-159">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="9b5e3-160">В этом случае можно использовать для создания сертификата программу ```makecert.exe``` или ```certutil.exe```.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-160">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="9b5e3-161">Альтернативным способом является [загрузка сценария New-SelfSignedCertificateEx.ps1 из центра сценариев Майкрософт](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) и использование этого файла для создания сертификата:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-161">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -StoreName 'My' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
```
<span data-ttu-id="9b5e3-162">После экспорта файл ```DscPublicKey.cer``` потребуется скопировать на **узел разработки**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-162">Once exported, the ```DscPublicKey.cer``` would need to be copied to the **Authoring Node**.</span></span>

#### <a name="on-the-authoring-node-import-the-certs-public-key"></a><span data-ttu-id="9b5e3-163">На узле разработки: импорт открытого ключа сертификата</span><span class="sxs-lookup"><span data-stu-id="9b5e3-163">On the Authoring Node: import the cert’s public key</span></span>
```powershell
# Import to the my store
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

### <a name="creating-the-certificate-on-the-authoring-node"></a><span data-ttu-id="9b5e3-164">Создание сертификата на узле разработки</span><span class="sxs-lookup"><span data-stu-id="9b5e3-164">Creating the Certificate on the Authoring Node</span></span>
<span data-ttu-id="9b5e3-165">Кроме того, сертификат шифрования можно создать на **узле разработки**, экспортировать его с **закрытым ключом** в виде PFX-файла, а затем импортировать на **целевой узел**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-165">Alternately, the encryption certificate can be created on the **Authoring Node**, exported with the **private key** as a PFX file and then imported on the **Target Node**.</span></span>
<span data-ttu-id="9b5e3-166">Это текущий метод реализации шифрования учетных данных DSC в системе _Nano Server_.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-166">This is the current method for implementing DSC credential encryption on _Nano Server_.</span></span>
<span data-ttu-id="9b5e3-167">Несмотря на то что PFX-файл защищен паролем, необходимо обеспечить его безопасность во время передачи.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-167">Although the PFX is secured with a password it should be kept secure during transit.</span></span>
<span data-ttu-id="9b5e3-168">В следующем примере</span><span class="sxs-lookup"><span data-stu-id="9b5e3-168">The following example:</span></span>
 1. <span data-ttu-id="9b5e3-169">сертификат создается на **узле разработки**;</span><span class="sxs-lookup"><span data-stu-id="9b5e3-169">creates a certificate on the **Authoring node**.</span></span>
 2. <span data-ttu-id="9b5e3-170">сертификат, включая закрытый ключ, экспортируется на **узел разработки**;</span><span class="sxs-lookup"><span data-stu-id="9b5e3-170">exports the certificate including the private key on the **Authoring node**.</span></span>
 3. <span data-ttu-id="9b5e3-171">закрытый ключ удаляется с **узла разработки**, однако сертификат открытого ключа сохраняется в хранилище **my**;</span><span class="sxs-lookup"><span data-stu-id="9b5e3-171">removes the private key from the **Authoring node**, but keeps the public key certificate in the **my** store.</span></span>
 4. <span data-ttu-id="9b5e3-172">сертификат открытого ключа импортируется в корневое хранилище сертификатов на **целевом узле разработки**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-172">imports the private key certificate into the root certificate store on the **Target node**.</span></span>
   - <span data-ttu-id="9b5e3-173">Его необходимо добавить в корневое хранилище, чтобы **целевой узел** считал его надежным.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-173">it must be added to the root store so that it will be trusted by the **Target node**.</span></span>

#### <a name="on-the-authoring-node-create-and-export-the-certificate"></a><span data-ttu-id="9b5e3-174">На узле разработки: создание и экспорт сертификата</span><span class="sxs-lookup"><span data-stu-id="9b5e3-174">On the Authoring Node: create and export the certificate</span></span>
><span data-ttu-id="9b5e3-175">Целевой узел: Windows Server 2016 и Windows 10</span><span class="sxs-lookup"><span data-stu-id="9b5e3-175">Target Node: Windows Server 2016 and Windows 10</span></span>

```powershell
# note: These steps need to be performed in an Administrator PowerShell session
$cert = New-SelfSignedCertificate -Type DocumentEncryptionCertLegacyCsp -DnsName 'DscEncryptionCert' -HashAlgorithm SHA256
# export the private key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```
<span data-ttu-id="9b5e3-176">После экспорта файл ```DscPrivateKey.pfx``` потребуется скопировать на **целевой узел**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-176">Once exported, the ```DscPrivateKey.pfx``` would need to be copied to the **Target Node**.</span></span>

><span data-ttu-id="9b5e3-177">Целевой узел: Windows Server 2012 R2 или Windows 8.1 и более ранних версий</span><span class="sxs-lookup"><span data-stu-id="9b5e3-177">Target Node: Windows Server 2012 R2/Windows 8.1 and earlier</span></span>

<span data-ttu-id="9b5e3-178">Поскольку командлет New-SelfSignedCertificate в операционных системах Windows, предшествующих Windows 10 и Windows Server 2016, не поддерживает параметр **Type**, для таких операционных систем необходим альтернативный способ создания этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-178">Because the New-SelfSignedCertificate cmdlet on Windows Operating Systems prior to Windows 10 and Windows Server 2016 do not support the **Type** parameter, an alternate method of creating this certificate is required on these operating systems.</span></span>
<span data-ttu-id="9b5e3-179">В этом случае можно использовать для создания сертификата программу ```makecert.exe``` или ```certutil.exe```.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-179">In this case you can use ```makecert.exe``` or ```certutil.exe``` to create the certificate.</span></span>

<span data-ttu-id="9b5e3-180">Альтернативным способом является [загрузка сценария New-SelfSignedCertificateEx.ps1 из центра сценариев Майкрософт](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) и использование этого файла для создания сертификата:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-180">An alternate method is to [download the New-SelfSignedCertificateEx.ps1 script from Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6) and use it to create the certificate instead:</span></span>
```powershell
# note: These steps need to be performed in an Administrator PowerShell session
# and in the folder that contains New-SelfSignedCertificateEx.ps1
. .\New-SelfSignedCertificateEx.ps1
New-SelfsignedCertificateEx `
    -Subject "CN=${ENV:ComputerName}" `
    -EKU 'Document Encryption' `
    -KeyUsage 'KeyEncipherment, DataEncipherment' `
    -SAN ${ENV:ComputerName} `
    -FriendlyName 'DSC Credential Encryption certificate' `
    -Exportable `
    -StoreLocation 'LocalMachine' `
    -KeyLength 2048 `
    -ProviderName 'Microsoft Enhanced Cryptographic Provider v1.0' `
    -AlgorithmName 'RSA' `
    -SignatureAlgorithm 'SHA256'
# Locate the newly created certificate
$Cert = Get-ChildItem -Path cert:\LocalMachine\My `
    | Where-Object {
        ($_.FriendlyName -eq 'DSC Credential Encryption certificate') `
        -and ($_.Subject -eq "CN=${ENV:ComputerName}")
    } | Select-Object -First 1
# export the public key certificate
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
$cert | Export-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -Password $mypwd -Force
# remove the private key certificate from the node but keep the public key certificate
$cert | Export-Certificate -FilePath "$env:temp\DscPublicKey.cer" -Force
$cert | Remove-Item -Force
Import-Certificate -FilePath "$env:temp\DscPublicKey.cer" -CertStoreLocation Cert:\LocalMachine\My
```

#### <a name="on-the-target-node-import-the-certs-private-key-as-a-trusted-root"></a><span data-ttu-id="9b5e3-181">На целевом узле: импорт закрытого ключа сертификата в качестве доверенного корневого сертификата</span><span class="sxs-lookup"><span data-stu-id="9b5e3-181">On the Target Node: import the cert’s private key as a trusted root</span></span>
```powershell
# Import to the root store so that it is trusted
$mypwd = ConvertTo-SecureString -String "YOUR_PFX_PASSWD" -Force -AsPlainText
Import-PfxCertificate -FilePath "$env:temp\DscPrivateKey.pfx" -CertStoreLocation Cert:\LocalMachine\Root -Password $mypwd > $null
```

## <a name="configuration-data"></a><span data-ttu-id="9b5e3-182">Данные конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5e3-182">Configuration data</span></span>

<span data-ttu-id="9b5e3-183">Блок данных конфигурации определяет, какие целевые узлы использовать, следует ли шифровать учетные данные, какие средства шифрования использовать и т. д.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-183">The configuration data block defines which target nodes to operate on, whether or not to encrypt the credentials, the means of encryption, and other information.</span></span> <span data-ttu-id="9b5e3-184">Дополнительные сведения о блоке данных конфигурации см. в разделе [Разделение данных конфигурации и данных среды](configData.md).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-184">For more information on the configuration data block, see [Separating Configuration and Environment Data](configData.md).</span></span>

<span data-ttu-id="9b5e3-185">Ниже перечислены элементы, связанные с учетными данными шифрования, которые можно настроить для каждого узла:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-185">The elements that can be configured for each node that are related to credential encryption are:</span></span>
* <span data-ttu-id="9b5e3-186">**NodeName** — имя целевого узла, для которого настраивается шифрование учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-186">**NodeName** - the name of the target node that the credential encryption is being configured for.</span></span>
* <span data-ttu-id="9b5e3-187">**PsDscAllowPlainTextPassword** — определяет, могут ли незашифрованные учетные данные передаваться на этот узел.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-187">**PsDscAllowPlainTextPassword** - whether unencrypted credentials will be allowed to be passed to this node.</span></span> <span data-ttu-id="9b5e3-188">Это делать **не рекомендуется**.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-188">This is **not recommended**.</span></span>
* <span data-ttu-id="9b5e3-189">**Thumbprint** — отпечаток сертификата, который будет использоваться для расшифровки учетных данных в конфигурации DSC на _целевом узле_.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-189">**Thumbprint** - the thumbprint of the certificate that will be used to decrypt the credentials in the DSC Configuration on the _Target Node_.</span></span> <span data-ttu-id="9b5e3-190">**Этот сертификат должен существовать в хранилище сертификатов локального компьютера на целевом узле.**</span><span class="sxs-lookup"><span data-stu-id="9b5e3-190">**This certificate must exist in the Local Machine certificate store on the Target Node.**</span></span>
* <span data-ttu-id="9b5e3-191">**CertificateFile** — файл сертификата (содержащий только открытый ключ), который следует использовать для шифрования учетных данных для _целевого узла_.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-191">**CertificateFile** - the certificate file (containing the public key only) that should be used to encrypt the credentials for the _Target Node_.</span></span> <span data-ttu-id="9b5e3-192">Формат этого файла сертификата — двоичный стандарт X.509 в кодировке DER или Base-64.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-192">This must be either a DER encoded binary X.509 or Base-64 encoded X.509 format certificate file.</span></span>

<span data-ttu-id="9b5e3-193">В этом примере показан блок данных конфигурации, в котором определен целевой узел для обработки, называемый targetNode, путь к файлу сертификата открытого ключа (с именем targetNode.cer) и отпечаток открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-193">This example shows a configuration data block that specifies a target node to act on named targetNode, the path to the public key certificate file (named targetNode.cer), and the thumbprint for the public key.</span></span>

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


## <a name="configuration-script"></a><span data-ttu-id="9b5e3-194">Сценарий конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5e3-194">Configuration script</span></span>

<span data-ttu-id="9b5e3-195">В самом сценарии конфигурации используйте параметр `PsCredential`, чтобы учетные данные хранились в течение минимально возможного срока.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-195">In the configuration script itself, use the `PsCredential` parameter to ensure that credentials are stored for the shortest possible time.</span></span> <span data-ttu-id="9b5e3-196">При запуске этого примера DSC запросит у вас учетные данные и затем зашифрует MOF-файл с помощью сертификата CertificateFile, который связан с этим целевым узлом в блоке данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-196">When you run the supplied example, DSC will prompt you for credentials and then encrypt the MOF file using the CertificateFile that is associated with the target node in the configuration data block.</span></span> <span data-ttu-id="9b5e3-197">В этом коде файл копируется из общей папки, которая защищена для пользователя.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-197">This code example copies a file from a share that is secured to a user.</span></span>

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

## <a name="setting-up-decryption"></a><span data-ttu-id="9b5e3-198">Настройка расшифровки</span><span class="sxs-lookup"><span data-stu-id="9b5e3-198">Setting up decryption</span></span>

<span data-ttu-id="9b5e3-199">Перед началом работы [`Start-DscConfiguration`](https://technet.microsoft.com/en-us/library/dn521623.aspx) вам необходимо сообщить локальному диспетчеру конфигураций каждого целевого узла, какой сертификат следует использовать для расшифровки учетных данных с помощью ресурса CertificateID для проверки отпечатка сертификата.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-199">Before [`Start-DscConfiguration`](https://technet.microsoft.com/en-us/library/dn521623.aspx) can work, you have to tell the Local Configuration Manager on each target node which certificate to use to decrypt the credentials, using the CertificateID resource to verify the certificate’s thumbprint.</span></span> <span data-ttu-id="9b5e3-200">Этот пример функции найдет соответствующий локальный сертификат (может потребоваться изменить его так, чтобы он нашел именно тот сертификат, который вы хотите использовать):</span><span class="sxs-lookup"><span data-stu-id="9b5e3-200">This example function will find the appropriate local certificate (you might have to customize it so it will find the exact certificate you want to use):</span></span>

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

<span data-ttu-id="9b5e3-201">С сертификатом, который определяется отпечатком, можно обновить сценарий конфигурации, чтобы он использовал это значение:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-201">With the certificate identified by its thumbprint, the configuration script can be updated to use the value:</span></span>

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

## <a name="running-the-configuration"></a><span data-ttu-id="9b5e3-202">Выполнение конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5e3-202">Running the configuration</span></span>

<span data-ttu-id="9b5e3-203">На этом этапе можно запустить конфигурацию, в результате чего вы получите два выходных файла:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-203">At this point, you can run the configuration, which will output two files:</span></span>

 * <span data-ttu-id="9b5e3-204">Файл *. meta.mof, настраивающий расшифровку учетных данных в локальном диспетчере конфигураций с помощью сертификата, который хранится в хранилище локального компьютера и определяется его отпечатком.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-204">A *.meta.mof file that configures the Local Configuration Manager to decrypt the credentials using the certificate that is stored on the local machine store and identified by its thumbprint.</span></span> <span data-ttu-id="9b5e3-205">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx) применяет файл *.meta.mof.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-205">[`Set-DscLocalConfigurationManager`](https://technet.microsoft.com/en-us/library/dn521621.aspx) applies the *.meta.mof file.</span></span>
 * <span data-ttu-id="9b5e3-206">MOF-файл, который фактически применяет конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-206">A MOF file that actually applies the configuration.</span></span> <span data-ttu-id="9b5e3-207">Командлет Start-DscConfiguration применяет конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-207">Start-DscConfiguration applies the configuration.</span></span>

<span data-ttu-id="9b5e3-208">Эти команды выполнят следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-208">These commands will accomplish those steps:</span></span>

```powershell
Write-Host "Generate DSC Configuration..."
CredentialEncryptionExample -ConfigurationData $ConfigData -OutputPath .\CredentialEncryptionExample

Write-Host "Setting up LCM to decrypt credentials..."
Set-DscLocalConfigurationManager .\CredentialEncryptionExample -Verbose 
 
Write-Host "Starting Configuration..."
Start-DscConfiguration .\CredentialEncryptionExample -wait -Verbose
```

<span data-ttu-id="9b5e3-209">В этом примере конфигурация DSC будет принудительно отправляться на целевой узел.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-209">This example would push the DSC configuration to the target node.</span></span>
<span data-ttu-id="9b5e3-210">Конфигурацию DSC также можно применить с помощью опрашивающего сервера DSC, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="9b5e3-210">The DSC configuration can also be applied using a DSC Pull Server if one is available.</span></span>

<span data-ttu-id="9b5e3-211">Дополнительные сведения о применении конфигурации DSC с помощью опрашивающего сервера DSC см. в статье [Setting up a DSC pull client](pullClient.md) (Настройка опрашивающего клиента DSC).</span><span class="sxs-lookup"><span data-stu-id="9b5e3-211">See [Setting up a DSC pull client](pullClient.md) for more information on applying DSC configurations using a DSC Pull Server.</span></span>

## <a name="credential-encryption-module-example"></a><span data-ttu-id="9b5e3-212">Пример модуля шифрования учетных данных</span><span class="sxs-lookup"><span data-stu-id="9b5e3-212">Credential Encryption Module Example</span></span>

<span data-ttu-id="9b5e3-213">Ниже приведен полный пример, включающий все эти действия, а также вспомогательный командлет, который экспортирует и копирует открытые ключи:</span><span class="sxs-lookup"><span data-stu-id="9b5e3-213">Here is a full example that incorporates all of these steps, plus a helper cmdlet that exports and copies the public keys:</span></span>

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

