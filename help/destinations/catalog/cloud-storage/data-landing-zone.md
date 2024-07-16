---
title: Destination de Data Landing Zone
description: Découvrez comment vous connecter à Data Landing Zone pour activer des audiences et exporter des jeux de données.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: ce78e320e78a67cd744fdf1c49b34f6fcddf4f15
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 44%

---

# Destination de Data Landing Zone

>[!IMPORTANT]
>
>Cette page de documentation fait référence à la [!DNL Data Landing Zone] *destination*. Il existe également une [!DNL Data Landing Zone] *source* dans le catalogue des sources. Pour plus d’informations, consultez la documentation [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md) .


## Présentation {#overview}

[!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform et qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers hors de Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients de Platform et de ses applications telles que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] et [!DNL Real-Time Customer Data Platform] sont configurés avec un conteneur [!DNL Data Landing Zone] par environnement de test. Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. SAS signifie [signature d’accès partagé](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone] via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre conteneur [!DNL Data Landing Zone], ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau.

Platform applique une durée de vie (TTL) stricte de sept jours sur tous les fichiers chargés dans un conteneur [!DNL Data Landing Zone]. Tous les fichiers sont supprimés au bout de sept jours.

## Connectez-vous à votre stockage [!UICONTROL Data Landing Zone] via l’API ou l’interface utilisateur. {#connect-api-or-ui}

