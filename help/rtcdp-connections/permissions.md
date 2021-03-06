---
title: Gestion des autorisations pour la collecte de données dans Experience Platform
description: Présentation générale de la gestion des autorisations et du contrôle de l’accès aux fonctionnalités dans les connexions Real-time Customer Data Platform (RTCDP).
source-git-commit: e0be090bfce602c7a6e22a1e4be187d4abdfd600
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 10%

---

# Gestion des autorisations pour la collecte de données dans Experience Platform

[Collecte de données dans Adobe Experience Platform](./home.md) est constitué de plusieurs technologies différentes qui travaillent ensemble pour collecter et transférer vos données. L’accès à ces technologies est contrôlé par le biais d’autorisations granulaires basées sur les rôles dans Adobe Admin Console.

Ce guide vous explique comment gérer les autorisations pour les fonctionnalités de collecte de données.

## Prise en main

Pour configurer le contrôle d’accès pour la collecte de données, vous devez disposer de droits d’administrateur pour une organisation qui dispose d’une intégration de produit avec la collecte de données Adobe Experience Platform. Le rôle minimum qui peut accorder ou retirer des autorisations est un administrateur de profil de produit. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les administrateurs de produit (qui peuvent gérer tous les profils au sein d’un produit) et les administrateurs système (aucune restriction). Consultez l’article sur [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) pour plus d’informations, voir le guide d’administration d’Adobe Enterprise.

Ce guide suppose que vous connaissez les concepts de Admin Console de base tels que les profils de produit et la manière dont ils accordent des autorisations de produit à des utilisateurs et à des groupes individuels. Pour plus d’informations, voir [Guide d’utilisation du Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).

## Autorisations disponibles

Les autorisations appropriées pour la collecte de données sont fournies par le biais de deux désignations de produit en Admin Console : **Adobe Experience Platform** et **Collecte de données Adobe Experience Platform**. Les sections ci-dessous décrivent les autorisations fournies sous chaque produit, ainsi que les fonctionnalités spécifiques auxquelles ils donnent accès.

### Autorisations Adobe Experience Platform

