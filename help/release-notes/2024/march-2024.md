---
title: Notes de mise à jour d’Adobe Experience Platform - Mars 2024
description: Les notes de mise à jour de mars 2024 pour Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 40%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 19 mars 2024**

>[!TIP]
>
>Utilisez la variable [Glossaire Adobe Experience Platform](/help/landing/glossary.md) pour vous familiariser avec la terminologie utilisée dans Real-Time Customer Data Platform et Adobe Experience Platform. Si vous ne trouvez pas de terme spécifique que vous recherchez, utilisez les options de commentaire de la page pour demander l’ajout de nouveaux termes au glossaire.

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Catalog Service](#catalog-service)
- [Collecte de données](#data-collection)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

| Fonctionnalité | Description |
| --- | --- |
| Actions supplémentaires | Pour rendre les opérations plus flexibles et vous aider à gérer vos données, vous pouvez désormais utiliser la fonction &quot;Autres actions&quot; de la vue Détails pour effectuer des tâches supplémentaires sur un jeu de données. Vous pouvez supprimer le jeu de données ou l’activer pour l’utiliser avec Real-time Customer Profile à partir de la page de détails d’un jeu de données sélectionné.<br>**Remarque :** si vous activez un jeu de données pour l’ingestion de Profile, le schéma du jeu de données doit être compatible avec Real-time Customer Profile.<br>![L’espace de travail des jeux de données avec le [!UICONTROL .. Plus] menu déroulant en surbrillance.](../2024/assets/march/more-actions.png "Espace de travail des jeux de données avec le menu déroulant Plus en surbrillance."){width="100" zoomable="yes"}.<br>Lisez la section [guide d’utilisation des jeux de données](../../catalog/datasets/user-guide.md) documentation pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations sur Catalog Service, consultez la [vue d’ensemble de Catalog Service](../../catalog/home.md).

## Préparation de données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles fonctions de mappeur pour Adobe Analytics | Vous pouvez désormais utiliser les fonctions suivantes pour extraire des données d’événement d’Adobe Analytics : <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Pour plus d’informations sur ces fonctions, consultez la section [Guide des fonctions de préparation de données](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Nouvelles fonctionnalités**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Extensions | [!DNL Merkury] Extension de balise | La variable [[!DNL Merkury] extension de balise](https://exchange.adobe.com/apps/ec/600027/merkury-tag) fournit des taux de correspondance de pointe pour les visiteurs anonymes de site web à une [!DNL Merkury] ID. Les marques peuvent tirer parti de la puissance de [!DNL Merkury] marquer et Adobe pour offrir des expériences de site web personnalisées en temps réel. En outre, la variable [!DNL Merkury] La balise permet la croissance de données numériques propriétaires avec des profils clients en ligne et hors ligne connectés. |

{style="table-layout:auto"}

Pour en savoir plus sur la collecte de données, consultez la [vue d’ensemble des collectes de données](../../tags/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Destinations nouvelles et mises à jour** {#new-updated-destinations}

| Destination | Type | Description |
| ----------- | --------- | ----------- |
| [(Beta) Connexion d’amélioration des données d’Acrobat](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nouveau | Utilisez ce connecteur pour activer les profils propriétaires de Real-Time CDP vers Acxiom afin d’enrichir les données et de les utiliser sur les canaux marketing. Vous pouvez ensuite utiliser la source Acxiom pour importer les profils contenant des données améliorées et travailler avec eux dans Real-Time CDP. |
| [(Beta) Connexion de suppression des prospects Acxiom](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nouveau | Exportez vos audiences propriétaires vers la destination Acxiom pour permettre à Acxiom de supprimer les clients connus ou convertis. Ensuite, utilisez le [Importation de données de prospection dans Acrobat](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) connecteur source pour ingérer et activer des listes de prospects à partir d’Acxiom, vos clients connus ou convertis étant supprimés. |
| [Connexion Amazon Ads](../../destinations/catalog/advertising/amazon-ads.md) | Mise à jour  | Lors de l’exportation de données vers la destination Amazon Ads, vous pouvez désormais acheminer les données vers la DSP Amazon ou le Marketing Cloud Amazon (nouveau). |
| [Connexion à l’intégration LiveRamp](../../destinations/catalog/advertising/liveramp-onboarding.md) | Mise à jour  | La destination d’intégration LiveRamp prend désormais en charge les diffusions vers l’Europe et l’Australie [!DNL LiveRamp] [!DNL SFTP] instances. La taille maximale du fichier exporté a également été augmentée à 10 millions de lignes (contre 5 millions auparavant). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge du type de données de carte de l’interface utilisateur Experience Platform | Personnalisez davantage votre structure de données de modèle de données d’expérience (XDM) en définissant des champs de mappage dans l’interface utilisateur de Platform. Vous pouvez désormais créer des champs de mappage dans l’éditeur de schémas pour modéliser des structures de données flexibles ou stocker efficacement des paires clé-valeur. Sélectionnez &quot;Mapper&quot; dans la liste déroulante Type lors de la définition d’un nouveau champ pour configurer des sous-champs et les affecter à des groupes de champs. Les types de valeurs de mappage pris en charge sont string et integer.<br>![L’éditeur de schémas avec les champs de type de valeur Type et Mappage mis en surbrillance.](../2024/assets/march/maps.png "L’éditeur de schémas avec les champs de type de valeur Type et Mappage mis en surbrillance."){width="100" zoomable="yes"}<br> Pour apprendre à [Définition des champs de mappage dans l’interface utilisateur](../../xdm/ui/fields/map.md), voir le guide de l’interface utilisateur. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [vue d’ensemble du système XDM](../../xdm/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| ------- | ----------- |
| Actions en masse | L’inventaire des audiences prend désormais en charge les actions en bloc. Grâce aux actions en bloc, vous pouvez sélectionner rapidement plusieurs audiences pour les déplacer vers un dossier, appliquer des balises, appliquer des étiquettes d’accès ou supprimer. <br> ![Actions en bloc dans l’espace de travail de l’interface utilisateur Audiences.](../2024/assets/march/bulk-actions.png "Actions en bloc dans l’espace de travail de l’interface utilisateur Audiences."){width="100" zoomable="yes"} <br>Pour plus d’informations sur cette fonctionnalité, consultez la section [Présentation d’Audience Portal](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Pour en savoir plus sur Segmentation Service, consultez la section [Présentation de Segmentation Service](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources et mises à jour**

| Fonctionnalité | Type | Description |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | Nouveau | Utilisez la variable [[!DNL Acxiom Data Ingestion] source](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) à ingérer [!DNL Acxiom] des données dans Real-Time Customer Data Platform et enrichissez les profils propriétaires. Vous pouvez ensuite utiliser la variable [!DNL Acxiom]profils propriétaires enrichis pour améliorer les audiences et les activer sur les canaux marketing. <br> ![La source d’ingestion de données Acxiom.](../2024/assets/march/acxiom-data-ingestion.png "Nouvelle source d’ingestion de données Acxiom."){width="100" zoomable="yes"} <br> Lisez la section [[!DNL Acxiom Data Ingestion] aperçu](../../sources/connectors/data-partners/acxiom-data-ingestion.md) pour plus d’informations sur la prise en main. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | Nouveau | Utilisez la variable [[!DNL Stripe] source](../../sources/connectors/payments/stripe.md) pour ingérer dans Experience Platform les données capturées pendant le flux d’achat par vos clients. Une fois ingérées, vous pouvez utiliser ces données pour créer des offres personnalisées et déverrouiller des informations commerciales plus riches. <br> ![Source du Stripe.](../2024/assets/march/stripe.png "Nouvelle source du Stripe."){width="100" zoomable="yes"} <br> Lisez la section [[!DNL Stripe] aperçu](../../sources/connectors/payments/stripe.md) pour plus d’informations sur la prise en main. |
| Prise en charge de l’interface utilisateur pour [!DNL Snowflake Streaming] | Nouveau | Vous pouvez désormais utiliser la variable [[!DNL Snowflake Streaming] source](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) dans l’interface utilisateur de l’Experience Platform, pour diffuser des données depuis votre [!DNL Snowflake] base de données. <br> ![Source de diffusion en continu du Snowflake.](../2024/assets/march/snowflake-streaming.png "Nouvelle source de diffusion en continu des Snowflake."){width="100" zoomable="yes"} <br> Lisez la section [[!DNL Snowflake Streaming] aperçu](../../sources/connectors/databases/snowflake-streaming.md) pour plus d’informations sur la prise en main. |

{style="table-layout:auto"}

Pour plus d’informations sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
