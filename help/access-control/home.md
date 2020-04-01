---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' de'
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


#  de

Le de la plateforme d’expérience est fourni par le biais de la console [d’administration](https://adminconsole.adobe.com)Adobe. Cette fonctionnalité tire parti des  de produits dans la Console d’administration, qui relient les utilisateurs à des autorisations et des sandbox.

## Hiérarchie des  et flux de travail

Pour configurer les  de la plateforme d’expérience, vous devez disposer de droits d’administrateur pour une organisation qui dispose d’une intégration de produit Experience Platform. Le rôle minimum qui accorde ou retire des autorisations est un administrateur **de de produits**. Les autres rôles d’administrateur pouvant gérer les autorisations sont les administrateurs **de** produits (ils peuvent gérer tous les  d’un produit) et les administrateurs **** système (sans restriction). Pour plus d’informations, reportez-vous à l’article du Centre d’aide d’Adobe sur les rôles [d’](https://helpx.adobe.com/enterprise/using/admin-roles.html) administration.

>[!NOTE] À partir de ce moment, toute mention de &quot;administrateur&quot; dans ce se rapporte à un administrateur de de produits ou plus (comme indiqué ci-dessus).

Un processus de haut niveau permettant d’obtenir et d’affecter des autorisations d’accès peut être résumé comme suit :

- Après vous être abonné à Adobe Experience Platform, un courrier électronique est envoyé à l’administrateur spécifié dans le formulaire d’inscription.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** dans le des produits sur la page d’aperçu.
- L’administrateur peut  le [de produit par défaut](#product-profiles) ou créer un nouveauproduit client, le cas échéant.
- L’administrateur peut modifier les autorisations et les utilisateurs de tout de produits existant.
- Lors de la création ou de la modification d’un  de produits, l’administrateur ajoute des utilisateurs au à l’aide de l’onglet **Utilisateurs** et leur accorde des autorisations (telles que &quot;Lire les jeux de données&quot; ou &quot;Gérer les **&quot;) en accédant à l’onglet** Autorisations. De même, l’administrateur peut affecter l’accès aux sandbox à l’aide du même onglet d’autorisations.
- Lorsque les utilisateurs se connectent à l’interface utilisateur de la plate-forme d’expérience, leur accès aux fonctionnalités de la plate-forme dépend des autorisations qui leur ont été accordées à partir de l’étape 2. Par exemple, si un utilisateur ne dispose pas de l’autorisation &quot; jeux de données&quot;, l’onglet *jeux* de données du menu latéral ne sera pas visible pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la gestion des  de dans la plateforme d’expérience, reportez-vous au guide [d’utilisation des  de](./ui/overview.md).

Tous les appels aux API de plateforme d’expérience sont validés pour les autorisations et renverront des erreurs si les autorisations appropriées ne sont pas trouvées dans le contexte utilisateur actuel. Dans l’interface utilisateur, les éléments sont masqués ou modifiés selon les autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console fournit un emplacement central pour la gestion des droits d’accès et des droits d’accès aux produits Adobe pour votre entreprise. Grâce à la console, vous pouvez octroyer à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités de la plateforme, telles que &quot;Gérer les jeux de données&quot;, &quot; jeux de données&quot; ou &quot;Gérer les  de&quot;.

### Profils de produit

Dans la console d’administration, les utilisateurs disposent d’autorisations grâce à l’utilisation des **de produits**. Le de produits vous permet d’accorder des autorisations à un ou plusieurs utilisateurs et de limiter leur accès à la portée des sandbox qui leur sont attribués par l’intermédiaire du de produits. Les utilisateurs peuvent être affectés à un ou plusieurs de produits  appartenant à votre organisation.

###  de produits par défaut

Experience Platform est fourni avec deux  de produits par défaut préconfigurés. Le tableau suivant décrit les éléments fournis dans chaque  par défaut, y compris le sandbox auquel ils donnent accès, ainsi que les autorisations qu’ils accordent dans le cadre de ce sandbox.

|  de produits | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Production par défaut - Accès complet | Production | Toutes les autorisations applicables à Experience Platform, à l’exception des autorisations d’administration de Sandbox. |
| Administration Sandbox par défaut | S.O. | Permet d’accéder uniquement aux autorisations d’administration de Sandbox. |

## Sandbox et autorisations

Experience Platform permet d’accéder à un sandbox Production et de créer des **sandbox** hors production. Les sandbox hors production sont une forme de virtualisation des données qui vous permet d’isoler les données des autres sandbox et sont généralement utilisés pour des expériences de développement, des tests ou des tests. Un de produits  **autorisations** donnent aux utilisateurs de  accès aux fonctionnalités de la plate-forme dans le de sandbox auquel ils ont accès.

Pour plus d’informations sur les sandbox dans Experience Platform, reportez-vous à la présentation [des](../sandboxes/home.md)sandbox.

### Accès aux sandbox

L’accès aux sandbox est géré par le biais des  de produits. Pour obtenir des instructions détaillées sur la manière d’activer l’accès à un sandbox pour un  de produit, reportez-vous au guide [d’utilisation de l’ de](./ui/overview.md).

Les utilisateurs peuvent accéder à un ou plusieurs sandbox dans un de produits. Si un utilisateur est inclus dans deux  de produits ou plus, il aura accès à tous les sandbox inclus dans ces  de produits.

L’autorisation &quot;Gestion des sandbox&quot; permet aux utilisateurs de gérer, de  ou de réinitialiser des sandbox.

### Autorisations

L’onglet **Autorisations** d’un de produits affiche les sandbox et les autorisations actives pour ce  :

![](./images/permissions-overview.png)

Les autorisations octroyées par l’intermédiaire de la Console d’administration sont triées par  de, avec certaines autorisations permettant d’accéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour la plateforme d’expérience dans la console d’administration, ainsi que les fonctionnalités spécifiques de la plateforme auxquelles ils donnent accès. Pour obtenir des instructions détaillées sur la manière d’ajouter des autorisations à un  de produits, reportez-vous au guide [d’utilisation de l’ de](./ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| Modélisation des données | Gérer les  de | Accès à la lecture, à la création, à la modification et à la suppression des  de et des ressources connexes. |
| Modélisation des données | View Schemas | Accès en lecture seule aux  de et aux ressources connexes. |
| Data Management | Gérer les jeux de données | Accès à la lecture, à la création, à la modification et à la suppression des jeux de données. Accès en lecture seule pour les  de. |
| Data Management |  de données | Accès en lecture seule pour les jeux de données et les  de. |
| Data Management | Surveillance des données | Accès en lecture seule aux jeux de données et aux flux de surveillance. |
| Gestion des  | Gestion des profils | Accès à la lecture, à la création, à la modification et à la suppression des jeux de données utilisés pour les  du client. Accès en lecture seule aux  disponibles. |
| Gestion des  | View Profiles | Accès en lecture seule aux  disponibles. |
| Gestion des  | Exporter   de pour le segment | Possibilité d’exporter un segment   évalué vers un jeu de données. |
| Identités | Gérer les  d&#39;identité  | Accès à la lecture, à la création, à la modification et à la suppression de l&#39;identité  . |
| Identités | identité   | Accès en lecture seule pour les  d&#39;identité . |
| Administration de Sandbox | Gestion des sandbox | Accès à la lecture, à la création, à la modification et à la suppression des sandbox. |
| Administration de Sandbox | Sandbox | Accès en lecture seule pour les sandbox appartenant à votre organisation. |
| Administration de Sandbox | Réinitialisation d’un sandbox | Possibilité de réinitialiser un sandbox. |
| Destinations | Gérer les destinations | Accès à des destinations de lecture, de création, de modification et de désactivation.* |
| Destinations | Destinations  | Accès en lecture seule aux destinations disponibles dans l’onglet *Catalogue* et aux destinations authentifiées dans l’onglet *Parcourir* .* |
| Destinations | Activer les destinations | Possibilité d’activer les données vers les destinations actives qui ont été créées. Cette autorisation requiert que &quot;Destinations &quot; ou &quot;Gérer les destinations&quot; soient accordées à l’utilisateur qui activera les destinations.* |
| Ingestion des données | Gestion des sources | Accès à la lecture, à la création, à la modification et à la désactivation des sources. |
| Ingestion des données | Sources de  | Accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* . |
| Espace de travail Data Science | Gestion de l’espace de travail Data Science | Accès à la lecture, à la création, à la modification et à la suppression dans Data Science Workspace. |

_(*) Cette autorisation requiert des dispositions sur la plateforme de données clientes en temps réel. Pour plus d&#39;informations sur le CDP en temps réel, veuillez commencer par lire la présentation[du CDP en temps](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)réel._

## Étapes suivantes

En lisant ce guide, vous avez été familiarisé avec les principes principaux de la  dans la plateforme d’expérience. Vous pouvez maintenant accéder au guide [de l’utilisateur des ](./ui/overview.md) pour obtenir des instructions détaillées sur l’utilisation de la Console d’administration pour créer des  de produits et attribuer des autorisations pour la plateforme.