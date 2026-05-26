---
title: Création d’une connexion Pendo Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Pendo à l’aide de l’interface utilisateur de Adobe Experience Platform.
badge: Beta
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
TQID: https://experienceleague.adobe.com/gFL7p-MHd8GMYuCpucyLKTR8Osi0osI5nfBiQ3EboCI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: f3ebbec0f5000c05bb5c40654b010073ef0f9658
workflow-type: tm+mt
source-wordcount: 1199
ht-degree: 12%

---

# Créer un flux de données de connexion source [!DNL Pendo] et dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Pendo] est en version Beta. Veuillez lire la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Pendo] et un flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Conditions préalables {#prerequisites}

La section suivante fournit des informations sur les conditions préalables à remplir avant de pouvoir créer une connexion source [!DNL Pendo].

### Exemple de JSON pour définir le schéma source de [!DNL Pendo] {#prerequisites-json-schema}

Avant de créer une connexion source [!DNL Pendo], vous devez disposer d’un schéma source. Vous pouvez utiliser le fichier JSON ci-dessous.

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

Pour plus d’informations, consultez le [[!DNL Pendo] guide sur les Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### Création d’un schéma Experience Platform pour [!DNL Pendo] {#create-platform-schema}

Vous devez également vous assurer d’abord de créer un schéma Experience Platform à utiliser pour votre source. Pour obtenir des instructions complètes sur la création d’un schéma](../../../../../xdm/schema/composition.md) consultez le tutoriel sur la [création d’un schéma Experience Platform).

![Interface utilisateur d’Experience Platform montrant un exemple de schéma pour Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## Connecter votre compte [!DNL Pendo] {#connect-account}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] et consulter le catalogue des sources disponibles dans Experience Platform.

Utilisez le menu *[!UICONTROL Categories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique à partir du catalogue.

Accédez à la catégorie [!UICONTROL Analytics] pour afficher la carte source [!DNL Pendo]. Pour commencer, sélectionnez **[!UICONTROL Add data]**.

![Le catalogue source de l’interface utilisateur d’Experience Platform avec la carte Pendo.](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## Sélectionner les données {#select-data}

L’étape **[!UICONTROL Select data]** s’affiche, fournissant une interface vous permettant de sélectionner les données que vous souhaitez importer dans Experience Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Upload files]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau [!UICONTROL Drag and drop files].

![Étape d’ajout de données du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

Une fois votre fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface de prévisualisation vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Search field] pour accéder à des éléments spécifiques depuis votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Next]**.

![Étape de prévisualisation du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## Détails du flux de données {#dataflow-detail}

L’étape **Détails du flux de données** s’affiche, vous offrant des options pour utiliser un jeu de données existant ou établir un nouveau jeu de données pour votre flux de données, ainsi que la possibilité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer les paramètres d’ingestion de profil, de diagnostics d’erreur, d’ingestion partielle et d’alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Next]**.

![Étape du flux de données-détail du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## Mappage {#mapping}

L’étape [!UICONTROL Mapping] s’affiche, vous fournissant une interface pour mapper les champs source de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [ Guide de l’interface utilisateur de la préparation des données ](../../../../../data-prep/ui/mapping.md).

Les mappages répertoriés ci-dessous sont obligatoires et doivent être configurés avant de passer à l’étape [!UICONTROL Review].

| Champ cible | Description |
| --- | --- |
| `uniqueId` | Identifiant [!DNL Pendo] de l’événement. |

Une fois les données sources mappées, sélectionnez **[!UICONTROL Next]**.

![Étape de mappage du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## Réviser {#review}

L’étape **[!UICONTROL Review]** s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connection]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Assign dataset & map fields]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez révisé votre flux de données, sélectionnez **[!UICONTROL Finish]** et patientez quelques instants le temps que le flux de données soit créé.

![Étape de révision du workflow des sources.](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## Obtention de l’URL du point d’entrée de diffusion en continu {#get-streaming-endpoint-url}

Une fois votre flux de données en continu créé, vous pouvez récupérer votre URL de point d’entrée en continu. Ce point d’entrée sera utilisé pour vous abonner à votre webhook, ce qui permettra à votre source de diffusion en continu de communiquer avec Experience Platform.

Pour construire l’URL utilisée pour configurer le webhook sur [!DNL Pendo], vous devez récupérer les éléments suivants :

* **[!UICONTROL Dataflow ID]**
* **[!UICONTROL Streaming endpoint]**

Pour récupérer vos **[!UICONTROL Dataflow ID]** et **[!UICONTROL Streaming endpoint]**, accédez à la page [!UICONTROL Dataflow activity] du flux de données que vous venez de créer et copiez les détails depuis le bas du panneau [!UICONTROL Properties].

![Point d’entrée de flux continu dans l’activité de flux de données.](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

Une fois que vous avez récupéré votre point d’entrée de diffusion en continu et votre identifiant de flux de données, créez une URL basée sur le modèle suivant : `{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}`. Par exemple, une URL webhook construite peut ressembler à ceci : `https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95`

## Configuration du Webhook dans [!DNL Pendo] {#set-up-webhook}

Ensuite, connectez-vous à votre compte sur [[!DNL Pendo]](https://pendo.io/) et créez un webhook. Pour savoir comment créer un webhook à l’aide de l’interface utilisateur [!DNL Pendo], reportez-vous au guide [[!DNL Pendo]  sur la création d’un webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

Une fois votre webhook créé, accédez à la page des paramètres de votre webhook [!DNL Pendo] et saisissez l’URL de votre webhook dans le champ [!DNL URL] .

![Capture d’écran de l’interface utilisateur Pendo affichant le champ de point d’entrée webhook](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>Vous pouvez vous abonner à différentes catégories d’événements pour déterminer le type d’événements à envoyer de votre instance [!DNL Pendo] à Experience Platform. Pour plus d’informations sur les différents événements, reportez-vous à la [[!DNL Pendo] documentation](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez configuré un flux de données en continu pour importer vos données [!DNL Pendo] dans Experience Platform. Pour surveiller les données ingérées, reportez-vous au guide sur la [surveillance des flux de données en flux continu à l’aide de l’interface utilisateur d’Experience Platform](../../monitor-streaming.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL Pendo].

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et [!DNL Pendo] messages sont ingérés, procédez comme suit :

* Vous pouvez vérifier la page [!DNL Pendo] **[!UICONTROL Reports]** > **[!UICONTROL Chat History]** pour identifier les événements capturés par [!DNL Pendo].

![Capture d’écran de l’interface utilisateur de Pendo montrant l’historique des conversations](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL View Dataflows]** à côté du menu de carte [!DNL Pendo] dans le catalogue de sources. Sélectionnez ensuite **[!UICONTROL Preview dataset]** pour vérifier les données ingérées pour les Webhooks que vous avez configurés dans [!DNL Pendo].

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant les événements ingérés](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### Erreurs et résolution des problèmes {#errors-and-troubleshooting}

Lors de la vérification d’une exécution de flux de données, vous pouvez rencontrer le message d’erreur suivant : `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Capture d’écran de l’interface utilisateur d’Experience Platform affichant une erreur.](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

Pour corriger cette erreur, vous devez vérifier que le mappage *uniqueID* a été configuré. Pour plus d’informations, consultez la section [ Mappage ](#mapping).

Pour plus d&#39;informations, consultez le [[!DNL Pendo] Centre d&#39;aide](https://www.pendo.io/help-center/).
