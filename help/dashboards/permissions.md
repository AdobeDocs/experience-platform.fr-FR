---
solution: Experience Platform
title: Comment obtenir et octroyer des autorisations dʼaccès pour les tableaux de bord Experience Platform
type: Documentation
description: Octroyez aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord Experience Platform à lʼaide dʼAdobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 28%

---

# Autorisations dʼaccès pour les tableaux de bord

Afin dʼoctroyer aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord, vous devez dʼabord activer les autorisations. Dans Adobe Experience Platform, le contrôle d’accès est fourni via le [Adobe Admin Console](https://adminconsole.adobe.com/). Les utilisateurs sont liés à des autorisations et des environnements de test par le biais de profils de produit dans [!DNL Admin Console].

Ce document résume les autorisations disponibles pour les tableaux de bord, notamment les fonctionnalités auxquelles ils donnent accès et les fonctions utilisateur qu’ils activent. Pour obtenir des informations détaillées sur lʼobtention et lʼattribution dʼautorisations dʼaccès, commencez par lire la [Présentation du contrôle dʼaccès](../access-control/home.md).

## Conditions préalables

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

## Autorisations disponibles pour les tableaux de bord {#available-permissions}

Le service [!DNL Dashboards] fournit trois autorisations qui, lorsqu’elles sont combinées, fournissent un accès complet aux tableaux de bord [!UICONTROL Profils], [!UICONTROL Segments], [!UICONTROL Destinations] et [!UICONTROL Utilisation de la licence] dans Adobe Experience Platform. Ces autorisations sont les suivantes :

| Autorisation | Description |
|---|---|
| **Gestion des tableaux de bord standard** | Cette autorisation est une **autorisation globale de lecture et d’écriture**. Il vous permet de [créer des widgets personnalisés](./customize/custom-widgets.md) et de [modifier le schéma de widget](./customize/edit-schema.md) par l’intermédiaire de la [!UICONTROL bibliothèque de widgets]. |
| **Afficher les tableaux de bord standard** | Cela fournit une fonctionnalité de **lecture seule** pour les tableaux de bord [!UICONTROL Profils], [!UICONTROL Destinations] et [!UICONTROL Segments] et permet d’y accéder par le biais de la navigation de gauche de Platform. Il ajoute également [!UICONTROL Tableaux de bord] dans le volet de navigation de gauche et l’accès à l’onglet [!UICONTROL  Tableaux de bord] d’inventaire et d’intégrations. |
| **Afficher le tableau de bord d’utilisation des licences** | Cette autorisation permet aux utilisateurs **lecture seule** d’accéder à [ le tableau de bord de l’utilisation des licences](./guides/license-usage.md) dans l’interface utilisateur de l’Experience Platform. |

Cinq autorisations ne sont pas incluses dans la catégorie [!DNL Dashboard] et peuvent être requises selon vos besoins. Le tableau suivant décrit les emplacements des catégories dans l’Admin Console :

>[!IMPORTANT]
>
>Les autorisations **[!DNL Manage Standard Dashboards]** et **[!DNL View Standard Dashboards]** **nécessitent** une autorisation &quot;vue&quot; ou &quot;gérer&quot; de la catégorie [!DNL Profile Management] ou [!DNL Destinations] de l’Admin Console pour activer les sections appropriées dans l’interface utilisateur de Platform.

| Autorisation | Emplacement des catégories Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice de contrôle d&#39;accès

La matrice de contrôle d’accès suivante présente une répartition des autorisations requises et de la fonction qu’elles remplissent en ce qui concerne l’accès aux différentes fonctions du tableau de bord. Les autorisations sont répertoriées sur la ligne horizontale supérieure et l’espace de travail de l’interface utilisateur de Platform est répertorié le long de la colonne de gauche.

|   | [!UICONTROL Afficher Le Tableau De Bord Standard] OU [!UICONTROL Gérer Le Tableau De Bord Standard] | [!UICONTROL Afficher les profils],<br/>[!UICONTROL Afficher les segments],<br/> [!UICONTROL Affichage des destinations] | [!UICONTROL Gérer les requêtes] et [!UICONTROL Gérer les environnements de test] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dans la navigation de gauche. | S/O | **Une autorisation &quot;Vue&quot; ou &quot;Gérer&quot; est REQUISE** pour chaque tableau de bord respectif. | S.O. | S.O. |
| [!DNL Dashboards] dans la navigation de gauche. | ACTIVÉ | **Au moins un OBLIGATOIRE**. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (onglet de navigation) | ACTIVÉ | S.O. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Integrations] onglet <br/> (utilisé pour installer Power BI) | ACTIVÉ | **Au moins un OBLIGATOIRE** | S.O. | S.O. |
| Bouton d’installation et workflow de Power BI | ACTIVÉ | S/O | **REQUIRED** | S/O |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] tableaux de bord.<br/>Possibilité de modifier des schémas de widget et d’ajouter de nouveaux attributs pour la personnalisation de widgets | **Gérer le tableau de bord standard REQUIRED** | **OBLIGATOIRE (pour chaque tableau de bord respectif)** | S.O. | S.O. |
| [!DNL License Usage Dashboard] | S.O. | S.O. | S.O. | ACTIVÉ |

{style="table-layout:auto"}

## Ajout d’autorisations à votre profil de produit

Utilisez les informations fournies ci-dessus pour ajouter les autorisations appropriées à votre profil de produit. Consultez la documentation pour obtenir des instructions complètes sur [l’ajout d’autorisations via l’interface utilisateur de contrôle d’accès](../access-control/ui/permissions.md).

Pour obtenir une description des autorisations, reportez-vous à la section [Autorisations disponibles](#available-permissions) plus haut dans ce document.

>[!NOTE]
>
>Il nʼest pas nécessaire dʼactiver toutes les autorisations pour tous les utilisateurs. Selon la structure de votre entreprise, vous pouvez créer des profils de produit distincts pour certains utilisateurs et accorder un accès limité (comme la lecture seule). Consultez la documentation sur la gestion des utilisateurs pour un profil de produit afin d’apprendre [comment attribuer des autorisations à des utilisateurs spécifiques](../access-control/ui/users.md).

Une fois que vous avez ajouté les autorisations d’accès nécessaires, les utilisateurs de votre entreprise peuvent commencer à afficher les tableaux de bord dans l’interface utilisateur de l’Experience Platform et effectuer d’autres actions en fonction des autorisations que vous avez attribuées.
