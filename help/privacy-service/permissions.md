---
title: Gérer les autorisations pour Privacy Service
description: Découvrez comment gérer les autorisations utilisateur pour Adobe Experience Platform Privacy Service à l’aide d’Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 60%

---

# Gérer les autorisations pour Privacy Service

>[!IMPORTANT]
>
>Les autorisations pour Adobe Experience Platform Privacy Service ont été améliorées afin d’augmenter leur niveau de granularité. Ces modifications permettent aux administrateurs et administratrices de l’organisation d’accorder l’accès à plus d’utilisateurs et d’utilisatrices avec le rôle et le niveau d’autorisation souhaités.Les utilisateurs et utilisatrices de comptes techniques doivent mettre à jour leurs autorisations de Privacy Service, car cette mise à jour imminente constitue une modification irréversible. L’application de cette modification des autorisations aura lieu le **13 avril 2023**. Consultez la documentation relative à [migration des informations d’identification d’API héritées](#migrate-tech-accounts) pour obtenir des conseils sur la résolution de ce problème.
>
>Les comptes techniques sont disponibles pour les clientes et clients d’entreprise et créés via l’Adobe Developers Console. L’Adobe ID d’une personne titulaire de compte technique se termine par `@techacct.adobe.com`. Si vous ne savez pas si vous êtes titulaire d’un compte technique, contactez l’administrateur ou l’administratrice de votre organisation.

L’accès à [Adobe Experience Platform Privacy Service](./home.md) est contrôlé par des autorisations granulaires en fonction du rôle dans Adobe Admin Console. En créant des profils de produit qui attribuent des autorisations à des groupes d’utilisateurs, vous pouvez déterminer qui a accès aux fonctionnalités de l’[Interface utilisateur](./ui/overview.md) et des [API](./api/overview.md) de Privacy Service.

>[!NOTE]
>
>Lors de la création d’une intégration pour l’API de Privacy Service, vous devez sélectionner un profil de produit existant afin de déterminer les fonctionnalités ou actions pour lesquelles l’intégration dispose d’autorisations. Consultez le guide sur la [prise en main de l’API de Privacy Service](./api/getting-started.md) pour plus d’informations.

Ce guide vous explique comment gérer les autorisations pour Privacy Service.

## Prise en main

Pour configurer le contrôle d’accès de Privacy Service, vous devez disposer de droits d’administrateur pour une organisation qui dispose d’une intégration de produit avec Adobe Experience Platform Privacy Service. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un **administrateur de profils de produit**. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les **administrateurs de produit** (qui peuvent gérer tous les profils au sein d’un produit) et les **administrateurs système** (aucune restriction). Consultez l’article sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) dans le guide d’administration d’Adobe Enterprise pour plus d’informations.

Ce guide suppose que vous connaissez les concepts de base d’Admin Console tels que les profils de produit et la manière dont ils accordent des autorisations de produit à des utilisateurs et utilisatrices individuels et à des groupes. Pour plus d’informations, consultez le [guide d’utilisation d’Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

## Autorisations disponibles

Le tableau suivant décrit les autorisations disponibles pour Privacy Service avec des descriptions des fonctionnalités spécifiques auxquelles elles donnent accès :

>[!NOTE]
>
>Tous les Privacy Service et [!UICONTROL Exclusion de la vente] Les autorisations sont distinctes et distinctes les unes des autres, sans chevauchement fonctionnel. Cela est possible, car l’API du Privacy Service est considérée comme idempotent.

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!UICONTROL Autorisations de Privacy Service] | [!UICONTROL Autorisation de lecture des informations personnelles] | Détermine si l’utilisateur ou l’utilisatrice peut afficher les requêtes d’accès et de suppression existantes, ainsi que leurs détails. |
| [!UICONTROL Autorisations de Privacy Service] | [!UICONTROL Autorisation d’écriture sur des informations personnelles] | Détermine si un utilisateur ou une utilisatrice peut créer de nouvelles requêtes d’accès et de suppression. |
| [!UICONTROL Autorisations de Privacy Service] | [!UICONTROL Autorisation de diffusion de contenu en lecture (accès)] | Lorsqu’une requête d’accès est traitée par Privacy Service, un fichier ZIP contenant les données du client ou de la cliente lui est envoyé. Lorsque vous recherchez les détails d’une requête d’accès, cette autorisation détermine si l’utilisateur ou l’utilisatrice peut accéder au lien de téléchargement pour le fichier ZIP de la requête. |
| [!UICONTROL Autorisations de désinscription de la vente] | [!UICONTROL Autorisation de lecture - Désinscription de la vente] | Détermine si l’utilisateur ou l’utilisatrice peut afficher les requêtes de désinscription à la vente existantes, ainsi que leurs détails. |
| [!UICONTROL Autorisations de désinscription de la vente] | [!UICONTROL Droit d’écriture - Désinscription de la vente] | Détermine si un utilisateur ou une utilisatrice peut créer de nouvelles requêtes de désinscription de la vente. |

