---
keywords: Experience Platform;accueil;rubriques les plus consultées;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de l’interface utilisateur ;
solution: Experience Platform
title: Mappage d’un fichier CSV à un schéma XDM
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 0e79d339ddc0301486ea3e53a3fd52877ff6a2c8
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 44%

---

# Mappage d’un fichier CSV à un schéma XDM

Pour ingérer des données CSV dans [!DNL Adobe Experience Platform], les données doivent être mappées à un [!DNL Experience Data Model] Schéma (XDM). Ce tutoriel explique comment mapper un fichier CSV à un schéma XDM à l’aide du [!DNL Platform] de l’interface utilisateur.

En outre, l’annexe du présent tutoriel fournit des informations supplémentaires sur l’utilisation des [fonctions de mappage](#mapping-functions).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): La méthode par laquelle [!DNL Platform] ingère des données à partir de fichiers de données fournis par l’utilisateur.

Vous devez également avoir créé un jeu de données dans lequel ingérer vos données CSV pour suivre ce tutoriel. Pour connaître les étapes de création d’un jeu de données dans l’interface utilisateur, consultez le [tutoriel sur l’ingestion de données](./ingest-batch-data.md).

## Choix d’une destination

Connectez-vous à [[!DNL Adobe Experience Platform]](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Workflows]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Workflows]** workspace.

Dans la **[!UICONTROL Workflows]** écran, sélectionnez **[!UICONTROL Mappage du fichier CSV au schéma XDM]** sous le **[!UICONTROL Ingestion des données]** , puis sélectionnez **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Le **[!UICONTROL Mappage du fichier CSV au schéma XDM]** s’affiche, en commençant par **[!UICONTROL Destination]** étape . Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

**Utiliser un jeu de données existant**

Pour ingérer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Utilisation d’un jeu de données existant]**. Vous pouvez récupérer un jeu de données existant à l’aide de la fonction de recherche ou en faisant défiler la liste des jeux de données existants dans le panneau.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Pour ingérer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Création d’un jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Sélectionnez un schéma à l’aide de la fonction de recherche ou en faisant défiler la liste des schémas fournis. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Ajout de données

L’étape **[!UICONTROL Ajouter les données]** apparaît. Faites glisser votre fichier CSV dans l’espace prévu à cet effet ou sélectionnez **[!UICONTROL Sélection de fichiers]** pour saisir manuellement votre fichier CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

Le **[!UICONTROL Exemples de données]** s’affiche une fois le fichier chargé, avec les dix premières lignes de données. Une fois que vous avez confirmé que les données ont été téléchargées comme prévu, sélectionnez **[!UICONTROL Suivant]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappage des champs CSV aux champs de schéma XDM

L’étape **[!UICONTROL Mappage]** apparaît. Les colonnes du fichier CSV sont répertoriées sous **[!UICONTROL Champ source]**, et les champs de schéma XDM correspondants sont répertoriés sous **[!UICONTROL Champ cible]**.

[!DNL Platform] fournit automatiquement des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Pour accepter toutes les valeurs de mappage qui génèrent automatiquement, cochez la case &quot;Identifier&quot;[!UICONTROL Accepter tous les champs cibles]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Parfois, plusieurs recommandations sont disponibles pour le schéma source. Dans ce cas, la carte de mappage affiche la recommandation la plus en évidence, suivie d’un cercle bleu contenant le nombre de recommandations supplémentaires disponibles. Si vous sélectionnez l’icône en forme d’ampoule, une liste des recommandations supplémentaires s’affiche. Vous pouvez choisir l’une des autres recommandations en cochant la case en regard de la recommandation que vous souhaitez mapper à la place.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Vous pouvez également choisir de mapper manuellement votre schéma source à votre schéma cible. Pointez sur le schéma source à mapper, puis sélectionnez l’icône plus.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Le **[!UICONTROL Associer la source au champ cible]** s’affiche. À partir de là, vous pouvez sélectionner le champ à mapper, suivi de **[!UICONTROL Enregistrer]** pour ajouter votre nouveau mappage.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Si vous souhaitez supprimer l’un des mappages, passez la souris sur ce mappage, puis sélectionnez l’icône moins.

### Ajouter un champ calculé {#add-calculated-field}

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible. Vous pouvez également leur fournir un nom et une description pour en faciliter la référence.

Sélectionnez la **[!UICONTROL Ajouter un champ calculé]** pour continuer.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ calculé]** sʼaffiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez lʼun des onglets pour commencer à ajouter des fonctions, des champs ou des opérateurs à lʼéditeur dʼexpression.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulation | Description |
| --------- | ----------- |
| Champs | Lʼonglet Champs répertorie les champs et attributs disponibles dans le schéma source. |
| Fonctions | Lʼonglet Fonctions répertorie les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide dʼ [utilisation des fonctions Data Prep (Mapper)](../../data-prep/functions.md). |
| Opérateurs | Lʼonglet Opérateurs répertorie les opérateurs disponibles pour la transformation des données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à lʼaide de lʼéditeur dʼexpression situé au centre. Sélectionnez lʼéditeur pour commencer à créer une expression.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

Lʼécran des mappings réapparaît avec le champ source que vous venez de créer. Appliquez le champ cible correspondant et sélectionnez **[!UICONTROL Terminer]** pour terminer le mapping.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Surveillance de l’ingestion des données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données ingérées par celui-ci. Pour plus d’informations sur la surveillance de l’ingestion des données, consultez le tutoriel sur [surveillance de l’ingestion des données](../../ingestion/quality/monitor-data-ingestion.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez mappé un fichier CSV plat à un schéma XDM et l’avez ingéré dans [!DNL Platform]. Ces données peuvent désormais être utilisées en aval. [!DNL Platform] des services tels que [!DNL Real-time Customer Profile]. Consultez la présentation pour [[!DNL Real-time Customer Profile]](../../profile/home.md) pour plus d’informations.
