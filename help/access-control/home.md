---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation du Contrôle d'accès
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 4%

---


# Présentation du Contrôle d&#39;accès

Le Contrôle d&#39;accès de l&#39;Experience Platform est fourni par l&#39;intermédiaire du Adobe [Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produits en Admin Console, qui lient les utilisateurs avec des autorisations et des sandbox.

## Hiérarchie des Contrôles d&#39;accès et processus

Pour configurer le contrôle d&#39;accès pour l’Experience Platform, vous devez disposer de droits d’administrateur pour une organisation qui dispose d’une intégration de produit Experience Platform. Le rôle minimum qui accorde ou retire des autorisations est un administrateur **de profil de** produits. Les autres rôles d’administrateur qui peuvent gérer les autorisations sont les administrateurs **de** produits (ils peuvent gérer tous les profils d’un produit) et les administrateurs **** système (sans restriction). Pour plus d’informations, consultez l’article du Centre d’aide Adobe sur les rôles [](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) administratifs.

>[!NOTE]
>
>Dès lors, toute mention d&#39;&quot;administrateur&quot; dans ce document se rapporte à un administrateur de profil de produits ou plus (comme indiqué ci-dessus).

Un processus de haut niveau permettant d’obtenir et d’attribuer des autorisations d’accès peut être résumé comme suit :

