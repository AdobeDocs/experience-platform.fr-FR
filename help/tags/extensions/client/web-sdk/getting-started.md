---
title: Prise en main de l’extension de balises Web SDK
description: Envoyez des données d’événement à Adobe Experience Platform Edge Network à l’aide de l’extension de balise Web SDK.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 5%

---

# Prise en main de l’extension de balises Web SDK

Utilisez Adobe Experience Platform **balises** (anciennement Launch) pour envoyer des données d’événement de votre site web aux solutions Edge Network et Adobe en aval.

Avant de suivre ces étapes, vérifiez que vous pouvez accéder aux [droits de propriété](/help/tags/ui/administration/user-permissions.md) suivants :

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Assurez-vous également de disposer de toutes les [autorisations](/help/access-control/home.md#permissions) dans les catégories suivantes :

* Modélisation des données
* Identités

## Créer un schéma XDM {#schema}

Le [modèle de données d’expérience (XDM)](/help/xdm/home.md) est une spécification open source qui fournit des structures et des définitions communes pour les données sous la forme de schémas. La configuration d’un schéma est vivement recommandée lors de l’envoi de données à Edge Network.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Sélectionnez **[!UICONTROL Create schema]**.
1. Sélectionnez **[!UICONTROL Experience Event]**, puis sélectionnez **[!UICONTROL Next]**.
1. Attribuez un nom au schéma, puis sélectionnez **[!UICONTROL Finish]**.
1. (Facultatif) Vous pouvez ajouter d’autres champs ou [groupes de champs](/help/xdm/ui/resources/field-groups.md) pour toutes les données supplémentaires que vous souhaitez collecter.

![Zone de travail des schémas](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>Une fois enregistrés, les schémas n’autorisent que des modifications *additifs*. Voir [évolution des schémas](/help/xdm/schema/composition.md#evolution) pour plus d’informations.

## Création dʼun flux de données {#datastream}

Un [flux de données](/help/datastreams/overview.md) est une configuration qui indique à Edge Network comment gérer les données que vous lui envoyez. Lorsque vous configurez un flux de données pour envoyer des données à un produit donné, le flux de données transmet automatiquement les données pertinentes à chaque produit respectif d’une manière que le produit spécifique comprend.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Sélectionnez **[!UICONTROL New datastream]**.
1. Attribuez le nom souhaité au flux de données, puis sélectionnez le schéma récemment créé sous **[!UICONTROL Mapping schema]**.
1. Sélectionnez **[!UICONTROL Save]**.

![Liste des flux de données](assets/getting-started/datastreams.png)

## Création d’une propriété de balise

Une fois que vous avez créé un schéma et un flux de données, vous pouvez créer et configurer une propriété de balise.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez **[!UICONTROL New property]**.
1. Attribuez un nom et un domaine à la propriété de balise, puis sélectionnez **[!UICONTROL Save]**.

## Installation de l’extension de balise

L’extension de balise Web SDK est installée sur une propriété de balise donnée.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Sélectionnez l’onglet **[!UICONTROL Catalog]** .
1. Utilisez la recherche pour localiser l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Sélectionnez la carte d’extension, puis sélectionnez **[!UICONTROL Install]** à droite.

![Installer SDK](assets/getting-started/install-sdk.png)

## Configuration de l’extension de balise

Lorsque vous installez l’extension de balise Web SDK, vous accédez automatiquement à la page [Configuration](configure/config-overview.md).

1. Sous la section [Flux de données](configure/datastreams.md), sélectionnez le flux de données de votre choix pour chaque environnement.

Tous les autres paramètres de configuration sont renseignés pour vous ou facultatifs. Définissez les paramètres de configuration souhaités, puis sélectionnez **[!UICONTROL Save]**.

## Créer un élément de données variable

Adobe recommande d’utiliser des éléments de données [Variable](data-element-types.md#variable) pour stocker la payload que vous souhaitez envoyer à Adobe. Les objets XDM sont également des éléments de données disponibles, mais ils sont plus anciens et plus limités dans les cas d’utilisation applicables.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Sélectionnez **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**.
1. Attribuez à l’élément de données les propriétés suivantes sur la gauche :
   * **[!UICONTROL Name]** : tout nom souhaité
   * **[!UICONTROL Extension]** : [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]** : [!UICONTROL Variable]
1. Définissez les propriétés suivantes sur la droite :
   **Type de variable** : XDM
   **[!UICONTROL Sandbox]** : sandbox dans lequel vous avez créé votre schéma
   **[!UICONTROL Schema]** : schéma souhaité
1. Sélectionnez **[!UICONTROL Save]**.

## Créer une règle

Les règles déterminent à quel moment déclencher quelque chose ou définir des variables. La création d’une règle qui s’exécute chaque fois que la bibliothèque est chargée vous permet de renseigner facilement les variables que vous souhaitez voir contenir une valeur sur chaque page.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Sélectionnez **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**.
1. Donnez un nom à la règle.
1. Sélectionnez l’icône « `+` » en regard de **[!UICONTROL Events]**.
1. Attribuez à l’événement les paramètres suivants :
   * **[!UICONTROL Extension]** : [!UICONTROL Core]
   * **[!UICONTROL Event type]** : [!UICONTROL Library loaded (page top)]
1. Sélectionnez **[!UICONTROL Keep changes]**.

Les étapes ci-dessus établissent la partie critères de la règle, qui doit se déclencher une fois la bibliothèque chargée. Les étapes suivantes définissent l’action à entreprendre lorsque ce critère est rempli.

1. Sélectionnez l’icône « `+` » en regard de **[!UICONTROL Actions]**.
1. Définissez l’action sur les paramètres suivants à gauche :
   * **[!UICONTROL Extension]** : [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]** : [!UICONTROL Send event]
1. Définissez les champs suivants sur la droite :
   * **[!UICONTROL XDM]** : élément de données de la variable XDM
1. Sélectionnez **[!UICONTROL Keep changes]**.

![Configuration de l’action](assets/getting-started/action-config.png)

## Publier

La propriété de balise contient tous les composants nécessaires pour envoyer des données à Edge Network.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Sélectionnez **[!UICONTROL Add library]**.
1. Attribuez un nom à la bibliothèque. Ce nom doit être similaire à un nom de validation lorsque vous utilisez un logiciel de contrôle de version.
1. Définissez le menu déroulant de l’environnement sur **[!UICONTROL Development]**.
1. Sélectionnez **[!UICONTROL Add all changed resources]**.
1. Sélectionnez **[!UICONTROL Save & build to Development]**.

Vos modifications sont maintenant déployées dans votre environnement de développement.

1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Sélectionnez l’icône d’installation en regard de l’environnement de développement
1. Installez le code incorporé dans une page web de test sur votre site.

Une fois que vous avez vérifié que la balise fonctionne dans votre environnement de développement, vous pouvez utiliser l’interface [!UICONTROL Publishing flow] pour publier la bibliothèque vers l’environnement d’évaluation, puis éventuellement vers l’environnement de production.

1. Ajoutez l’extension et la règle à une **bibliothèque**, créez-les dans un **environnement** et installez le code incorporé sur votre site.
2. Validez avec **Adobe Experience Platform Debugger**.

Vous disposez désormais d’une configuration allégée qui capture les événements et les envoie à Edge Network. Vous pouvez désormais développer davantage votre implémentation en ajoutant des champs à votre schéma, en ajoutant des produits à un flux de données ou en ajoutant des éléments de données à votre propriété de balise.
