---
title: Création d’une connexion Chatlio Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Chatlio à l’aide de l’interface utilisateur de Adobe Experience Platform.
badge: Beta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 21%

---

# Créer une connexion source [!DNL Chatlio] dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Chatlio] est en version Beta. Veuillez lire la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Chatlio] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Conditions préalables {#prerequisites}

La section suivante fournit des informations sur les conditions préalables à remplir avant de pouvoir créer une connexion source [!DNL Chatlio].

### Exemple de JSON pour définir le schéma source de [!DNL Chatlio] {#prerequisites-json-schema}

Avant de créer une connexion source [!DNL Chatlio], vous devez disposer d’un schéma source. Vous pouvez utiliser le fichier JSON ci-dessous.

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### Création d’un schéma Experience Platform pour [!DNL Chatlio] {#create-platform-schema}

Vous devez également vous assurer de créer un schéma Experience Platform à utiliser pour votre source. Lisez le tutoriel sur la [création d’un schéma Experience Platform](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

![Interface utilisateur d’Experience Platform présentant un exemple de schéma pour Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Connecter votre compte [!DNL Chatlio] {#connect-account}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] et consulter un catalogue de sources disponibles dans Experience Platform.

Utilisez le menu *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique à partir du catalogue.

Accédez à la catégorie [!UICONTROL Automatisation du marketing] pour afficher la carte source du [!DNL Chatlio]. Pour commencer, sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue de l’interface utilisateur d’Experience Platform avec la carte Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Sélectionner les données {#select-data}

L’étape **[!UICONTROL Sélectionner les données]** s’affiche, fournissant une interface vous permettant de sélectionner les données que vous souhaitez importer dans Experience Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Télécharger des fichiers]** pour télécharger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau [!UICONTROL Glisser-déposer des fichiers].

![Étape d’ajout de données du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Une fois votre fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface de prévisualisation vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques à partir de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape de prévisualisation du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Détails du flux de données {#dataflow-detail}

L’étape **Détails du flux de données** s’affiche, vous offrant des options pour utiliser un jeu de données existant ou établir un nouveau jeu de données pour votre flux de données, ainsi que la possibilité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer les paramètres d’ingestion de profil, de diagnostics d’erreur, d’ingestion partielle et d’alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Étape du flux de données-détail du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mappage {#mapping}

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [&#x200B; Guide de l’interface utilisateur de la préparation des données &#x200B;](../../../../../data-prep/ui/mapping.md).

Les mappages répertoriés ci-dessous sont obligatoires et doivent être configurés avant de passer à l’étape [!UICONTROL Révision].

| Champ cible | Description |
| --- | --- |
| `UUID` | Identifiant [!DNL Chatlio] de l’événement. |

Une fois vos données source mappées, sélectionnez **[!UICONTROL Suivant]**.

![Étape de mappage du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Révision {#review}

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![Étape de révision du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Obtention de l’URL du point d’entrée de diffusion en continu {#get-streaming-endpoint-url}

Une fois votre flux de données en continu créé, vous pouvez récupérer votre URL de point d’entrée en continu. Ce point d’entrée sera utilisé pour vous abonner à votre webhook, ce qui permettra à votre source de diffusion en continu de communiquer avec Experience Platform.

Pour construire l’URL utilisée pour configurer le webhook sur [!DNL Chatlio], vous devez récupérer les éléments suivants :

* **[!UICONTROL Identifiant du flux de données]**
* **[!UICONTROL Point d’entrée de diffusion en continu]**

Pour récupérer vos **[!UICONTROL ID de flux de données]** et **[!UICONTROL Point d’entrée de diffusion en continu]**, accédez à la page [!UICONTROL Activité de flux de données] du flux de données que vous venez de créer et copiez les détails au bas du panneau [!UICONTROL Propriétés].

![Point d’entrée de flux continu dans l’activité de flux de données.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Une fois que vous avez récupéré votre point d’entrée de diffusion en continu et votre identifiant de flux de données, créez une URL basée sur le modèle suivant : ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Par exemple, une URL webhook construite peut ressembler à ceci : ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Configuration du webhook dans [!DNL Chatlio] {#set-up-webhook}

Une fois l’URL de webhook créée, vous pouvez configurer votre webhook à l’aide de l’interface utilisateur [!DNL Chatlio].

Connectez-vous à votre compte [[!DNL Chatlio]](https://chatlio.com/) et suivez [le guide d’installation et de configuration](https://chatlio.com/docs/setup/) pour créer un widget.

Une fois un widget créé, accédez à la page des paramètres du widget pour ajouter votre URL webhook à ce widget.

![La page des paramètres webhook sur Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Sélectionnez ensuite l’onglet **[!DNL Behavior]** et ajoutez votre URL webhook au champ *[!DNL Webhook when a new conversation starts]* et à tout autre champ d’événements webhook auquel vous souhaitez vous abonner.

![Interface utilisateur de Chatlio affichant le champ de point d’entrée webhook.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Vous pouvez vous abonner à différents événements pour votre webhook [!DNL Chatlio]. Pour plus d’informations sur les différents événements, reportez-vous à la documentation [[!DNL Chatlio] événements](https://chatlio.com/docs/webhooks/).

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez configuré un flux de données en continu pour importer vos données [!DNL Chatlio] dans Experience Platform. Pour surveiller les données ingérées, reportez-vous au guide sur la [surveillance des flux de données en flux continu à l’aide de l’interface utilisateur d’Experience Platform](../../monitor-streaming.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL Chatlio].

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et [!DNL Chatlio] messages sont ingérés, procédez comme suit :

* Vous pouvez vérifier la page [!DNL Chatlio] **[!UICONTROL Rapports]** > **[!UICONTROL Historique de conversation]** pour identifier les événements capturés par [!DNL Chatlio].

![Capture d’écran de l’interface utilisateur de Chatlio montrant l’historique des conversations](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Afficher les flux de données]** à côté du menu de carte [!DNL Chatlio] dans le catalogue de sources. Sélectionnez ensuite **[!UICONTROL Prévisualiser le jeu de données]** pour vérifier les données ingérées pour les Webhooks que vous avez configurés dans [!DNL Chatlio].

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant les événements ingérés](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Pour plus d’informations sur les [!DNL Chatlio], consultez les [[!DNL Chatlio] documentation](https://chatlio.com/docs/) et [FAQ](https://chatlio.com/pricing/#FAQ).
