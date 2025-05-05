---
title: Profils des participants à Rainfocus
description: Découvrez comment utiliser le connecteur de destination Profils de participants RainFocus pour synchroniser les profils d’audience avec le profil de participant global RainFocus.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 46%

---

# Profils des participants à Rainfocus {#rainfocus-destination}

## Vue d’ensemble {#overview}

Utilisez la destination [!DNL RainFocus Attendee Profiles] pour diffuser des profils clientèle d’Adobe Experience Platform vers la plateforme [!DNL RainFocus] afin de créer et de mettre à jour des profils de participantes et participants.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL RainFocus]. Pour toute demande de renseignements ou de mise à jour, veuillez communiquer directement avec eux à l&#39;adresse `clientcare@rainfocus.com` ou visiter le Centre d&#39;aide [RainFocus](https://help.rainfocus.com/hc/en-us).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination RainFocus, consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1 {#use-case-1}

Une grande entreprise technologique est sur le point de s’inscrire pour sa prochaine exposition internationale et souhaite envoyer les profils clients vers [!DNL RainFocus] afin de rationaliser le processus d’inscription.

### Cas d’utilisation #2 {#use-case-2}

Une marque de services financiers doit organiser une série de tournées destinées aux nouveaux clients et aux clients existants. Ils disposent d’une série de segments ciblés avec les clients cibles dans Adobe Experience Platform. À l’aide du connecteur de destination [!DNL RainFocus], ils peuvent facilement envoyer ces profils à [!DNL RainFocus] pour activation.

## Conditions préalables {#prerequisites}

Avant de pouvoir utiliser la destination [!DNL RainFocus], veillez à respecter les conditions préalables suivantes :

* Créez un profil d’API [!DNL RainFocus] avec OAuth (global).
   * Le point d’entrée **Attendee Store** doit être activé.
   * Un **ID client** et un **Secret client** devront être générés.

Vous devez également disposer d’un identifiant RainFocus **code d’événement** dans lequel vous souhaitez envoyer les profils.

## Identités prises en charge {#supported-identities}

[!DNL RainFocus] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Fournissez des détails d’authentification pour le connecteur de destination RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL ID client]** : renseignez les [!DNL Client ID] fournies par le profil d’API RainFocus.
* **[!UICONTROL Secret client]** : renseignez les [!DNL Client Secret] fournies par le profil d’API RainFocus.
* **[!UICONTROL Environnement]** : spécifiez l’environnement RainFocus auquel vous vous connectez, par exemple `dev`, `prod`.
* **[!UICONTROL ID d’organisation]** : indiquez le `orgid` unique de votre instance de RainFocus.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Fournissez les détails de connexion pour le connecteur de destination RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de l’événement]** : identifiant du code de l’événement [!DNL RainFocus], dans lequel vous souhaitez que les profils soient envoyés.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Le ou les espaces de noms d&#39;identité cible suivants doivent être mappés selon le cas d&#39;utilisation :

* **E-mail** doit être mappé en tant que champ cible à l’aide de **Champ cible > Sélectionner un espace de noms d’identité > E-mail**

![Comment mapper des champs de profil et d’identité](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

Il est recommandé de mapper des champs de profil supplémentaires, car cela garantit que le profil du participant dans [!DNL RainFocus] est entièrement renseigné. Les champs cibles suivants sont disponibles à partir de [!DNL RainFocus] :

| Champ cible | Description |
|------------|-------------|
| `address1` | Première ligne de l’adresse postale |
| `address2` | Deuxième ligne de l&#39;adresse postale (le cas échéant) |
| `city` | Nom de la ville |
| `companyname` | Nom de la société |
| `countryid` | Identifiant de code pays ISO 3166-1 alpha-2 pour le pays |
| `email` | Adresse e-mail |
| `firstname` | Prénom de la personne |
| `lastname` | Nom de la personne |
| `jobtitle` | Fonction de la personne |
| `phone` | Numéro de téléphone |
| `state` | Code alpha d&#39;état FIPS pour l&#39;état ou la province |
| `zip` | Code postal |

{style="table-layout:auto"}

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois qu’un ensemble de profils a été envoyé à [!DNL RainFocus], utilisez l’[!DNL RainFocus] de connexion Profil d’API pour vérifier que les profils ont bien été ingérés.

![Afficher les journaux dans le profil d’API dans RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Vérifiez que les profils ont bien été ingérés](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

* [ Connecteur Source de streaming RainFocus ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/analytics/rainfocus)
