---
keywords: Experience Platform ; accueil ; rubriques populaires ; mapper csv ; mapper le fichier csv ; mapper le fichier csv à xdm ; mapper csv à xdm ; guide de lʼinterface utilisateur ; mappeur ; mappage ; data prep ; préparation des données ; préparer des données ;
title: Guide de l’interface utilisateur de la préparation des données
description: Découvrez comment utiliser les fonctions de préparation de données dans l’interface utilisateur d’Experience Platform pour mapper des fichiers CSV à un schéma XDM.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 06aa84aaccf3aeb45bfe19f8741b6bca96258d89
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 36%

---

# Guide de l’interface utilisateur de la préparation des données

Lisez ce guide pour savoir comment utiliser les fonctions de mappage [préparation des données](../home.md) dans l’interface utilisateur de Adobe Experience Platform pour mapper des fichiers CSV à un schéma [modèle de données d’expérience (XDM)](../../xdm/home.md).

## Prise en main

Ce tutoriel nécessite une connaissance pratique des composants Platform suivants :

* [[!DNL Experience Data Model (XDM)] Système](../../xdm/home.md) : Le cadre normalisé par lequel Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [Service d’identités](../../identity-service/home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en reliant les identités entre les appareils et les systèmes.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [Sources](../../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.

## Accès à l’interface de mappage dans l’interface utilisateur

Vous pouvez accéder à l’interface de mappage dans l’interface utilisateur par le biais de deux chemins différents.

1. Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Workflows]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Mapper CSV à un schéma XDM]**. Indiquez ensuite les détails de votre flux de données et sélectionnez les données à ingérer. Lorsque vous avez terminé, vous accédez à l’interface de mappage dans laquelle vous pouvez configurer le mappage entre vos données source et un schéma XDM.
2. Vous pouvez également accéder à l’interface de mappage via l’espace de travail des sources.

## Mappage de fichiers CSV dans un schéma XDM

Utilisez l’interface de mappage et l’ensemble d’outils complet qu’elle fournit pour mapper les champs de données de votre schéma source à leurs champs XDM cibles appropriés dans le schéma cible.

![Interface de mappage dans l’interface utilisateur d’Experience Platform.](../images/ui/mapping/base_mapping.png)

### Comprendre l’interface de mappage {#mapping-interface}

Reportez-vous au tableau de bord en haut de l’interface pour plus d’informations sur l’intégrité de vos champs de mappage dans le contexte du workflow d’ingestion. Le tableau de bord affiche les détails suivants concernant vos champs de mappage :

| Propriété | Description |
| --- | --- |
| [!UICONTROL Champs mappés] | Affiche le nombre total de champs sources qui ont été mappés à un champ XDM cible, quelles que soient les erreurs. |
| [!UICONTROL Champs obligatoires] | Affiche le nombre de champs de mappage obligatoires. |
| [!UICONTROL Champs d’identité] | Affiche le nombre total de champs de mappage définis comme identité. Ces champs de mappage sont représentés par une icône d’empreinte. |
| [!UICONTROL Erreurs] | Affiche le nombre de champs de mappage comportant des erreurs. |

{style="table-layout:auto"}

Vous pouvez ensuite utiliser les options répertoriées dans l’en-tête pour mieux interagir ou filtrer les champs de mappage.

