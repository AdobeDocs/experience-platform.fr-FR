---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Présentation du contrôle d’accès
description: Dans Adobe Experience Platform, le contrôle dʼaccès est fourni par le biais dʼAdobe Admin Console. Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 4425f7d61aa5ff357c7ba25cf986201fefeacd67
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 97%

---

# Présentation du contrôle d’accès

Dans [!DNL Experience Platform], le contrôle dʼaccès est fourni par le biais dʼ[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans [!DNL Admin Console], liant les utilisateurs à des autorisations et des environnements de test.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un administrateur de profils de produit. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les administrateurs de produit (qui peuvent gérer tous les profils au sein d’un produit) et les administrateurs système (aucune restriction). Pour en savoir plus, consultez l’article d’Adobe Help Center sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de là, toute mention du terme « administrateur » dans ce document désigne un administrateur de profils de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après lʼoctroi de la licence pour Adobe Experience Platform, ou pour une application/service dʼapplication utilisant Experience Platform, un courrier électronique est envoyé à lʼadministrateur spécifié lors de lʼoctroi de la licence.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page d’aperçu.
- L’administrateur peut afficher les [profils de produit](#product-profiles) par défaut ou créer de nouveaux profils de produit clients si nécessaire.
- L’administrateur peut modifier les autorisations et les utilisateurs pour tout profil de produit existant.
- Lors de la création ou de la modification dʼun profil de produit, lʼadministrateur ajoute les utilisateurs au profil à lʼaide de lʼonglet **[!UICONTROL Utilisateurs]**, et accorde des autorisations à ces utilisateurs (comme « [!UICONTROL Lecture des jeux de données] » ou « [!UICONTROL Gestion des schémas] ») en y accédant depuis lʼonglet **[!UICONTROL Autorisations]**. De même, l’administrateur peut attribuer des accès aux environnements de test à l’aide du même onglet Autorisations.
- Lorsque les utilisateurs se connectent à lʼinterface utilisateur dʼ[!DNL Experience Platform], leur accès aux fonctionnalités [!DNL Platform] est géré par les autorisations qui leur ont été accordées à lʼétape 2. Par exemple, si un utilisateur ne dispose pas de lʼautorisation « [!UICONTROL Affichage des jeux de données] », lʼonglet **[!UICONTROL Jeux de données]** nʼapparaîtra pas dans le menu latéral pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la manière de gérer le contrôle dʼaccès dans [!DNL Experience Platform], consultez le [guide dʼutilisation du contrôle dʼaccès](./ui/overview.md).

Les autorisations sont activées pour tous les appels vers les API dʼ[!DNL Experience Platform] et renverront des erreurs si la ou les autorisations appropriées ne sont pas trouvées dans le contexte de lʼutilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console permet de centraliser la gestion des droits et accès de vos produits Adobe pour votre organisation. Grâce à la console, vous pouvez accorder des autorisations dʼaccès à des groupes dʼutilisateurs à différentes fonctionnalités de [!DNL Platform] comme « [!UICONTROL Gestion des jeux de données] », « [!UICONTROL Affichage des jeux de données] » ou « [!UICONTROL Gestion des profils] ».

### Profils de produit

Dans [!DNL Admin Console], des autorisations sont attribuées à des utilisateurs grâce à lʼutilisation des profils de produit. Les profils de produit vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs, mais aussi de contenir leur accès aux environnements de test qui leur sont attribués par le biais des profils de produit. Il est possible d’attribuer un ou plusieurs profils de produit appartenant à votre organisation.

### Profils de produit par défaut

[!DNL Experience Platform] sʼaccompagne de deux profils de produit préconfigurés par défaut. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, l’environnement de test auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein de l’environnement de test.

| Profil de produit | Accès aux environnements de test | Autorisations |
| --- | --- | --- |
| Tous les accès de la production par défaut | Production | Toutes les autorisations applicables à [!DNL Experience Platform] à lʼexception des autorisations Sandbox Administration. |
| Administrateurs Sandbox | N/A | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Environnements de test et autorisations

Les environnements de test hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres environnements de test et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations dʼun profil de produit donnent aux utilisateurs du profil lʼaccès aux fonctionnalités de [!DNL Platform] dans les environnements de test auxquels ils se sont vus accorder lʼaccès. Une licence Experience Platform par défaut vous accorde cinq environnements de test (un de production et quatre de non-production). Vous pouvez ajouter des packs de dix environnements de test de non-production jusquʼà un maximum de 75 environnements de test au total. Contactez votre administrateur dʼorganisation IMS ou votre représentant commercial Adobe pour plus de détails.

Pour plus dʼinformations sur les environnements de test dans [!DNL Experience Platform], reportez-vous à la [présentation des environnements de test](../sandboxes/home.md).

### Accès aux environnements de test

L’accès aux environnements de test est géré par l’intermédiaire des profils de produit. Pour obtenir des instructions détaillées sur la manière dont activer l’accès à un environnement de test pour un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les utilisateurs peuvent se voir accorder l’accès à un ou plusieurs environnements de test au sein d’un profil de produit. Si un utilisateur fait partie de deux profils de produit ou plus, cet utilisateur aura accès à tous les environnements de test inclus dans ces profils.

L’autorisation « Gestion des environnements de test » permet aux utilisateurs de gérer, d’afficher ou de réinitialiser des environnements de test.

### Autorisations

L’onglet Autorisations au sein d’un profil de produit affiche les environnements de test et les autorisations actives pour ce profil :

![présentation-autorisations](./images/permissions-overview.png)

Les autorisations accordées par lʼintermédiaire dʼ[!DNL Admin Console] sont triées par catégorie, certaines autorisations permettant dʼaccéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour [!DNL Experience Platform] dans [!DNL Admin Console], avec des descriptions des fonctionnalités spécifiques de [!DNL Platform] auxquelles elles donnent accès. Pour obtenir des instructions détaillées sur la manière dont ajouter des autorisations à un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès à la lecture, la création, la modification et la suppression des schémas et des ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Affichage des schémas] | Accès en lecture seule aux schémas et aux ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des relations] | Accès à la lecture, la création, la modification et la suppression des relations de schéma. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des métadonnées dʼidentité] | Accès à la lecture, la création, la modification et la suppression des métadonnées dʼidentité pour les schémas. |
| [!DNL Data Management] | [!UICONTROL Gestion des jeux de données] | Accès à la lecture, la création, la modification et la suppression des jeux de données. Accès en lecture seule aux schémas. |
| [!DNL Data Management] | [!UICONTROL Affichage des jeux de données] | Accès en lecture seule aux jeux de données et aux schémas. |
| [!DNL Data Management] | [!UICONTROL Surveillance des données] | Accès en lecture seule à la surveillance des jeux de données et des flux. |
| [!DNL Profile Management] | [!UICONTROL Gestion des profils] | Accès à la lecture, la création, la modification et la suppression des jeux de données utilisés pour les profils de clients. Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Affichage des profils] | Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des segments] | Accès à la lecture, la création, la modification et la suppression des segments. |
| [!DNL Profile Management] | [!UICONTROL Affichage des segments] | Accès en lecture seule aux segments disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des stratégies de fusion] | Accès à la lecture, la création, la modification et la suppression des stratégies de fusion. |
| [!DNL Profile Management] | [!UICONTROL Affichage des stratégies de fusion] | Accès en lecture seule aux stratégies de fusion disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportation de l’audience pour un segment] | Capacité à exporter un segment ciblé évalué vers un jeu de données. |
| [!DNL Profile Management] | [!UICONTROL Évaluation dʼun segment sur une audience] | Capacité à générer des profils pour une audience en évaluant une définition de segment. |
| [!DNL Identities] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identities] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des environnements de test] | Accès à la lecture, la création, la modification et la suppression des environnements de test. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des environnements de test] | Accès en lecture seule aux environnements de test appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un environnement de test] | Capacité à réinitialiser un environnement de test. |
| [!DNL Destinations] | [!UICONTROL Gestion des destinations] | Accès à la lecture, la création, la modification et la désactivation des destinations. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Capacité à activer les données vers les destinations actives qui ont été créées. Cette autorisation nécessite dʼaccorder soit « Affichage des destinations » ou « Gestion des [!UICONTROL destinations »] à lʼutilisateur qui activera les destinations. |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accès pour créer, accepter et refuser des poignées de main de partenaire afin de connecter deux organisations IMS et d’activer des flux [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accès à la lecture, la création, la modification et la publication de flux [!DNL Segment Match] avec des partenaires principaux. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de Data Science Workspace] | Accès à la lecture, la création, la modification et la suppression dans [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Application dʼétiquettes dʼutilisation des données] | Accès à la lecture, la création et la suppression des étiquettes dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Gestion des stratégies dʼutilisation des données] | Accès à la lecture, la création, la modification et la suppression des stratégies dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Affichage des stratégies dʼutilisation des données] | Accès en lecture seule pour les stratégies dʼutilisation des données appartenant à votre organisation. |
| [!DNL Data Governance] | [!UICONTROL Afficher le journal d’audit] | Accès en lecture seule à la vue des [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) enregistrés des activités de Platform. |
| [!DNL Dashboards] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] | Accès en lecture seule pour afficher le tableau de bord de l’utilisation des licences. |
| [!DNL Dashboards] | [!UICONTROL Gestion des tableaux de bord standard] | Ajoutez des attributs personnalisés qui ne se trouvent pas encore dans l’entrepôt de données. |
| [!DNL Query Service] | [!UICONTROL Gestion des requêtes] | Accès à la lecture, la création, la modification et la suppression des requêtes SQL structurées pour les données Platform. |

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](./ui/overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Platform].
