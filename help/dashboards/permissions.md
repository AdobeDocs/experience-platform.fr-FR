---
solution: Experience Platform
title: Comment obtenir et octroyer des autorisations dʼaccès pour les tableaux de bord Experience Platform
type: Documentation
description: Octroyez aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord Experience Platform à lʼaide dʼAdobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 28%

---

# Autorisations dʼaccès pour les tableaux de bord

Afin dʼoctroyer aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord, vous devez dʼabord activer les autorisations. Dans Adobe Experience Platform, le contrôle d’accès est fourni via [Adobe Admin Console](https://adminconsole.adobe.com/). Les utilisateurs sont liés à des autorisations et à des sandbox par le biais de profils de produit dans l’[!DNL Admin Console].

Ce document fournit un résumé des autorisations disponibles pour les tableaux de bord, y compris les fonctionnalités auxquelles ils donnent accès et les fonctions utilisateur qu’ils activent. Pour obtenir des informations détaillées sur lʼobtention et lʼattribution dʼautorisations dʼaccès, commencez par lire la [Présentation du contrôle dʼaccès](../access-control/home.md).

## Conditions préalables

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

## Autorisations disponibles pour les tableaux de bord {#available-permissions}

Le service [!DNL Dashboards] fournit trois autorisations qui, lorsqu’elles sont combinées, offrent un accès complet aux tableaux de bord [!UICONTROL Profils], [!UICONTROL Segments], [!UICONTROL Destinations] et [!UICONTROL Utilisation de la licence] dans Adobe Experience Platform. Ces autorisations sont les suivantes :

| Autorisation | Description |
|---|---|
| **Gestion des tableaux de bord standard** | Cette autorisation est une **autorisation globale en lecture et écriture**. Il vous permet de [créer des widgets personnalisés](./customize/custom-widgets.md) et [modifier le schéma de widget](./customize/edit-schema.md) via la [!UICONTROL bibliothèque de widgets]. |
| **Afficher les tableaux de bord standard** | Cette interface fournit une fonctionnalité **lecture seule** pour les tableaux de bord [!UICONTROL Profils], [!UICONTROL Destinations] et [!UICONTROL Segments] et permet d’y accéder via le volet de navigation de gauche d’Experience Platform. Elle ajoute également [!UICONTROL Tableaux de bord] au volet de navigation de gauche et permet d’accéder à l’onglet Inventaire et intégrations [!UICONTROL Tableaux de bord]. |
| **Afficher le tableau de bord d’utilisation des licences** | Cette autorisation permet aux utilisateurs d’accéder **en lecture seule** au tableau de bord [’utilisation des licences](./guides/license-usage.md) dans l’interface utilisateur d’Experience Platform. |

Cinq autorisations non incluses dans la catégorie [!DNL Dashboard] peuvent être requises en fonction de vos besoins. Le tableau suivant décrit les emplacements des catégories dans Admin Console :

>[!IMPORTANT]
>
>Les autorisations **[!DNL Manage Standard Dashboards]** et **[!DNL View Standard Dashboards]** **nécessitent** une autorisation « afficher » ou « gérer » de la catégorie [!DNL Profile Management] ou [!DNL Destinations] d’Admin Console pour activer les sections appropriées dans l’interface utilisateur d’Experience Platform.

| Autorisation | Emplacement de la catégorie Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice de contrôle d’accès

La matrice de contrôle d’accès suivante fournit une répartition des autorisations requises et des fonctions qu’elles fournissent concernant l’accès aux différentes fonctionnalités des tableaux de bord. Les autorisations sont répertoriées dans la ligne horizontale supérieure et l’espace de travail de l’interface utilisateur d’Experience Platform est répertorié dans la colonne de gauche.

|   | [!UICONTROL Afficher le tableau de bord standard] OU [!UICONTROL Gérer le tableau de bord standard] | [!UICONTROL Affichage des profils],<br/>[!UICONTROL Affichage des segments],<br/> [!UICONTROL Affichage des destinations] | [!UICONTROL Gérer les requêtes] et [!UICONTROL Gérer les sandbox] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dans le volet de navigation de gauche. | S/O | **Une autorisation « Afficher » ou « Gérer » est REQUISE** pour chaque tableau de bord respectif. | S.O. | S.O. |
| [!DNL Dashboards] dans le volet de navigation de gauche. | ACTIVÉ | **Au moins un OBLIGATOIRE**. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (l’onglet parcourir ) | ACTIVÉ | S.O. | S.O. | S.O. |
| [!DNL Dashboards] onglet [!DNL Integrations] <br/> (utilisé pour installer Power BI) | ACTIVÉ | **Au moins un OBLIGATOIRE** | S.O. | S.O. |
| Bouton et workflow d’installation de Power BI | ACTIVÉ | S/O | **OBLIGATOIRE** | S/O |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] tableaux de bord.<br/>La possibilité de modifier les schémas de widget et d’ajouter de nouveaux attributs pour la personnalisation des widgets | **Manage-standard-dashboard REQUIRED** | **OBLIGATOIRE (pour chaque tableau de bord respectif)** | S.O. | S.O. |
| [!DNL License Usage Dashboard] | S.O. | S.O. | S.O. | ACTIVÉ |

{style="table-layout:auto"}

## Ajouter des autorisations à votre profil de produit

Utilisez les informations fournies ci-dessus pour ajouter les autorisations appropriées à votre profil de produit. Consultez la documentation pour obtenir des instructions complètes sur [comment ajouter des autorisations via l’interface utilisateur de contrôle d’accès](../access-control/ui/permissions.md).

Pour obtenir une description des autorisations, reportez-vous à la section [Autorisations disponibles](#available-permissions) plus haut dans ce document.

>[!NOTE]
>
>Il nʼest pas nécessaire dʼactiver toutes les autorisations pour tous les utilisateurs. Selon la structure de votre entreprise, vous pouvez créer des profils de produit distincts pour certains utilisateurs et accorder un accès limité (par exemple en lecture seule). Consultez la documentation sur la gestion des utilisateurs pour un profil de produit pour savoir [comment attribuer des autorisations à des utilisateurs spécifiques](../access-control/ui/users.md).

Une fois que vous avez ajouté les autorisations d’accès nécessaires, les utilisateurs de votre organisation peuvent commencer à afficher les tableaux de bord dans l’interface utilisateur d’Experience Platform et à effectuer d’autres actions en fonction des autorisations que vous avez attribuées.
