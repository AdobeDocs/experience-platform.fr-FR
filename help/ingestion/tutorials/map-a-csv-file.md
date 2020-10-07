---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mappage d’un fichier CSV à un schéma XDM
topic: tutorial
type: Tutorial
description: Ce didacticiel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 28%

---


# Mappage d’un fichier CSV à un schéma XDM

In order to ingest CSV data into [!DNL Adobe Experience Platform], the data must be mapped to an [!DNL Experience Data Model] (XDM) schema. This tutorial covers how to map a CSV file to an XDM schema using the [!DNL Platform] user interface.

En outre, l’annexe du présent tutoriel fournit des informations supplémentaires sur l’utilisation des [fonctions de mappage](#mapping-functions).

## Prise en main

This tutorial requires a working understanding of the following components of [!DNL Platform]:

- [[ ! Modèle de données d’expérience DNL (système XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.
- [[ ! Apport du lot DNL]](../batch-ingestion/overview.md): Méthode par laquelle [!DNL Platform] ingère les données des fichiers de données fournis par l’utilisateur.

Vous devez également avoir créé un jeu de données dans lequel ingérer vos données CSV pour suivre ce tutoriel. Pour connaître les étapes de création d’un jeu de données dans l’interface utilisateur, consultez le [tutoriel sur l’ingestion de données](./ingest-batch-data.md).

## Choix d’une destination

Connectez-vous à [[ !DNL Adobe Experience Platform]](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Workflows]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Workflows]** .

Dans l’écran **[!UICONTROL Workflows]** , sélectionnez **[!UICONTROL Mapper le fichier CSV au schéma]** XDM sous la section d’assimilation **[!UICONTROL des]** données, puis sélectionnez **[!UICONTROL Lancement.]**

![](../images/tutorials/map-a-csv-file/workflows.png)

The **[!UICONTROL Map CSV to XDM schema]** workflow appears, starting on the **[!UICONTROL Destination]** step. Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

**Utilisation d’un jeu de données existant**

Pour importer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Utiliser un jeu de données]** existant. Vous pouvez récupérer un jeu de données existant à l&#39;aide de la fonction de recherche ou en faisant défiler la liste des jeux de données existants dans le panneau.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Pour intégrer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Créer un nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Sélectionnez un schéma en utilisant la fonction de recherche ou en faisant défiler la liste des schémas fournis. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Ajout de données

L’étape **[!UICONTROL Ajouter les données]** apparaît. Faites glisser votre fichier CSV dans l’espace prévu à cet effet ou sélectionnez **[!UICONTROL Choisir les fichiers]** pour entrer manuellement votre fichier CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

The **[!UICONTROL Sample data]** section appears once the file is uploaded, showing the first ten rows of data. Once you have confirmed that the data has uploaded as expected, select **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappage des champs CSV aux champs de schéma XDM

L’étape **[!UICONTROL Mappage]** apparaît. Les colonnes du fichier CSV sont répertoriées sous **[!UICONTROL Champ source]**, et les champs de schéma XDM correspondants sont répertoriés sous **[!UICONTROL Champ cible]**. Les champs cibles non sélectionnés sont indiqués en rouge. Vous pouvez utiliser l’option de filtre de champs pour restreindre la liste des champs source disponibles.

>[!TIP]
>
>[!DNL Platform] fournit des recommandations intelligentes pour les champs à mappage automatique en fonction du schéma de cible ou du jeu de données que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

Pour mapper une colonne CSV à un champ XDM, sélectionnez l’icône de schéma en regard du champ de cible correspondant à la colonne.

![](../images/tutorials/map-a-csv-file/mapping.png)

La fenêtre **[!UICONTROL Sélectionner un champ de schéma]** apparaît. Ici, vous pouvez parcourir la structure du schéma XDM et localiser le champ vers lequel vous souhaitez mapper la colonne CSV. Cliquez sur un champ XDM pour le sélectionner, puis sur **[!UICONTROL Sélectionner]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Une fois que vous avez terminé les étapes pour les champs source non mappés restants, l’écran **[!UICONTROL Mappage]** s’affiche de nouveau avec le champ XDM sélectionné qui s’affiche désormais sous Champ **[!UICONTROL de]** Cible.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Lors du mappage des champs, vous pouvez également inclure des fonctions pour calculer les valeurs en fonction des champs sources d’entrée. Pour plus d’informations, consultez la section relative aux [fonctions de mappage](#mapping-functions) de l’annexe.

### Ajouter le champ calculé

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être attribuées à des attributs dans le schéma de cible et recevoir un nom et une description pour faciliter la référence.

Sélectionnez le bouton **[!UICONTROL Ajouter le champ]** calculé pour continuer.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

Le panneau **[!UICONTROL Créer un champ]** calculé s’affiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez l’un des onglets à début pour ajouter des fonctions, des champs ou des opérateurs à l’éditeur d’expressions.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulation | Description |
| --------- | ----------- |
| Champs | L’onglet Champs liste les champs et les attributs disponibles dans le schéma source. |
| Fonctions | L&#39;onglet Fonctions liste les fonctions disponibles pour transformer les données. |
| Opérateurs | L’onglet opérateurs liste les opérateurs disponibles pour transformer les données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à l’aide de l’éditeur d’expressions situé au centre. Sélectionnez l’éditeur à début de la création d’une expression.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

L’écran de mappage s’affiche à nouveau avec votre nouveau champ source. Appliquez le champ de cible approprié et sélectionnez **[!UICONTROL Terminer]** pour terminer le mappage.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Surveiller votre flux de données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d’informations sur la surveillance des flux de données, voir le didacticiel sur la [surveillance des flux](../../ingestion/quality/monitor-data-flows.md)de données en flux continu.

## Utilisation des fonctions de mappage

Pour utiliser une fonction, saisissez-la sous **[!UICONTROL Champ source]** avec la syntaxe et les entrées appropriées.

Par exemple, pour concaténer les champs CSV city et country et les attribuer au champ XDM city, définissez le champ source en tant que `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Pour en savoir plus sur le mappage des colonnes aux champs XDM, consultez le guide sur l’ [utilisation des fonctions](../../data-prep/functions.md)d’aperçu des données (Mapper).

## Étapes suivantes

En suivant ce tutoriel, vous avez mappé un fichier CSV plat à un schéma XDM et l’avez ingéré dans [!DNL Platform]. This data can now be used by downstream [!DNL Platform] services such as [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la présentation du Profil client [[ !DNL en temps réel]](../../profile/home.md) .
