---
title: Connexion à Adobe Campaign Managed Cloud Services
description: Adobe Campaign Managed Cloud Services offre une plateforme pour concevoir des expériences client cross-canal et un environnement pour l’orchestration visuelle des campagnes, la gestion des interactions en temps réel et l’exécution cross-canal.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 35%

---

# Connexion à Adobe Campaign Managed Cloud Services {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Cette intégration fonctionne avec [Adobe Campaign version 8.4 ou ultérieure](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Vue d’ensemble {#overview}

Adobe Campaign Managed Cloud Services offre une plateforme pour concevoir des expériences client cross-canal ainsi qu’un environnement pour l’orchestration visuelle de campagnes, la gestion d’interactions en temps réel et l’exécution cross-canal. [Prise en main de Campaign](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=fr)

En utilisant Campaign, vous pouvez :
* Stimuler la personnalisation et l&#39;engagement au travers d&#39;une vue accessible unique du client,
* Intégrer les canaux email, mobile, en ligne et hors ligne dans le parcours client,
* Automatisez la diffusion de messages et d’offres pertinents et en temps voulu.

>[!IMPORTANT]
>
>Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de la connexion Adobe Campaign Managed Cloud Services :
>
>* 50 segments au maximum peuvent être [activé](#activate) pour la destination,
>* Pour chaque segment, vous pouvez ajouter jusqu’à 20 champs à la variable [map](#map) vers Adobe Campaign,
>* Conservation des données sur la zone d’entrée des données de stockage Azure Blob (DLZ) : 7 jours,
>* La fréquence d&#39;activation est d&#39;au moins 3 heures.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination de gestion du service Adobe Campaign, voici un exemple de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

* Adobe Experience Platform crée un profil client qui incorpore des informations telles que le graphique d’identités, les données comportementales des analyses, fusionne les données hors ligne et en ligne, etc. Avec cette intégration, vous pouvez augmenter les fonctionnalités de segmentation qui existent déjà dans Adobe Campaign avec ces audiences Adobe Experience Platform, et vous pouvez donc activer ces données dans Campaign.

  Par exemple, une société de vêtements de sport souhaite exploiter les segments intelligents optimisés par Adobe Experience Platform et les activer à l’aide d’Adobe Campaign pour atteindre sa base de clients via les différents canaux pris en charge par Adobe Campaign. Une fois les messages envoyés, ils souhaitent améliorer le profil client dans Adobe Experience Platform avec les données d’expérience d’Adobe Campaign telles que les envois, l’ouverture et les clics.

  Il en résulte des campagnes cross-canal plus cohérentes dans l’écosystème Experience Cloud d’Adobe et un profil client riche qui s’adapte et apprend rapidement.


* Outre l’activation des segments dans Campaign, vous pouvez utiliser la destination Managed Services Adobe Campaign pour importer des attributs de profil supplémentaires liés à un profil sur Adobe Experience Platform et avoir un processus de synchronisation en place afin qu’ils soient mis à jour dans la base de données Adobe Campaign.

  Supposons, par exemple, que vous capturiez des valeurs d&#39;opt-in et d&#39;opt-out dans Adobe Experience Platform. Avec cette connexion, vous pouvez importer ces valeurs dans Adobe Campaign et mettre en place un processus de synchronisation afin de les mettre à jour régulièrement.

  >[!NOTE]
  >
  >La synchronisation des attributs de profil est disponible pour les profils déjà présents dans la base de données Adobe Campaign.

[En savoir plus sur l’intégration d’Adobe Campaign à Adobe Experience Platform](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=fr)

## Identités prises en charge {#supported-identities}

*Adobe Campaign Managed Cloud Services* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. Nous vous recommandons d’utiliser cette identité et de la mapper à l’identifiant de votre instance Campaign qui représente le client (loyalty_ID, account_ID, customer_ID..). |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| GAID | Google Advertising ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Sélectionner une instance]**: votre **[!DNL Campaign]** instance marketing.
* **[!UICONTROL Mapping de ciblage]**: sélectionnez le mapping de ciblage utilisé dans **[!DNL Adobe Campaign]** pour envoyer des diffusions. [En savoir plus](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Sélectionner le type de synchronisation]**:

   * **[!UICONTROL Synchronisation de l’audience]**: utilisez cette option pour envoyer des audiences Adobe Experience Platform vers Adobe Campaign.
   * **[!UICONTROL Synchronisation des profils (mise à jour uniquement)]**: utilisez cette option pour importer les attributs de profil Adobe Experience Platform dans Adobe Campaign et mettre en place un processus de synchronisation afin qu’ils puissent être mis à jour régulièrement.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d&#39;informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Politiques de gouvernance et actions d’application {#governance}

Sélectionnez les actions marketing applicables aux données que vous souhaitez exporter vers la destination. Pour Adobe Campaign, il est recommandé de sélectionner la variable **[!UICONTROL Ciblage des emails]** action marketing.

Pour plus d’informations sur les actions marketing, consultez la page [présentation des politiques d’utilisation des données](/help/data-governance/policies/overview.md).

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) pour obtenir des instructions sur l’activation des données d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Sélectionnez les champs XDM à exporter avec les profils et les mappez aux champs Adobe Campaign correspondants.[En savoir plus sur la sélection des identités et des attributs pour les destinations de marketing par e-mail](overview.md)

