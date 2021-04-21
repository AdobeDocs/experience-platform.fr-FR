---
keywords: Experience Platform ; accueil ; rubriques populaires ; mapper csv ; mapper le fichier csv ; mapper le fichier csv à xdm ; mapper csv à xdm ; ui guide ;
solution: Experience Platform
title: Mappage d’un fichier CSV à un Schéma XDM
topic-legacy: tutorial
type: Tutorial
description: Ce didacticiel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 16%

---

# Mappage d’un fichier CSV à un schéma XDM

Pour importer des données CSV dans [!DNL Adobe Experience Platform], les données doivent être mises en correspondance avec un schéma [!DNL Experience Data Model] (XDM). Ce didacticiel explique comment mapper un fichier CSV à un schéma XDM à l’aide de l’interface utilisateur [!DNL Platform].

En outre, l’annexe du présent tutoriel fournit des informations supplémentaires sur l’utilisation des [fonctions de mappage](#mapping-functions).

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de [!DNL Platform] :

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): Méthode par laquelle  [!DNL Platform] ingère des données à partir de fichiers de données fournis par l’utilisateur.

Vous devez également avoir créé un jeu de données dans lequel ingérer vos données CSV pour suivre ce tutoriel. Pour connaître les étapes de création d’un jeu de données dans l’interface utilisateur, consultez le [tutoriel sur l’ingestion de données](./ingest-batch-data.md).

## Choix d’une destination

Connectez-vous à [[!DNL Adobe Experience Platform]](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Workflows]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Workflows]**.

Dans l’écran **[!UICONTROL Workflows]**, sélectionnez **[!UICONTROL Faire correspondre le fichier CSV au schéma XDM]** sous la section **[!UICONTROL Importation de données]**, puis sélectionnez **[!UICONTROL Lancer]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Le flux de travaux **[!UICONTROL Faire correspondre le fichier CSV au schéma XDM]** s’affiche, en commençant par l’étape **[!UICONTROL Destination]**. Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez soit utiliser un jeu de données existant, soit en créer un nouveau.

**Utilisation d’un jeu de données existant**

Pour importer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Utiliser un jeu de données existant]**. Vous pouvez récupérer un jeu de données existant à l&#39;aide de la fonction de recherche ou en faisant défiler la liste des jeux de données existants dans le panneau.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Pour importer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Créer un nouveau jeu de données]** et entrez un nom et une description pour le jeu de données dans les champs fournis. Sélectionnez un schéma en utilisant la fonction de recherche ou en faisant défiler la liste des schémas fournis. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Ajout de données

L’étape **[!UICONTROL Ajouter les données]** apparaît. Faites glisser votre fichier CSV dans l’espace prévu à cet effet ou sélectionnez **[!UICONTROL Choisir les fichiers]** pour saisir manuellement votre fichier CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

La section **[!UICONTROL Exemple de données]** s’affiche une fois le fichier téléchargé et affiche les dix premières lignes de données. Une fois que vous avez confirmé que les données ont été téléchargées comme prévu, sélectionnez **[!UICONTROL Suivant]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mappage des champs CSV aux champs de schéma XDM

L’étape **[!UICONTROL Mappage]** apparaît. Les colonnes du fichier CSV sont répertoriées sous **[!UICONTROL Champ source]**, et les champs de schéma XDM correspondants sont répertoriés sous **[!UICONTROL Champ cible]**.

[!DNL Platform] fournit automatiquement des recommandations intelligentes pour les champs à mappage automatique en fonction du schéma de cible ou du jeu de données que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Pour accepter toutes les valeurs de mappage générées automatiquement, cochez la case &quot;[!UICONTROL Accepter tous les champs de cible]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Il arrive que plusieurs recommandations soient disponibles pour le schéma source. Dans ce cas, la carte de mappage affiche la recommandation la plus visible, suivie d’un cercle bleu contenant le nombre de recommandations supplémentaires disponibles. La sélection de l&#39;icône représentant une ampoule affiche la liste des recommandations supplémentaires. Vous pouvez choisir l’une des autres recommandations en cochant la case en regard de la recommandation à laquelle vous souhaitez mapper.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Vous pouvez également choisir de mapper manuellement votre schéma source à votre schéma de cible. Passez la souris sur le schéma source à mapper, puis sélectionnez l’icône Plus.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

La fenêtre contextuelle **[!UICONTROL Associer la source au champ de cible]** s’affiche. A partir de là, vous pouvez sélectionner le champ à mapper, suivi de **[!UICONTROL Enregistrer]** pour ajouter votre nouveau mappage.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Si vous souhaitez supprimer l’un des mappages, passez la souris sur ce mappage, puis sélectionnez l’icône Moins.

### Ajouter le champ calculé

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être attribuées à des attributs dans le schéma de cible et recevoir un nom et une description pour faciliter la référence.

Sélectionnez le bouton **[!UICONTROL Ajouter le champ calculé]** pour continuer.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ calculé]** apparaît. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez l’un des onglets à début pour ajouter des fonctions, des champs ou des opérateurs à l’éditeur d’expressions.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulation | Description |
| --------- | ----------- |
| Champs | L’onglet Champs liste les champs et les attributs disponibles dans le schéma source. |
| Fonctions | L&#39;onglet Fonctions liste les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide [à l&#39;aide des fonctions d&#39;aperçu des données (Mapper)](../../data-prep/functions.md). |
| Opérateurs | L’onglet opérateurs liste les opérateurs disponibles pour transformer les données. |

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à l’aide de l’éditeur d’expressions situé au centre. Sélectionnez l’éditeur à début de la création d’une expression.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

L’écran de mappage s’affiche à nouveau avec votre nouveau champ source. Appliquez le champ de cible correspondant approprié et sélectionnez **[!UICONTROL Terminer]** pour terminer le mappage.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Surveillance de l’ingestion des données

Une fois votre fichier CSV mappé et créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d&#39;informations sur la surveillance de l&#39;assimilation des données, consultez le didacticiel [surveillance de l&#39;assimilation des données](../../ingestion/quality/monitor-data-ingestion.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez mappé un fichier CSV plat à un schéma XDM et l’avez ingéré dans [!DNL Platform]. Ces données peuvent désormais être utilisées par des services [!DNL Platform] en aval tels que [!DNL Real-time Customer Profile]. Pour plus d&#39;informations, consultez l&#39;aperçu de [[!DNL Real-time Customer Profile]](../../profile/home.md).