{style="table-layout:auto"}

## Gérer les autorisations {#manage}

Pour gérer les autorisations de Privacy Service, connectez-vous à [Admin Console](https://adminconsole.adobe.com/) et sélectionnez **[!UICONTROL Produits]** dans la barre de navigation supérieure. À partir de là, sélectionnez **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Image montrant la carte de produit de Privacy Service dans Admin Console.](./images/permissions/privacy-service-card.png)

### Sélectionner ou créer un profil de produit

L’écran suivant affiche une liste des profils de produits disponibles pour Privacy Service sous votre organisation. S’il n’existe aucun profil de produit, sélectionnez **[!UICONTROL Nouveau profil]** pour en créer un. Si votre organisation compte plusieurs rôles ou groupes d’utilisateurs et d’utilisatrices nécessitant différents niveaux d’accès, vous devez créer un profil de produit distinct pour chacun d’eux.

![Image montrant les profils de produit pour Privacy Service dans Admin Console.](./images/permissions/select-or-create-profile.png)

Après avoir sélectionné un profil de produit, vous pouvez utiliser l’onglet **[!UICONTROL Autorisations]** pour démarrer la [modification des autorisations](#edit-permissions) pour le profil, ou sélectionner l’onglet **[!UICONTROL Utilisateurs]** pour démarrer l’[attribution d’utilisateurs](#assign-users) au profil.

![Image montrant l’onglet Autorisations d’un profil de produit dans Admin Console.](./images/permissions/users-permissions-tabs.png)

### Modifier les autorisations pour le profil {#edit-permissions}

Sur l’onglet **[!UICONTROL Autorisations]**, sélectionnez l’une des catégories d’autorisations affichées pour accéder à la vue d’édition des autorisations.

Lors de l’édition des autorisations d’un profil, les autorisations disponibles sont répertoriées dans la colonne de gauche tandis que celles qui sont incluses dans le profil sont répertoriées dans la colonne de droite. Sélectionnez les autorisations répertoriées pour les déplacer entre les colonnes.

![Image montrant les colonnes d’autorisations disponibles et incluses.](./images/permissions/edit-permissions.png)

Les autorisations sont organisées en catégories. Pour passer d’une catégorie à l’autre, sélectionnez la catégorie souhaitée dans le volet de navigation de gauche.

![Image montrant la section [!UICONTROL Désinscription de la vente] sous autorisations.](./images/permissions/switch-category.png)

Sélectionnez **[!UICONTROL Enregistrer]** une fois que vous avez terminé de configurer les autorisations.

![Image montrant la configuration des autorisations en cours d’enregistrement pour le profil de produit.](./images/permissions/save-permissions.png)

La vue Profil de produit réapparaît avec les autorisations ajoutées reflétées.

![Image montrant les autorisations ajoutées pour le profil de produit.](./images/permissions/permissions-added.png)

### Attribution d’utilisateurs et d’utilisatrices au profil {#assign-users}

Pour affecter des utilisateurs et utilisatrices au profil de produit (et leur accorder les autorisations configurées du profil), sélectionnez l’onglet **[!UICONTROL Utilisateurs]**, suivi de **[!UICONTROL Ajouter un utilisateur]**.

![Image montrant l’onglet utilisateurs d’un profil de produit dans Admin Console.](./images/permissions/manage-users.png)

Pour plus d’informations sur la gestion des utilisateurs et utilisatrices pour un profil de produit, voir la [Documentation concernant Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html).

### Migrer les informations d’identification d’API héritées vers le profil {#migrate-tech-accounts}

>[!NOTE]
>
>Cette section s’applique uniquement aux informations d’identification d’API existantes qui ont été créées avant l’intégration des autorisations de Privacy Service dans Adobe Admin Console. Pour les nouvelles informations d’identification, les profils de produit (et leurs autorisations) sont plutôt attribués via les [Projets d’Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/projects/).<br><br>Voir la section sur l’[attribution de profils de produit à un projet](./api/getting-started.md#product-profiles) dans le guide de prise en main de l’API Privacy Service pour obtenir plus d’informations.

Auparavant, les comptes techniques ne nécessitaient pas de profil de produit pour l’intégration et les autorisations. Cependant, en raison des récentes améliorations apportées aux autorisations de Privacy Service, il est désormais nécessaire de migrer les informations d’identification d’API héritées vers le profil de produit. Cette mise à jour permet d’accorder des autorisations granulaires aux titulaires d’un compte technique. Suivez les étapes ci-dessous pour mettre à jour les autorisations de compte technique pour Privacy Service.

#### Mise à jour des autorisations de compte technique {#update-tech-account-permissions}

La première étape de l’attribution d’un jeu d’autorisations pour votre compte technique consiste à accéder au [Adobe Admin Console](https://adminconsole.adobe.com/) et créez un profil de produit pour Privacy Service.

Dans l’interface utilisateur du Admin Console, sélectionnez **Produits** à partir de la barre de navigation, suivie de **[!UICONTROL Experience Cloud]** et **[!UICONTROL Adobe Experience Platform Privacy Service]** dans la barre latérale gauche. Le [!UICONTROL Profils de produit] s’affiche. Sélectionner **Nouveau profil** pour créer un profil de produit pour Privacy Service.

![L’onglet Profils de produit du Privacy Service Experience Platform dans Adobe Admin Console avec un nouveau profil mis en surbrillance.](./images/permissions/create-product-profile.png)

Le [!UICONTROL Création d’un profil de produit] s’affiche. Vous trouverez des instructions complètes sur la création d’un profil de produit dans la section [Guide de l’interface utilisateur pour la création de profils](../access-control/ui/create-profile.md).

Après avoir enregistré votre nouveau profil de produit, accédez à la [Console Adobe Developer](https://developer.adobe.com/console/home) et connectez-vous à ce produit ou à ce projet. Sélectionner **[!UICONTROL Projets]** dans le volet de navigation supérieur, suivi de la carte de votre projet.

>[!NOTE]
>
>Vous devrez peut-être vider votre cache et/ou attendre un certain temps pour que le nouveau projet apparaisse dans la liste de vos projets Developer Console.

Une fois connecté à votre projet, sélectionnez l’option **[!UICONTROL API Privacy Service]** intégration à partir de la barre latérale gauche.

![L’onglet Projets de la console Adobe Developer avec les projets et l’API Privacy Service mis en surbrillance.](./images/permissions/login-to-dev-console-project.png)

Le tableau de bord de l’intégration de l’API du Privacy Service s’affiche. Dans ce tableau de bord, vous pouvez modifier le profil de produit associé à ce projet. Sélectionner **[!UICONTROL Modification des profils de produit]** pour lancer le processus. Le [!UICONTROL Configuration de l’API] s’affiche.

![Le tableau de bord de l’intégration de l’API du Privacy Service dans la console Adobe Developer avec l’option Modifier les profils de produit mise en surbrillance](./images/permissions/edit-product-profiles.png)

Le [!UICONTROL Configuration de l’API] La boîte de dialogue affiche les profils de produit disponibles qui existent actuellement dans le service. Ils sont en corrélation avec les profils de produit créés dans la console d’administration. Dans la liste des profils de produit disponibles, cochez la case correspondant au nouveau profil de produit que vous avez créé pour le compte technique dans la console d’administration. Ce compte technique est ainsi automatiquement associé aux autorisations du profil de produit sélectionné. Sélectionner **[!UICONTROL Enregistrer l’API configurée]** pour confirmer vos paramètres.

>[!NOTE]
>
>Si un compte technique est déjà associé à un profil de produit, l’une des cases à cocher de la liste des profils de produit disponibles est déjà sélectionnée.

![La boîte de dialogue Configurer l’API dans la console Adobe Developer avec une case à cocher Profil de produit et Enregistrer l’API configurée est mise en surbrillance.](./images/permissions/select-profile-for-tech-account.png)

#### Vérifiez que les paramètres ont été appliqués. {#confirm-applied-settings}

Pour confirmer que vos paramètres ont été appliqués au compte. Revenez au [Admin Console](https://adminconsole.adobe.com/) et accédez à votre profil de produit nouvellement créé. Sélectionnez la **[!UICONTROL Informations d’identification de l’API]** pour afficher la liste des projets associés. Le projet utilisé dans Developer Console dans lequel vous avez affecté le profil de produit au compte technique s’affiche dans la liste des informations d’identification. Le nom de chaque information d’identification d’API est composé du nom du projet avec un nombre généré de manière aléatoire, suffixé à la fin. Sélectionnez des informations d’identification pour ouvrir la [!UICONTROL Détails] du panneau.

![Un profil de produit dans le Admin Console avec l’onglet Informations d’identification de l’API et une ligne d’informations d’identification du projet mis en surbrillance.](./images/permissions/confirm-credentials-in-admin-console.png)

Le [!UICONTROL Détails] contient des informations sur les informations d’identification de l’API, notamment l’identifiant technique associé, la clé API, la date de création et de dernière modification, ainsi que les produits d’Adobe associés.

![Panneau Détails surligné des informations d’identification d’une API dans Admin Console.](./images/permissions/admin-console-details-panel.png)

## Étapes suivantes

Ce guide couvrait les autorisations disponibles pour Privacy Service et la manière de les gérer via Admin Console.

Pour savoir comment créer une intégration d’API après avoir configuré les profils de produit, reportez-vous au [guide de prise en main pour l’API Privacy Service](./api/getting-started.md). Pour plus d’informations sur la gestion des autorisations pour d’autres fonctionnalités d’Adobe Experience Platform, reportez-vous à la [documentation sur le contrôle d’accès](../access-control/home.md).
