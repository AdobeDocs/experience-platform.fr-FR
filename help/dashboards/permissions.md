---
solution: Experience Platform
title: Comment obtenir et octroyer des autorisations dʼaccès pour les tableaux de bord Experience Platform
type: Documentation
description: Octroyez aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord Experience Platform à lʼaide dʼAdobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: 052e365c6127961363b7b5333cb0f4f82ab5479a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 32%

---

# Autorisations dʼaccès pour les tableaux de bord

Afin dʼoctroyer aux utilisateurs la possibilité dʼafficher, de modifier et de mettre à jour les tableaux de bord, vous devez dʼabord activer les autorisations. Dans Adobe Experience Platform, le contrôle d’accès est fourni via la variable [Adobe Admin Console](https://adminconsole.adobe.com/). Les utilisateurs sont liés à des autorisations et des environnements de test par le biais de profils de produit dans la variable [!DNL Admin Console].

Ce document résume les autorisations disponibles pour les tableaux de bord, notamment les fonctionnalités auxquelles ils donnent accès et les fonctions utilisateur qu’ils activent. Pour obtenir des informations détaillées sur lʼobtention et lʼattribution dʼautorisations dʼaccès, commencez par lire la [Présentation du contrôle dʼaccès](../access-control/home.md).

## Conditions préalables

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Pour en savoir plus, consultez l’article d’Adobe Help Center sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

## Autorisations des tableaux de bord disponibles {#available-permissions}

Le [!DNL Dashboards] Le service fournit trois autorisations qui, lorsqu’elles sont combinées, donnent un accès complet à la variable [!UICONTROL Profils], [!UICONTROL Segments], [!UICONTROL Destinations], et [!UICONTROL Utilisation de la licence] tableaux de bord dans Adobe Experience Platform. Ces autorisations sont les suivantes :

| Autorisation | Description |
|---|---|
| **Gestion des tableaux de bord standard** | Cette autorisation est une **autorisation globale de lecture et d&#39;écriture**. Il vous permet de [créer des widgets personnalisés](./customize/custom-widgets.md) et [modification du schéma du widget](./customize/edit-schema.md) via la [!UICONTROL Bibliothèque de widgets]. |
| **Affichage des tableaux de bord standard** | Cette variable fournit les **lecture seule** de la fonction [!UICONTROL Profils], [!UICONTROL Destinations], et [!UICONTROL Segments] Les tableaux de bord et permettent d’y accéder par le biais de la navigation de gauche de Platform. Il ajoute aussi : [!UICONTROL Tableaux de bord] à la navigation de gauche et à l’accès au [!UICONTROL Tableaux de bord] onglet inventaire et intégrations . |
| **Afficher le tableau de bord d’utilisation des licences** | Cette autorisation permet aux utilisateurs **lecture seule** accès à [le tableau de bord de l’utilisation des licences](./guides/license-usage.md) dans l’interface utilisateur de l’Experience Platform. |

Cinq autorisations ne sont pas incluses dans la variable [!DNL Dashboard] qui sont éventuellement requises en fonction de vos besoins. Le tableau suivant décrit les emplacements des catégories dans le Admin Console :

>[!IMPORTANT]
>
>Les deux **[!DNL Manage Standard Dashboards]** et le **[!DNL View Standard Dashboards]** permissions **require** une autorisation &quot;view&quot; ou &quot;manage&quot; de la [!DNL Profile Management] ou [!DNL Destinations] catégorie dans le Admin Console pour activer les sections pertinentes dans l’interface utilisateur de Platform.

| Autorisation | Emplacement des catégories de Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice de contrôle d&#39;accès

La matrice de contrôle d’accès suivante présente une répartition des autorisations requises et de la fonction qu’elles remplissent en ce qui concerne l’accès aux différentes fonctions du tableau de bord. Les autorisations sont répertoriées sur la ligne horizontale supérieure et l’espace de travail de l’interface utilisateur de Platform est répertorié le long de la colonne de gauche.

|  | [!UICONTROL Afficher le tableau de bord standard] OU [!UICONTROL Gérer le tableau de bord standard] | [!UICONTROL Afficher les profils],<br/>[!UICONTROL Affichage de segments],<br/> [!UICONTROL Affichage des destinations] | [!UICONTROL Gestion des requêtes] &amp; [!UICONTROL Gestion des environnements de test] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dans le volet de navigation de gauche. | S/O | **Une autorisation &quot;Afficher&quot; ou &quot;Gérer&quot; est requise** pour chaque tableau de bord respectif. | S.O. | S.O. |
| [!DNL Dashboards] dans le volet de navigation de gauche. | ACTIVÉ | **Au moins une**. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Inventory] <br/>(onglet Parcourir ) | ACTIVÉ | S.O. | S.O. | S.O. |
| [!DNL Dashboards] [!DNL Integrations] tab <br/>(utilisé pour installer Power BI) | ACTIVÉ | **Au moins une** | S.O. | S.O. |
| Bouton d’installation et workflow de Power BI | ACTIVÉ | S/O | **OBLIGATOIRE** | S/O |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] des tableaux de bord.<br/>Possibilité de modifier des schémas de widget d’ajouter de nouveaux attributs pour la personnalisation de widgets | **Gestion du tableau de bord standard REQUIS** | **REQUIS (pour chaque tableau de bord respectif)** | S.O. | S.O. |
| [!DNL License Usage Dashboard] | S.O. | S.O. | S.O. | ACTIVÉ |

{style=&quot;table-layout:auto&quot;}

## Ajout d’autorisations à votre profil de produit

Utilisez les informations fournies ci-dessus pour ajouter les autorisations appropriées à votre profil de produit. Consultez la documentation pour obtenir des instructions complètes sur [comment ajouter des autorisations via l’interface utilisateur de contrôle d’accès](../access-control/ui/permissions.md).

Pour obtenir une description des autorisations, reportez-vous à la section [Autorisations disponibles](#available-permissions) plus haut dans ce document.

>[!NOTE]
>
>Il nʼest pas nécessaire dʼactiver toutes les autorisations pour tous les utilisateurs. Selon la structure de votre entreprise, vous pouvez choisir de créer des profils de produit distincts pour certains utilisateurs ainsi quʼoctroyer un accès limité à dʼautres (comme la lecture seule). Pour en savoir plus, consultez la documentation sur la gestion des utilisateurs pour un profil de produit . [comment attribuer des autorisations à des utilisateurs spécifiques](../access-control/ui/users.md).

Une fois que vous avez ajouté les autorisations d’accès nécessaires, les utilisateurs de votre entreprise peuvent commencer à afficher les tableaux de bord dans l’interface utilisateur de l’Experience Platform et effectuer d’autres actions en fonction des autorisations que vous avez attribuées.
