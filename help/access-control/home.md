---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
title: Présentation du contrôle d’accès
description: Dans Adobe Experience Platform, le contrôle dʼaccès est fourni par le biais dʼAdobe Admin Console. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88bfcdef65b4a938d573b1beb1952c7e030ebc13
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 65%

---

# Présentation du contrôle d’accès

Le contrôle d’accès de Adobe Experience Platform est fourni via le **[!UICONTROL Autorisations]** in [Adobe Experience Cloud](https://experience.adobe.com/). Cette fonctionnalité exploite des rôles et des stratégies qui lient les utilisateurs à des autorisations et des environnements de test.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle d’accès pour un Experience Platform, vous devez disposer de droits d’administrateur système ou produit pour une organisation disposant d’un produit Experience Platform. Le rôle minimum pouvant accorder ou retirer des autorisations est un administrateur de produit. Les autres rôles d’administrateur qui peuvent gérer les autorisations sont les administrateurs système (aucune restriction). Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de là, toute mention du terme &quot;administrateur&quot; dans ce document désigne un administrateur de produit ou plus (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après lʼattribution dʼune licence pour Adobe Experience Platform, ou pour une application/un service applicatif qui utilise Experience Platform, un e-mail est envoyé à lʼadministrateur spécifié lors de lʼattribution de la licence.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page d’aperçu.
- Pour accorder l’accès à Experience Platform, l’administrateur doit ajouter des utilisateurs au profil de produit par défaut : `AEP-Default-All-Users`.
- Dans Autorisations des Experience Platform, l’administrateur peut créer de nouveaux rôles ou modifier les autorisations et les utilisateurs pour tous les rôles existants.
- Lors de la création ou de la modification d’un rôle, l’administrateur ajoute des utilisateurs au rôle à l’aide de la fonction **[!UICONTROL utilisateurs]** et accorde des autorisations à ces utilisateurs (par exemple, &quot;[!UICONTROL Lire les jeux de données]&quot; ou &quot;[!UICONTROL Gestion des schémas]&quot;) en modifiant les autorisations du rôle. De même, l’administrateur peut attribuer l’accès aux environnements de test à l’aide de la même option de modification.
- Lorsque les utilisateurs se connectent à l’interface utilisateur de l’Experience Platform, leur accès aux fonctionnalités de l’Experience Platform dépend des autorisations qui leur ont été accordées à l’étape précédente. Par exemple, si un utilisateur ne dispose pas de la variable [!UICONTROL Affichage des jeux de données] l’autorisation, **[!UICONTROL Jeux de données]** dans le menu latéral ne sera pas visible pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la manière dont gérer le contrôle d’accès dans Experience Platform, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les autorisations sont activées pour tous les appels vers les API Experience Platform et renverront des erreurs si la ou les autorisations appropriées ne sont pas trouvées dans le contexte de l’utilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Autorisations {#platform-permissions}

[!UICONTROL Autorisations] fournit un emplacement central pour la gestion de l’accès des Experience Platform pour votre entreprise. Via [!UICONTROL Autorisations], vous pouvez octroyer à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités Experience Platform, telles que [!UICONTROL Gestion des jeux de données], [!UICONTROL Affichage des jeux de données]ou [!UICONTROL Gestion des profils].

### Rôles

Dans le [!UICONTROL Rôles] , des autorisations sont attribuées aux utilisateurs par l’intermédiaire de rôles. Les rôles vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs et de contenir leur accès à la portée des environnements de test qui leur sont affectés par le biais de rôles. Les utilisateurs peuvent être affectés à un ou plusieurs rôles appartenant à votre organisation.

### Rôles par défaut

Experience Platform est fourni avec deux rôles par défaut préconfigurés. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, le sandbox auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein du sandbox.

| Rôle | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Tous les accès de la production par défaut | Production | Toutes les autorisations applicables à Experience Platform à l’exception des autorisations Sandbox Administration |
| Administrateurs Sandbox | S/O | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Sandbox et autorisations

Les sandbox hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres sandbox et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations d’un rôle donnent aux utilisateurs du rôle l’accès aux fonctionnalités Experience Platform dans les environnements de test auxquels ils ont accès. Une licence Experience Platform par défaut vous accorde cinq sandbox (un de production et quatre hors production). Vous pouvez ajouter des packs de dix sandbox hors production jusquʼà un maximum de 75 sandbox au total. Veuillez contacter l’administration de votre organisation ou le service commercial d’Adobe pour plus de détails.

Pour plus d’informations sur les sandbox dans Experience Platform, reportez-vous à la [présentation des sandbox](../sandboxes/home.md).

### Accès aux sandbox

L’accès aux environnements de test est géré au moyen de rôles. Pour obtenir des instructions détaillées sur la manière d’activer l’accès à un environnement de test pour un rôle, reportez-vous à la section [guide des rôles de contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

Les utilisateurs peuvent se voir accorder l’accès à un ou plusieurs environnements de test au sein d’un rôle. Si un utilisateur fait partie de deux rôles ou plus, il aura accès à tous les environnements de test inclus dans ces rôles.

L’autorisation « Gestion des sandbox » permet aux utilisateurs de gérer, d’afficher ou de réinitialiser des sandbox.

### Autorisations des ressources {#permissions}

La ressource [!UICONTROL Autorisations] dans un rôle affiche les environnements de test et les autorisations principales pour ce rôle :

![présentation-autorisations](./images/permissions.png)

Les autorisations accordées par le biais des autorisations de ressources sont triées par catégorie, certaines autorisations permettant d’accéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour les Experience Platform dans le rôle, avec des descriptions des fonctionnalités d’Experience Platform spécifiques auxquelles ils accordent l’accès. Pour obtenir des instructions détaillées sur l’ajout d’autorisations à un rôle, reportez-vous à la section [guide des rôles de contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

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
| [!DNL Profile Management] | [!UICONTROL Gestion des politiques de fusion] | Accès à la lecture, la création, la modification et la suppression des politiques de fusion. |
| [!DNL Profile Management] | [!UICONTROL Affichage des politiques de fusion] | Accès en lecture seule aux politiques de fusion disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportation de l’audience pour un segment] | Capacité à exporter un segment ciblé évalué vers un jeu de données. |
| [!DNL Profile Management] | [!UICONTROL Évaluation dʼun segment sur une audience] | Capacité à générer des profils pour une audience en évaluant une définition de segment. |
| [!DNL Identity Management] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Afficher un graphique d’identité] | Accès en lecture seule aux graphiques d’identité. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des sandbox] | Accès à la lecture, la création, la modification et la suppression des sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des sandbox] | Accès en lecture seule aux sandbox appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un sandbox] | Capacité à réinitialiser un sandbox. |
| [!DNL Destinations] | [!UICONTROL Gestion des destinations] | Accès à la lecture, à la création et à la suppression des flux d’activation de destination et des comptes de destination. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Permet aux utilisateurs et utilisatrices d’activer des segments vers des destinations existantes. Active l’étape de mappage dans le workflow d’activation. Cette autorisation nécessite d’accorder les autorisations [!UICONTROL Afficher les destinations] ou [!UICONTROL Gérer les destinations] à l’utilisateur ou utilisatrice qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Activer un segment sans mappage] | Permet aux utilisateurs et utilisatrices d’activer des segments vers des destinations existantes, sans afficher l’[étape de mappage](../destinations/ui/activate-batch-profile-destinations.md#mapping). Les utilisateurs et utilisatrices peuvent ajouter et supprimer des segments dans les workflows d’activation, mais ne peuvent pas ajouter ni supprimer des attributs ou des identités mappés. Cette autorisation nécessite d’accorder l’autorisation [!UICONTROL Activer les destinations] à l’utilisateur ou l’utilisatrice qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Gérer et activer des destinations de jeu de données] | Possibilité de lire, créer, modifier et désactiver les flux d’exportation des jeux de données. Possibilité d’activer les données vers les jeux de données actifs qui ont été créés. |
| [!DNL Destinations] | [!UICONTROL Création de destinations] | Possibilité de créer des destinations à lʼaide du [SDK Destination Adobe Experience Platform](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accès à la création, lʼacceptation et le refus de négociations entre partenaires afin de connecter deux organisations et d’activer les flux [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accès à la lecture, la création, la modification et la publication de flux [!DNL Segment Match] avec des partenaires actifs. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de l’espace de travail de science des données] | Accès à la lecture, la création, la modification et la suppression dans [!DNL Data Science Workspace]. |
| Gouvernance des données | [!UICONTROL Application dʼétiquettes dʼutilisation des données] | Accès à la lecture, la création et la suppression des étiquettes dʼutilisation des données. |
| Gouvernance des données | [!UICONTROL Gestion des politiques dʼutilisation des données] | Accès à la lecture, la création, la modification et la suppression des politiques dʼutilisation des données. |
| Gouvernance des données | [!UICONTROL Affichage des politiques dʼutilisation des données] | Accès en lecture seule pour les politiques dʼutilisation des données appartenant à votre organisation. |
| Gouvernance des données | [!UICONTROL Afficher le journal d’activité de l’utilisateur] | Accès en lecture seule pour afficher les [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) enregistrés des activités de Platform. |
| [!DNL Dashboards] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] | Accès en lecture seule pour afficher le tableau de bord de l’utilisation des licences. |
| [!DNL Dashboards] | [!UICONTROL Gestion des tableaux de bord standard] | Ajoutez des attributs personnalisés qui ne se trouvent pas encore dans l’entrepôt de données. |
| [!DNL Query Service] | [!UICONTROL Gestion des requêtes] | Accès à la lecture, la création, la modification et la suppression des requêtes SQL structurées pour les données Platform. |
| [!DNL Query Service] | [!UICONTROL Gestion de lʼintégration de Query Service] | Accès à la création, la mise à jour et la suppression des informations dʼidentification sans date dʼexpiration pour lʼaccès à Query Service. |

## Étapes suivantes

En lisant ce guide, les principes du contrôle d’accès dans Experience Platform vous ont été présentés. Vous pouvez maintenant continuer à [guide d’utilisation du contrôle d’accès basé sur les attributs](./abac/overview.md) pour obtenir des instructions détaillées sur l’utilisation d’Experience Cloud pour créer des rôles et attribuer des autorisations à Experience Platform.
