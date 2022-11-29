---
title: Gestion des autorisations pour Privacy Service
description: Découvrez comment gérer les autorisations utilisateur pour Adobe Experience Platform Privacy Service à l’aide de Adobe Admin Console.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 6%

---

# Gestion des autorisations pour Privacy Service

Accès à [Adobe Experience Platform Privacy Service](./home.md) est contrôlée par des autorisations granulaires basées sur les rôles dans Adobe Admin Console. En créant des profils de produit qui attribuent des autorisations à des groupes d’utilisateurs, vous pouvez déterminer qui a accès aux fonctionnalités du Privacy Service. [Interface utilisateur](./ui/overview.md) et [API](./api/overview.md).

>[!NOTE]
>
>Lors de la création d’une intégration pour l’API du Privacy Service, vous devez sélectionner un profil de produit existant afin de déterminer les fonctionnalités ou actions pour lesquelles l’intégration dispose d’autorisations. Consultez le guide sur la [prise en main de l’API du Privacy Service](./api/getting-started.md) pour plus d’informations.

Ce guide vous explique comment gérer les autorisations pour Privacy Service.

## Prise en main

Pour configurer le contrôle d’accès de Privacy Service, vous devez disposer de droits d’administrateur pour une organisation qui dispose d’une intégration de produit avec Adobe Experience Platform Privacy Service. Le rôle minimum qui peut accorder ou retirer des autorisations est un **administrateur de profil de produit**. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les **administrateurs de produit** (qui peuvent gérer tous les profils au sein d’un produit) et les **administrateurs système** (aucune restriction). Consultez l’article sur [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) pour plus d’informations, voir le guide d’administration d’Adobe Enterprise.

Ce guide suppose que vous connaissez les concepts de Admin Console de base tels que les profils de produit et la manière dont ils accordent des autorisations de produit à des utilisateurs et à des groupes individuels. Pour plus d’informations, voir [Guide d’utilisation du Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

## Autorisations disponibles

Le tableau suivant décrit les autorisations disponibles pour Privacy Service avec des descriptions des fonctionnalités spécifiques auxquelles elles donnent accès :

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!UICONTROL Autorisations du Privacy Service] | [!UICONTROL Autorisation de lecture des informations personnelles] | Détermine si l’utilisateur peut afficher les demandes d’accès et de suppression existantes, ainsi que leurs détails. |
| [!UICONTROL Autorisations du Privacy Service] | [!UICONTROL Droit d’écriture sur des informations personnelles] | Détermine si un utilisateur peut créer de nouvelles requêtes d’accès et de suppression. |
| [!UICONTROL Autorisations du Privacy Service] | [!UICONTROL Autorisation de diffusion de contenu (accès)] | Lorsqu’une demande d’accès est traitée par un Privacy Service, un fichier ZIP contenant les données du client est envoyé à ce client. Lorsque vous recherchez les détails d’une demande d’accès, cette autorisation détermine si l’utilisateur peut accéder au lien de téléchargement pour le fichier ZIP de la demande. |
| [!UICONTROL Autorisations d’exclusion de la vente] | [!UICONTROL Autorisation de lecture - Exclusion de la vente] | Détermine si l’utilisateur peut afficher les requêtes d’opposition à la vente existantes, ainsi que leurs détails. |
| [!UICONTROL Autorisations d’exclusion de la vente] | [!UICONTROL Droit d’écriture - Droit d’opposition à la vente] | Détermine si un utilisateur peut créer de nouvelles requêtes d’opposition à la vente. |

{style=&quot;table-layout:auto&quot;}

## Gestion des autorisations {#manage}

