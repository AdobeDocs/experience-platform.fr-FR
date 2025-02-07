---
title: Source de la zone d’atterrissage des données
description: Découvrez comment connecter Data Landing Zone à Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 1d4dd60180ef2a3cbf6dcd565c2f09dd575716b9
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 21%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Cette page est spécifique au connecteur [!DNL Data Landing Zone] *source* dans l’Experience Platform. Pour plus d’informations sur la connexion au connecteur [!DNL Data Landing Zone] *destination*, consultez la page de documentation [[!DNL Data Landing Zone] destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform. Elle vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients d’Experience Platform sont configurés avec un conteneur [!DNL Data Landing Zone] par sandbox. Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone] via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre conteneur [!DNL Data Landing Zone], ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau. Experience Platform applique un délai d’expiration strict de sept jours sur tous les fichiers et dossiers chargés dans un conteneur [!DNL Data Landing Zone]. Tous les fichiers et les dossiers sont supprimés au bout de sept jours.

## Configurer votre source [!DNL Data Landing Zone] pour Experience Platform sur Azure {#azure}

Suivez les étapes ci-dessous pour savoir comment configurer votre compte [!DNL Data Landing Zone] pour Experience Platform sur Azure.

>[!NOTE]
>
>Si vous souhaitez accéder au [!DNL Data Landing Zone] à partir de [!DNL Azure Data Factory], vous devez créer un service lié à [!DNL Data Landing Zone] à l’aide des informations d’identification [SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) fournies par l’Experience Platform. Une fois que vous avez créé votre service lié, vous pouvez explorer votre [!DNL Data Landing Zone] en sélectionnant le chemin du conteneur au lieu du chemin racine par défaut.

### Contraintes de dénomination pour fichiers et répertoires

Voici une liste des contraintes dont vous devez tenir compte lorsque vous nommez vos fichiers ou répertoires de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, comme les caractères de contrôle (tels que `0x00` à `0x1F`, `\u0081`, etc.), ne sont pas autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

### Gestion du contenu de votre zone d’atterrissage de données{#manage-the-contents-of-your-data-landing-zone}

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/fr-fr/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone].

Dans l’interface utilisateur de [!DNL Azure Storage Explorer], sélectionnez l’icône de connexion dans le volet de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionnez **[!DNL Blob container]** pour vous connecter à [!DNL Data Landing Zone].

