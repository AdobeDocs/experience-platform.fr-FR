---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Source de la zone d’entrée de données
description: Découvrez comment connecter la zone d’entrée des données à Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: cb37eda87b8fcc0d0284db7a0bab8d48eab5aae6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 35%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Cette page est spécifique aux [!DNL Data Landing Zone] *source* connecteur dans Experience Platform. Pour plus d’informations sur la connexion à la variable [!DNL Data Landing Zone] *destination* connecteur, voir [[!DNL Data Landing Zone] page de documentation de destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est un [!DNL Azure Blob] Interface de stockage configurée par Adobe Experience Platform, qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients de Platform et de ses applications, telles que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], et [!DNL Adobe Real-Time Customer Data Platform] sont configurés avec un [!DNL Data Landing Zone] conteneur par environnement de test. Vous pouvez lire et écrire des fichiers dans votre conteneur par le biais de [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone] via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre [!DNL Data Landing Zone] , ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau. Platform applique un délai d’expiration de sept jours strict pour tous les fichiers chargés dans un [!DNL Data Landing Zone] conteneur. Tous les fichiers sont supprimés au bout de sept jours.

## Contraintes de dénomination pour fichiers et répertoires

Vous trouverez ci-dessous une liste des contraintes dont vous devez tenir compte lorsque vous nommez vos fichiers ou répertoires de stockage dans le cloud.

- Les noms des composants de répertoire et de fichier ne doivent pas dépasser 255 caractères.
- Les noms de répertoire et de fichier ne peuvent pas se terminer par une barre oblique (`/`). Elle sera le cas échéant automatiquement supprimée.
- Les caractères d’URL réservés suivants doivent être des caractères d’échappement : `! ' ( ) ; @ & = + $ , % # [ ]`
- Les caractères suivants ne sont pas autorisés : `" \ / : | < > * ?`.
- Caractères de chemin d’URL illégaux interdits. Les points de code tels que `\uE000`, bien que valides dans les noms de fichier NTFS, ne sont pas des caractères Unicode valides. En outre, certains caractères ASCII ou Unicode, tels que les caractères de contrôle (tels que `0x00` to `0x1F`, `\u0081`, etc.), ne sont pas non plus autorisés. Pour les règles régissant les chaînes Unicode en HTTP/1.1, voir [RFC 2616, section 2.2 : règles de base](https://www.ietf.org/rfc/rfc2616.txt) et [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Les noms de fichier suivants ne sont pas autorisés : LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, point (.) et deux points (..).

## Gestion du contenu de votre zone d’entrée des données{#manage-the-contents-of-your-data-landing-zone}

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/fr-fr/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone].

Dans le [!DNL Azure Storage Explorer] , sélectionnez l’icône de connexion dans le volet de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionner **[!DNL Blob container]** pour se connecter à [!DNL Data Landing Zone].

![Sélection de ressource](../../images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![Sélection d’une méthode de connexion](../../images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez ensuite fournir un **nom d&#39;affichage** et la variable **[!DNL Blob]container SAS URL** qui correspond à votre [!DNL Data Landing Zone] conteneur.

>[!TIP]
>
>Vous pouvez récupérer votre [!DNL Data Landing Zone] informations d’identification provenant du catalogue des sources dans l’interface utilisateur de Platform.

Fournissez les [!DNL Data Landing Zone] URL SAS , puis sélectionnez **Suivant**

![Saisie des informations de connexion](../../images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Résumé](../../images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Conteneur utilisateur DLZ](../../images/tutorials/create/dlz/dlz-user-container.png)

Avec votre [!DNL Data Landing Zone] conteneur connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à charger des fichiers dans votre [!DNL Data Landing Zone] conteneur. Pour charger, sélectionnez **Télécharger** puis sélectionnez **Chargement de fichiers**.

![charger](../../images/tutorials/create/dlz/upload.png)

Une fois que vous avez sélectionné le fichier à charger, vous devez alors identifier la variable [!DNL Blob] saisissez pour le charger en tant que et dans le répertoire de destination de votre choix. Lorsque vous avez terminé, sélectionnez **Télécharger**.

| [!DNL Blob] types | Description |
| --- | --- |
| Bloc [!DNL Blob] | Bloc [!DNL Blobs] sont optimisés pour le transfert efficace de grandes quantités de données. Bloc [!DNL Blobs] sont l’option par défaut pour [!DNL Data Landing Zone]. |
| Ajouter [!DNL Blob] | Ajouter [!DNL Blobs] sont optimisés pour ajouter des données à la fin du fichier. |

![upload-files](../../images/tutorials/create/dlz/upload-files.png)

## Chargement de fichiers dans [!DNL Data Landing Zone] utilisation de l’interface de ligne de commande

Vous pouvez également utiliser l’interface de ligne de commande de votre périphérique et accéder aux fichiers de transfert vers votre [!DNL Data Landing Zone].

### Chargement d’un fichier à l’aide de Bash

L’exemple suivant utilise Bash et cURL pour charger un fichier vers un [!DNL Data Landing Zone] avec la propriété [!DNL Azure Blob Storage] API REST :

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

L’exemple suivant utilise [!DNL Microsoft's] SDK Python v12 pour charger un fichier dans une [!DNL Data Landing Zone]:

>[!TIP]
>
>Bien que l’exemple ci-dessous utilise l’URI SAS complet pour se connecter à un [!DNL Azure Blob] conteneur, vous pouvez utiliser d’autres méthodes et opérations pour vous authentifier. Voir [[!DNL Microsoft] document sur le SDK Python v12](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) pour plus d’informations.

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

L’exemple suivant utilise [!DNL Microsoft's] [!DNL AzCopy] pour télécharger un fichier vers un [!DNL Data Landing Zone]:

>[!TIP]
>
>Bien que l’exemple ci-dessous utilise la variable `copy` , vous pouvez utiliser d’autres commandes et options pour charger un fichier dans votre [!DNL Data Landing Zone], en utilisant [!DNL AzCopy]. Voir [[!DNL Microsoft AzCopy] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) pour plus d’informations.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connexion [!DNL Data Landing Zone] to [!DNL Platform]

La documentation ci-dessous fournit des informations sur la manière d’importer des données de votre [!DNL Data Landing Zone] conteneur vers Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.

### Utiliser les API

- [Créez un [!DNL Data Landing Zone] Connexion source à l’aide de l’API Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une source de stockage dans le cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utiliser l’interface utilisateur

- [Connexion [!DNL Data Landing Zone] vers Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Créer un flux de données pour une connexion de stockage dans le cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>Les liens privés ne sont actuellement pas pris en charge lors de la connexion à Experience Platform à l’aide de la variable [!DNL Data Landing Zone]. Les seules méthodes d’accès prises en charge sont les méthodes répertoriées. [here](#manage-the-contents-of-your-data-landing-zone).

