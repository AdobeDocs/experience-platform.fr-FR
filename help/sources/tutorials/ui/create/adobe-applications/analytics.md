---
title: Connexion D’Adobe Analytics À Experience Platform
description: Découvrez comment importer les données de votre suite de rapports Adobe Analytics dans Experience Platform
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: d9dad6b5da413740559e6c8de7392bc2e169d5d9
workflow-type: tm+mt
source-wordcount: '2731'
ht-degree: 14%

---

# Connexion d’Adobe Analytics à Experience Platform

Lisez ce guide pour savoir comment utiliser la source Adobe Analytics pour ingérer les données de votre suite de rapports Analytics dans Adobe Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Profil client en temps réel](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Terminologie clé

Il est important de comprendre les termes clés suivants utilisés dans ce document :

* **Attribut standard :** les attributs standard sont tous les attributs prédéfinis par Adobe. Ils renferment la même signification pour tous les clients et sont disponibles dans les groupes de champs des données sources et du schéma Analytics d’Analytics .
* **Attribut personnalisé** : les attributs personnalisés sont tout attribut de la hiérarchie des variables personnalisées dans Analytics. Les attributs personnalisés sont utilisés dans une implémentation d’Adobe Analytics pour capturer des informations spécifiques dans une suite de rapports. Leur utilisation peut varier d’une suite de rapports à l’autre. Les attributs personnalisés comprennent les eVars, les props et les listes. Pour plus d’informations sur les eVars[&#x200B; consultez la &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=fr)documentation Analytics sur les variables de conversion .
* **Tout attribut dans les groupes de champs personnalisés :** les attributs qui proviennent de groupes de champs créés par les clients sont tous définis par l’utilisateur et sont considérés comme des attributs ni standard ni personnalisés.

## Parcourir le catalogue des sources

>[!NOTE]
>
>Lorsque vous créez un flux de données source Analytics dans un sandbox de production, deux flux de données sont créés :
>
>* Flux de données qui renvoie pendant 13 mois les données historiques de la suite de rapports dans le lac de données. Ce flux de données se termine lorsque le renvoi est terminé.
>* Flux de données qui envoie des données actives au lac de données et à [!DNL Real-Time Customer Profile]. Ce flux de données s’exécute en continu.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Dans la catégorie *[!UICONTROL Adobe applications]* , sélectionnez la vignette Adobe Analytics , puis sélectionnez **[!UICONTROL Add data]**.

![Le catalogue des sources avec la carte source Adobe Analytics sélectionnée.](../../../../images/tutorials/create/analytics/catalog.png)

## Sélectionner les données

>[!IMPORTANT]
>
>* Les suites de rapports répertoriées à l’écran peuvent provenir de différentes régions. Il vous incombe de connaître les limites et obligations relatives à vos données et la manière dont vous les utilisez dans Adobe Experience Platform d’une région à l’autre. Assurez-vous que votre entreprise l’autorise.
>* Les données provenant de plusieurs suites de rapports ne peuvent être activées pour le profil client en temps réel que s’il n’existe aucun conflit de données, comme deux propriétés personnalisées (eVars, listes et props) ayant une signification différente.

Une suite de rapports est un conteneur de données qui forme la base des rapports Analytics. Une organisation peut avoir de nombreuses suites de rapports, chacune contenant des jeux de données différents.

Vous pouvez ingérer des suites de rapports à partir de n’importe quelle région (États-Unis, Royaume-Uni ou Singapour), à condition qu’elles soient mappées à la même organisation que l’instance sandbox Experience Platform dans laquelle la connexion source est en cours de création. Une suite de rapports peut être ingérée à l’aide d’un seul flux de données actif. Si une suite de rapports est grise et ne peut pas être sélectionnée, elle a déjà été ingérée dans le sandbox que vous utilisez ou dans un autre sandbox.

Il est possible d’établir plusieurs connexions entrantes pour importer plusieurs suites de rapports dans le même sandbox. Si les suites de rapports comportent des schémas différents pour les variables (telles que des eVars ou des événements), elles doivent être mappées à des champs spécifiques dans les groupes de champs personnalisés et éviter les conflits de données à l’aide de [Préparation de données](../../../../../data-prep/ui/mapping.md). Les suites de rapports ne peuvent être ajoutées qu’à un seul sandbox.

Sélectionnez **[!UICONTROL Report suite]** puis utilisez l’interface *[!UICONTROL Analytics source add data]* pour parcourir la liste et identifier la suite de rapports Analytics à ingérer dans Experience Platform. Sélectionnez **[!UICONTROL Next]** pour continuer.

![Une suite de rapports Analytics est sélectionnée pour l’ingestion et le bouton « Suivant » est mis en surbrillance](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!: les suites de rapports Analytics peuvent être configurées pour un sandbox à la fois. Pour importer la même suite de rapports dans un autre sandbox, le flux du jeu de données devra être supprimé et instancié à nouveau via la configuration pour un autre sandbox.—>

## Mappage {#mapping}

>[!IMPORTANT]
>
>Les transformations de la préparation des données peuvent ajouter de la latence au flux de données global. La latence supplémentaire ajoutée varie en fonction de la complexité de la logique de transformation.

Avant de pouvoir mapper vos données Analytics à un schéma XDM cible, vous devez d’abord déterminer si vous utilisez un schéma par défaut ou un schéma personnalisé.

>[!BEGINTABS]

>[!TAB  Schéma par défaut ]

Un schéma par défaut crée un schéma à votre place. Ce schéma nouvellement créé contient le groupe de champs [!DNL Adobe Analytics ExperienceEvent Template]. Pour utiliser un schéma par défaut, sélectionnez **[!UICONTROL Default schema]**.

![Étape de sélection du schéma du workflow source Analytics, avec « Schéma par défaut » sélectionné.](../../../../images/tutorials/create/analytics/default-schema.png)

>[!TAB  Schéma personnalisé ]

Un schéma personnalisé vous permet de choisir n’importe quel schéma disponible pour vos données Analytics, à condition que ce schéma contienne le groupe de champs [!DNL Adobe Analytics ExperienceEvent Template]. Pour utiliser un schéma personnalisé, sélectionnez **[!UICONTROL Custom schema]**.

![Étape de sélection du schéma du workflow source Analytics, avec « Schéma personnalisé » sélectionné.](../../../../images/tutorials/create/analytics/custom-schema.png)

>[!ENDTABS]

Utilisez l’interface *[!UICONTROL Mapping]* pour mapper les champs source aux champs de schéma cible appropriés. Vous pouvez mapper des variables personnalisées à de nouveaux groupes de champs de schéma et appliquer des calculs pris en charge par la préparation des données. Sélectionnez un schéma cible pour démarrer le processus de mappage.

>[!TIP]
>
>Seuls les schémas comportant le groupe de champs [!DNL Adobe Analytics ExperienceEvent Template] s’affichent dans le menu de sélection des schémas. Les autres schémas sont ignorés. Si aucun schéma approprié n’est disponible pour les données de votre suite de rapports, vous devez créer un schéma. Pour obtenir des instructions détaillées sur la création de schémas, consultez le guide de [création et de modification des schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md).

![Panneau de sélection du schéma cible de l’interface de mappage.](../../../../images/tutorials/create/analytics/select-schema.png)

Reportez-vous au panneau [!UICONTROL Map standard fields] pour connaître les mesures de votre [!UICONTROL Standard mappings applied]. [!UICONTROL Standard mappings with descriptor name conflicts] et [!DNL Custom mappings].

| Mappage des champs standard | Description |
| --- | --- |
| [!UICONTROL Standard mappings applied] | Le panneau [!UICONTROL Standard mappings applied] affiche le nombre total d’attributs mappés. Les mappages standard font référence aux mappages entre tous les attributs des données Analytics sources et les attributs correspondants du groupe de champs Analytics . Ils sont prémappés et ne peuvent pas être modifiés. |
| [!UICONTROL Standard mappings with descriptor name conflicts] | Le panneau [!UICONTROL Standard mappings with descriptor name conflicts] fait référence au nombre d’attributs mappés contenant des conflits de noms. Ces conflits apparaissent lorsque vous réutilisez un schéma qui contient déjà un ensemble de descripteurs de champ provenant d’une autre suite de rapports. Vous pouvez continuer à utiliser votre flux de données Analytics malgré la présence de conflits de noms. |
| [!UICONTROL Custom mappings] | Le panneau [!UICONTROL Custom mappings] affiche le nombre d’attributs personnalisés mappés, y compris les eVars, les props et les listes. Les mappages personnalisés font référence au mappage entre les attributs personnalisés des données Analytics sources et les attributs des groupes de champs personnalisés inclus dans le schéma sélectionné. |

### Mappages standard {#standard-mappings}

Experience Platform détecte automatiquement tout conflit de nom dans votre mappage. S’il n’y a aucun conflit avec vos mappages, sélectionnez **[!UICONTROL Next]** pour continuer.

![En-tête de mappages standard sans conflit de nom](../../../../images/tutorials/create/analytics/standard.png)

>[!TIP]
>
>En cas de conflits de noms entre votre suite de rapports source et votre schéma sélectionné, vous pouvez tout de même continuer à utiliser votre flux de données Analytics, mais les descripteurs de champ ne seront pas modifiés. Vous pouvez également choisir de créer un autre schéma avec un jeu de descripteurs vierge.

## Mappings personnalisés {#custom-mappings}

Vous pouvez utiliser les fonctions de préparation de données pour ajouter de nouveaux mappages personnalisés ou des champs calculés pour les attributs personnalisés. Pour ajouter des mappages personnalisés, sélectionnez **[!UICONTROL Custom]**.

![Onglet de mappage personnalisé dans le workflow source Analytics.](../../../../images/tutorials/create/analytics/custom.png)

* **[!UICONTROL Filter fields]** : utilisez la saisie de texte [!UICONTROL Filter fields] pour filtrer les champs de mappage spécifiques dans vos mappages.
* **[!UICONTROL Add new mapping]** : pour ajouter un nouveau mappage champ source et champ cible, sélectionnez **[!UICONTROL Add new mapping]**.
* **[!UICONTROL Add calculated field]** : si nécessaire, vous pouvez sélectionner **[!UICONTROL Add calculated field]** pour créer un champ calculé pour vos mappages.
* **[!UICONTROL Import mapping]** : vous pouvez réduire le temps de configuration manuelle de votre processus d’ingestion de données et limiter les erreurs à l’aide de la fonctionnalité de mappage d’importation de la préparation des données. Sélectionnez **[!UICONTROL Import mapping]** pour importer des mappages à partir d’un flux existant ou d’un fichier exporté. Pour plus d’informations, consultez [le guide sur l’importation et l’exportation de mappages](../../../../../data-prep/ui/mapping.md#import-mapping).
* **[!UICONTROL Download template]** : vous pouvez également télécharger une copie CSV de vos mappages et configurer vos mappages sur votre appareil local. Sélectionnez **[!UICONTROL Download template]** pour télécharger une copie CSV de vos mappages. Vous devez vous assurer que vous utilisez uniquement les champs fournis dans votre fichier source et votre schéma cible.

Pour plus d’informations sur la préparation des données, consultez la documentation suivante.

* [Présentation de la préparation des données](../../../../../data-prep/home.md)
* [Fonctions de mappage de la préparation des données](../../../../../data-prep/functions.md)
* [Ajouter des champs calculés](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

## Filtrage pour le profil client en temps réel {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="Créer des règles de filtrage"
>abstract="Définissez des règles de filtrage au niveau des lignes et des colonnes lors de l&#39;envoi de données au profil client en temps réel. Utilisez le filtrage au niveau des lignes pour appliquer des conditions et dicter les données à **inclure lors de l&#39;ingestion de profils**. Utilisez le filtrage au niveau des colonnes pour sélectionner les colonnes de données à **exclure lors de l&#39;ingestion de profils**. Les règles de filtrage ne s&#39;appliquent pas aux données envoyées au lac de données."

Une fois que vous avez terminé les mappages pour les données de votre suite de rapports Analytics, vous pouvez appliquer des règles et des conditions de filtrage pour inclure ou exclure de manière sélective des données de l’ingestion vers le profil client en temps réel. La prise en charge du filtrage est uniquement disponible pour les données Analytics et les données ne sont filtrées qu’avant la saisie [!DNL Profile.] Toutes les données sont ingérées dans le lac de données.

>[!BEGINSHADEBOX]

**Informations supplémentaires sur la préparation et le filtrage des données Analytics pour le profil client en temps réel**

* Vous pouvez utiliser la fonctionnalité de filtrage pour les données qui vont dans Profil, mais pas pour celles qui vont dans le lac de données.
* Vous pouvez utiliser le filtrage pour les données actives, mais vous ne pouvez pas filtrer les données de renvoi.
   * La source Analytics ne renvoie pas les données dans le profil.
* Si vous utilisez des configurations de préparation de données lors de la configuration initiale d’un flux Analytics, ces modifications sont également appliquées au renvoi automatique de 13 mois.
   * Ce n’est toutefois pas le cas pour le filtrage, car celui-ci est réservé aux données actives.
* La préparation des données est appliquée aux chemins d’ingestion en flux continu et par lots. Si vous modifiez une configuration de préparation de données existante, ces modifications sont ensuite appliquées aux nouvelles données entrantes sur les chemins d’ingestion par lots et par flux.
   * Toutefois, les configurations de préparation de données ne s’appliquent pas aux données déjà ingérées dans Experience Platform, qu’il s’agisse de données en flux continu ou de données par lots.
* Les attributs standard d’Analytics sont toujours mappés automatiquement. Par conséquent, vous ne pouvez pas appliquer de transformations aux attributs standard.
   * Cependant, vous pouvez filtrer les attributs standard tant qu’ils ne sont pas obligatoires dans le service d’identités ou le profil.
* Vous ne pouvez pas utiliser le filtrage au niveau des colonnes pour filtrer les champs obligatoires et les champs d’identité.
* Bien que vous puissiez filtrer les identités secondaires, en particulier AAID et AACustomID, vous ne pouvez pas exclure l’ECID.
* Lorsqu’une erreur de transformation se produit, la colonne correspondante donne la valeur NULL.

>[!ENDSHADEBOX]

### Filtrage au niveau des lignes

>[!IMPORTANT]
>
>Utilisez le filtrage au niveau des lignes pour appliquer des conditions et dicter les données à **inclure lors de l&#39;ingestion de profils**. Utilisez le filtrage au niveau des colonnes pour sélectionner les colonnes de données à **exclure lors de l&#39;ingestion de profils**.

Vous pouvez filtrer les données pour l’ingestion de profils au niveau des lignes et des colonnes. Utilisez le filtrage au niveau des lignes pour définir des critères tels que la chaîne contient, est égal à, commence ou se termine par. Vous pouvez également utiliser le filtrage au niveau des lignes pour joindre des conditions à l’aide de `AND` et de `OR`, et annuler des conditions à l’aide de `NOT`.

Pour filtrer vos données Analytics au niveau des lignes, sélectionnez **[!UICONTROL Row filter]** et utilisez le rail de gauche pour parcourir la hiérarchie du schéma et identifier l’attribut de schéma à sélectionner.

![Interface de filtre de ligne pour les données Analytics.](../../../../images/tutorials/create/analytics/row-filter.png)

Une fois que vous avez identifié l’attribut à configurer, sélectionnez-le et faites-le glisser du rail de gauche vers le panneau de filtrage.

![Attribut « Manufacturer » sélectionné pour le filtrage.](../../../../images/tutorials/create/analytics/filtering-panel.png)

Pour configurer différentes conditions, sélectionnez **[!UICONTROL equals]**, puis sélectionnez une condition dans la fenêtre déroulante qui s’affiche.

La liste des conditions configurables comprend :

* [!UICONTROL equals]
* [!UICONTROL does not equal]
* [!UICONTROL starts with]
* [!UICONTROL ends with]
* [!UICONTROL does not end with]
* [!UICONTROL contains]
* [!UICONTROL does not contain]
* [!UICONTROL exists]
* [!UICONTROL does not exist]

![Liste déroulante des conditions avec une liste d’opérateurs de condition.](../../../../images/tutorials/create/analytics/conditions.png)

Saisissez ensuite les valeurs à inclure en fonction de l’attribut que vous avez sélectionné. Dans l’exemple ci-dessous, [!DNL Apple] et [!DNL Google] sont sélectionnés pour l’ingestion dans le cadre de l’attribut **[!UICONTROL Manufacturer]** .

![Panneau de filtrage avec les attributs et valeurs sélectionnés inclus.](../../../../images/tutorials/create/analytics/include.png)

Pour spécifier davantage vos conditions de filtrage, ajoutez un autre attribut du schéma, puis ajoutez des valeurs basées sur cet attribut. Dans l’exemple ci-dessous, l’attribut **[!UICONTROL Model]** est ajouté et les modèles tels que [!DNL iPhone 16] et [!DNL Google Pixel 9] sont filtrés pour l’ingestion.

![Attributs et valeurs supplémentaires inclus dans le conteneur.](../../../../images/tutorials/create/analytics/include-model.png)

Pour ajouter un nouveau conteneur, sélectionnez les points de suspension (`...`) en haut à droite de l’interface de filtrage, puis sélectionnez **[!UICONTROL Add container]**.

![Menu déroulant « Ajouter un conteneur » sélectionné.](../../../../images/tutorials/create/analytics/add-container.png)

Une fois qu’un nouveau conteneur est ajouté, sélectionnez **[!UICONTROL Include]** , puis **[!UICONTROL Exclude]** dans le menu déroulant. Ajoutez les attributs et les valeurs à exclure, puis, lorsque vous avez terminé, sélectionnez **[!UICONTROL Next]**.

![Attributs et valeurs filtrés pour l’exclusion.](../../../../images/tutorials/create/analytics/exclude.png)

### Filtrage au niveau des colonnes

Sélectionnez **[!UICONTROL Column filter]** dans l’en-tête pour appliquer le filtrage au niveau des colonnes.

La page se met à jour dans une arborescence de schéma interactif, affichant les attributs de votre schéma au niveau de la colonne. À partir de là, vous pouvez sélectionner les colonnes de données que vous souhaitez exclure de l’ingestion de profils. Vous pouvez également développer une colonne et sélectionner des attributs spécifiques à exclure.

Par défaut, toutes les analyses sont transmises au profil et ce processus permet d’exclure des branches de données XDM de l’ingestion de profils.

![Interface du filtre des colonnes avec l’arborescence du schéma.](../../../../images/tutorials/create/analytics/column-filter.png)

### Filtrer les identités secondaires

Utilisez un filtre de colonne pour exclure les identités secondaires de l’ingestion de profils. Pour filtrer les identités secondaires, sélectionnez **[!UICONTROL Column filter]** puis **[!UICONTROL _identities]**.

Le filtre s’applique uniquement lorsqu’une identité est marquée comme secondaire. Si des identités sont sélectionnées, mais qu’un événement arrive avec l’une des identités marquées comme principales, elles ne sont pas filtrées.

![Identités secondaires dans l’arborescence du schéma pour le filtrage des colonnes.](../../../../images/tutorials/create/analytics/secondary-identities.png)

### Fournir des détails sur le flux de données

L’étape **[!UICONTROL Dataflow detail]** s’affiche, où vous devez fournir un nom et une description facultative pour le flux de données. Sélectionnez **[!UICONTROL Next]** (Enregistrer) une fois terminé.

![Interface détaillée du flux de données. du workflow d’ingestion.](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### Réviser

L’étape [!UICONTROL Review] s’affiche, vous permettant de vérifier votre nouveau flux de données Analytics avant sa création. Les détails de la connexion sont regroupés par catégories, notamment :

* [!UICONTROL Connection] : affiche la plateforme source de la connexion.
* [!UICONTROL Data type] : affiche la suite de rapports sélectionnée et l’identifiant de suite de rapports correspondant.

![Interface de révision du workflow d’ingestion.](../../../../images/tutorials/create/analytics/review.png)

>[!TIP]
>
>Suivez ces bonnes pratiques pour éviter de dépasser vos droits de licence et de surcharger vos mesures de stockage total et de richesse des données :
>
>* Configurez la durée de vie (TTL) de rétention des jeux de données d’événements d’expérience dès le début pour optimiser la gestion du cycle de vie des données et l’efficacité du stockage. Pour plus d’informations, consultez le guide sur la [gestion de la conservation des jeux de données d’événements d’expérience dans le lac de données à l’aide de TTL](../../../../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md).
>
>* Lorsque vous créez un flux de données source Analytics, commencez par configurer le connecteur afin d’ingérer les données uniquement dans le lac de données. Après avoir confirmé que le flux de données fonctionne, vous pouvez activer l’ingestion de profil pour le jeu de données. Cette approche fonctionne mieux lorsque les filtres de ligne et de colonne réduisent efficacement le volume de données.

## Surveiller votre flux de données {#monitor-your-dataflow}

Une fois votre flux de données terminé, vous pouvez utiliser l’interface *[!UICONTROL Dataflows]* pour surveiller le statut de votre flux de données Analytics.

Utilisez l’interface [!UICONTROL Dataset activity] pour plus d’informations sur la progression des données envoyées d’Analytics vers Experience Platform. L’interface affiche des mesures telles que le total des enregistrements du mois précédent, le total des enregistrements ingérés au cours des sept derniers jours et la taille des données du mois précédent.

La source instancie deux flux de jeux de données. L’un représente les données de renvoi, l’autre les données actives. Les données de renvoi ne sont pas configurées pour l’ingestion dans le profil client en temps réel, mais sont envoyées au lac de données à des fins d’analyse et de cas d’utilisation en science des données.

Pour plus d’informations sur le renvoi, les données actives et leurs latences respectives, consultez la [présentation de la source Analytics](../../../../connectors/adobe-applications/analytics.md).

![Page d’activité du jeu de données pour un jeu de données cible donné pour les données Adobe Analytics.](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>La page d’activité du jeu de données n’affiche pas d’informations sur les lots, car le connecteur source Analytics est entièrement géré par Adobe. Vous pouvez surveiller le flux de données en examinant les mesures relatives aux enregistrements ingérés.

## Supprimer le flux de données {#delete-dataflow}

>[!NOTE]
>
>Vous ne pouvez pas désactiver un flux de données Analytics. Pour arrêter le flux de données Analytics, vous devez **supprimer** l’intégralité du flux de données.

Pour supprimer votre flux de données Analytics, sélectionnez **[!UICONTROL Dataflows]** dans l’en-tête supérieur de l’espace de travail des sources. Utilisez la page Flux de données pour localiser le flux de données Analytics à supprimer, puis sélectionnez les points de suspension (`...`) en regard. Ensuite, utilisez le menu déroulant et sélectionnez **[!UICONTROL Delete]**.

* La suppression du flux de données Analytics actif supprimera également son jeu de données sous-jacent.
* La suppression du flux de données d’analyse de renvoi ne supprime pas le jeu de données sous-jacent, mais arrête le processus de renvoi de la suite de rapports correspondante. Si vous supprimez le flux de données de renvoi, les données ingérées peuvent toujours être consultées via le jeu de données.

## Étapes suivantes et ressources supplémentaires

Une fois la connexion créée, le flux de données est automatiquement créé pour contenir les données entrantes et renseigner un jeu de données avec votre schéma sélectionné. En outre, un remplissage de données se produit et ingeste jusqu’à 13 mois de données historiques. Une fois l’ingestion initiale terminée, les données Analytics peuvent être utilisées par les services Experience Platform en aval, tels que [!DNL Real-Time Customer Profile] et Segmentation Service. Consultez les documents suivants pour plus d’informations :

* [Présentation de [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Présentation de [!DNL Segmentation Service]](../../../../../segmentation/home.md)
* [Présentation de [!DNL Data Science Workspace]](../../../../../data-science-workspace/home.md)
* [Présentation de [!DNL Query Service]](../../../../../query-service/home.md)

La vidéo suivante est destinée à vous aider à comprendre l’ingestion de données à l’aide du connecteur source Adobe Analytics :

>[!WARNING]
>
> Lʼinterface utilisateur de [!DNL Experience Platform] affichée dans la vidéo suivante est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