![L’espace de travail Sélectionner la ressource sur Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![La méthode de connexion Select sur Azure Explorer, avec la signature d’accès partagé sélectionnée.](../../images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez fournir un **nom d’affichage** ainsi que l’URL SAS du conteneur **[!DNL Blob]** qui correspond à votre conteneur [!DNL Data Landing Zone].

>[!TIP]
>
>Vous pouvez récupérer vos informations d’identification [!DNL Data Landing Zone] à partir du catalogue de sources dans l’interface utilisateur de Platform.

Indiquez votre URL SAS [!DNL Data Landing Zone], puis sélectionnez **Suivant**

![L’espace de travail Saisir les informations de connexion sur Azure Explorer dans lequel le nom d’affichage et l’URL SAS sont saisis.](../../images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Espace de travail de résumé de l’explorateur Azure qui récapitule les paramètres de votre connexion aux ressources.](../../images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Espace de travail de navigation de la zone d’atterrissage des données sur Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Maintenant que votre conteneur [!DNL Data Landing Zone] est connecté à [!DNL Azure Storage Explorer], vous pouvez commencer à charger des fichiers dans votre conteneur [!DNL Data Landing Zone]. Pour charger, sélectionnez **Télécharger** puis **Télécharger des fichiers**.

![Espace de travail des fichiers de chargement d’Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

Une fois le fichier à charger sélectionné, vous devez identifier le type de [!DNL Blob] sous lequel vous souhaitez le charger, ainsi que le répertoire de destination souhaité. Lorsque vous avez terminé, sélectionnez **Charger**.

| [!DNL Blob] types | Description |
| --- | --- |
| Bloquer les [!DNL Blob] | Les [!DNL Blobs] de blocs sont optimisés pour charger de grandes quantités de données de manière efficace. Les [!DNL Blobs] de bloc sont l’option par défaut pour les [!DNL Data Landing Zone]. |
| Ajouter un [!DNL Blob] | Les [!DNL Blobs] d’ajout sont optimisées pour l’ajout de données à la fin du fichier. |

![La fenêtre Charger des fichiers d’Azure Explorer dans laquelle les fichiers sélectionnés, le type d’objet Blob et la catégorie de destination s’affichent.](../../images/tutorials/create/dlz/upload-files.png)

### Chargez des fichiers dans votre [!DNL Data Landing Zone] à l’aide de l’interface de ligne de commande

Vous pouvez également utiliser l’interface de ligne de commande de votre appareil et accéder aux fichiers de chargement de votre [!DNL Data Landing Zone].

### Charger un fichier à l’aide de Bash

L’exemple suivant utilise Bash et cURL pour charger un fichier dans un [!DNL Data Landing Zone] avec l’API REST [!DNL Azure Blob Storage] :

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Charger un fichier à l’aide de Python

L&#39;exemple suivant utilise [!DNL Microsoft's] SDK Python v12 pour charger un fichier dans un [!DNL Data Landing Zone] :

>[!TIP]
>
>Bien que l’exemple ci-dessous utilise l’URI SAS complet pour se connecter à un conteneur [!DNL Azure Blob], vous pouvez utiliser d’autres méthodes et opérations pour vous authentifier. Voir ce [[!DNL Microsoft] document sur Python v12 SDK](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) pour plus d’informations.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Chargement d’un fichier à l’aide de [!DNL AzCopy]

L’exemple suivant utilise [!DNL Microsoft's] utilitaire [!DNL AzCopy] pour charger un fichier dans un [!DNL Data Landing Zone] :

>[!TIP]
>
>Bien que l’exemple ci-dessous utilise la commande `copy` , vous pouvez utiliser d’autres commandes et options pour charger un fichier dans votre [!DNL Data Landing Zone] à l’aide de [!DNL AzCopy]. Voir ce [[!DNL Microsoft AzCopy] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) pour plus d’informations.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Configurer votre source [!DNL Data Landing Zone] pour Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Un Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la présentation multi-cloud de [Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Pour découvrir comment configurer votre compte [!DNL Data Landing Zone] pour Experience Platform sur Amazon Web Services (AWS), procédez comme suit.

### Configuration de l’interface de ligne de commande AWS et exécution d’opérations

- Lisez le guide sur [l’installation ou la mise à jour vers la dernière version de l’interface de ligne de commande AWS](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### Configuration de l’interface de ligne de commande AWS avec des informations d’identification temporaires

Utilisez la commande AWS `configure` pour configurer votre interface de ligne de commande avec des clés d’accès et un jeton de session.

```shell
aws configure
```

À l’invite, saisissez les valeurs suivantes :

- Identifiant de la clé d&#39;accès AWS : `{YOUR_ACCESS_KEY_ID}`
- Clé d’accès secrète AWS : `{YOUR_SECRET_ACCESS_KEY}`
- Nom de la région par défaut : `{YOUR_REGION}` (par exemple, `us-west-2`)
- Format de sortie par défaut : `json`

Ensuite, définissez le jeton de session :

```shell
aws configure set aws_session_token your-session-token
```

### Utiliser des fichiers sur [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB Charger un fichier dans Amazon S3]

Modèle :

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Exemple :

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB Télécharger un fichier à partir d’Amazon S3]

Modèle :

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Exemple :

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Utiliser vos informations d’identification [!DNL Data Landing Zone] pour vous connecter à la console AWS

#### Extraire vos informations d’identification

Tout d&#39;abord, vous devez obtenir les éléments suivants :

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Générer un jeton de connexion

Ensuite, utilisez les informations d’identification extraites pour créer une session et générer un jeton de connexion à l’aide du point d’entrée AWS Federation :

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### Construire l’URL de connexion à la console AWS

Une fois que vous disposez d’un jeton de connexion, vous pouvez créer l’URL qui vous connecte dans la console AWS et qui pointe directement vers le compartiment de [!DNL Amazon S3] souhaité.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### Accès à la console AWS

Enfin, accédez à l’URL générée pour vous connecter directement à la console AWS à l’aide de vos informations d’identification [!DNL Data Landing Zone], qui permettent d’accéder à un dossier spécifique dans un compartiment [!DNL Amazon S3]. L’URL de connexion vous conduit directement à ce dossier, ce qui garantit que vous ne voyez et ne gérez que les données autorisées.

## Connecter [!DNL Data Landing Zone] à l’Experience Platform

>[!IMPORTANT]
>
>- Pour vous connecter à la source, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]**. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../../access-control/home.md) ou contactez l’administrateur de votre produit pour obtenir les autorisations requises.
>
>- Les liens privés ne sont actuellement pas pris en charge lors de la connexion à l’Experience Platform à l’aide du [!DNL Data Landing Zone]. Les seules méthodes d’accès prises en charge sont les méthodes répertoriées [ici](#manage-the-contents-of-your-data-landing-zone).

La documentation ci-dessous fournit des informations sur la manière d’importer des données de votre conteneur [!DNL Data Landing Zone] dans Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.

### Utiliser les API

- [Créer une connexion  [!DNL Data Landing Zone]  source à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Connexion  [!DNL Data Landing Zone]  Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)

