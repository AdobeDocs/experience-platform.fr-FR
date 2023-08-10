---
title: Création d’une connexion source Pendo dans l’interface utilisateur
description: Découvrez comment créer une connexion source Pendo à l’aide de l’interface utilisateur de Adobe Experience Platform.
badge: Version Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: 249a12e6a079e3c99bf13bec4bf83b2a53cd522b
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 21%

---

# Créez un [!DNL Pendo] Flux de données de connexion source et dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Pendo] est en version Beta. Voir [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Pendo] connexion source et flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Conditions préalables {#prerequisites}

La section suivante fournit des informations sur les conditions préalables à la création d’un [!DNL Pendo] connexion source.

### Exemple de fichier JSON pour définir le schéma source pour [!DNL Pendo] {#prerequisites-json-schema}

Avant de créer un [!DNL Pendo] connexion source, un schéma source doit être fourni. Vous pouvez utiliser le fichier JSON ci-dessous.

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

Pour plus d’informations, consultez la section [[!DNL Pendo] guide sur les webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Création d’un schéma Platform pour [!DNL Pendo] {#create-platform-schema}

Vous devez également veiller à créer au préalable un schéma Platform à utiliser pour votre source. Voir le tutoriel sur [création d’un schéma Platform](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

![L’interface utilisateur de Platform affiche un exemple de schéma pour Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Connecter votre compte [!DNL Pendo] {#connect-account}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Sources] workspace et afficher un catalogue de sources disponibles dans Experience Platform.

Utilisez la variable *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique dans le catalogue.

Accédez au [!UICONTROL Analytics] pour afficher la catégorie [!DNL Pendo] carte source. Pour commencer, sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources de l’interface utilisateur de Platform avec la carte Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Sélectionner les données {#select-data}

La variable **[!UICONTROL Sélectionner des données]** s’affiche, fournissant une interface vous permettant de sélectionner les données à importer dans Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionner **[!UICONTROL Chargement de fichiers]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le [!UICONTROL Glisser-déposer des fichiers] du panneau.

![L’étape d’ajout de données du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Une fois le fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser la variable [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape d’aperçu du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Détails du flux de données {#dataflow-detail}

La variable **Détails du flux de données** s’affiche, vous fournissant des options permettant d’utiliser un jeu de données existant ou d’établir un nouveau jeu de données pour votre flux de données, ainsi qu’une opportunité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer des paramètres pour l’ingestion de profils, les diagnostics d’erreur, l’ingestion partielle et les alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données du processus des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappage {#mapping}

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, voir la section [Guide de l’interface utilisateur de la préparation de données](../../../../../data-prep/ui/mapping.md).

Les mappages répertoriés ci-dessous sont obligatoires et doivent être configurés avant de passer à la [!UICONTROL Réviser] scène.

| Champ cible | Description |
| --- | --- |
| `uniqueId` | La variable [!DNL Pendo] identifiant de l’événement. |

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Révision {#review}

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision du processus des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Obtention de l’URL de votre point de terminaison de diffusion {#get-streaming-endpoint-url}

Une fois votre flux de données de diffusion en continu créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform.

Pour construire l’URL utilisée pour configurer le webhook sur [!DNL Pendo] vous devez récupérer les éléments suivants :

* **[!UICONTROL Identifiant de flux de données]**
* **[!UICONTROL Point de terminaison de diffusion]**

Pour récupérer votre **[!UICONTROL Identifiant de flux de données]** et **[!UICONTROL Point de terminaison de diffusion]**, accédez au [!UICONTROL Activité Flux de données] de la page du flux de données que vous venez de créer et de copier les détails depuis le bas de la page [!UICONTROL Propriétés] du panneau.

![Point de terminaison de diffusion en continu dans l’activité de flux de données.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Une fois que vous avez récupéré votre point de terminaison de diffusion en continu et votre identifiant de flux de données, créez une URL basée sur le modèle suivant : ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Par exemple, une URL webhook construite peut se présenter comme suit : ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## Configuration de Webhook dans [!DNL Pendo] {#set-up-webhook}

Ensuite, connectez-vous à votre compte sur [[!DNL Pendo]](https://pendo.io/) et créez un webhook. Pour savoir comment créer un webhook à l’aide de la variable [!DNL Pendo] , reportez-vous à la section [[!DNL Pendo] guide de création de webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Une fois votre webhook créé, accédez à la page des paramètres de votre [!DNL Pendo] webhook et entrez votre URL webhook dans [!DNL URL] champ .

![Capture d’écran de l’interface utilisateur de Pendo montrant le champ de point de terminaison webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Vous pouvez vous abonner à différentes catégories d’événements afin de déterminer le type d’événements que vous souhaitez envoyer à partir de votre [!DNL Pendo] vers Platform. Pour plus d’informations sur les différents événements, reportez-vous au [[!DNL Pendo] documentation](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez correctement configuré un flux de données en continu pour importer votre [!DNL Pendo] données à Experience Platform. Pour surveiller les données en cours d’ingestion, reportez-vous au guide sur [surveillance des flux de données en continu à l’aide de l’interface utilisateur de Platform](../../monitor-streaming.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous contiennent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la variable [!DNL Pendo] source.

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et [!DNL Pendo] les messages sont en cours d’ingestion. Procédez comme suit :

* Vous pouvez vérifier les [!DNL Pendo] **[!UICONTROL Rapports]** > **[!UICONTROL Historique des conversations]** pour identifier les événements capturés par [!DNL Pendo].

![Capture d’écran de l’interface utilisateur de Pendo montrant l’historique des conversations](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Afficher les flux de données]** en regard de la variable [!DNL Pendo] menu de carte dans le catalogue des sources. Ensuite, sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]** pour vérifier les données ingérées pour les webhooks dans lesquels vous avez configuré [!DNL Pendo].

![Copie d’écran de l’interface utilisateur de Platform montrant les événements ingérés](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Erreurs et résolution des problèmes {#errors-and-troubleshooting}

Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Copie d’écran de l’interface utilisateur de Platform affichant l’erreur.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Pour corriger cette erreur, vous devez vérifier que la variable *uniqueID* a été configuré. Pour plus d’informations, reportez-vous au [Mmbox](#mapping) .

Pour plus d’informations, voir [[!DNL Pendo] Centre d’aide](https://www.pendo.io/help-center/).
