---
title: Destination de Data Landing Zone
description: Découvrez comment vous connecter à Data Landing Zone pour activer des audiences et exporter des jeux de données.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1978'
ht-degree: 32%

---

# Destination de Data Landing Zone

>[!IMPORTANT]
>
>Cette page de documentation fait référence à la [!DNL Data Landing Zone] *destination*. Le catalogue des sources contient également une [!DNL Data Landing Zone] *source*. Pour plus d’informations, consultez la documentation de [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md).


## Vue d’ensemble {#overview}

[!DNL Data Landing Zone] est une interface de stockage dans le cloud fournie par Adobe Experience Platform et qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers en dehors d’Experience Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Experience Platform. Tous les clients d’Experience Platform et ses applications, telles que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] et [!DNL Real-Time Customer Data Platform], sont configurés avec un conteneur [!DNL Data Landing Zone] par sandbox.

Experience Platform applique une durée de vie (TTL) stricte de sept jours sur tous les fichiers chargés dans un conteneur [!DNL Data Landing Zone]. Tous les fichiers sont supprimés au bout de sept jours.

Le connecteur de destination [!DNL Data Landing Zone] est disponible pour les clients qui utilisent la prise en charge cloud d’Azure ou d’Amazon Web Service. Le mécanisme d’authentification est différent en fonction du cloud dans lequel la destination est configurée, tout le reste concernant la destination et ses cas d’utilisation est le même. Pour en savoir plus sur les deux mécanismes d’authentification différents, consultez les sections [Authentification à la zone d’atterrissage de données configurée dans Azure Blob](#authenticate-dlz-azure) et [Authentification à la zone d’atterrissage de données configurée par AWS](#authenticate-dlz-aws).

![Diagramme montrant les différences d’implémentation de la destination de zone d’atterrissage de données en fonction de la prise en charge du cloud.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png "Implémentation de la destination Data Landing Zone par l’assistance cloud"){zoomable="yes"}

## Connexion à votre stockage [!UICONTROL Data Landing Zone] via l’API ou l’interface utilisateur {#connect-api-or-ui}

* Pour vous connecter à votre emplacement de stockage [!UICONTROL Data Landing Zone] à l’aide de l’interface utilisateur d’Experience Platform, lisez les sections [Se connecter à la destination](#connect) et [Activer des audiences vers cette destination](#activate) ci-dessous.
* Pour vous connecter par programmation à votre emplacement de stockage [!UICONTROL Data Landing Zone], consultez le tutoriel [ Activer les audiences vers des destinations basées sur des fichiers à l’aide de l’API Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (par exemple votre PPID), tels que choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez les tutoriels :

* Comment [exporter des jeux de données à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-datasets.md).
* Comment [exporter des jeux de données par programmation à l’aide de l’API Flow Service](/help/destinations/api/export-datasets.md).

## Format des données exportées {#file-format}

Lors de l’exportation de *données d’audience*, Experience Platform crée un fichier `.csv`, `parquet` ou `.json` à l’emplacement de stockage indiqué. Pour plus d’informations sur les fichiers, consultez la section [formats de fichiers pris en charge pour l’exportation](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) dans le tutoriel sur l’activation des audiences.

Lors de l’exportation de *jeux de données*, Experience Platform crée un fichier `.parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [vérifier la réussite de l’exportation du jeu de données](../../ui/export-datasets.md#verify) dans le tutoriel sur l’exportation des jeux de données.

## Authentifiez-vous sur la zone d’atterrissage de données configurée dans Azure Blob {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Microsoft Azure. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. SAS signifie [signature d’accès partagé](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Pour protéger vos données sur une connexion Internet publique, utilisez l’authentification SAS pour accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone]. Aucune modification réseau n’est requise pour accéder à votre conteneur [!DNL Data Landing Zone], ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau.

### Connecter votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer]

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone]. Pour commencer à utiliser [!DNL Data Landing Zone], vous devez d’abord récupérer vos informations d’identification, les saisir dans [!DNL Azure Storage Explorer] et connecter votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer].

Dans l’interface utilisateur [!DNL Azure Storage Explorer], sélectionnez l’icône de connexion dans la barre de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionnez **[!DNL Blob container]** pour vous connecter à votre espace de stockage [!DNL Data Landing Zone].

![Sélectionnez la ressource mise en surbrillance dans l’interface utilisateur d’Azure.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![Sélectionnez la méthode de connexion mise en surbrillance dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez fournir un **nom d’affichage** et l’URL du conteneur SAS **[!DNL Blob]** qui correspond à votre conteneur [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Récupérer les informations d’identification pour votre [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Vous devez utiliser les API d’Experience Platform pour récupérer vos informations d’identification [!DNL Data Landing Zone]. L’appel API permettant de récupérer vos informations d’identification est décrit ci-dessous. Pour plus d’informations sur l’obtention des valeurs requises pour vos en-têtes, consultez le guide [Prise en main des API Adobe Experience Platform](/help/landing/api-guide.md).

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Paramètres de requête | Description |
| --- | --- |
| `dlz_destination` | Le type `dlz_destination` permet à l’API de distinguer un conteneur de destination de zone d’atterrissage des autres types de conteneurs disponibles. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête suivant récupère les informations d’identification d’une zone d’atterrissage existante.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie les informations d’identification de votre zone d’atterrissage, y compris votre `SASToken` et votre `SASUri` actuels, ainsi que la `storageAccountName` correspondant à votre conteneur de zone d’atterrissage.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de votre zone d’atterrissage. |
| `SASToken` | Jeton de signature d’accès partagé pour votre zone d’atterrissage. Cette chaîne contient toutes les informations nécessaires pour autoriser une requête. |
| `SASUri` | URI de signature d’accès partagé pour votre zone d’atterrissage. Cette chaîne est une combinaison de l’URI de la zone d’atterrissage à laquelle vous êtes authentifié et de son jeton SAS correspondant, |

{style="table-layout:auto"}

### Mettre à jour les informations d’identification [!DNL Data Landing Zone] {#update-dlz-credentials}

Vous pouvez également actualiser vos informations d’identification lorsque vous le souhaitez. Vous pouvez mettre à jour votre `SASToken` en effectuant une requête POST vers le point d’entrée `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Paramètres de requête | Description |
| --- | --- |
| `dlz_destination` | Le type `dlz_destination` permet à l’API de distinguer un conteneur de destination de zone d’atterrissage des autres types de conteneurs disponibles. |
| `refresh` | L’action `refresh` vous permet de réinitialiser les informations d’identification de votre zone d’atterrissage et de générer automatiquement une nouvelle `SASToken`. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour vos informations d’identification de zone d’atterrissage.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie des valeurs mises à jour pour vos `SASToken` et `SASUri`.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Indiquez votre nom d’affichage (`containerName`) et [!DNL Data Landing Zone] URL SAS, tel que renvoyé dans l’appel API décrit ci-dessus, puis sélectionnez **Suivant**.

![Saisissez les informations de connexion mises en surbrillance dans l’interface utilisateur d’Azure.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Résumé des paramètres affichés dans l’interface utilisateur d’Azure.](/help/sources/images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Résumé du conteneur utilisateur DLZ mis en surbrillance dans l’interface utilisateur d’Azure.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Avec votre conteneur [!DNL Data Landing Zone] connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à exporter des fichiers d’Experience Platform vers votre conteneur [!DNL Data Landing Zone]. Pour exporter des fichiers, vous devez établir une connexion à la destination [!DNL Data Landing Zone] dans l’interface utilisateur d’Experience Platform, comme décrit dans la section ci-dessous.

## Authentification à la zone d’atterrissage de données configurée par AWS {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Effectuez les opérations ci-dessous pour obtenir les informations d’identification de votre instance [!DNL Data Landing Zone] configurée sur AWS. Utilisez ensuite un client de votre choix pour vous connecter à votre instance [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Récupérer les informations d’identification pour votre [!DNL Data Landing Zone] {#retrieve-dlz-credentials-aws}

Vous devez utiliser les API d’Experience Platform pour récupérer vos informations d’identification [!DNL Data Landing Zone]. L’appel API permettant de récupérer vos informations d’identification est décrit ci-dessous. Pour plus d’informations sur l’obtention des valeurs requises pour vos en-têtes, consultez le guide [Prise en main des API Adobe Experience Platform](/help/landing/api-guide.md).

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Paramètres de requête | Description |
| --- | --- |
| `dlz_destination` | Ajoutez le paramètre de requête `dlz_destination` pour spécifier que vous souhaitez récupérer le type d’informations d’identification de conteneur [!DNL Data Landing Zone] *destination*. Pour vous connecter et récupérer les informations d’identification d’une Data Landing Zone *source*, consultez la documentation sur les [ sources](/help/sources/connectors/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

**Requête**

L’exemple de requête suivant récupère les informations d’identification d’une zone d’atterrissage existante.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Réponse**

La réponse suivante renvoie les informations d’identification de votre zone d’atterrissage, y compris votre `awsAccessKeyId` actuelle, votre `awsSecretAccessKey` et d’autres informations.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Propriété | Description |
| --- | --- |
| `credentials` | Cet objet comprend les `awsAccessKeyId`, `awsSecretAccessKey` et `awsSessionToken` utilisés par Experience Platform pour exporter des fichiers vers votre emplacement Data Landing Zone configuré. |
| `dlzPath` | Cet objet inclut le chemin d’accès à l’emplacement AWS configuré par Adobe où les fichiers exportés sont déposés. |
| `dlzProvider` | Indique qu’il s’agit d’une zone d’atterrissage de données configurée pour Amazon S3. |
| `expiryTime` | Indique à quel moment les informations d’identification de l’objet `credentials` expireront. Pour actualiser les informations d’identification, effectuez à nouveau la requête. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Assurez-vous d’avoir connecté votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer] comme décrit dans la section [conditions préalables](#prerequisites). Étant donné que [!DNL Data Landing Zone] est un stockage configuré par Adobe, vous n’avez pas besoin d’effectuer d’autres étapes dans l’interface utilisateur d’Experience Platform pour vous authentifier auprès de la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui héberge les fichiers exportés.
* **[!UICONTROL Type de fichier]** : sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Lors de la sélection de l’option [!UICONTROL CSV], vous pouvez également [configurer les options de formatage des fichiers](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]** : sélectionnez le type de compression qu’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Inclure le fichier manifeste]** : activez cette option si vous souhaitez que les exportations incluent un fichier JSON de manifeste contenant des informations sur l’emplacement d’exportation, la taille d’exportation, etc. Le manifeste est nommé à l’aide du format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Affichez un [exemple de fichier de manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier manifeste comprend les champs suivants :
   * `flowRunId` : exécution [flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.
   * `scheduledTime` : heure en UTC à laquelle le fichier a été exporté.
   * `exportResults.sinkPath` : chemin d’accès à l’emplacement de stockage où le fichier exporté est déposé.
   * `exportResults.name` : nom du fichier exporté.
   * `size` : taille du fichier exporté, en octets.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [ Activer les données d’audience vers des destinations d’exportation de profils par lots ](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Planification

Dans l’étape **[!UICONTROL Planifier]**, vous pouvez [configurer le planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre destination [!DNL Data Landing Zone] et vous pouvez également [configurer le nom de vos fichiers exportés](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapper les attributs et les identités {#map}

Dans l’étape **[!UICONTROL Mappage]**, vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez le stockage [!DNL Data Landing Zone] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
