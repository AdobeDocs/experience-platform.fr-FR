---
solution: Experience Platform
title: Comment obtenir et octroyer des autorisations dʼaccès pour les tableaux de bord Experience Platform
type: Documentation
description: Octroyez aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord Experience Platform à lʼaide dʼAdobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
TQID: https://experienceleague.adobe.com/ZuPk5map-epe3a7-yCh6BmkrsxRWUIfy6t6MzKuQ2gM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebfid: c132d929-fa62-4271-803e-b823be07b914id: ed0d8d0e-04b9-4326-be72-a0fbca265377id: eec185bd-7d60-4193-ba3f-da427569936a
subfeature_v2: id: a16ec9c0-4484-4842-b9a0-5504cde38e6aid: a9b953c0-98db-499b-97f5-a0dc3290bda3id: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d175cb4c-5781-454e-a826-bf6dff786265id: d21bd11d-08df-4cd6-ad8f-cb59a09de5c0
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 621
ht-degree: 28%

---

# Autorisations dʼaccès pour les tableaux de bord

Afin dʼoctroyer aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord, vous devez dʼabord activer les autorisations. Dans Adobe Experience Platform, le contrôle d’accès est fourni via [Adobe Admin Console](https://adminconsole.adobe.com/). Les utilisateurs sont liés à des autorisations et à des sandbox par le biais de profils de produit dans l’[!DNL Admin Console].

Ce document fournit un résumé des autorisations disponibles pour les tableaux de bord, y compris les fonctionnalités auxquelles ils donnent accès et les fonctions utilisateur qu’ils activent. Pour obtenir des informations détaillées sur lʼobtention et lʼattribution dʼautorisations dʼaccès, commencez par lire la [Présentation du contrôle dʼaccès](../access-control/home.md).

## Conditions préalables

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

## Autorisations disponibles pour les tableaux de bord {#available-permissions}

Le service [!DNL Dashboards] fournit trois autorisations qui, lorsqu’elles sont combinées, offrent un accès complet aux tableaux de bord [!UICONTROL Profiles], [!UICONTROL Segments], [!UICONTROL Destinations] et [!UICONTROL License Usage] dans Adobe Experience Platform. Ces autorisations sont les suivantes :

| Autorisation | Description |
|---|---|
| **Gestion des tableaux de bord standard** | Cette autorisation est une **autorisation globale en lecture et écriture**. Il vous permet de [créer des widgets personnalisés](./customize/custom-widgets.md) et [modifier le schéma de widget](./customize/edit-schema.md) via le [!UICONTROL Widget library]. |
| **Afficher les tableaux de bord standard** | Cette fonctionnalité **lecture seule** est destinée aux tableaux de bord [!UICONTROL Profiles], [!UICONTROL Destinations] et [!UICONTROL Segments]. Elle permet d’y accéder via le volet de navigation de gauche d’Experience Platform. Il ajoute également des [!UICONTROL Dashboards] au volet de navigation de gauche et permet d’accéder à l’onglet Inventaire et intégrations des [!UICONTROL Dashboards] . |
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

|   | [!UICONTROL View Standard Dashboard] OU [!UICONTROL Manage Standard Dashboard] | [!UICONTROL View Profiles],<br/>[!UICONTROL View Segments],<br/> [!UICONTROL View Destinations] | [!UICONTROL Manage Queries] &amp; [!UICONTROL Manage Sandboxes] | [!UICONTROL View License Usage Dashboard] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dans le volet de navigation de gauche. | S.O. | **Une autorisation « Afficher » ou « Gérer » est REQUISE** pour chaque tableau de bord respectif. | S.O. | S.O. |
| [!DNL Dashboards] dans le volet de navigation de gauche. | ACTIVÉ | **Au moins un OBLIGATOIRE**. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (l’onglet parcourir ) | ACTIVÉ | S.O. | S.O. | S.O. |
| [!DNL Dashboards] onglet [!DNL Integrations] <br/> (utilisé pour installer Power BI) | ACTIVÉ | **Au moins un OBLIGATOIRE** | S.O. | S.O. |
| Bouton et workflow d’installation de Power BI | ACTIVÉ | S.O. | **OBLIGATOIRE** | S.O. |
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
