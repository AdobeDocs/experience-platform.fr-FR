---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
title: Présentation du contrôle d’accès
description: Dans Adobe Experience Platform, le contrôle dʼaccès est fourni par le biais dʼAdobe Admin Console. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 5d5c57dfb9e4abda6b1bca96147a95d063bc17c6
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 78%

---

# Présentation du contrôle d’accès

Le contrôle d’accès d’Adobe Experience Platform est fourni via les **[!UICONTROL autorisations]** dans [Adobe Experience Cloud](https://experience.adobe.com/). Cette fonctionnalité exploite les rôles et les politiques, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle d’accès dans Experience Platform, vous devez posséder des droits d’administrateur système ou produit pour une organisation qui dispose d’un produit Experience Platform. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un administrateur ou une administratrice de produit. Les autres rôles d’administrateur ou d’administratrice qui peuvent gérer les autorisations sont les administrateurs ou administratrices système (aucune restriction). Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de maintenant, le terme « administrateur ou administratrice » dans ce document désigne un administrateur ou une administratrice de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après lʼattribution dʼune licence pour Adobe Experience Platform, ou pour une application/un service applicatif qui utilise Experience Platform, un e-mail est envoyé à lʼadministrateur spécifié lors de lʼattribution de la licence.
- L’administrateur ou l’administratrice se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page de la vue d’ensemble.
- Pour accorder l’accès à Experience Platform, il est recommandé que l’administrateur ajoute des utilisateurs au profil de produit par défaut : `AEP-Default-All-Users`.
- Dans Autorisations dans Experience Platform, l’administrateur ou administratrice peut créer de nouveaux rôles ou modifier les autorisations et les utilisateurs et utilisatrices pour tous les rôles existants.
- Lors de la création ou de la modification dʼun rôle, lʼadministrateur ou administratrice ajoute les utilisateurs et utilisatrices au rôle à lʼaide de lʼonglet **[!UICONTROL Utilisateurs]**, et accorde des autorisations à ces utilisateurs et utilisatrices (comme « [!UICONTROL Lecture des jeux de données] » ou « [!UICONTROL Gestion des schémas] ») en modifiant les autorisations des rôles. De même, l’administrateur ou administratrice peut attribuer des accès aux sandbox à l’aide de la même option de modification.
- Lorsque les utilisateurs et utilisatrices se connectent à l’interface utilisateur Experience Platform, leur accès aux fonctionnalités d’Experience Platform est géré par les autorisations qui leur ont été accordées à l’étape précédente. Par exemple, si un utilisateur ou une utilisatrice ne dispose pas de lʼautorisation « [!UICONTROL Affichage des jeux de données] », lʼonglet **[!UICONTROL Jeux de données]** nʼapparaîtra pas dans le menu latéral pour cet utilisateur ou utilisatrice.

Pour obtenir des instructions plus détaillées sur la manière dont gérer le contrôle d’accès dans Experience Platform, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les autorisations sont activées pour tous les appels vers les API Experience Platform et renverront des erreurs si la ou les autorisations appropriées ne sont pas trouvées dans le contexte de l’utilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Autorisations {#platform-permissions}

Les [!UICONTROL autorisations] fournissent un emplacement central pour la gestion de l’accès à Experience Platform pour votre organisation. Grâce aux [!UICONTROL autorisations], vous pouvez accorder des autorisations d’accès à des groupes d’utilisateurs et utilisatrices à différentes fonctionnalités d’Experience Platform telles que [!UICONTROL « Gestion des jeux de données »], [!UICONTROL « Affichage des jeux de données »] ou [!UICONTROL « Gestion des profils »].

### Rôles

Dans la section [!UICONTROL Rôles] , des autorisations sont attribuées aux utilisateurs et utilisatrices par l’intermédiaire de rôles. Les rôles vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs ou utilisatrices, mais aussi de contenir leur accès aux sandbox qui leur sont attribués par le biais des rôles. Les utilisateurs et utilisatrices peuvent recevoir un ou plusieurs rôles appartenant à votre organisation.

### Rôles par défaut

Experience Platform s’accompagne de deux rôles préconfigurés par défaut. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, le sandbox auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein du sandbox.

| Rôle | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Tous les accès de la production par défaut | Production | Toutes les autorisations applicables à Experience Platform à l’exception des autorisations Sandbox Administration |
| Administrateurs Sandbox | S/O | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Sandbox et autorisations

Les sandbox hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres sandbox et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations d’un rôle donnent aux utilisateurs et utilisatrices du rôle l’accès aux fonctionnalités d’Experience Platform dans les environnements de sandbox auxquels ils se sont vus accorder l’accès. Une licence Experience Platform par défaut vous accorde cinq sandbox (un de production et quatre hors production). Vous pouvez ajouter des packs de dix sandbox hors production jusquʼà un maximum de 75 sandbox au total. Veuillez contacter l’administration de votre organisation ou le service commercial d’Adobe pour plus de détails.

Pour plus d’informations sur les sandbox dans Experience Platform, reportez-vous à la [présentation des sandbox](../sandboxes/home.md).

### Accès aux sandbox

L’accès aux sandbox est géré par l’intermédiaire des rôles. Pour obtenir des instructions détaillées sur la manière d’activer l’accès à un sandbox pour un rôle, consultez le [guide des rôles du contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

Les utilisateurs et utilisatrices peuvent se voir accorder l’accès à un ou plusieurs sandbox au sein d’un rôle. Si un utilisateur ou une utilisatrice fait partie de deux rôles ou plus, il ou elle aura accès à tous les sandbox inclus dans ces rôles.

L’autorisation « Gestion des sandbox » permet aux utilisateurs et aux utilisatrices de gérer, d’afficher ou de réinitialiser des sandbox.

### Autorisations des ressources {#permissions}

L’onglet [!UICONTROL Autorisations] des ressources au sein d’un rôle affiche les sandbox et les autorisations actives pour ce rôle :

![présentation-autorisations](./images/permissions.png)

Les autorisations accordées par l’intermédiaire des autorisations de ressources sont triées par catégorie, certaines autorisations permettant d’accéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour Experience Platform dans le rôle, avec des descriptions des fonctionnalités spécifiques d’Experience Platform auxquelles elles donnent accès. Pour obtenir des instructions détaillées sur comment ajouter des autorisations à un rôle, consultez le [guide des rôles du contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL AI Assistant] | [!UICONTROL Activer l’assistant d’IA] | Possibilité de poser les questions de l’ [assistant d’IA](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL  Afficher les statistiques opérationnelles] | Accès pour obtenir des réponses aux requêtes [statistiques opérationnelles](../ai-assistant/home.md##operational-insights). |
| [!DNL Alerts] | [!UICONTROL Afficher l’historique des alertes] | Accès en lecture seule à l’historique des alertes. |
| [!DNL Alerts] | [!UICONTROL Résoudre les alertes] | Accès à la lecture, la modification et la suppression des alertes. |
| [!DNL Alerts] | [!UICONTROL Affichage des alertes] | Accès en lecture seule aux alertes. |
| [!DNL Alerts] | [!UICONTROL Gérer les alertes] | Accès à la lecture, la création, la modification et la suppression de l’historique des alertes. |
| [!DNL Computed Attributes] | [!UICONTROL Afficher les attributs calculés] | Accès en lecture seule à l’onglet Attributs calculés, à l’inventaire et aux détails. |
| [!DNL Computed Attributes] | [!UICONTROL Gérer les attributs calculés] | Accès à la lecture, la création, la suppression de brouillons et la désactivation des attributs calculés. |
| [!DNL Dashboards] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] | Accès en lecture seule pour afficher le tableau de bord de l’utilisation des licences. |
| [!DNL Dashboards] | [!UICONTROL Gestion des tableaux de bord standard] | Ajoutez des attributs personnalisés qui ne se trouvent pas encore dans l’entrepôt de données. |
| [!DNL Data Governance] | [!UICONTROL Gérer les libellés d’utilisation] | Accès à la lecture, la création et la suppression des étiquettes dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Gestion des politiques dʼutilisation des données] | Accès à la lecture, la création, la modification et la suppression des politiques dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Affichage des politiques dʼutilisation des données] | Accès en lecture seule pour les politiques dʼutilisation des données appartenant à votre organisation. |
| [!DNL Data Governance] | [!UICONTROL Afficher le journal d’activité de l’utilisateur] | Accès en lecture seule pour afficher les [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) enregistrés des activités de Platform. |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accès à la création, lʼacceptation et le refus de négociations entre partenaires afin de connecter deux organisations et d’activer les flux [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accès à la lecture, la création, la modification et la publication de flux [!DNL Segment Match] avec des partenaires actifs. |
| [!DNL Data Lifecycle] | [!UICONTROL Afficher le cycle de vie des données] | Accès en lecture seule au cycle de vie des données. |
| [!DNL Data Lifecycle] | [!UICONTROL Gérer le cycle de vie des données] | Accès à la lecture, la création, la modification et la suppression du cycle de vie des données. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès pour lire, créer, modifier et supprimer des schémas et des ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Affichage des schémas] | Accès en lecture seule aux schémas et aux ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des relations] | Accès à la lecture, la création, la modification et la suppression des relations de schéma. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des métadonnées dʼidentité] | Accès à la lecture, la création, la modification et la suppression des métadonnées dʼidentité pour les schémas. |
| [!DNL Data Management] | [!UICONTROL Gestion des jeux de données] | Accès à la lecture, la création, la modification et la suppression des jeux de données. Accès en lecture seule aux schémas. |
| [!DNL Data Management] | [!UICONTROL Affichage des jeux de données] | Accès en lecture seule aux jeux de données et aux schémas. |
| [!DNL Data Management] | [!UICONTROL Surveillance des données] | Accès en lecture seule à la surveillance des jeux de données et des flux. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de l’espace de travail de science des données] | Accès à la lecture, la création, la modification et la suppression dans [!DNL Data Science Workspace]. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Gérer les destinations] | Accès à la lecture, la création et la suppression des connexions de destination et des comptes de destination. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Permet aux utilisateurs et utilisatrices d’activer des segments vers des destinations existantes. Active l’étape de mappage dans le workflow d’activation. Cette autorisation nécessite également l’autorisation [!UICONTROL Afficher les destinations] pour être accordée à l’utilisateur qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Activer un segment sans mappage] | Permet aux utilisateurs et utilisatrices d’activer des segments vers des destinations existantes, sans afficher l’[étape de mappage](../destinations/ui/activate-batch-profile-destinations.md#mapping). Les utilisateurs et utilisatrices peuvent ajouter et supprimer des segments dans les workflows d’activation, mais ne peuvent pas ajouter ni supprimer des attributs ou des identités mappés. Cette autorisation nécessite également l’autorisation [!UICONTROL Afficher les destinations] pour être accordée à l’utilisateur qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Gérer et activer des destinations de jeu de données] | Possibilité de lire, créer, modifier et désactiver les flux d’exportation des jeux de données. Possibilité d’activer des données vers des jeux de données actifs qui ont été créés. Cette autorisation nécessite également l’autorisation [!UICONTROL Afficher les destinations] pour être accordée à l’utilisateur qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Création de destinations] | Possibilité de créer des destinations à lʼaide du [SDK Destination Adobe Experience Platform](../destinations/destination-sdk/overview.md). |
| [!DNL Identity Management] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Afficher un graphique d’identité] | Accès en lecture seule aux graphiques d’identité. |
| [!DNL Intelligent Services] | [!UICONTROL Afficher l’Attribution AI] | Accès en lecture seule aux paramètres et informations Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Gérer Attribution AI] | Accès à la lecture, la création, la modification et la suppression des modèles Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Afficher Customer AI] | Accès à la lecture ou à l’affichage des modèles de Customer AI. |
| [!DNL Intelligent Services] | [!UICONTROL Gérer l’IA dédiée aux clients] | Accès pour créer, mettre à jour, supprimer, activer ou désactiver des modèles Customer AI. |
| [!DNL Profile Management] | [!UICONTROL Gestion des profils] | Ingérez des données provenant de plusieurs sources, créez des profils fiables pour les clients individuels et stockez des données activées pour les profils dans le lac de données et dans la banque de données de Real-time Customer Profile. |
| [!DNL Profile Management] | [!UICONTROL Affichage des profils] | Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des segments] | Accès à la lecture, la création, la modification et la suppression des segments. |
| [!DNL Profile Management] | [!UICONTROL Affichage des segments] | Accès en lecture seule aux segments disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des politiques de fusion] | Accès à la lecture, la création, la modification et la suppression des politiques de fusion. |
| [!DNL Profile Management] | [!UICONTROL Affichage des politiques de fusion] | Accès en lecture seule aux politiques de fusion disponibles. |
| [!DNL Profile Management] | [!UICONTROL Importer des audiences] | Accès à la lecture, la création, la modification et la suppression des audiences importées. |
| [!DNL Profile Management] | [!UICONTROL Exportation de l’audience pour un segment] | Capacité à exporter un segment ciblé évalué vers un jeu de données. |
| [!DNL Profile Management] | [!UICONTROL Évaluation dʼun segment sur une audience] | Possibilité de générer des profils pour une audience en évaluant une définition de segment. |
| [!DNL Profile Management] | [!UICONTROL Afficher l’IA B2B] | Accès en lecture seule aux paramètres et aux configurations pour tous les services B2B AI/ML. |
| [!DNL Profile Management] | [!UICONTROL Gérer l’IA B2B] | Accès à la lecture, la création, la modification et la suppression des paramètres et des configurations pour tous les services B2B AI/ML. |
| [!DNL Profile Management] | [!UICONTROL Afficher le profil B2B] | Accès en lecture seule aux profils d’entité B2B (tels que Compte, Opportunité, etc.), aux paramètres et configurations pour tous les services B2B AI/ML et aux widgets de tableau de bord B2B. |
| [!DNL Profile Management] | [!UICONTROL Gérer le profil B2B] | Accès à la lecture, la création, la modification et la suppression des profils d’entité B2B (tels que Compte, Opportunité, etc.). Accès en lecture seule aux paramètres et configurations pour tous les services B2B AI/ML et aux widgets de tableau de bord B2B. |
| [!DNL Query Service] | [!UICONTROL Gestion des requêtes] | Accès à la lecture, la création, la modification et la suppression des requêtes SQL structurées pour les données Platform. |
| [!DNL Query Service] | [!UICONTROL Gestion de lʼintégration de Query Service] | Accès à la création, la mise à jour et la suppression des informations dʼidentification sans date dʼexpiration pour lʼaccès à Query Service. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des sandbox] | Accès à la lecture, la création, la modification et la suppression des sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des sandbox] | Accès en lecture seule aux sandbox appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un sandbox] | Capacité à réinitialiser un sandbox. |

## Étapes suivantes

En lisant ce guide, les principes du contrôle d’accès dans Experience Platform vous ont été présentés. Vous pouvez maintenant consulter le [guide d’utilisation du contrôle d’accès basé sur les attributs](./abac/overview.md) pour obtenir des instructions détaillées sur l’utilisation d’Experience Cloud pour créer des rôles et attribuer des autorisations à Experience Platform.
