---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
title: Présentation du contrôle d’accès
description: Dans Adobe Experience Platform, le contrôle dʼaccès est fourni par le biais dʼAdobe Admin Console. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 56f1cbc622450b154e6e29a8116789b316901f66
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 100%

---

# Présentation du contrôle d’accès

Dans [!DNL Experience Platform], le contrôle dʼaccès est fourni par le biais dʼ[Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produit dans [!DNL Admin Console], liant les utilisateurs à des autorisations et des sandbox.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle dʼaccès dans [!DNL Experience Platform], vous devez posséder des droits dʼadministrateur pour une organisation qui dispose dʼune intégration de produit [!DNL Experience Platform]. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un administrateur de profils de produit. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les administrateurs de produit (qui peuvent gérer tous les profils au sein d’un produit) et les administrateurs système (aucune restriction). Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de maintenant, le terme « administrateur » dans ce document désigne un administrateur de profils de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après lʼattribution dʼune licence pour Adobe Experience Platform, ou pour une application/un service applicatif qui utilise Experience Platform, un e-mail est envoyé à lʼadministrateur spécifié lors de lʼattribution de la licence.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page d’aperçu.
- L’administrateur peut afficher les [profils de produit](#product-profiles) par défaut ou créer de nouveaux profils de produit clients si nécessaire.
- L’administrateur peut modifier les autorisations et les utilisateurs pour tout profil de produit existant.
- Lors de la création ou de la modification dʼun profil de produit, lʼadministrateur ajoute les utilisateurs au profil à lʼaide de lʼonglet **[!UICONTROL Utilisateurs]**, et accorde des autorisations à ces utilisateurs (comme « [!UICONTROL Lecture des jeux de données] » ou « [!UICONTROL Gestion des schémas] ») en y accédant depuis lʼonglet **[!UICONTROL Autorisations]**. De même, l’administrateur peut attribuer des accès aux sandbox à l’aide du même onglet Autorisations.
- Lorsque les utilisateurs se connectent à lʼinterface utilisateur dʼ[!DNL Experience Platform], leur accès aux fonctionnalités [!DNL Platform] est géré par les autorisations qui leur ont été accordées à lʼétape 2. Par exemple, si un utilisateur ne dispose pas de lʼautorisation « [!UICONTROL Affichage des jeux de données] », lʼonglet **[!UICONTROL Jeux de données]** nʼapparaîtra pas dans le menu latéral pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la manière de gérer le contrôle dʼaccès dans [!DNL Experience Platform], consultez le [guide dʼutilisation du contrôle dʼaccès](./ui/overview.md).

Les autorisations sont activées pour tous les appels vers les API dʼ[!DNL Experience Platform] et renverront des erreurs si la ou les autorisations appropriées ne sont pas trouvées dans le contexte de lʼutilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console permet de centraliser la gestion des droits et accès de vos produits Adobe pour votre organisation. Grâce à la console, vous pouvez accorder des autorisations dʼaccès à des groupes dʼutilisateurs à différentes fonctionnalités de [!DNL Platform] comme « [!UICONTROL Gestion des jeux de données] », « [!UICONTROL Affichage des jeux de données] » ou « [!UICONTROL Gestion des profils] ».

### Profils de produit

Dans [!DNL Admin Console], des autorisations sont attribuées à des utilisateurs grâce à lʼutilisation des profils de produit. Les profils de produit vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs, mais aussi de contenir leur accès aux sandbox qui leur sont attribués par le biais des profils de produit. Il est possible d’attribuer un ou plusieurs profils de produit appartenant à votre organisation.

### Profils de produit par défaut

[!DNL Experience Platform] sʼaccompagne de deux profils de produit préconfigurés par défaut. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, le sandbox auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein du sandbox.

| Profil de produit | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Tous les accès de la production par défaut | Production | Toutes les autorisations applicables à [!DNL Experience Platform] à lʼexception des autorisations Sandbox Administration. |
| Administrateurs Sandbox | S/O | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Sandbox et autorisations

Les sandbox hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres sandbox et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations dʼun profil de produit donnent aux utilisateurs du profil lʼaccès aux fonctionnalités de [!DNL Platform] dans les sandbox auxquels ils se sont vus accorder lʼaccès. Une licence Experience Platform par défaut vous accorde cinq sandbox (un de production et quatre hors production). Vous pouvez ajouter des packs de dix sandbox hors production jusquʼà un maximum de 75 sandbox au total. Contactez votre administrateur dʼorganisation IMS ou votre représentant commercial Adobe pour plus de détails.

Pour plus dʼinformations sur les sandbox dans [!DNL Experience Platform], reportez-vous à la [présentation des sandbox](../sandboxes/home.md).

### Accès aux sandbox

L’accès aux sandbox est géré par l’intermédiaire des profils de produit. Pour obtenir des instructions détaillées sur la manière d’activer l’accès à un sandbox pour un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les utilisateurs peuvent se voir accorder l’accès à un ou plusieurs sandbox au sein d’un profil de produit. Si un utilisateur fait partie de deux profils de produit ou plus, cet utilisateur aura accès à tous les sandbox inclus dans ces profils.

L’autorisation « Gestion des sandbox » permet aux utilisateurs de gérer, d’afficher ou de réinitialiser des sandbox.

### Autorisations {#permissions}

L’onglet Autorisations au sein d’un profil de produit affiche les sandbox et les autorisations actifs pour ce profil :

![présentation-autorisations](./images/permissions.png)

Les autorisations accordées par lʼintermédiaire dʼ[!DNL Admin Console] sont triées par catégorie, certaines autorisations permettant dʼaccéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour [!DNL Experience Platform] dans [!DNL Admin Console], avec des descriptions des fonctionnalités spécifiques de [!DNL Platform] auxquelles elles donnent accès. Pour obtenir des instructions détaillées sur la manière dont ajouter des autorisations à un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL Afficher l’historique des alertes] | Accès en lecture seule à l’historique des alertes. |
| [!DNL Alerts] | [!UICONTROL Résoudre les alertes] | Accès à la lecture, la modification et la suppression des alertes. |
| [!DNL Alerts] | [!UICONTROL Affichage des alertes] | Accès en lecture seule aux alertes. |
| [!DNL Alerts] | [!UICONTROL Gérer les alertes] | Accès à la lecture, la création, la modification et la suppression de l’historique des alertes. |
| [!DNL Data Hygiene] | [!UICONTROL Afficher l’hygiène des données] | Accès en lecture seule à l’hygiène des données. |
| [!DNL Data Hygiene] | [!UICONTROL Gérer l’hygiène des données] | Accès à la lecture, la création, la modification et la suppression de lʼhygiène des données. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès pour lire, créer, modifier et supprimer des schémas et des ressources associées. |
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
| [!DNL Identity Management] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Afficher un graphique d’identité] | Accès en lecture seule aux graphiques d’identité. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des sandbox] | Accès à la lecture, la création, la modification et la suppression des sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des sandbox] | Accès en lecture seule aux sandbox appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un sandbox] | Capacité à réinitialiser un sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestion des destinations] | Accès à la lecture, la création, la modification et la désactivation des destinations. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Capacité à activer les données vers les destinations actives qui ont été créées. Cette autorisation nécessite d’accorder soit [!UICONTROL Afficher les destinations] ou [!UICONTROL Gérer les destinations] à l’utilisateur ou utilisatrice qui activera les destinations. |
| [!DNL Destinations] | [!UICONTROL Gérer et activer des destinations de jeu de données] | Possibilité de lire, créer, modifier et désactiver les flux d’exportation des jeux de données. Possibilité d’activer les données vers les jeux de données actifs qui ont été créés. |
| [!DNL Destinations] | [!UICONTROL Création de destinations] | Possibilité de créer des destinations à lʼaide du [SDK Destination Adobe Experience Platform](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accès à la création, lʼacceptation et le refus des négociations entre partenaires afin de connecter deux organisations IMS et dʼactiver les flux [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accès à la lecture, la création, la modification et la publication de flux [!DNL Segment Match] avec des partenaires actifs. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de l’espace de travail de science des données] | Accès à la lecture, la création, la modification et la suppression dans [!DNL Data Science Workspace]. |
| Gouvernance des données | [!UICONTROL Application dʼétiquettes dʼutilisation des données] | Accès à la lecture, la création et la suppression des étiquettes dʼutilisation des données. |
| Gouvernance des données | [!UICONTROL Gestion des stratégies dʼutilisation des données] | Accès à la lecture, la création, la modification et la suppression des stratégies dʼutilisation des données. |
| Gouvernance des données | [!UICONTROL Affichage des stratégies dʼutilisation des données] | Accès en lecture seule pour les stratégies dʼutilisation des données appartenant à votre organisation. |
| Gouvernance des données | [!UICONTROL Afficher le journal d’activité de l’utilisateur] | Accès en lecture seule pour afficher les [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) enregistrés des activités de Platform. |
| [!DNL Dashboards] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] | Accès en lecture seule pour afficher le tableau de bord de l’utilisation des licences. |
| [!DNL Dashboards] | [!UICONTROL Gestion des tableaux de bord standard] | Ajoutez des attributs personnalisés qui ne se trouvent pas encore dans l’entrepôt de données. |
| [!DNL Query Service] | [!UICONTROL Gestion des requêtes] | Accès à la lecture, la création, la modification et la suppression des requêtes SQL structurées pour les données Platform. |
| [!DNL Query Service] | [!UICONTROL Gestion de lʼintégration de Query Service] | Accès à la création, la mise à jour et la suppression des informations dʼidentification sans date dʼexpiration pour lʼaccès à Query Service. |

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](./ui/overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Platform].