Les autorisations sous Adobe Experience Platform incluent l’accès aux jeux de données, aux identités, aux schémas et aux environnements de test. Pour obtenir des instructions sur la configuration des autorisations Adobe Experience Platform, voir [guide d’utilisation du contrôle d’accès](../access-control/ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| Sandbox | (S/O) | Selon le [sandbox](../sandboxes/home.md) qui ont été créés sous votre organisation, vous pouvez contrôler l’accès à chacun d’eux par le biais de cette catégorie d’autorisations dans Admin Console. |
| Modélisation des données | Gestion des schémas | Permet d’afficher, de créer et de modifier des [Schémas de modèle de données d’expérience (XDM)](../xdm/home.md). |
| Modélisation des données | Affichage des schémas | Accorde l’accès en lecture seule aux schémas. |
| Identity Management | Gestion des espaces de noms d’identité | Permet d’afficher, de créer et de modifier des [espaces de noms d’identité](../identity-service/namespaces.md). |
| Identity Management | Affichages des espaces de noms d’identité | Accorde l’accès en lecture seule aux espaces de noms d’identité. |
| Collecte de données | Gestion des flux de données | Permet d’afficher, de créer et de modifier des [datastreams](../edge/datastreams/overview.md). |
| Collecte de données | Affichage des flux de données | Accorde l’accès en lecture seule aux flux de données. |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Autorisations de collecte de données Adobe Experience Platform

Les autorisations de la collecte de données Adobe Experience Platform contrôlent l’accès aux balises et aux fonctionnalités de transfert d’événement, y compris les propriétés, les extensions et les environnements. Pour obtenir des instructions sur la configuration des autorisations de la collecte de données Adobe Experience Platform, reportez-vous à la section [section ci-dessous](#manage).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| Plateformes | Web | Accorde l’accès à [propriétés web](../tags/ui/administration/companies-and-properties.md) lorsqu’elles sont combinées avec d’autres droits de propriété. |
| Plateformes | Mobile | Accorde l’accès à [propriétés mobiles](../tags/ui/administration/companies-and-properties.md) lorsqu’elles sont combinées avec d’autres droits de propriété. |
| Propriétés | (S/O) | Selon les propriétés qui ont été créées sous votre organisation, vous pouvez contrôler l’accès à chacune d’elles par le biais de cette catégorie d’autorisations dans Admin Console.<br><br>Les droits de propriété attribués à un utilisateur s’appliquent uniquement aux propriétés auxquelles il a eu accès par le biais de cette catégorie d’autorisations. |
| Droits de propriété | Approuver | Permet d’approuver une version de bibliothèque dans le cadre du [flux de publication](../tags/ui/publishing/publishing-flow.md). |
| Droits de propriété | Développer | Permet de développer une version de bibliothèque dans le cadre du [flux de publication](../tags/ui/publishing/publishing-flow.md). |
| Droits de propriété | Modifier la propriété | Permet de modifier la configuration de base des propriétés auxquelles un utilisateur a accès. |
| Droits de propriété | Gérer les environnements | Permet de gérer le [environnements](../tags/ui/publishing/environments.md) pour les propriétés auxquelles un utilisateur a accès. |
| Droits de propriété | Gérer les extensions | Permet de gérer le [extensions](../tags/ui/managing-resources/extensions/overview.md) pour les propriétés auxquelles un utilisateur a accès. |
| Droits de propriété | Publier | Permet de publier une version de bibliothèque dans le cadre du [flux de publication](../tags/ui/publishing/publishing-flow.md). |
| Droits d’entreprise | Développement dʼextensions | Permet de créer et de modifier des modules d’extension dont votre organisation est propriétaire, y compris les versions privées et les demandes de publication publique. |
| Droits d’entreprise | Gérer les extensions | Cette autorisation n’est applicable que si vous disposez d’une licence pour Adobe Journey Optimizer ou une autre solution qui accorde l’accès aux messages in-app et push mobiles. Cela vous permet de gérer les applications dont Adobe Experience Cloud a connaissance, ainsi que les informations d’identification push nécessaires pour communiquer avec le service Firebase Cloud Messaging et le service Apple Push Notification. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Pour plus d’informations sur la façon dont ces autorisations affectent les fonctionnalités des balises, y compris les stratégies d’administration pour les scénarios courants, consultez la documentation sur les balises sur [permissions utilisateur](../tags/ui/administration/user-permissions.md).

## Gestion des autorisations pour la collecte de données Adobe Experience Platform {#manage}

>[!IMPORTANT]
>
>Cette section décrit uniquement comment gérer les autorisations du produit Collecte de données Adobe Experience Platform dans Admin Console. Toutefois, les étapes de gestion des autorisations sous le produit Adobe Experience Platform sont similaires.
>
>Voir [guide de l’interface utilisateur du contrôle d’accès](../access-control/ui/overview.md) pour obtenir des instructions détaillées sur la gestion des autorisations de Platform. Selon les SKU du produit auxquels votre entreprise a accès, il se peut que vous ne disposiez pas de toutes les autorisations.

Pour gérer les autorisations relatives à la collecte de données, connectez-vous à [Admin Console](https://adminconsole.adobe.com/) et sélectionnez **[!UICONTROL Produits]** dans la barre de navigation supérieure. À partir de là, sélectionnez la carte pour **[!UICONTROL Collecte de données Adobe Experience Platform]**.

![Image montrant la carte de produit de la collecte de données en Admin Console](./images/permissions/data-collection-card.png)

### Sélection ou création d’un profil de produit

L’écran suivant affiche une liste des profils de produit disponibles pour la collecte de données sous votre organisation, le profil par défaut étant **[!DNL Default Data Collection All Access]**. Si vous le souhaitez, vous pouvez modifier le profil de produit par défaut ou sélectionner **[!UICONTROL Nouveau profil]** pour en créer un. Si votre organisation compte plusieurs rôles ou groupes d’utilisateurs nécessitant différents niveaux d’accès, vous devez créer un profil de produit distinct pour chacun d’eux.

![Image montrant les profils de produit pour la collecte de données dans Admin Console](./images/permissions/new-profile.png)

Après avoir sélectionné ou créé un profil de produit, vous pouvez utiliser la variable **[!UICONTROL Modifier]** icônes de démarrage [modification des autorisations](#edit-permissions) pour le profil, ou sélectionnez l’événement **[!UICONTROL Utilisateurs]** pour démarrer [attribution d’utilisateurs](#assign-users) au profil.

![Image montrant l’onglet Autorisations d’un Admin Console de profil de produit](./images/permissions/edit-permission-categories.png)

### Modifier les autorisations pour le profil de produit {#edit-permissions}

Lors de l’édition des autorisations d’un profil, les autorisations disponibles sont répertoriées dans la colonne de gauche tandis que celles qui sont incluses dans le profil sont répertoriées dans la colonne de droite. Sélectionnez les autorisations répertoriées pour les déplacer entre les colonnes.

![Image montrant les autorisations ajoutées sous la colonne incluse](./images/permissions/added-permissions.png)

Les autorisations sont organisées en catégories. Pour passer d’une catégorie à l’autre, sélectionnez la catégorie souhaitée dans le volet de navigation de gauche.

![Image présentant la section des droits de l’entreprise sous autorisations](./images/permissions/switch-category.png)

Sélectionner **[!UICONTROL Enregistrer]** une fois que vous avez terminé de configurer les autorisations.

![Image montrant la configuration des autorisations en cours d’enregistrement pour le profil de produit](./images/permissions/save-permissions.png)

La vue Profil de produit réapparaît avec les autorisations ajoutées reflétées.

![Image montrant les autorisations ajoutées pour le profil de produit](./images/permissions/permissions-added.png)

### Affecter des utilisateurs au profil de produits {#assign-users}

Pour affecter des utilisateurs au profil de produit (et leur accorder les autorisations configurées du profil), sélectionnez la variable **[!UICONTROL Utilisateurs]** , suivie de **[!UICONTROL Ajouter un utilisateur]**.

![Image montrant l’onglet utilisateurs d’un profil de produit dans Admin Console](./images/permissions/manage-users.png)

Pour plus d’informations sur la gestion des utilisateurs pour un profil de produit, voir [Documentation du Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html).

## Étapes suivantes

Ce guide couvrait les autorisations disponibles pour l’interface utilisateur de collecte de données et la manière de les gérer via Admin Console. Pour plus d’informations sur la gestion des autorisations pour d’autres fonctionnalités de Adobe Experience Platform, reportez-vous à la section [documentation sur le contrôle d’accès](../access-control/home.md).