* Pour vous connecter à l’emplacement de stockage [!UICONTROL Data Landing Zone] à l’aide de l’interface utilisateur de Platform, lisez les sections [Se connecter à la destination](#connect) et [Activer les audiences vers cette destination](#activate) ci-dessous.
* Pour vous connecter par programmation à votre emplacement de stockage [!UICONTROL Data Landing Zone], lisez le tutoriel [  Activation des audiences vers des destinations basées sur des fichiers à l’aide de l’API Flow Service](../../api/activate-segments-file-based-destinations.md).

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
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

* Comment [exporter des jeux de données à l’aide de l’interface utilisateur de Platform](/help/destinations/ui/export-datasets.md).
* Comment [exporter des jeux de données par programmation à l’aide de l’API Flow Service](/help/destinations/api/export-datasets.md).

## Format de fichier des données exportées {#file-format}

Lors de l’exportation de *données d’audience*, Platform crée un fichier `.csv`, `parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [Formats de fichiers pris en charge pour l’exportation](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) du tutoriel sur l’activation de l’audience.

Lors de l’exportation de *jeux de données*, Platform crée un fichier `.parquet` ou `.json` dans l’emplacement de stockage que vous avez fourni. Pour plus d’informations sur les fichiers, consultez la section [Vérification de l’exportation des jeux de données réussie](../../ui/export-datasets.md#verify) du tutoriel sur l’exportation des jeux de données.

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes qui doivent être remplies pour pouvoir utiliser la destination [!DNL Data Landing Zone].

### Connectez votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer]

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone]. Pour commencer à utiliser [!DNL Data Landing Zone], vous devez d’abord récupérer vos informations d’identification, les entrer dans [!DNL Azure Storage Explorer] et connecter votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer].

Dans l’interface utilisateur [!DNL Azure Storage Explorer], sélectionnez l’icône de connexion dans la barre de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionnez **[!DNL Blob container]** pour vous connecter à votre espace de stockage [!DNL Data Landing Zone].

![Sélectionnez la ressource mise en surbrillance dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![Sélectionnez la méthode de connexion mise en surbrillance dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez fournir un **nom d’affichage** et l’URL du conteneur SAS **[!DNL Blob]** qui correspond à votre conteneur [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Récupérez les informations d’identification de votre [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Vous devez utiliser les API de Platform pour récupérer vos informations d’identification [!DNL Data Landing Zone]. L’appel API pour récupérer vos informations d’identification est décrit ci-dessous. Pour plus d’informations sur l’obtention des valeurs requises pour vos en-têtes, consultez le guide [Prise en main des API Adobe Experience Platform](/help/landing/api-guide.md) .

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Paramètres de requête | Description |
| --- | --- |
| `dlz_destination` | Le type `dlz_destination` permet à l’API de distinguer un conteneur de destination de zone d’entrée des autres types de conteneurs disponibles. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête suivant récupère les informations d’identification d’une zone d’entrée existante.

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

La réponse suivante renvoie les informations d’identification pour votre zone d’entrée, y compris vos `SASToken` et `SASUri` actuels, et l’ `storageAccountName` correspondant au conteneur de votre zone d’entrée.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Le nom de votre zone d’entrée. |
| `SASToken` | Jeton de signature d’accès partagé pour votre zone d’entrée. Cette chaîne contient toutes les informations nécessaires pour autoriser une requête. |
| `SASUri` | URI de signature d’accès partagé pour votre zone d’entrée. Cette chaîne est une combinaison de l’URI de la zone d’entrée pour laquelle vous êtes authentifié et de son jeton SAS correspondant, |

{style="table-layout:auto"}

### Mise à jour des informations d’identification [!DNL Data Landing Zone] {#update-dlz-credentials}

Vous pouvez également actualiser vos informations d’identification si vous le souhaitez. Vous pouvez mettre à jour votre `SASToken` en envoyant une requête de POST au point de terminaison `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Paramètres de requête | Description |
| --- | --- |
| `dlz_destination` | Le type `dlz_destination` permet à l’API de distinguer un conteneur de destination de zone d’entrée des autres types de conteneurs disponibles. |
| `refresh` | L’action `refresh` vous permet de réinitialiser les informations d’identification de votre zone d’entrée et de générer automatiquement un nouveau `SASToken`. |

{style="table-layout:auto"}

**Requête**

La requête suivante met à jour les informations d’identification de votre zone d’entrée.

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
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Indiquez votre nom d’affichage (`containerName`) et l’URL SAS [!DNL Data Landing Zone], comme indiqué dans l’appel API décrit ci-dessus, puis sélectionnez **Suivant**.

![Saisissez les informations de connexion mises en surbrillance dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Résumé des paramètres affichés dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Résumé du conteneur utilisateur DLZ mis en surbrillance dans l’interface utilisateur Azure.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Avec votre conteneur [!DNL Data Landing Zone] connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à exporter des fichiers d’Experience Platform vers votre conteneur [!DNL Data Landing Zone]. Pour exporter des fichiers, vous devez établir une connexion à la destination [!DNL Data Landing Zone] dans l’interface utilisateur de l’Experience Platform, comme décrit dans la section ci-dessous.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Assurez-vous d’avoir connecté votre conteneur [!DNL Data Landing Zone] à [!DNL Azure Storage Explorer] comme décrit dans la section [conditions préalables](#prerequisites) . Étant donné que [!DNL Data Landing Zone] est un stockage configuré par Adobe, vous n’avez pas besoin d’effectuer d’autres étapes dans l’interface utilisateur de l’Experience Platform pour vous authentifier à la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui héberge les fichiers exportés.
* **[!UICONTROL Type de fichier]** : sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Lorsque vous sélectionnez l’option [!UICONTROL CSV] , vous pouvez également [ configurer les options de formatage de fichier ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]** : sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Inclure le fichier manifeste]** : activez cette option si vous souhaitez que les exportations incluent un fichier JSON manifeste contenant des informations sur l’emplacement d’exportation, la taille de l’exportation, etc. Le manifeste est nommé au format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Affichez un [exemple de fichier manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier de manifeste comprend les champs suivants :
   * `flowRunId` : [exécution de flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.
   * `scheduledTime` : heure en UTC à laquelle le fichier a été exporté.
   * `exportResults.sinkPath` : chemin d’accès dans l’emplacement de stockage où le fichier exporté est déposé.
   * `exportResults.name` : nom du fichier exporté.
   * `size` : taille du fichier exporté, en octets.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activation des données d’audience vers des destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Planification

Dans l’étape **[!UICONTROL Planifier]**, vous pouvez [configurer le planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre destination [!DNL Data Landing Zone] et vous pouvez également [configurer le nom de vos fichiers exportés](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapper les attributs et les identités {#map}

Dans l’étape **[!UICONTROL Mappage]**, vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez le stockage [!DNL Data Landing Zone] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
