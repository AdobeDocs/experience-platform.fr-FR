---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Contrôle d’accès pour Attribution AI
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs pour Attribution AI.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 43%

---


# Contrôle d’accès

Le contrôle d’accès d’Attribution AI est fourni via Adobe Experience Platform dans la variable [Adobe Admin Console](https://adminconsole.adobe.com/). Cette fonctionnalité exploite les profils de produit dans Admin Console, liant les utilisateurs à des autorisations et des sandbox.

Pour plus d’informations sur le contrôle d’accès, consultez la [présentation du contrôle d’accès](../../access-control/home).

## Contrôle d’accès basé sur les attributs

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée uniquement.

[Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.](../../../help/access-control/abac/overview.md) Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma d’un modèle de données d’expérience (XDM) avec des libellés définissant l’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD) et aux informations d’identification personnelle (PII) sur l’ensemble des workflows et ressources de Platform. Les administrateurs peuvent définir des rôles utilisateur ayant accès uniquement à des champs et données spécifiques qui correspondent à ces champs.

En raison du contrôle d’accès basé sur les attributs, certains champs et certaines fonctionnalités peuvent avoir un accès limité et ne pas être disponibles pour certains modèles de service Attribution AI. Par exemple, &quot;Identité&quot;, &quot;Définition de score&quot; et &quot;Cloner&quot;.

En haut de l’espace de travail Attribution AI **page insights**, les détails affichés dans la barre latérale ont un accès restreint.

![Espace de travail Attribution AI avec les champs de schéma restreints mis en surbrillance.](./images/user-guide/access-restricted.png)

Si vous sélectionnez des jeux de données avec des schémas restreints sur la variable **[!UICONTROL Workflow Créer un modèle]** , un signe d’avertissement s’affiche en regard du nom du jeu de données avec le message : [!UICONTROL Les informations restreintes sont exclues].

![Espace de travail Attribution AI avec les champs de jeu de données restreint mis en surbrillance.](./images/user-guide/restricted-info-excluded.png)

Lorsque vous prévisualisez des jeux de données avec un schéma limité sur l’objet **[!UICONTROL Workflow Créer un modèle]** , un avertissement s’affiche pour vous informer que [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans l’aperçu du jeu de données.]

![Espace de travail Attribution AI avec les résultats des champs de schéma prévisualisés restreints mis en surbrillance.](./images/user-guide/restricted-dataset-preview.png)

Après avoir créé un modèle contenant des informations restreintes, passez à la **[!UICONTROL Définition d’un objectif]** , un avertissement s’affiche en haut de l’écran : [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans la configuration.]

![Espace de travail Attribution AI avec les champs restreints des résultats du modèle mis en surbrillance.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](./ui/overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Platform].
