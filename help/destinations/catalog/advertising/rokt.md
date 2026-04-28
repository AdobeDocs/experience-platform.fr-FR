---
title: Racine
description: Découvrez comment connecter les audiences Adobe Experience Platform à Root pour améliorer les performances des campagnes grâce à un ciblage, une suppression et une personnalisation plus intelligents.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 25%

---


# Connexion [!DNL Rokt] {#rokt-destination}

## Vue d’ensemble {#overview}

[[!DNL Rokt]](https://www.rokt.com) libère de la valeur dans l’e-commerce à l’aide de la prise de décision en temps réel pilotée par l’IA pour rendre chaque moment de transaction plus pertinent™ Il offre des expériences personnalisées et connecte les annonceurs aux clients aux intentions élevées. Connectez les audiences [!DNL Adobe Experience Platform] à [!DNL Rokt] pour améliorer les performances des campagnes grâce à un ciblage, une suppression et une personnalisation plus intelligents. Touchez les bons clients au bon moment tout en réduisant les dépenses inutiles.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Rokt]. Pour toute question ou demande de mise à jour, contactez votre gestionnaire de compte [!DNL Rokt] ou contactez-`support@rokt.com`.

## Cas d’utilisation {#use-cases}

Les cas d’utilisation suivants montrent comment [!DNL Experience Platform] clients peuvent utiliser la destination [!DNL Rokt].

### Cas pratique #1 : reciblage {#use-case-1}

Réengagez les clients à forte intention qui ont visité votre site ou votre application mais n’ont pas effectué de conversion. Créez une audience dans [!DNL Experience Platform], y compris les utilisateurs et utilisatrices qui ont parcouru des catégories de produits spécifiques ou abandonné un flux de passage en caisse. Envoyez ensuite cette audience à [!DNL Rokt] pour diffuser des offres personnalisées au point d’achat sur les sites partenaires. [!DNL Rokt] fonctionne au moment de la transaction, immédiatement après qu&#39;un client a effectué un achat ailleurs. Les audiences reciblées sont atteintes lorsque l’intention d’achat est à son apogée, ce qui entraîne des taux de conversion plus élevés que le reciblage d’affichage traditionnel.

### Cas pratique #2 : listes de suppression {#use-case-2}

Prévenez les dépenses inutiles et les expériences non pertinentes en supprimant les audiences qui ne doivent pas recevoir certaines offres [!DNL Rokt]. Les cas d’utilisation de suppression courants incluent l’exclusion des convertisseurs récents, des membres du programme de fidélité d’une promotion active ou des utilisateurs qui se sont désinscrits du marketing. Par exemple, excluez les clients qui ont acheté au cours des 30 derniers jours. Synchronisez ces audiences de suppression de [!DNL Experience Platform] à [!DNL Rokt] en temps réel. Les campagnes restent ainsi axées sur les nouveaux utilisateurs et utilisatrices, ou sur les utilisateurs et utilisatrices réengageants. Cela améliore le retour sur investissement et protège l’expérience client.

## Conditions préalables {#prerequisites}

Avant de configurer la destination [!DNL Rokt] dans [!DNL Adobe Experience Platform], vous devez obtenir les informations d’identification suivantes auprès de votre gestionnaire de compte **[!DNL Rokt]** :

* **Clé API** : utilisez-la comme **[!UICONTROL Username]** lors de l’[authentification de la connexion de destination](#authenticate).
* **Secret API** : utilisez-le comme **[!UICONTROL Password]** lors de l’[authentification de la connexion de destination](#authenticate).

Votre gestionnaire de compte [!DNL Rokt] fournira ces informations d’identification sur la plateforme [!DNL Rokt] avant votre configuration. Contactez votre gestionnaire de compte si vous ne l’avez pas encore reçu.

## Identités prises en charge {#supported-identities}

[!DNL Rokt] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresse e-mail en clair | Recommandé. Utilisé pour la correspondance de profils dans [!DNL Rokt]. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Le texte brut et les adresses e-mail hachées SHA256 sont pris en charge. Lorsque votre champ source contient des attributs non hachés, sélectionnez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| phone | Numéro de téléphone en clair | Utilisé pour la correspondance de profils dans [!DNL Rokt]. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Le texte brut et les numéros de téléphone hachés SHA256 sont pris en charge. Lorsque votre champ source contient des attributs non hachés, sélectionnez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| GAID | [!DNL Google] ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | ID de [!DNL Apple] pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| aepProfileId | ID de profil [!DNL Adobe Experience Platform] | Mappe l’identifiant de profil (`xdm:_id`) en tant qu’identifiant de secours. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via le [[!DNL Segmentation Service]](/help/segmentation/home.md) [!DNL Experience Platform]. |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](/help/segmentation/ui/audience-portal.md#import-audience) dans [!DNL Experience Platform] à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications [!DNL Experience Platform] telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}

Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client. Utilisez-les pour cibler des groupes spécifiques de personnes dans le cadre de campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail, téléphone, identifiant d’annonce mobile ou autres) utilisés dans la destination [!DNL Rokt]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans [!DNL Experience Platform] en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval à [!DNL Rokt]. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](/help/destinations/ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]** : votre clé API, fournie par votre gestionnaire de compte [!DNL Rokt].
* **[!UICONTROL Password]** : votre secret API, fourni par votre gestionnaire de compte [!DNL Rokt].

  ![Écran de configuration de la destination [!DNL Rokt] dans [!DNL Experience Platform], avec les détails du compte, les champs d’authentification et les détails de destination renseignés.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir (par exemple, « [!DNL Rokt] - Reciblage des audiences »).
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](/help/destinations/ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès [**[!UICONTROL View Identity Graph]**](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

La destination [!DNL Rokt] prend en charge le mappage des espaces de noms d’identité de [!DNL Experience Platform] à [!DNL Rokt] champs d’identité. Vous devez mapper au moins une identité pour activer une audience. Les mappages recommandés sont présentés dans le tableau ci-dessous.

| Champ source | Champ cible | Considérations |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Recommandé |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Recommandé |
| `IdentityMap: Phone` | `Identity: phone` | Facultatif |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Facultatif |
| `IdentityMap: GAID` | `Identity: gaid` | Facultatif |
| `IdentityMap: IDFA` | `Identity: idfa` | Facultatif |
| `xdm: _id` | `Identity: aepProfileId` | Facultatif |

{style="table-layout:auto"}

Voici un exemple de mappage complet :

![L’étape de mappage du workflow d’activation de destination [!DNL Rokt] dans [!DNL Experience Platform], avec les champs d’identité source et cible configurés.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Il est vivement recommandé d’utiliser au moins un mappage d’identité basé sur les e-mails (`email` ou `emailSha256`) pour optimiser les taux de correspondance dans [!DNL Rokt].

### Configurer le planning d’audience {#audience-schedule}

Une fois l’étape de mappage terminée, configurez un planning d’audience pour chaque audience sélectionnée. Fournissez une **[!UICONTROL Start date]** pour le moment où l’audience doit commencer à se synchroniser, ainsi qu’un **[!UICONTROL Mapping ID]** (un libellé utilisé pour identifier cette audience dans [!DNL Rokt]). Vous pouvez utiliser le nom de l’audience [!DNL Experience Platform] ou toute chaîne descriptive qui vous aide, vous et votre gestionnaire de compte [!DNL Rokt], à identifier l’audience.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

* [Documentation destinée aux développeurs [!DNL Rokt]](https://docs.rokt.com)
* [Présentation des destinations Adobe Experience Platform](/help/destinations/home.md)
