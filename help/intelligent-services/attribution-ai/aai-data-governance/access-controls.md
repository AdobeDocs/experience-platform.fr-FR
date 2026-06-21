---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Contrôle d’accès pour Attribution AI
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs pour Attribution AI.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
TQID: https://experienceleague.adobe.com/EBwNWb-jybovAgSyrBCxIGgrovs8roXij-sgP2ZqpME
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebfid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: a16ec9c0-4484-4842-b9a0-5504cde38e6aid: a9b953c0-98db-499b-97f5-a0dc3290bda3id: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d175cb4c-5781-454e-a826-bf6dff786265
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 502
ht-degree: 74%

---

# Contrôle d’accès dans Attribution AI

Le contrôle d’accès pour Attribution AI est fourni via Adobe Experience Platform dans l’[Adobe Admin Console](https://adminconsole.adobe.com/). Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.

Pour plus d’informations sur le contrôle d’accès, consultez la [présentation du contrôle d’accès](../../../access-control/home.md).

## Contrôle d’accès basé sur les attributs

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée uniquement.

[Le contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs et administratrices de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des politiques d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma d’un modèle de données d’expérience (XDM) avec des libellés définissant l’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD) et aux informations d’identification personnelle (PII) sur l’ensemble des workflows et ressources d’Experience Platform. Les administrateurs et administratrices peuvent définir des rôles d’utilisation qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

En raison du contrôle d’accès basé sur les attributs, certains champs et certaines fonctionnalités peuvent avoir un accès limité et ne pas être disponibles pour certains modèles de service Attribution AI. Par exemple, « Identité », « Définition de score » et « Clone ».

En haut de la **page Insights** dans l’espace de travail d’Attribution AI, les détails affichés dans la barre latérale ont un accès restreint.

![L’espace de travail d’Attribution AI avec les champs de schéma restreints mis en surbrillance.](../images/user-guide/access-restricted.png)

Si vous sélectionnez des jeux de données avec des schémas restreints sur la page **[!UICONTROL Créer un workflow de modèle]**, un signe d’avertissement s’affiche à côté du nom du jeu de données avec le message : [!UICONTROL Les informations restreintes sont exclues].

![L’espace de travail d’Attribution AI avec les champs de jeu de données restreints mis en surbrillance.](../images/user-guide/restricted-info-excluded.png)

Lorsque vous prévisualisez des jeux de données avec un schéma limité sur la page **[!UICONTROL Créer un workflow de modèle]**, un avertissement s’affiche pour vous informer qu’[!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans l’aperçu du jeu de données.]

![L’espace de travail d’Attribution AI avec les résultats des champs de schéma prévisualisés restreints mis en surbrillance.](../images/user-guide/restricted-dataset-preview.png)

Après avoir créé un modèle contenant des informations restreintes, passez à l’étape **[!UICONTROL Définir un objectif]**, un avertissement s’affiche en haut de l’écran : [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans la configuration.]

![L’espace de travail d’Attribution AI avec les champs restreints des résultats du modèle mis en surbrillance.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](../overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Experience Platform].