- Après s’être abonné à l’Adobe Experience Platform, un courrier électronique est envoyé à l’administrateur spécifié dans le formulaire d’inscription.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **l’Adobe Experience Platform** dans la liste des produits sur la page d’aperçu.
- L’administrateur peut vue les profils [de](#product-profiles) produits par défaut ou créer de nouveaux profils de produits client si nécessaire.
- L’administrateur peut modifier les autorisations et les utilisateurs pour tout profil de produits existant.
- Lors de la création ou de la modification d’un profil de produits, l’administrateur ajoute des utilisateurs au profil à l’aide de l’onglet **utilisateurs** et leur accorde des autorisations (telles que &quot;Lire les jeux de données&quot; ou &quot;Gérer les Schémas&quot;) en accédant à l’onglet **autorisations** . De même, l’administrateur peut attribuer l’accès aux sandbox à l’aide du même onglet d’autorisations.
- Lorsque les utilisateurs se connectent à l’interface utilisateur de l’Experience Platform, leur accès aux fonctionnalités Platform dépend des autorisations qui leur ont été accordées à partir de l’étape 2. Par exemple, si un utilisateur ne dispose pas de l’autorisation &quot;Jeu de données de Vue&quot;, l’onglet *Jeu de données* du menu latéral ne sera pas visible pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la gestion du contrôle d&#39;accès dans l’Experience Platform, consultez le guide [d’utilisation du](./ui/overview.md)contrôle d&#39;accès.

Tous les appels aux API Experience Platform sont validés pour les autorisations et renvoient des erreurs si les autorisations appropriées ne sont pas trouvées dans le contexte utilisateur actuel. Dans l’interface utilisateur, les éléments seront masqués ou modifiés selon les autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console fournit un emplacement central pour la gestion des droits de produits Adobe et l’accès pour votre entreprise. Par l’intermédiaire de la console, vous pouvez accorder à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités Platform, telles que &quot;Gérer les jeux de données&quot;, &quot;Vues de données&quot; ou &quot;Gérer les Profils&quot;.

### Profils de produit

Dans l’Admin Console, des autorisations sont attribuées aux utilisateurs par le biais de profils **de** produits. Les profils de produits vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs et de limiter leur accès à l’étendue des sandbox qui leur sont assignés par le biais de profils de produits. Les utilisateurs peuvent être affectés à un ou plusieurs profils de produits appartenant à votre organisation.

### profils de produits par défaut

Experience Platform est fourni avec deux profils de produit par défaut préconfigurés. Le tableau suivant décrit les éléments fournis dans chaque profil par défaut, notamment le sandbox auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent dans le cadre de ce sandbox.

| Profil de produits | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Production par défaut - Accès complet | Production | Toutes les autorisations applicables à l’Experience Platform, à l’exception des autorisations d’administration Sandbox. |
| Administration de sandbox par défaut | S.O. | Fournit l’accès uniquement aux autorisations d’administration de Sandbox. |

## Sandbox et autorisations

L’Experience Platform permet d’accéder à un sandbox de production et de créer des **sandbox** de non production. Les sandbox hors production sont une forme de virtualisation des données qui vous permet d&#39;isoler les données des autres sandbox et sont généralement utilisés pour des expériences de développement, des tests ou des essais. Les **autorisations** d’un profil de produits donnent aux utilisateurs du profil l’accès aux fonctionnalités Platform dans les environnements sandbox auxquels ils ont accès.

Pour plus d&#39;informations sur les sandbox dans l&#39;Experience Platform, consultez la présentation [des](../sandboxes/home.md)sandbox.

### Accès aux sandbox

L’accès aux sandbox est géré par le biais des profils de produits. Pour obtenir des instructions détaillées sur la façon d’activer l’accès à un sandbox pour un profil de produits, consultez le guide [d’utilisation du](./ui/overview.md)contrôle d&#39;accès.

Les utilisateurs peuvent accéder à un ou plusieurs sandbox dans un profil de produits. Si un utilisateur est inclus dans deux ou plusieurs profils de produits, il aura accès à tous les sandbox inclus dans ces profils.

L’autorisation &quot;Gestion des sandbox&quot; permet aux utilisateurs de gérer, de vue ou de réinitialiser des sandbox.

### Autorisations

L’onglet **Autorisations** d’un profil de produit affiche les sandbox et les autorisations qui sont actifs pour ce profil :

![](./images/permissions-overview.png)

Les autorisations octroyées par l’intermédiaire de l’Admin Console sont triées par catégorie, certaines autorisations permettant d’accéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour les Experience Platform dans l’Admin Console, avec des descriptions des fonctionnalités Platform spécifiques auxquelles ils accordent l’accès. Pour obtenir des instructions détaillées sur l’ajout d’autorisations à un profil de produits, consultez le guide [d’utilisation du](./ui/overview.md)contrôle d&#39;accès.

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| Modélisation des données | Gérer les Schémas | Accès à la lecture, à la création, à la modification et à la suppression de schémas et de ressources connexes. |
| Modélisation des données | Afficher schémas | Accès en lecture seule aux schémas et aux ressources connexes. |
| Data Management | Gérer les jeux de données | Accès à la lecture, à la création, à la modification et à la suppression de jeux de données. Accès en lecture seule pour les schémas. |
| Data Management | Afficher jeux de données | Accès en lecture seule pour les jeux de données et les schémas. |
| Data Management | Surveillance des données | Accès en lecture seule aux jeux de données et aux flux de surveillance. |
| Gestion des Profils | Gestion des profils | Accès à la lecture, à la création, à la modification et à la suppression des jeux de données utilisés pour les profils client. Accès en lecture seule aux profils disponibles. |
| Gestion des Profils | Profils de Vue | Accès en lecture seule aux profils disponibles. |
| Gestion des Profils | Exporter une Audience pour un segment | Possibilité d’exporter un segment d’audience évalué vers un jeu de données. |
| Identités | Gérer les Espaces de nommage d’identité | Accès à la lecture, à la création, à la modification et à la suppression d&#39;espaces de nommage d&#39;identité. |
| Identités | Espaces de nommage d&#39;identité Vue | Accès en lecture seule pour les espaces de nommage d&#39;identité. |
| Administration de Sandbox | Gérer les sandbox | Accès à la lecture, à la création, à la modification et à la suppression des sandbox. |
| Administration de Sandbox | Afficher les sandbox | Accès en lecture seule pour les sandbox appartenant à votre organisation. |
| Administration de Sandbox | Réinitialiser un sandbox | Possibilité de réinitialiser un sandbox. |
| Destinations | Gérer les destinations | Accès à des destinations de lecture, de création, de modification et de désactivation.* |
| Destinations | Destinations des Vues | Accès en lecture seule aux destinations disponibles dans l&#39;onglet *Catalogue* et aux destinations authentifiées dans l&#39;onglet *Parcourir* .* |
| Destinations | Activer les destinations | Possibilité d’activer les données vers les destinations actives qui ont été créées. Cette autorisation requiert que &quot;Destinations de Vue&quot; ou &quot;Gérer les Destinations&quot; soit accordée à l’utilisateur qui activera les destinations.* |
| Incorporation de données | Gérer les sources | Accès à des sources lues, créées, modifiées et désactivées. |
| Incorporation de données | Sources de Vue | Accès en lecture seule aux sources disponibles dans l’onglet *Catalogue* et aux sources authentifiées dans l’onglet *Parcourir* . |
| Espace de travail Data Science | Gérer l’espace de travail Data Science | Accès à la lecture, à la création, à la modification et à la suppression dans Data Science Workspace. |

_(*) Cette autorisation requiert des dispositions pour Platform de données client en temps réel. Pour plus d&#39;informations sur le CDP en temps réel, veuillez commencer par lire la présentation[du CDP en temps](https://docs.adobe.com/content/help/fr-FR/experience-platform/rtcdp/overview.html)réel._

## Étapes suivantes

En lisant ce guide, vous avez été familiarisé avec les principaux principes de l&#39;contrôle d&#39;accès en Experience Platform. Vous pouvez maintenant consulter le guide [d’utilisation du](./ui/overview.md) contrôle d&#39;accès pour obtenir des instructions détaillées sur l’utilisation de l’Admin Console pour créer des profils de produits et attribuer des autorisations pour Platform.