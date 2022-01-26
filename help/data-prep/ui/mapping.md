---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
title: Guide de l’interface utilisateur de la préparation de données
description: Ce document fournit des instructions sur l’utilisation des fonctions de préparation de données dans l’interface utilisateur de Platform pour mapper des fichiers CSV à un schéma XDM.
source-git-commit: 4c2e3380881e6a032100ef00502b55112f3b103f
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 17%

---

# Guide de l’interface utilisateur de la préparation de données

Ce document fournit des instructions sur l’utilisation des fonctions de préparation de données dans l’interface utilisateur de Adobe Experience Platform pour mapper des fichiers CSV à un schéma XDM.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants Platform suivants :

* [[!DNL Experience Data Model (XDM)] Système](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [Identity Service](../../identity-service/home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sources](../../sources/home.md): Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.

## Détails du flux de données

>[!TIP]
>
>Vous pouvez accéder aux détails du flux de données en sélectionnant une source dans le catalogue de sources. Pour plus d’informations, voir [présentation des sources](../../sources/home.md).

Avant de pouvoir mapper vos données CSV à un schéma XDM, vous devez d’abord établir les détails de votre flux de données.

Le [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez ingérer vos données CSV dans un jeu de données cible existant ou un nouveau jeu de données cible. Un jeu de données existant est fourni avec un schéma cible prédéfini auquel mapper vos données, tandis qu’un nouveau jeu de données vous demande de sélectionner un schéma existant ou de créer un nouveau schéma vers lequel mapper vos données.

### Utilisation d’un jeu de données cible existant

Pour ingérer vos données CSV dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**. Vous pouvez récupérer un jeu de données existant à l’aide de la variable [!UICONTROL Recherche avancée] ou en faisant défiler la liste des jeux de données existants dans le menu déroulant.

Une fois qu’un jeu de données est sélectionné, attribuez un nom à votre flux de données et une description facultative.

Au cours de ce processus, vous pouvez également activer [!UICONTROL Diagnostics d’erreur] et [!UICONTROL Ingestion partielle]. [!UICONTROL Diagnostics d’erreur] permet la génération de messages d’erreur détaillés pour tout enregistrement erroné qui se produit dans votre flux de données, tandis que [!UICONTROL Ingestion partielle] vous permet d’ingérer des données contenant des erreurs, jusqu’à un certain seuil que vous définissez manuellement. Voir [Présentation de l’ingestion par lots partielle](../../ingestion/batch-ingestion/partial.md) pour plus d’informations.

![existing-dataset](../images/ui/mapping/existing-dataset.png)

### Utilisation d’un nouveau jeu de données cible

Pour ingérer vos données CSV dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** puis fournissez un nom de jeu de données de sortie et une description facultative. Sélectionnez ensuite un schéma à mapper à l’aide de la propriété [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant.

Une fois le schéma sélectionné, attribuez un nom à votre flux de données et une description facultative, puis appliquez la variable [!UICONTROL Diagnostics d’erreur] et [!UICONTROL Ingestion partielle] paramètres de votre flux de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![new-dataset](../images/ui/mapping/new-dataset.png)

## Sélectionner des données

Le [!UICONTROL Sélectionner des données] s’affiche, fournissant une interface pour télécharger vos fichiers locaux et prévisualiser leur structure et leur contenu. Sélectionner **[!UICONTROL Sélection de fichiers]** pour charger un fichier CSV à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier CSV que vous souhaitez transférer dans le [!UICONTROL Glisser-déposer des fichiers] du panneau.

>[!TIP]
>
>Seuls les fichiers CSV sont actuellement pris en charge par le téléchargement de fichiers local. La taille de fichier maximale pour chaque fichier est de 1 Go.

![choice-files](../images/ui/mapping/choose-files.png)

Une fois le fichier téléchargé, l’interface de prévisualisation se met à jour pour afficher le contenu et la structure du fichier.

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

Selon votre fichier, vous pouvez sélectionner un délimiteur de colonne (tabulations, virgules, barres verticales, ou un délimiteur de colonne personnalisé) pour vos données source. Sélectionnez la **[!UICONTROL Délimiteur]** Flèche de liste déroulante, puis sélectionnez le délimiteur approprié dans le menu.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![délimiteur](../images/ui/mapping/delimiter.png)

## Mappage

Le **[!UICONTROL mapping]** L’interface de propose un outil complet pour mapper les champs sources de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### Présentation de l’interface de mappage

L’interface de mappage comprend un tableau de bord qui fournit des informations sur l’intégrité de vos jeux de mappages dans le contexte du processus d’ingestion. Le tableau de bord affiche les détails suivants concernant vos jeux de mappages :

| Propriété | Description |
| --- | --- |
| [!UICONTROL Champs mappés] | Affiche le nombre total de champs source qui ont été mappés à un champ XDM cible, quelles que soient les erreurs. |
| [!UICONTROL Champs obligatoires] | Affiche le nombre de champs de mappage requis. |
| [!UICONTROL Champs d’identité] | Affiche le nombre total de jeux de mappages définis comme identité. Ces ensembles de mappages sont représentés par une icône d’empreinte digitale. |
| [!UICONTROL Erreurs] | Affiche le nombre de jeux de mappages erronés. |

![panneau supérieur](../images/ui/mapping/top-panel.png)

L’interface de mappage propose également un panneau d’options parmi lesquelles choisir afin de mieux interagir ou filtrer vos jeux de mappages.

![deuxième panneau](../images/ui/mapping/second-panel.png)

Pour rechercher un jeu de mappages particulier, sélectionnez **[!UICONTROL Recherche de champs source]** et saisissez le nom des données source à isoler.

![de recherches](../images/ui/mapping/search.png)

Sélectionner **[!UICONTROL Tous les champs sources]** pour afficher un menu déroulant des options de filtrage afin de mieux préciser votre vue de l’interface de mappage.

Les options de filtrage sont les suivantes :

| Champs source | Description |
| --- | --- |
| [!UICONTROL Tous les champs sources] | Cette option affiche tous les champs source de votre schéma source. Cette option est affichée par défaut. |
| [!UICONTROL Champs obligatoires] | Cette option filtre le schéma source pour n’afficher que les champs nécessaires à la réalisation du mapping. |
| [!UICONTROL Champs d’identité] | Cette option filtre le schéma source pour n’afficher que les champs marqués pour l’identité. |
| [!UICONTROL Champs mappés] | Cette option filtre le schéma source pour n’afficher que les champs déjà mappés. |
| [!UICONTROL Champs non mappés] | Cette option filtre le schéma source pour n’afficher que les champs qui doivent encore être mappés. |
| [!UICONTROL Champs avec recommandation] | Cette option filtre le schéma source pour n’afficher que les champs contenant les recommandations de mappage. |

Sélectionner **[!UICONTROL Champs en erreur]** pour afficher tous les ensembles de mappages avec des erreurs.

![filter](../images/ui/mapping/filter.png)

Une vue isolée des jeux de mappages en erreur s’affiche, ce qui vous permet de corriger les erreurs par le biais de recommandations de mappage intelligent ou de l’arborescence de mappage manuelle.

![fields-with-errors](../images/ui/mapping/fields-with-errors.png)

### Ajouter un nouveau type de champ

Vous pouvez ajouter un nouveau champ de mappage ou un champ calculé en sélectionnant **[!UICONTROL Nouveau type de champ]**.

#### Nouveau champ de mappage

Pour ajouter un nouveau champ de mappage, sélectionnez **[!UICONTROL Nouveau type de champ]** puis sélectionnez **[!UICONTROL Ajouter un nouveau champ]** dans le menu déroulant qui s’affiche.

![add-new-field](../images/ui/mapping/add-new-field.png)

Sélectionnez ensuite le champ source que vous souhaitez ajouter dans l’arborescence du schéma source qui s’affiche, puis sélectionnez **[!UICONTROL Sélectionner]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

L&#39;interface de mappage est mise à jour avec le champ source que vous avez sélectionné et un champ cible vide. Sélectionner **[!UICONTROL Champ cible de la carte]** pour commencer à mapper le nouveau champ source à son champ XDM cible approprié.

![map-target-field](../images/ui/mapping/map-target-field.png)

Une arborescence de schéma cible interactive s’affiche, vous permettant de parcourir manuellement le schéma cible et de trouver le champ XDM cible approprié pour votre champ source.

![mapping manuelle](../images/ui/mapping/manual-mapping.png)

Lorsque vous avez terminé, sélectionnez l’icône de schéma pour fermer l’interface du schéma cible.

![schema-tree](../images/ui/mapping/schema-tree.png)

#### Les champs calculés {#calculated-fields}

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible. Vous pouvez également leur fournir un nom et une description pour en faciliter la référence.

Pour créer un champ calculé, sélectionnez **[!UICONTROL Nouveau type de champ]** puis sélectionnez **[!UICONTROL Ajouter un champ calculé]**

![add-calculate-field](../images/ui/mapping/add-calculated-field.png)

Le panneau **[!UICONTROL Créer un champ calculé]** sʼaffiche. La boîte de dialogue de gauche contient les champs, fonctions et opérateurs pris en charge dans les champs calculés. Sélectionnez lʼun des onglets pour commencer à ajouter des fonctions, des champs ou des opérateurs à lʼéditeur dʼexpression.

| Tabulation | Description |
| --- | ----------- |
| [!UICONTROL Fonction] | Lʼonglet Fonctions répertorie les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide dʼ [utilisation des fonctions Data Prep (Mapper)](../functions.md). |
| [!UICONTROL Champ] | Lʼonglet Champs répertorie les champs et attributs disponibles dans le schéma source. |
| [!UICONTROL Opérateur] | Lʼonglet Opérateurs répertorie les opérateurs disponibles pour la transformation des données. |

![onglets](../images/ui/mapping/tabs.png)

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à lʼaide de lʼéditeur dʼexpression situé au centre. Sélectionnez lʼéditeur pour commencer à créer une expression. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

![create-calculate-field](../images/ui/mapping/create-calculated-field.png)

Sélectionner **[!UICONTROL Aperçu des données]** pour afficher les résultats de mappage de 100 lignes maximum de données d’exemple du jeu de données sélectionné.

![preview-data](../images/ui/mapping/preview-data.png)

Lors de la prévisualisation, la colonne d’identité est considérée comme le premier champ, car il s’agit des informations clés nécessaires à la validation des résultats du mapping. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**.

![aperçu-écran](../images/ui/mapping/preview-screen.png)

Pour supprimer tous les jeux de mappages, sélectionnez **[!UICONTROL Effacer tous les mappages]**.

![clear-all](../images/ui/mapping/clear-all.png)

### Utilisation de l’interface de mappage

Platform fournit automatiquement des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation ou corriger les jeux de mappages dupliqués afin d’effacer les erreurs.

![mapping-interface](../images/ui/mapping/mapping-interface.png)

Sélectionnez l’icône d’ampoule dans le champ cible que vous souhaitez ajuster.

![mapping-recc](../images/ui/mapping/mapping-recc.png)

Le [!UICONTROL Mappage des recommandations] le panneau contextuel s’affiche, affichant une liste des champs cibles recommandés qui peuvent être mappés à un champ source particulier. Par défaut, la première recommandation est automatiquement appliquée.

Parfois, plusieurs recommandations sont disponibles pour le schéma source. Dans ce cas, la carte de mappage affiche la recommandation la plus en vue, suivie d’une icône contenant le nombre de recommandations supplémentaires disponibles. Si vous sélectionnez l’icône d’ampoule, une liste des recommandations supplémentaires s’affiche. Vous pouvez choisir l’une des autres recommandations en cochant la case en regard de la recommandation à laquelle vous souhaitez mapper la page à la place.

À partir de là, vous pouvez modifier le champ cible sélectionné pour corriger une erreur ou répondre à votre cas d’utilisation.

Vous pouvez également sélectionner **[!UICONTROL Sélectionner manuellement]** pour utiliser manuellement l’arborescence interactive de mappage de schéma cible.

![recc-panel](../images/ui/mapping/recc-panel.png)

L’interface de mappage de schéma cible apparaît dans la même vue que vos jeux de mappages, ce qui vous permet de modifier des paires de mappages dans le même écran. Sélectionnez le champ cible correspondant à votre cas d’utilisation ou corrigez vos erreurs.

![select-target-field](../images/ui/mapping/select-target-field.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Terminer]** pour continuer.

![terminer](../images/ui/mapping/finish.png)

## Étapes suivantes

En lisant ce document, vous avez mappé un fichier CSV à un schéma XDM cible à l’aide de l’interface de mappage dans l’interface utilisateur de Platform. Consultez les documents suivants pour plus d’informations :

* [Présentation de la préparation des données](../home.md)
* [Présentation des sources](../../sources/home.md)
* [Surveillance des flux de données de sources dans l’interface utilisateur](../../dataflows/ui/monitor-sources.md)
