---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Source Zone d’entrée de données
description: Découvrez comment connecter la zone d’entrée des données à Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecef17ed454c7b1f30543278bba6b0e3b70399da
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 33%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Cette page est spécifique au connecteur [!DNL Data Landing Zone] *source* dans Experience Platform. Pour plus d&#39;informations sur la connexion au connecteur [!DNL Data Landing Zone] *destination*, consultez la [[!DNL Data Landing Zone] page de documentation de destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] configurée par Adobe Experience Platform, qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients d’Experience Platform sont configurés avec un conteneur [!DNL Data Landing Zone] par environnement de test. Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone] via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre conteneur [!DNL Data Landing Zone], ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau. Experience Platform applique un délai d’expiration de sept jours strict pour tous les fichiers et dossiers chargés dans un conteneur [!DNL Data Landing Zone]. Tous les fichiers et dossiers sont supprimés au bout de sept jours.

>[!NOTE]
>
>Si vous souhaitez accéder à [!DNL Data Landing Zone] à partir de [!DNL Azure Data Factory], vous devez créer un service lié pour [!DNL Data Landing Zone] à l&#39;aide des [informations d&#39;identification SAS](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) fournies par l&#39;Experience Platform. Une fois que vous avez créé votre service lié, vous pouvez explorer votre [!DNL Data Landing Zone] en sélectionnant le chemin du conteneur au lieu du chemin racine par défaut.

## Contraintes de dénomination pour fichiers et répertoires

Vous trouverez ci-dessous une liste des contraintes dont vous devez tenir compte lorsque vous nommez vos fichiers ou répertoires de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (tels que `0x00` à `0x1F`, `\u0081`, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Gestion du contenu de votre zone d’entrée des données{#manage-the-contents-of-your-data-landing-zone}

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/fr-fr/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone].

Dans l’interface utilisateur de [!DNL Azure Storage Explorer], sélectionnez l’icône de connexion dans le volet de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionnez **[!DNL Blob container]** pour vous connecter à [!DNL Data Landing Zone].

![Sélection de ressource](../../images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![Sélection d’une méthode de connexion](../../images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez ensuite fournir un **nom d’affichage** et l’ **[!DNL Blob]conteneur SAS URL** correspondant à votre conteneur [!DNL Data Landing Zone].

>[!TIP]
>
>Vous pouvez récupérer vos informations d’identification [!DNL Data Landing Zone] du catalogue des sources dans l’interface utilisateur de Platform.

Fournissez l’URL SAS [!DNL Data Landing Zone], puis sélectionnez **Suivant**

![Saisie des informations de connexion](../../images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Résumé](../../images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Conteneur utilisateur DLZ](../../images/tutorials/create/dlz/dlz-user-container.png)

Avec votre conteneur [!DNL Data Landing Zone] connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à charger des fichiers dans votre conteneur [!DNL Data Landing Zone]. Pour télécharger, sélectionnez **Télécharger**, puis **Télécharger des fichiers**.

![upload](../../images/tutorials/create/dlz/upload.png)

Une fois que vous avez sélectionné le fichier que vous souhaitez charger, vous devez identifier le type [!DNL Blob] dans lequel vous souhaitez le charger et le répertoire de destination souhaité. Lorsque vous avez terminé, sélectionnez **Télécharger**.

| [!DNL Blob] types | Description |
| --- | --- |
| Bloc [!DNL Blob] | Le bloc [!DNL Blobs] est optimisé pour le chargement de grandes quantités de données de manière efficace. Le bloc [!DNL Blobs] est l&#39;option par défaut pour [!DNL Data Landing Zone]. |
| Ajouter [!DNL Blob] | Les [!DNL Blobs] ajoutés sont optimisés pour ajouter des données à la fin du fichier. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Chargez des fichiers sur votre [!DNL Data Landing Zone] à l’aide de l’interface de ligne de commande

Vous pouvez également utiliser l’interface de ligne de commande de votre appareil et accéder aux fichiers de chargement vers votre [!DNL Data Landing Zone].

### Chargement d’un fichier à l’aide de Bash

L’exemple suivant utilise Bash et cURL pour charger un fichier vers un [!DNL Data Landing Zone] avec l’API REST [!DNL Azure Blob Storage] :

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

### Téléchargement d’un fichier à l’aide de Python

L’exemple suivant utilise le SDK [!DNL Microsoft's] Python v12 pour charger un fichier vers un [!DNL Data Landing Zone] :

>[!TIP]
>
>Bien que l’exemple ci-dessous utilise l’URI SAS complet pour se connecter à un conteneur [!DNL Azure Blob], vous pouvez utiliser d’autres méthodes et opérations pour vous authentifier. Pour plus d’informations, consultez ce [[!DNL Microsoft] document sur le SDK Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) .

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

### Télécharger un fichier à l’aide de [!DNL AzCopy]

L’exemple suivant utilise l’utilitaire [!DNL Microsoft's] [!DNL AzCopy] pour charger un fichier vers un [!DNL Data Landing Zone] :

>[!TIP]
>
>Bien que l&#39;exemple ci-dessous utilise la commande `copy`, vous pouvez utiliser d&#39;autres commandes et options pour télécharger un fichier vers votre [!DNL Data Landing Zone], à l&#39;aide de [!DNL AzCopy]. Pour plus d’informations, consultez ce [[!DNL Microsoft AzCopy] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) .

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connectez [!DNL Data Landing Zone] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la manière d’importer des données de votre conteneur [!DNL Data Landing Zone] vers Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.

### Utiliser les API

- [Création d’une connexion source  [!DNL Data Landing Zone]  à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Connexion de  [!DNL Data Landing Zone]  à Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>Les liens privés ne sont actuellement pas pris en charge lors de la connexion à Experience Platform à l’aide de [!DNL Data Landing Zone]. Les seules méthodes prises en charge pour l’accès sont les méthodes répertoriées [ici](#manage-the-contents-of-your-data-landing-zone).

