---
keywords: Experience Platform;home;popular topics;access control;adobe admin console
solution: Experience Platform
topic: overview
title: Présentation du contrôle d’accès
description: Le contrôle d'accès de Adobe Experience Platform est fourni par l'intermédiaire du Adobe Admin Console. Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test.
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 63%

---


# Présentation du contrôle d’accès

Access control for [!DNL Experience Platform] is provided through the [Adobe Admin Console](https://adminconsole.adobe.com). This functionality leverages product profiles in [!DNL Admin Console], which link users with permissions and sandboxes.

## Hiérarchie et workflow du contrôle d’accès

In order to configure access control for [!DNL Experience Platform], you must have administrator privileges for an organization that has an [!DNL Experience Platform] product integration. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un **[!UICONTROL administrateur de profils de produit]**. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les **[!UICONTROL administrateurs de produit]** (qui peuvent gérer tous les profils au sein d’un produit) et les **[!UICONTROL administrateurs système]** (aucune restriction). Pour en savoir plus, consultez l’article d’Adobe Help Center sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de là, toute mention du terme « administrateur » dans ce document désigne un administrateur de profils de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après l’octroi de la licence de Adobe Experience Platform ou d’un service d’application/d’application utilisant l’Experience Platform, un courrier électronique est envoyé à l’administrateur spécifié lors de l’octroi de la licence.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page d’aperçu.
- L’administrateur peut afficher les [profils de produit](#product-profiles) par défaut ou créer de nouveaux profils de produit clients si nécessaire.
- L’administrateur peut modifier les autorisations et les utilisateurs pour tout profil de produit existant.
- When creating or editing a product profile, the administrator adds users to the profile using the **[!UICONTROL users]** tab, and grants permissions to these users (such as &quot;[!UICONTROL Read Datasets]&quot; or &quot;[!UICONTROL Manage Schemas]&quot;) by accessing the **[!UICONTROL permissions]** tab. De même, l’administrateur peut attribuer des accès aux environnements de test à l’aide du même onglet Autorisations.
- When users log in to the [!DNL Experience Platform] user interface, their access to [!DNL Platform] capabilities is driven by the permissions that have been granted to them from Step 2. For example, if a user does not have the &quot;[!UICONTROL View Datasets]&quot; permission, the **[!UICONTROL Datasets]** tab in the side menu will not be visible to that user.

For more detailed steps on how to manage access control in [!DNL Experience Platform], see the [access control user guide](./ui/overview.md).

All calls to [!DNL Experience Platform] APIs are validated for permissions, and will return errors if the appropriate permission(s) are not found in the current user context. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console permet de centraliser la gestion des droits et accès de vos produits Adobe pour votre organisation. Through the console, you can grant groups of users access permissions for various [!DNL Platform] capabilities, such as &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot;, or &quot;[!UICONTROL Manage Profiles]&quot;.

### Profils de produit

In the [!DNL Admin Console], permissions are assigned to users through the use of **[!UICONTROL product profiles]**. Les profils de produit vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs, mais aussi de contenir leur accès aux environnements de test qui leur sont attribués par le biais des profils de produit. Il est possible d’attribuer un ou plusieurs profils de produit appartenant à votre organisation.

### Profils de produit par défaut

[!DNL Experience Platform] est fourni avec deux profils de produits par défaut préconfigurés. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, l’environnement de test auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein de l’environnement de test.

| Profil de produit | Accès aux environnements de test | Autorisations |
| --- | --- | --- |
| Production par défaut - Tous les accès | Production | All permissions applicable to [!DNL Experience Platform], except for Sandbox Administration permissions. |
| Sandbox Administration par défaut | N/A | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Environnements de test et autorisations

Les environnements de test hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres environnements de test et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les **[!UICONTROL autorisations]** d’un profil de produit donnent aux utilisateurs du profil l’accès aux fonctionnalités de dans les environnements de test auxquels ils se sont vus accorder l’accès. [!DNL Platform] Une licence d’Experience Platform par défaut vous accorde cinq sandbox (une production et quatre non-production). Vous pouvez ajouter des packs de dix sandbox hors production jusqu’à un maximum de 75 sandbox au total. Veuillez contacter votre administrateur d&#39;entreprise IMS ou votre représentant commercial d&#39;Adobe pour plus de détails.

For more information about sandboxes in [!DNL Experience Platform], please refer to the [sandboxes overview](../sandboxes/home.md).

### Accès aux environnements de test

L’accès aux environnements de test est géré par l’intermédiaire des profils de produit. Pour obtenir des instructions détaillées sur la manière dont activer l’accès à un environnement de test pour un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les utilisateurs peuvent se voir accorder l’accès à un ou plusieurs environnements de test au sein d’un profil de produit. Si un utilisateur fait partie de deux profils de produit ou plus, cet utilisateur aura accès à tous les environnements de test inclus dans ces profils.

L’autorisation « Gestion des environnements de test » permet aux utilisateurs de gérer, d’afficher ou de réinitialiser des environnements de test.

### Autorisations

L’onglet **Autorisations** au sein d’un profil de produit affiche les environnements de test et les autorisations actives pour ce profil :

![](./images/permissions-overview.png)

Permissions that are granted through the [!DNL Admin Console] are sorted by category, with some permissions granting access to several low-level functionalities.

The following table outlines the available permissions for [!DNL Experience Platform] in the [!DNL Admin Console], with descriptions of the specific [!DNL Platform] capabilities they grant access to. Pour obtenir des instructions détaillées sur la manière dont ajouter des autorisations à un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès à la lecture, la création, la modification et la suppression des schémas et des ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Affichage des schémas] | Accès en lecture seule aux schémas et aux ressources associées. |
| [!DNL Data Management] | [!UICONTROL Gestion des jeux de données] | Accès à la lecture, la création, la modification et la suppression des jeux de données. Accès en lecture seule aux schémas. |
| [!DNL Data Management] | [!UICONTROL Affichage des jeux de données] | Accès en lecture seule aux jeux de données et aux schémas. |
| [!DNL Data Management] | [!UICONTROL Surveillance des données] | Accès en lecture seule à la surveillance des jeux de données et des flux. |
| [!DNL Profile Management] | [!UICONTROL Gestion des profils] | Accès à la lecture, la création, la modification et la suppression des jeux de données utilisés pour les profils de clients. Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Affichage des profils] | Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportation de l’audience pour un segment] | Capacité à exporter un segment ciblé évalué vers un jeu de données. |
| [!DNL Identities] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identities] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des environnements de test] | Accès à la lecture, la création, la modification et la suppression des environnements de test. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des environnements de test] | Accès en lecture seule aux environnements de test appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un environnement de test] | Capacité à réinitialiser un environnement de test. |
| [!DNL Destinations] | [!UICONTROL Gestion des destinations] | Accès à la lecture, la création, la modification et la désactivation des destinations.* |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**.* |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Capacité à activer les données vers les destinations actives qui ont été créées. This permission requires either “View Destinations” or “Manage [!UICONTROL Destinations”] to be granted to the user who will activate destinations.* |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de Data Science Workspace] | Access to read, create, edit, and delete in [!DNL Data Science Workspace]. |

_(*) Cette autorisation requiert des dispositions pour[!DNL Real-time Customer Data Platform]. Pour plus d’informations concernant la plateforme de données clients en temps réel d’Adobe, commencez par lire la[présentation de la plateforme de données clients en temps réel d’Adobe](https://docs.adobe.com/content/help/fr-FR/experience-platform/rtcdp/overview.html)._

## Étapes suivantes

By reading this guide, you have been introduced to the main principles of access control in [!DNL Experience Platform]. You can now continue to the [access control user guide](./ui/overview.md) for detailed steps on how use the [!DNL Admin Console] to create product profiles and assign permissions for [!DNL Platform].