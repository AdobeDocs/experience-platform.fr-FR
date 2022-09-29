---
title: Connexion Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services offre une plateforme pour concevoir des expériences client cross-canal et un environnement pour l’orchestration visuelle des campagnes, la gestion des interactions en temps réel et l’exécution cross-canal.
source-git-commit: 10dc6ac0f78237f8d6bea01d63d07e61662278df
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Connexion Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

## Présentation {#overview}

Adobe Campaign Managed Cloud Services offre une plateforme pour concevoir des expériences client cross-canal et un environnement pour l’orchestration visuelle des campagnes, la gestion des interactions en temps réel et l’exécution cross-canal. [Prise en main de Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

En utilisant Campaign, vous pouvez :
* Favoriser la personnalisation et l’engagement par le biais d’une vue unique et accessible du client,
* Intégrer les canaux e-mail, mobiles, en ligne et hors ligne au parcours client,
* Automatiser la diffusion de messages et d’offres pertinents et opportuns.

>[!IMPORTANT]
>
>Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de la connexion Adobe Campaign Managed Cloud Services :
>
>* 50 segments au maximum peuvent être [activé](#activate) pour la destination,
>* Pour chaque segment, vous pouvez ajouter jusqu’à 20 champs à la variable [map](#map) vers Adobe Campaign,
>* Conservation des données sur la zone d’entrée des données de stockage Azure Blob (DLZ) : 7 jours,
>* La fréquence d&#39;activation est d&#39;au moins 3 heures.


## Cas d&#39;utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination de gestion du service Adobe Campaign, voici un exemple de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

Adobe Experience Platform crée un profil client qui incorpore des informations telles que le graphique d’identités, les données comportementales des analyses, fusionne les données hors ligne et en ligne, etc. Avec cette intégration, vous pouvez augmenter les fonctionnalités de segmentation qui existent déjà dans Adobe Campaign avec ces audiences Adobe Experience Platform, et vous pouvez donc activer ces données dans Campaign.

Par exemple, une société de vêtements de sport souhaite exploiter les segments intelligents optimisés par Adobe Experience Platform et les activer à l’aide d’Adobe Campaign pour atteindre sa base de clients via les différents canaux pris en charge par Adobe Campaign.

Une fois les messages envoyés, ils souhaitent améliorer le profil client dans Adobe Experience Platform avec les données d’expérience d’Adobe Campaign telles que les envois, les ouvertures et les clics.

Il en résulte des campagnes cross-canal plus cohérentes dans l’écosystème cloud d’Adobe Experience Cloud et un profil client riche qui s’adapte et apprend rapidement.

[En savoir plus sur l’intégration d’Adobe Campaign à Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)


## Conditions préalables {#prerequisites}

Pour que Campaign puisse récupérer des données à partir de Adobe Experience Platform, vous devez créer un projet d’API Campaign et demander à l’assistance clientèle d’ajouter l’identifiant client associé à une liste autorisée.

>[!NOTE]
>
>Les informations générales sur la création d’un projet d’API sont présentées dans la section [cette documentation](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman.html)

1. Connectez-vous à [Console Adobe Developer](https://console.adobe.io/) et créez un projet.

1. Sélectionner **[!UICONTROL Ajout d’une API]** et choisissez **[!UICONTROL Adobe Campaign]**.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/create-api.png)

1. Générez une paire de clés.

1. Sélectionnez la `<Instance Name> - admin` profil de produit et sélectionnez **[!UICONTROL Enregistrer l’API configurée]**.

1. Votre projet d’API est créé. Notez que **[!UICONTROL ID client]** affiché dans votre projet. Contactez le service à la clientèle et demandez-lui d’ajouter votre ID de client à une liste autorisée.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/client-id.png)

## Identités prises en charge {#supported-identities}

*Adobe Campaign Managed Cloud Services* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. Nous vous recommandons d’utiliser cette identité et de la mapper à l’identifiant de votre instance Campaign qui représente le client (loyalty_ID, account_ID, customer_ID..). |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consultez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| GAID | Google Advertising ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Sélectionner une instance]**: Votre **[!DNL Campaign]** instance marketing.
* **[!UICONTROL Mapping de ciblage]**: Sélectionnez le mapping de ciblage que vous utilisez dans **[!DNL Adobe Campaign]** pour envoyer des diffusions. [En savoir plus](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d&#39;informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Politiques de gouvernance et actions d’application {#governance}

Sélectionnez les actions marketing applicables aux données que vous souhaitez exporter vers la destination. Pour Adobe Campaign, il est recommandé de sélectionner la variable **[!UICONTROL Ciblage des emails]** action marketing.

Pour plus d’informations sur les actions marketing, voir [présentation des stratégies d’utilisation des données](/help/data-governance/policies/overview.md) page.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) pour obtenir des instructions sur l’activation des données d’audience vers cette destination.

### Mise en correspondance des attributs et des identités {#map}

Sélectionnez les champs XDM à exporter avec les profils et les mappez aux champs Adobe Campaign correspondants.[En savoir plus sur la sélection des identités et des attributs pour les destinations de marketing par e-mail](overview.md)

1. Sélectionner les champs source :

   * Sélectionnez une **identifier** (Par exemple : le champ email ) comme identité source qui identifie de manière unique un profil dans Adobe Experience Platform et Adobe Campaign.

   * Tout autre **Attributs de profil source XDM** qui doivent être exportés vers Adobe Campaign.
   >[!NOTE]
   >
   >Le champ &quot;segmentMembershipStatus&quot; est un mappage obligatoire pour refléter l’état segmentMembership. Ce champ est ajouté par défaut et ne peut pas être modifié ni supprimé.

1. Mappez chaque champ avec son champ cible dans Adobe Campaign. Les champs de cible disponibles sont déterminés par le mapping de ciblage sélectionné lors de la [création de la destination](#destination-details).

1. Identifiez les attributs obligatoires et les clés de déduplication. Notez que les valeurs des attributs marqués comme &quot;Obligatoire&quot; ou &quot;Clé de déduplication&quot; ne peuvent pas être nulles.

   * [Attributs obligatoires](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) assurez-vous que tous les enregistrements de profil contiennent le ou les attributs sélectionnés. Par exemple : tous les profils exportés contiennent une adresse email. Il est recommandé de définir sur obligatoire le champ d’identité et le champ utilisés comme clé de déduplication.
   * [Clé de déduplication](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) est une clé Principale qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils.

      >[!IMPORTANT]
      >
      >Assurez-vous que le nom de l&#39;attribut de clé de déduplication correspond à un nom de colonne du mapping de ciblage sélectionné.
   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Une fois le mappage effectué, vous pouvez vérifier et terminer la configuration de destination pour commencer à envoyer des données à **[!DNL Campaign]**.
   [Découvrez comment passer en revue et terminer la configuration de destination](/help/destinations/destination-types.md#review).

## Données exportées / Validation de l’exportation des données {#exported-data}

Une fois une destination activée, vous pouvez accéder au traitement correspondant et aux données exportées dans Campaign.

### Surveillance des traitements d’exportation de données {#jobs}

Accédez au **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Tâches de chargement d’audience]** pour surveiller toutes les tâches d’exportation activées à partir de Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Accès aux données exportées {#data}

Accédez au **[!UICONTROL Profil et cible]** > **[!UICONTROL Liste]** > **[!UICONTROL Audiences AEP]** pour accéder aux audiences créées après l’activation d’une destination.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
