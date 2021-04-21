---
keywords: Experience Platform ; accueil ; rubriques populaires ; contrôle d'accès ; adobe admin Console
solution: Experience Platform
topic-legacy: overview
title: Présentation du contrôle d’accès
description: Le contrôle d'accès de Adobe Experience Platform est fourni par l'intermédiaire du Adobe Admin Console. Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des environnements de test.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 53%

---

# Présentation du contrôle d’accès

Le contrôle d&#39;accès de [!DNL Experience Platform] est fourni par le biais du [Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité exploite les profils de produits dans [!DNL Admin Console], qui lient les utilisateurs avec des autorisations et des sandbox.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle d&#39;accès pour [!DNL Experience Platform], vous devez disposer des droits d&#39;administrateur pour une organisation qui dispose d&#39;une intégration de produit [!DNL Experience Platform]. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un administrateur de profils de produit. Les autres rôles d’administrateur qui peuvent gérer des autorisations sont les administrateurs de produit (qui peuvent gérer tous les profils au sein d’un produit) et les administrateurs système (aucune restriction). Pour en savoir plus, consultez l’article d’Adobe Help Center sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de là, toute mention du terme « administrateur » dans ce document désigne un administrateur de profils de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après l’octroi de la licence de Adobe Experience Platform ou d’un service d’application/d’application utilisant l’Experience Platform, un courrier électronique est envoyé à l’administrateur spécifié lors de l’octroi de la licence.
- L’administrateur se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page d’aperçu.
- L’administrateur peut afficher les [profils de produit](#product-profiles) par défaut ou créer de nouveaux profils de produit clients si nécessaire.
- L’administrateur peut modifier les autorisations et les utilisateurs pour tout profil de produit existant.
- Lors de la création ou de la modification d&#39;un profil de produits, l&#39;administrateur ajoute des utilisateurs au profil à l&#39;aide de l&#39;onglet **[!UICONTROL users]** et leur accorde des autorisations (telles que &quot;[!UICONTROL Lire les jeux de données]&quot; ou &quot;[!UICONTROL Gérer les Schémas]&quot;) en accédant à l&#39;onglet **[!UICONTROL .]** De même, l’administrateur peut attribuer des accès aux environnements de test à l’aide du même onglet Autorisations.
- Lorsque les utilisateurs se connectent à l&#39;interface utilisateur [!DNL Experience Platform], leur accès aux fonctionnalités [!DNL Platform] est déterminé par les autorisations qui leur ont été accordées à partir de l&#39;étape 2. Par exemple, si un utilisateur ne dispose pas de l&#39;autorisation &quot;[!UICONTROL Vue Datasets]&quot;, l&#39;onglet **[!UICONTROL Datasets]** du menu latéral ne sera pas visible pour cet utilisateur.

Pour obtenir des instructions plus détaillées sur la gestion du contrôle d&#39;accès dans [!DNL Experience Platform], consultez le [Guide de l&#39;utilisateur du contrôle d&#39;accès](./ui/overview.md).

Tous les appels aux API [!DNL Experience Platform] sont validés pour les autorisations et renvoient des erreurs si les autorisations appropriées ne sont pas trouvées dans le contexte utilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Adobe Admin Console

Adobe Admin Console permet de centraliser la gestion des droits et accès de vos produits Adobe pour votre organisation. Grâce à la console, vous pouvez accorder à des groupes d’utilisateurs des autorisations d’accès pour diverses fonctionnalités [!DNL Platform], telles que &quot;[!UICONTROL Gérer les jeux de données]&quot;, &quot;[!UICONTROL jeux de données de Vue]&quot; ou &quot;[!UICONTROL Gérer les Profils]&quot;.

### Profils de produit

Dans le [!DNL Admin Console], des autorisations sont attribuées aux utilisateurs par le biais de profils de produits. Les profils de produit vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs, mais aussi de contenir leur accès aux environnements de test qui leur sont attribués par le biais des profils de produit. Il est possible d’attribuer un ou plusieurs profils de produit appartenant à votre organisation.

### Profils de produit par défaut

[!DNL Experience Platform] est fourni avec deux profils de produits par défaut préconfigurés. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, l’environnement de test auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein de l’environnement de test.

| Profil de produit | Accès aux environnements de test | Autorisations |
| --- | --- | --- |
| Accès complet par défaut à la production | Production | Toutes les autorisations applicables à [!DNL Experience Platform], à l’exception des autorisations d’administration Sandbox. |
| Administrateurs de sandbox | N/A | Fournit un accès uniquement aux autorisations Sandbox Administration. |

## Environnements de test et autorisations

Les environnements de test hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres environnements de test et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations d&#39;un profil de produits permettent aux utilisateurs du profil d&#39;accéder aux fonctionnalités [!DNL Platform] des environnements sandbox auxquels ils ont accès. Une licence d’Experience Platform par défaut vous accorde cinq sandbox (une production et quatre non-production). Vous pouvez ajouter des packs de dix sandbox hors production jusqu’à un maximum de 75 sandbox au total. Veuillez contacter votre administrateur d&#39;entreprise IMS ou votre représentant commercial d&#39;Adobe pour plus de détails.

Pour plus d&#39;informations sur les sandbox dans [!DNL Experience Platform], consultez l&#39;[aperçu des sandbox](../sandboxes/home.md).

### Accès aux environnements de test

L’accès aux environnements de test est géré par l’intermédiaire des profils de produit. Pour obtenir des instructions détaillées sur la manière dont activer l’accès à un environnement de test pour un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les utilisateurs peuvent se voir accorder l’accès à un ou plusieurs environnements de test au sein d’un profil de produit. Si un utilisateur fait partie de deux profils de produit ou plus, cet utilisateur aura accès à tous les environnements de test inclus dans ces profils.

L’autorisation « Gestion des environnements de test » permet aux utilisateurs de gérer, d’afficher ou de réinitialiser des environnements de test.

### Autorisations

L’onglet Autorisations au sein d’un profil de produit affiche les environnements de test et les autorisations actives pour ce profil :

![permissions-aperçu](./images/permissions-overview.png)

Les autorisations accordées par l&#39;intermédiaire de [!DNL Admin Console] sont triées par catégorie, certaines autorisations permettant d&#39;accéder à plusieurs fonctionnalités de bas niveau.

Le tableau suivant décrit les autorisations disponibles pour [!DNL Experience Platform] dans le [!DNL Admin Console], avec des descriptions des capacités [!DNL Platform] spécifiques auxquelles ils accordent l&#39;accès. Pour obtenir des instructions détaillées sur la manière dont ajouter des autorisations à un profil de produit, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès à la lecture, la création, la modification et la suppression des schémas et des ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Affichage des schémas] | Accès en lecture seule aux schémas et aux ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Gérer les relations] | Accès à la lecture, à la création, à la modification et à la suppression de relations de schéma. |
| [!DNL Data Modeling] | [!UICONTROL Gérer les métadonnées d’identité] | Accès à la lecture, à la création, à la modification et à la suppression des métadonnées d’identité pour les schémas. |
| [!DNL Data Management] | [!UICONTROL Gestion des jeux de données] | Accès à la lecture, la création, la modification et la suppression des jeux de données. Accès en lecture seule aux schémas. |
| [!DNL Data Management] | [!UICONTROL Affichage des jeux de données] | Accès en lecture seule aux jeux de données et aux schémas. |
| [!DNL Data Management] | [!UICONTROL Surveillance des données] | Accès en lecture seule à la surveillance des jeux de données et des flux. |
| [!DNL Profile Management] | [!UICONTROL Gestion des profils] | Accès à la lecture, la création, la modification et la suppression des jeux de données utilisés pour les profils de clients. Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Affichage des profils] | Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des segments] | Accès à la lecture, à la création, à la modification et à la suppression de segments. |
| [!DNL Profile Management] | [!UICONTROL Segments de vue] | Accès en lecture seule aux segments disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gérer les stratégies de fusion] | Accès à la lecture, à la création, à la modification et à la suppression des stratégies de fusion. |
| [!DNL Profile Management] | [!UICONTROL Stratégies de fusion de vues] | Accès en lecture seule aux stratégies de fusion disponibles. |
| [!DNL Profile Management] | [!UICONTROL Exportation de l’audience pour un segment] | Capacité à exporter un segment ciblé évalué vers un jeu de données. |
| [!DNL Profile Management] | [!UICONTROL Évaluer un segment sur une Audience] | Capacité à générer des profils pour une audience en évaluant une définition de segment. |
| [!DNL Identities] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identities] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des environnements de test] | Accès à la lecture, la création, la modification et la suppression des environnements de test. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des environnements de test] | Accès en lecture seule aux environnements de test appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un environnement de test] | Capacité à réinitialiser un environnement de test. |
| [!DNL Destinations] | [!UICONTROL Gestion des destinations] | Accès à la lecture, la création, la modification et la désactivation des destinations. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule aux destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Capacité à activer les données vers les destinations actives qui ont été créées. Cette autorisation requiert que &quot;Destinations de Vue&quot; ou &quot;Gérer [!UICONTROL Destinations&quot;] soit accordée à l&#39;utilisateur qui activera les destinations. |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de Data Science Workspace] | Accès à la lecture, à la création, à la modification et à la suppression dans [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Appliquer les étiquettes d’utilisation des données] | Accès à la lecture, à la création et à la suppression des étiquettes d’utilisation. |
| [!DNL Data Governance] | [!UICONTROL Gérer les stratégies d’utilisation des données] | Accès à la lecture, à la création, à la modification et à la suppression des stratégies d’utilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Stratégies d’utilisation des données de vue] | Accès en lecture seule pour les stratégies d’utilisation des données appartenant à votre organisation. |
| [!DNL Query Service] | [!UICONTROL Gérer les Requêtes] | Accès à la lecture, à la création, à la modification et à la suppression de requêtes SQL structurées pour les données de la plate-forme. |

## Étapes suivantes

En lisant ce guide, vous avez été familiarisé avec les principes principaux du contrôle d&#39;accès dans [!DNL Experience Platform]. Vous pouvez maintenant accéder au [guide de l&#39;utilisateur du contrôle d&#39;accès](./ui/overview.md) pour obtenir des instructions détaillées sur l&#39;utilisation de [!DNL Admin Console] pour créer des profils de produits et attribuer des autorisations pour [!DNL Platform].