1. Sélectionner les champs source :

   * Sélectionnez une **identifier** (Par exemple : le champ email) comme identité source qui identifie de manière unique un profil dans Adobe Experience Platform et Adobe Campaign.

   * Tout autre **Attributs de profil source XDM** qui doivent être exportés vers Adobe Campaign.

   >[!NOTE]
   >
   >Le champ &quot;segmentMembershipStatus&quot; est un mappage obligatoire pour refléter l’état segmentMembership. Ce champ est ajouté par défaut et ne peut pas être modifié ni supprimé.

1. Mappez chaque champ avec son champ cible dans Adobe Campaign. Les champs de cible disponibles sont déterminés par le mapping de ciblage sélectionné lors de la [création de la destination](#destination-details).

1. Identifiez les attributs obligatoires et les clés de déduplication. Notez que les valeurs des attributs marqués comme &quot;Obligatoire&quot; ou &quot;Clé de déduplication&quot; ne peuvent pas être nulles.

   * [Attributs obligatoires](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) assurez-vous que tous les enregistrements de profil contiennent le ou les attributs sélectionnés. Par exemple : tous les profils exportés contiennent une adresse email. Il est recommandé de définir sur obligatoire le champ d’identité et le champ utilisés comme clé de déduplication.
   * [Clé de déduplication](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) est une clé primaire qui détermine l’identité par laquelle les utilisateurs souhaitent dédupliquer leurs profils.

     >[!IMPORTANT]
     >
     >Assurez-vous que le nom de l&#39;attribut de clé de déduplication correspond à un nom de colonne du mapping de ciblage sélectionné.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Une fois le mappage effectué, vous pouvez vérifier et terminer la configuration de destination pour commencer à envoyer des données à **[!DNL Campaign]**.
   [Découvrez comment passer en revue et terminer la configuration de destination](/help/destinations/destination-types.md#review).

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois une destination activée, vous pouvez accéder au traitement correspondant et aux données exportées dans Campaign.

### Surveillance des traitements d’exportation de données {#jobs}

Accédez au **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Tâches de chargement d’audience]** pour surveiller toutes les tâches d’exportation activées à partir de Adobe Experience Platform.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Accès aux données exportées {#data}

Pour **[!UICONTROL Synchronisation de l’audience]**, vous pouvez vérifier l’audience exportée en accédant à la variable **[!UICONTROL Profil et cible]** > **[!UICONTROL Liste]** > **[!UICONTROL Audiences AEP]** .

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Pour **[!UICONTROL Synchronisation des profils (mise à jour uniquement)]**, les données sont automatiquement mises à jour dans la base de données Campaign pour chaque profil ciblé par le segment activé dans la destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
