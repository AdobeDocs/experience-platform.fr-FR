---
title: Création d’une connexion Source Chatlio dans l’interface utilisateur
description: Découvrez comment créer une connexion source Chatlio à l’aide de l’interface utilisateur de Adobe Experience Platform.
badge: Version bêta
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '1156'
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

### Exemple JSON pour définir le schéma source pour [!DNL Chatlio] {#prerequisites-json-schema}

Avant de créer une connexion source [!DNL Chatlio], vous devez fournir un schéma source. Vous pouvez utiliser le fichier JSON ci-dessous.

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

### Création d’un schéma de plateforme pour [!DNL Chatlio] {#create-platform-schema}

Vous devez également vous assurer de créer un schéma Platform à utiliser pour votre source. Lisez le tutoriel sur la [création d’un schéma de plateforme](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

![L’interface utilisateur de Platform présentant un exemple de schéma pour Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## Connecter votre compte [!DNL Chatlio] {#connect-account}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] et afficher un catalogue de sources disponibles dans Experience Platform.

Utilisez le menu *[!UICONTROL Catégories]* pour filtrer les sources par catégorie. Vous pouvez également saisir un nom de source dans la barre de recherche pour trouver une source spécifique dans le catalogue.

Accédez à la catégorie [!UICONTROL Automatisation marketing] pour afficher la carte source [!DNL Chatlio]. Pour commencer, sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue de l’interface utilisateur de Platform avec carte Chatlio](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## Sélectionner les données {#select-data}

L’étape **[!UICONTROL Sélectionner les données]** s’affiche, vous permettant ainsi de sélectionner les données à importer dans Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Télécharger des fichiers]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau [!UICONTROL Glisser-déposer des fichiers].

![L’étape d’ajout de données du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

Une fois le fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Search field] pour accéder à des éléments spécifiques à partir de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape d’aperçu du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## Détails du flux de données {#dataflow-detail}

L’étape **Détails du flux de données** s’affiche, vous fournissant des options permettant d’utiliser un jeu de données existant ou d’établir un nouveau jeu de données pour votre flux de données, ainsi qu’une opportunité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer des paramètres pour l’ingestion de profils, les diagnostics d’erreur, l’ingestion partielle et les alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données du flux de sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## Mappage {#mapping}

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [guide de l’interface utilisateur de la préparation des données](../../../../../data-prep/ui/mapping.md).

Les mappages répertoriés ci-dessous sont obligatoires et doivent être configurés avant de passer à l’étape [!UICONTROL Révision].

| Champ cible | Description |
| --- | --- |
| `UUID` | L’identifiant [!DNL Chatlio] de l’événement. |

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## Révision {#review}

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision du workflow des sources.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## Obtention de l’URL de votre point de terminaison de diffusion {#get-streaming-endpoint-url}

Une fois votre flux de données de diffusion en continu créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform.

Pour construire l’URL utilisée pour configurer le webhook sur [!DNL Chatlio], vous devez récupérer les éléments suivants :

* **[!UICONTROL Identifiant de flux de données]**
* **[!UICONTROL Point d’entrée de diffusion en continu]**

Pour récupérer votre **[!UICONTROL identifiant de flux de données]** et votre **[!UICONTROL point d’entrée de flux]**, accédez à la page [!UICONTROL activité de flux de données] du flux de données que vous venez de créer et copiez les détails depuis le bas du panneau [!UICONTROL Propriétés].

![Le point d’entrée de diffusion en continu dans l’activité de flux de données.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

Une fois que vous avez récupéré votre point de terminaison de diffusion en continu et votre identifiant de flux de données, créez une URL basée sur le modèle suivant : ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. Par exemple, une URL webhook construite peut se présenter comme suit : ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## Configuration du webhook dans [!DNL Chatlio] {#set-up-webhook}

Une fois votre URL webhook créée, vous pouvez configurer votre webhook à l’aide de l’interface utilisateur [!DNL Chatlio].

Connectez-vous à votre compte [[!DNL Chatlio]](https://chatlio.com/) et suivez [le guide de configuration et d&#39;installation](https://chatlio.com/docs/setup/) pour créer un widget.

Une fois qu’un widget est créé, accédez à la page des paramètres du widget pour ajouter l’URL du webhook à ce widget.

![Page des paramètres webhook sur Chatlio.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

Ensuite, sélectionnez l’onglet **[!DNL Behavior]** et ajoutez votre URL webhook au champ *[!DNL Webhook when a new conversation starts]* et aux autres champs d’événements webhook auxquels vous souhaitez vous abonner.

![L’interface utilisateur de Chatlio affichant le champ de point de terminaison webhook.](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>Vous pouvez vous abonner à divers événements pour votre webhook [!DNL Chatlio]. Pour plus d&#39;informations sur les différents événements, consultez la [[!DNL Chatlio] documentation sur les événements](https://chatlio.com/docs/webhooks/).

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez correctement configuré un flux de données en continu pour importer vos données [!DNL Chatlio] dans Experience Platform. Pour surveiller les données ingérées, reportez-vous au guide sur la [surveillance des flux de données en continu à l’aide de l’interface utilisateur de Platform](../../monitor-streaming.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL Chatlio].

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et que les messages [!DNL Chatlio] sont ingérés, procédez comme suit :

* Vous pouvez consulter la page [!DNL Chatlio] **[!UICONTROL Rapports]** > **[!UICONTROL Historique de conversation]** pour identifier les événements capturés par [!DNL Chatlio].

![Copie d’écran de l’interface utilisateur de Chatlio montrant l’historique de la conversation](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Afficher les flux de données]** en regard du menu de carte [!DNL Chatlio] du catalogue des sources. Ensuite, sélectionnez **[!UICONTROL Prévisualiser le jeu de données]** pour vérifier les données ingérées pour les webhooks que vous avez configurés dans [!DNL Chatlio].

![Copie d’écran de l’interface utilisateur de Platform montrant les événements ingérés](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

Pour plus d&#39;informations sur [!DNL Chatlio], consultez la [[!DNL Chatlio] documentation](https://chatlio.com/docs/) et la [FAQ](https://chatlio.com/pricing/#FAQ).