| Option | Description |
| --- | --- |
| [!UICONTROL Rechercher les champs sources] | Utilisez la barre de recherche pour accéder à un champ source spécifique. |
| [!UICONTROL Tous les champs] | Sélectionnez **[!UICONTROL Tous les champs]** pour afficher un menu déroulant des options permettant de filtrer vos mappages. Les options de filtrage disponibles sont les suivantes :<ul><li>**[!UICONTROL Champs obligatoires]** : filtre l’interface pour afficher uniquement les champs requis pour terminer le workflow.</li><li> **[!UICONTROL Champs d’identité]** : filtre l’interface pour afficher uniquement les champs marqués comme identités.</li><li>**[!UICONTROL Champs mappés]** : filtre l’interface pour afficher uniquement les champs déjà mappés.</li><li>**[!UICONTROL Champs non mappés]** : filtre l’interface pour afficher uniquement les champs qui doivent encore être mappés.</li><li>**[!UICONTROL Champs comportant des erreurs]** : filtre l’interface pour n’afficher que les champs comportant des erreurs.</li></ul> |
| [!UICONTROL Nouveau type de champ ] | Sélectionnez **[!UICONTROL Nouveau type de champ]** pour ajouter un nouveau champ ou un champ calculé. Pour plus d’informations, consultez la section sur [l’ajout d’un nouveau type de champ](#add-a-new-field-type). |
| [!UICONTROL Importer des mappages] | Sélectionnez **[!UICONTROL Importer des mappages]** pour importer des mappages à partir d’un fichier ou d’un flux de données existant. Pour plus d’informations, consultez la section sur l’[importation de mappages](#import-mapping). |
| [!UICONTROL  Valider ] | Sélectionnez **[!UICONTROL Valider]** pour vérifier les erreurs dans vos mappages. |
| [!UICONTROL Télécharger le modèle] | Sélectionnez **[!UICONTROL Télécharger le modèle]** pour exporter et télécharger un fichier CSV de vos mappages. |
| [!UICONTROL Prévisualiser les données] | Sélectionnez **[!UICONTROL Prévisualiser les données]** pour utiliser le panneau de prévisualisation et inspecter la structure et le contenu de votre jeu de données source. |
| [!UICONTROL Tout effacer] | Sélectionnez **[!UICONTROL Effacer tout]** pour supprimer tous les mappages dans l’interface. |

{style="table-layout:auto"}

### Ajout d’un nouveau type de champ {#add-a-new-field-type}

Vous pouvez ajouter un nouveau champ de mappage ou un champ calculé en sélectionnant **[!UICONTROL Nouveau type de champ]**.

#### Nouveau champ de mappage

Pour ajouter un nouveau champ de mappage, sélectionnez **[!UICONTROL Nouveau type de champ]**, puis **[!UICONTROL Ajouter un nouveau champ]** dans le menu déroulant qui s’affiche.

![Interface de mappage avec le bouton « Ajouter un nouveau champ » sélectionné.](../images/ui/mapping/add_new_field.png)

Sélectionnez ensuite le champ source que vous souhaitez ajouter dans l’arborescence du schéma source qui s’affiche, puis sélectionnez **[!UICONTROL Sélectionner]**.

![Schéma source avec « pays » sélectionné comme nouveau champ supplémentaire.](../images/ui/mapping/source_field.png)

L’interface de mappage est mise à jour avec le champ source que vous avez sélectionné et un champ cible vide. Sélectionnez **[!UICONTROL Mapper le champ cible]** pour commencer à mapper le nouveau champ source à son champ XDM cible approprié.

![Interface de mappage avec un nouveau champ source non mappé.](../images/ui/mapping/new_field_added.png)

Une arborescence de schéma cible interactive s’affiche, vous permettant de parcourir manuellement le schéma cible et de trouver le champ XDM cible approprié pour votre champ source.

![Arborescence interactive du schéma cible avec un nouveau champ cible sélectionné.](../images/ui/mapping/add_target_field.png)

#### Champs calculés {#calculated-fields}

Les champs calculés permettent de créer des valeurs en fonction des attributs du schéma d’entrée. Ces valeurs peuvent ensuite être affectées à des attributs dans le schéma cible. Vous pouvez également leur fournir un nom et une description pour en faciliter la référence. La longueur maximale des champs calculés est de 4 096 caractères.

Pour créer un champ calculé, sélectionnez **[!UICONTROL Nouveau type de champ]**, puis **[!UICONTROL Ajouter un champ calculé]**.

![Interface de mappage avec le bouton « Ajouter un champ calculé » sélectionné.](../images/ui/mapping/new_calculated_field.png)

La fenêtre **[!UICONTROL Créer un champ calculé]** s’affiche. Utilisez l’interface pour saisir vos champs calculés et reportez-vous à la boîte de dialogue à gauche pour les champs, fonctions et opérateurs pris en charge.

| Tabulation | Description |
| --- | ----------- |
| [!UICONTROL Fonction] | Lʼonglet Fonctions répertorie les fonctions disponibles pour transformer les données. Pour en savoir plus sur les fonctions que vous pouvez utiliser dans les champs calculés, consultez le guide dʼ [utilisation des fonctions Data Prep (Mapper)](../functions.md). |
| [!UICONTROL Champ] | Lʼonglet Champs répertorie les champs et attributs disponibles dans le schéma source. |
| [!UICONTROL Opérateur] | Lʼonglet Opérateurs répertorie les opérateurs disponibles pour la transformation des données. |

![Interface des champs calculés](../images/ui/mapping/calculated_field.png)

Vous pouvez ajouter manuellement des champs, des fonctions et des opérateurs à lʼaide de lʼéditeur dʼexpression situé au centre. Sélectionnez lʼéditeur pour commencer à créer une expression. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour continuer.

### Importer le mapping {#import-mapping}

Vous pouvez réduire le temps de configuration manuelle de votre processus d’ingestion de données et limiter les erreurs à l’aide de la fonctionnalité de mappage d’importation de la préparation des données. Vous pouvez importer des mappages à partir d’un flux existant ou d’un fichier exporté.

>[!BEGINTABS]

>[!TAB Importer le mappage à partir du flux]

Si vous disposez de plusieurs flux de données basés sur des fichiers sources et des schémas cibles similaires, vous pouvez importer des mappages existants et les réutiliser pour de nouveaux flux de données.

Pour importer le mappage d’un flux de données existant, sélectionnez **[!UICONTROL Importer des mappages]** puis **[!UICONTROL Importer le mappage à partir d’un flux]**.

![Interface de mappage avec « importer le mappage » et « importer le mappage à partir du flux » sélectionnés.](../images/ui/mapping/import_from_flow.png)

Ensuite, utilisez la fenêtre pop-up pour localiser le flux de données dont vous souhaitez importer le mappage. Au cours de cette étape, vous pouvez également utiliser la fonction de recherche pour isoler un flux de données spécifique et récupérer ses mappages. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Sélectionner]**.

![Liste des flux de données existants dont les mappages correspondants peuvent être importés.](../images/ui/mapping/import_flow_window.png)

>[!TAB Importer le mappage depuis un fichier]

Dans certains cas, vous devrez peut-être mettre en œuvre un grand nombre de mappages pour vos données. Vous pouvez le faire manuellement avec l’interface de mappage, mais vous pouvez également exporter votre modèle de mappage et configurer vos mappages dans une feuille de calcul hors ligne pour gagner du temps et éviter les délais d’expiration des utilisateurs sur Experience Platform.

Pour importer le mappage d’un fichier exporté, sélectionnez **[!UICONTROL Importer les mappages]** puis **[!UICONTROL Importer le mappage à partir d’un fichier]**.

![L’interface de mappage avec « importer le mappage » et « importer le mappage à partir d’un fichier » sélectionnée.](../images/ui/mapping/import_from_file.png)

Utilisez ensuite la fenêtre [!UICONTROL Télécharger le modèle] pour télécharger une copie CSV de vos mappages. Vous pouvez ensuite configurer vos mappages localement sur votre appareil, à l’aide de n’importe quel logiciel prenant en charge la modification des types de fichiers CSV. Au cours de cette étape, vous devez vous assurer que vous utilisez uniquement les champs fournis dans votre fichier source et votre schéma cible.

![Fenêtre de modèle de chargement qui affiche des options permettant de télécharger et de charger un fichier csv exporté des mappages.](../images/ui/mapping/upload_template.png)

+++Sélectionner pour afficher un exemple de fichier de mappage exporté

![Fichier csv téléchargé du modèle de mappage.](../images/ui/mapping/mapping_csv_file.png)

+++

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Télécharger le fichier]** et sélectionnez le fichier csv mis à jour de vos mappages. Patientez quelques instants le temps que le système traite, puis sélectionnez **[!UICONTROL Terminé]**.

![La fenêtre de chargement du modèle avec un nouveau fichier chargé.](../images/ui/mapping/upload_successful.png)

>[!ENDTABS]

Une fois vos mappages terminés, vous pouvez sélectionner **[!UICONTROL Terminer]** et passer à l’étape suivante pour terminer votre flux de données.

![L’interface de mappage avec un ensemble complet de mappages.](../images/ui/mapping/completed_mappings.png)

## Étapes suivantes

Vous pouvez désormais mapper un fichier CSV à un schéma XDM cible à l’aide de l’interface de mappage dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez les documents suivants :

* [Présentation de la préparation des données](../home.md)
* [Présentation des sources](../../sources/home.md)
* [Surveillance des flux de données des sources dans l’interface utilisateur](../../dataflows/ui/monitor-sources.md)