Pour gérer les autorisations de Privacy Service, connectez-vous à [Admin Console](https://adminconsole.adobe.com/) et sélectionnez **[!UICONTROL Produits]** dans la barre de navigation supérieure. À partir de là, sélectionnez **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Image montrant la carte de produit du Privacy Service dans Admin Console](./images/permissions/privacy-service-card.png)

### Sélection ou création d’un profil de produit

L’écran suivant affiche une liste des profils de produits disponibles pour Privacy Service sous votre entreprise. S’il n’existe aucun profil de produit, sélectionnez **[!UICONTROL Nouveau profil]** pour en créer un. Si votre organisation compte plusieurs rôles ou groupes d’utilisateurs nécessitant différents niveaux d’accès, vous devez créer un profil de produit distinct pour chacun d’eux.

![Image montrant les profils de produit pour Privacy Service dans Admin Console](./images/permissions/select-or-create-profile.png)

Après avoir sélectionné un profil de produit, vous pouvez utiliser la variable **[!UICONTROL Autorisations]** pour démarrer [modification des autorisations](#edit-permissions) pour le profil, ou sélectionnez l’événement **[!UICONTROL Utilisateurs]** pour démarrer [attribution d’utilisateurs](#assign-users) au profil.

![Image montrant l’onglet Autorisations d’un Admin Console de profil de produit](./images/permissions/users-permissions-tabs.png)

### Modifier les autorisations pour le profil {#edit-permissions}

Sur le **[!UICONTROL Autorisations]** sélectionnez l’une des catégories d’autorisations affichées pour accéder à la vue d’édition des autorisations.

Lors de l’édition des autorisations d’un profil, les autorisations disponibles sont répertoriées dans la colonne de gauche tandis que celles qui sont incluses dans le profil sont répertoriées dans la colonne de droite. Sélectionnez les autorisations répertoriées pour les déplacer entre les colonnes.

![Image montrant les colonnes d’autorisations disponibles et incluses](./images/permissions/edit-permissions.png)

Les autorisations sont organisées en catégories. Pour passer d’une catégorie à l’autre, sélectionnez la catégorie souhaitée dans le volet de navigation de gauche.

![Image montrant le [!UICONTROL Exclusion de la vente] section sous autorisations](./images/permissions/switch-category.png)

Sélectionner **[!UICONTROL Enregistrer]** une fois que vous avez terminé de configurer les autorisations.

![Image montrant la configuration des autorisations en cours d’enregistrement pour le profil de produit](./images/permissions/save-permissions.png)

La vue Profil de produit réapparaît avec les autorisations ajoutées reflétées.

![Image montrant les autorisations ajoutées pour le profil de produit](./images/permissions/permissions-added.png)

### Attribution d’utilisateurs au profil {#assign-users}

Pour affecter des utilisateurs au profil de produit (et leur accorder les autorisations configurées du profil), sélectionnez la variable **[!UICONTROL Utilisateurs]** , suivie de **[!UICONTROL Ajouter un utilisateur]**.

![Image montrant l’onglet utilisateurs d’un profil de produit dans Admin Console](./images/permissions/manage-users.png)

Pour plus d’informations sur la gestion des utilisateurs pour un profil de produit, voir [Documentation du Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html).

### Migration des informations d’identification d’API héritées vers le profil {#migrate-tech-accounts}

>[!NOTE]
>
>Cette section s’applique uniquement aux informations d’identification d’API existantes qui ont été créées avant l’intégration des autorisations de Privacy Service dans Adobe Admin Console. Pour les nouvelles informations d’identification, les profils de produit (et leurs autorisations) sont attribués via [Projets de la console Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) au lieu de .<br><br>Voir la section sur [attribution de profils de produit à un projet](./api/getting-started.md#product-profiles) pour plus d’informations, consultez le guide de prise en main de l’API Privacy Service .

Pour migrer les informations d’identification d’API héritées vers le profil de produit, sélectionnez **[!UICONTROL Informations d’identification de l’API]**, suivie de **[!UICONTROL Ajout des informations d’identification API]**.

![[!UICONTROL Ajout des informations d’identification API] en cours de sélection dans Admin Console, sous [!UICONTROL Informations d’identification de l’API] onglet d’un profil de produit](./images/permissions/api-credentials.png)

Sélectionnez les projets Developer Console de votre choix dans la liste, puis sélectionnez **[!UICONTROL Enregistrer]** pour les ajouter au profil de produit. Tous les appels d’API qui utilisent les informations d’identification de ces projets hériteront des autorisations granulaires accordées par le profil de produit.

## Étapes suivantes

Ce guide couvrait les autorisations disponibles pour Privacy Service et la manière de les gérer via Admin Console.

Pour savoir comment créer une intégration d’API après avoir configuré les profils de produit, reportez-vous à la section [Guide de prise en main pour l’API du Privacy Service](./api/getting-started.md). Pour plus d’informations sur la gestion des autorisations pour d’autres fonctionnalités de Adobe Experience Platform, reportez-vous à la section [documentation sur le contrôle d’accès](../access-control/home.md).
