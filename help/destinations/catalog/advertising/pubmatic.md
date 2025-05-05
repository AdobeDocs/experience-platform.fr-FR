---
title: PubMatic Connect
description: PubMatic maximise la valeur client en fournissant la chaîne d'approvisionnement de marketing numérique programmatique du futur. PubMatic Connect associe la technologie de plateforme et un service dédié pour améliorer la manière dont les inventaires et les données sont compilés et traités.
last-substantial-update: 2025-02-12T00:00:00Z
exl-id: 21e07d2c-9a6a-4cfa-a4b8-7ca48613956c
source-git-commit: 2041c06e660e24f63d4c44adc0e8f3082bb007ae
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 37%

---


# Destination de connexion PubMatic {#pubmatic-connect}

## Vue d’ensemble {#overview}

Utilisez [!DNL PubMatic Connect] pour optimiser la valeur client en fournissant la chaîne d’approvisionnement de marketing numérique programmatique de demain. [!DNL PubMatic Connect] associe la technologie de plateforme et un service dédié pour améliorer la manière dont les stocks et les données sont compilés et traités.

Deux destinations sont disponibles pour envoyer des données d’audience à la plateforme PubMatic Connect. Elles diffèrent légèrement au niveau de leur fonctionnalité :

1. PubMatic Connect

   Lors de l’activation initiale, cette destination enregistre automatiquement les audiences dans la plateforme PubMatic et utilise l’identifiant Adobe Experience Platform interne pour le mappage.

2. PubMatic Connect (mappage d’ID d’audience personnalisé)

   Cette destination vous permet de choisir d’ajouter manuellement un identifiant de mappage pendant le workflow d’activation. Utilisez cette destination lorsque des données doivent être envoyées à des audiences existantes dans la plateforme PubMatic ou si un « ID d’audience Source » personnalisé est requis.

![Vue côte à côte des deux connecteurs PubMatic dans le catalogue des destinations.](/help/destinations/assets/catalog/advertising/pubmatic/two-pubmatic-connectors-side-by-side.png)

>[!IMPORTANT]
>
> Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL PubMatic]. Pour toute question ou demande de mise à jour, contactez directement l’équipe d’Amazon Ads au `support@pubmatic.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL PubMatic Connect], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Ciblage des utilisateurs sur les plateformes mobiles, web et CTV {#targeting}

Les éditeurs ou les fournisseurs de données souhaitent envoyer des audiences de Adobe Experience Platform vers [!DNL PubMatic Connect] pour cibler les utilisateurs sur des plateformes mobiles, web et CTV, à l’aide d’un large éventail d’identifiants.

## Conditions préalables {#prerequisites}

Contactez votre gestionnaire de compte [!DNL PubMatic] pour vous assurer que votre compte est correctement configuré et prend en charge l’intégration des segments ciblés. Ils s’assureront également que vous disposez de tous les détails pertinents pour utiliser cette destination et vous fournir une assistance pendant la configuration.

## Identités prises en charge {#supported-identities}

[!DNL PubMatic Connect] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
| --------------- | ------------------------ | ------------------------------------------------------------------------------- |
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| extern_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
| --------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| ---------------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination PubMatic Connect. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
> Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Comment s’authentifier ](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL Jeton porteur]** : renseignez le jeton porteur pour vous authentifier sur la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la destination](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
- **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
- **[!UICONTROL ID de partenaire de données]** : identifiant de partenaire de données configuré dans votre compte [!DNL PubMatic] pour cette intégration.
- **[!UICONTROL Code pays par défaut]** : code pays par défaut qui doit être appliqué à toutes les identités si aucune identité n’est fournie dans le profil.
- **[!UICONTROL Identifiant de compte]** : l’identifiant de votre compte [!DNL PubMatic Connect].
- **[!UICONTROL Type de compte]** : type de compte de votre compte [!DNL PubMatic] Platform. Si vous avez des questions, adressez-vous à votre gestionnaire de compte [!DNL PubMatic]. Les options disponibles sont les suivantes :
   - [!UICONTROL ÉDITEUR]
   - [!UICONTROL PARTENAIRE_DEMANDE]
   - [!UICONTROL ACHETEUR]

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
> - Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>
> - Pour exporter des _identités_, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Sélection des champs sources :

- Sélectionnez un identifiant (généralement des espaces de noms tels qu’IDFA ou un espace de noms d’identifiant personnalisé).

Sélection des champs cibles :

- Contactez votre gestionnaire de compte [!DNL PubMatic] pour obtenir les informations sur le type UID qui sera correct au cours de cette étape.
- Sélectionnez le numéro de type de [!DNL PubMatic UID] correspondant à l’identifiant que vous avez sélectionné à la première étape.

![Mappage des attributs et des identités](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

### Planification de l’audience

Si vous utilisez la destination PubMatic Connect (mappage d’ID d’audience personnalisés), vous devez fournir un ID de mappage pour chaque audience qui correspond à l’« ID d’audience Source » dans la plateforme PubMatic.

![Planification des audiences](../..//assets/catalog/advertising/pubmatic/audience-scheduling-mapping-id.png)

## Données exportées / Valider l’exportation des données {#exported-data}

L’interface utilisateur de [!DNL PubMatic] vous permet de vérifier si les données ont été transmises correctement et si les segments sont disponibles. La mise à jour de l’interface utilisateur [!DNL PubMatic] peut prendre jusqu’à 24 heures après le transfert des données.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
