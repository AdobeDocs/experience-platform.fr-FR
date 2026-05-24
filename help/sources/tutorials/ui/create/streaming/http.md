---
title: Créer une connexion en continu d’API HTTP à l’aide de l’interface utilisateur
description: Ce guide de l’interface utilisateur vous aidera à créer une connexion en continu à l’aide d’Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
TQID: https://experienceleague.adobe.com/hJCqDpKKk85JEmO4d8OFSVCUoUHQzCZ-zr7MwumVU1Y
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 962
ht-degree: 26%

---

# Créer une connexion en continu [!DNL HTTP API] à l’aide de l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source par flux à l’aide de l’espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Création d’une connexion en continu

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalog] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Streaming]** , sélectionnez **[!UICONTROL HTTP API]** puis **[!UICONTROL Add data]**.

![catalogue](../../../../images/tutorials/create/http/catalog.png)

La page **[!UICONTROL Connect HTTP API account]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte d’API HTTP avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Next]** pour continuer.

![compte-existant](../../../../images/tutorials/create/http/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL New account]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom de compte et une description facultative. Vous aurez également la possibilité de fournir les propriétés de configuration suivantes :

- **[!UICONTROL Authentication]:** Cette propriété détermine si la connexion en continu nécessite une authentification ou non. L’authentification garantit que les données sont collectées auprès de sources approuvées. Si vous avez affaire à des informations d’identification personnelle (PII), cette propriété doit être activée. Par défaut, cette propriété est désactivée.
- **[!UICONTROL XDM compatible]:** cette propriété indique si cette connexion en continu enverra des événements compatibles avec les schémas XDM. Par défaut, cette propriété est désactivée.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connect to source]** puis sélectionnez **[!UICONTROL Next]** pour continuer.

![nouveau-compte](../../../../images/tutorials/create/http/new.png)

## Sélectionner les données

Une fois la connexion à l’API HTTP créée, l’étape **[!UICONTROL Select data]** s’affiche, vous fournissant une interface pour charger et prévisualiser vos données.

Sélectionnez **[!UICONTROL Upload files]** pour charger vos données. Vous pouvez également faire glisser et déposer vos données dans la section [!UICONTROL Drag and drop files] de l’interface.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Une fois vos données chargées, vous pouvez utiliser le côté droit de l’interface pour prévisualiser votre hiérarchie de fichiers. Sélectionnez **[!UICONTROL Next]** pour continuer.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Mappage des champs de données à un schéma XDM

L’étape [!UICONTROL Mapping] s’affiche, fournissant une interface pour mapper les données sources à un jeu de données Experience Platform.

La source [!DNL HTTP API] prend en charge l’ingestion de fichiers JSON. Les fichiers JSON ne nécessitent pas de configuration manuelle s’ils sont marqués comme conformes à XDM. Si ce n’est pas le cas, vous devez configurer explicitement le mappage.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Créer un nouveau jeu de données

Pour créer un jeu de données, sélectionnez **[!UICONTROL New dataset]**. Dans le formulaire qui s’affiche, fournissez le nom, une description facultative, ainsi que le schéma cible du jeu de données. Si vous sélectionnez un schéma activé pour [!DNL Profile], vous pouvez choisir si le jeu de données doit également être activé pour [!DNL Profile].

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Utiliser un jeu de données existant

Pour utiliser un jeu de données existant, sélectionnez **[!UICONTROL Existing dataset]**. Dans le formulaire qui s’affiche, sélectionnez le jeu de données à utiliser. Une fois que vous avez sélectionné un jeu de données, vous pouvez choisir s’il doit être activé pour le [!DNL Profile].

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Mappage des champs standard

Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [&#x200B; Guide de l’interface utilisateur de la préparation des données &#x200B;](../../../../../data-prep/ui/mapping.md).

Pour ajouter un nouveau champ source, sélectionnez **[!UICONTROL Add new mapping]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Une nouvelle association entre le champ source et le champ cible apparaît. Pour ajouter un nouveau champ source, sélectionnez l’icône de flèche en regard de la barre de saisie [!UICONTROL Select source field].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Le panneau [!UICONTROL Select attributes] vous permet d’explorer votre hiérarchie de fichiers et de sélectionner un champ source spécifique à mapper à un champ XDM cible. Une fois que vous avez sélectionné le champ source à mapper, sélectionnez **[!UICONTROL Select]** pour continuer.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Une fois le champ source sélectionné, vous pouvez désormais identifier le champ XDM cible approprié à mapper. Sélectionnez l’icône de schéma sous la section champ cible .

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

La fenêtre [!UICONTROL Map source field to target field] s’affiche, vous fournissant une interface pour explorer le schéma de votre jeu de données cible. Sélectionnez le champ cible correspondant à votre champ source, puis sélectionnez **[!UICONTROL Select]** pour continuer.

![champ-mapper-à-cible](../../../../images/tutorials/create/http/map-to-target-field.png)

Une fois que vos champs source sont tous mappés à leurs champs XDM cibles appropriés, sélectionnez **[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Détails du flux de données

L’étape **[!UICONTROL Dataflow detail]** s’affiche. Sur cette page, vous pouvez fournir des détails sur le flux de données créé en indiquant un nom et une description facultative.

Après avoir fourni des détails sur le flux de données, sélectionnez **[!UICONTROL Next]**.

![dataflow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Réviser

L’étape **[!UICONTROL Review]** s’affiche, vous permettant de consulter les détails de votre flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- **[!UICONTROL Connection]** : affiche le nom du compte, la plateforme source et le nom de la source.
- **[!UICONTROL Assign dataset and map fields]** : affiche le jeu de données cible et le schéma auquel le jeu de données se conforme.

Après avoir confirmé que les détails sont corrects, sélectionnez **[!UICONTROL Finish]**.

![review](../../../../images/tutorials/create/http/review.png)

## Obtenir l’URL du point d’entrée de diffusion en continu

Une fois la connexion créée, la page des détails des sources s’affiche. Cette page affiche les détails de la connexion que vous venez de créer, y compris les flux de données précédemment exécutés, l’identifiant et l’URL du point d’entrée de diffusion en continu.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Étapes suivantes

Ce tutoriel vous a permis de créer une connexion HTTP en flux continu, qui vous permet d’utiliser le point d’entrée en flux continu pour accéder à diverses API [!DNL Data Ingestion]. Pour savoir comment créer une connexion en continu dans l’API, consultez le [tutoriel sur la création d’une connexion en continu](../../../api/create/streaming/http.md).

Pour savoir comment diffuser des données vers Experience Platform, consultez le tutoriel sur la [&#x200B; diffusion en continu de données de série temporelle &#x200B;](../../../../../ingestion/tutorials/streaming-time-series-data.md) ou le tutoriel sur la [&#x200B; diffusion en continu de données d’enregistrement &#x200B;](../../../../../ingestion/tutorials/streaming-record-data.md).
