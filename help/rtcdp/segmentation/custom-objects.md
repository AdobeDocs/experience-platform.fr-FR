---
title: Objets personnalisés avec B2B CDP
description: Découvrez comment créer un objet personnalisé de relation un-à-plusieurs pour B2B CDP.
source-git-commit: 1690d9e86f13fa01664a1f5b8a8d426aa35c3f22
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---


# Utiliser des objets personnalisés avec B2B CDP

B2B CDP prend en charge les objets personnalisés avec des relations un-à-plusieurs (1:M). Vous pouvez utiliser ces objets personnalisés dans la segmentation et les cas d’utilisation de Query Service. Par exemple, vous pouvez modéliser des objets CRM personnalisés, suivre les droits et les achats des produits et gérer les offres client. »

## Créer un schéma relationnel {#create-relational}

Pour commencer à connecter votre objet personnalisé à l’aide d’une relation un-à-plusieurs, vous devez d’abord créer un schéma relationnel pour modéliser vos données.

Sous la section **[!UICONTROL Data management]** , sélectionnez **[!UICONTROL Schemas]**. Sur la page Aperçu du schéma , sélectionnez **[!UICONTROL Create schema]**, puis **[!UICONTROL Relational]**.

![La section Schémas sous Gestion des données est mise en surbrillance, ainsi que le bouton Relationnel sous la zone Créer un schéma.](/help/rtcdp/assets/segmentation/custom-objects/create-relational.png)

La page **[!UICONTROL Create relational schema]** s’affiche. Vous pouvez ajouter les détails du schéma, notamment le nom d’affichage, la description et le comportement du schéma.

![La page Créer un schéma s’affiche.](/help/rtcdp/assets/segmentation/custom-objects/create-schema.png)

>[!IMPORTANT]
>
>Actuellement, seules les données **enregistrement** sont prises en charge. Les données de série temporelle ne sont **pas** prises en charge pour le moment.

| Comportement du schéma | Description |
| --------------- | ----------- |
| Enregistrement | Les données d’enregistrement fournissent des informations sur les attributs d’un sujet. Ce sujet peut être une organisation ou un individu. |

<!-- | Time series | Time series data provides a snapshot of the system at the time an action was taken either directly or indirectly by a record subject. | -->

## Ajouter vos champs {#add-fields}

Une fois le schéma relationnel créé, vous pouvez ajouter les champs de votre schéma, y compris le marquage de la clé primaire et de l’identifiant de version, dans l’éditeur de schémas.

![Le bouton d’ajout d’un champ est mis en surbrillance dans l’éditeur de schémas.](/help/rtcdp/assets/segmentation/custom-objects/add-field.png)

Pour plus d’informations sur la création de votre schéma relationnel, consultez le guide [créer un schéma](/help/xdm/ui/resources/schemas.md#create-manually).

## Créer un jeu de données {#create-dataset}

Une fois le schéma créé, vous devez créer un jeu de données qui utilise le schéma pour héberger les données de vos objets personnalisés.

![Le schéma précédemment créé est sélectionné sur la page Créer un jeu de données.](/help/rtcdp/assets/segmentation/custom-objects/create-dataset.png)

Pour plus d’informations sur la création d’un jeu de données, consultez le guide [créer un jeu de données](/help/catalog/datasets/user-guide.md#create)

## Activation du schéma pour la segmentation {#enable-schema}

>[!NOTE]
>
>Si vous utilisez **uniquement** des objets personnalisés avec Query Service, il n’est **nécessaire** d’activer le schéma pour la segmentation.
>
>En outre, vous ne pouvez activer qu’un maximum de 20 schémas **par sandbox pour la segmentation.** Une fois qu’un schéma est activé, vous **ne pouvez pas** désactiver le schéma de la segmentation ; vous devez supprimer le schéma pour le supprimer.

Une fois le jeu de données créé, vous pouvez activer le schéma pour la segmentation. Vous **devez** marquer le schéma comme étant activé pour la segmentation afin de l’utiliser pour les cas d’utilisation de segmentation avec des objets personnalisés dans B2B CDP.

![Le bouton (bascule) permettant d’activer le schéma pour la segmentation est mis en surbrillance.](/help/rtcdp/assets/segmentation/custom-objects/enable-for-segmentation.png)

## Ajouter vos relations {#add-relationship}

Maintenant que vous avez activé votre schéma pour la segmentation, vous pouvez continuer à créer votre schéma en définissant les relations pour les champs du schéma. Pour ajouter une relation au champ, sélectionnez **[!UICONTROL Add relationship]** dans le champ auquel vous souhaitez ajouter la relation.

![Le bouton Ajouter une relation est mis en surbrillance dans l’éditeur de schémas.](/help/rtcdp/assets/segmentation/custom-objects/select-add-relationship.png)

L’éditeur de relations s’affiche. Vous pouvez maintenant définir la relation entre le champ et les schémas.

![La fenêtre contextuelle Ajouter une relation s’affiche, montrant un exemple de relation terminée.](/help/rtcdp/assets/segmentation/custom-objects/add-relationship.png)

## Ingérer des données dans le jeu de données {#ingest-data}

>[!IMPORTANT]
>
>Vous **devez** inclure un fichier qui inclut un attribut `_change_request_type` dans la source, car cela indique à Experience Platform que les données seront utilisées pour les objets personnalisés. Si vous souhaitez insérer ou mettre à jour des données, définissez `_change_request_type` sur `u` pour l’upsert. Si vous souhaitez supprimer des données, définissez `_change_request_type` sur `d` pour suppression.

Une fois votre schéma entièrement créé, vous pouvez commencer à ingérer des données à partir de votre source dans le jeu de données.

Pour importer les données de votre source dans Experience Platform, vous devez créer un flux de données afin d’ingérer les données par lots de votre source dans le jeu de données . Les fournisseurs de sources de stockage dans le cloud suivants sont pris en charge : Amazon S3, SFTP, Data Landing Zone, Connecteur Marketo, Salesforce CRM, Microsoft Dynamics CRM et Connecteurs API HTTP.

>[!NOTE]
>
>Si vous utilisez le connecteur Marketo, le connecteur Marketo peut **automatiquement** créer le schéma pour l’objet personnalisé sélectionné si le schéma n’existe pas déjà.
>
>Le schéma créé comporte le préfixe `MKTO_CUST_OBJ_$(Custom object name)` et inclut par défaut primaryKey et versionDescriptors. Cependant, vous **devez** mettre à jour manuellement le schéma si des modifications sont requises, car les modifications apportées après la génération du schéma ne sont **pas** automatiquement appliquées.
>
>De la même manière que pour les autres connecteurs, vous **devez** activer le jeu de données pour la segmentation et configurer les relations.

Les données de votre source d’espace de stockage dans le cloud doivent être conformes aux spécifications suivantes :

- Le type de fichier est délimité (par exemple CSV ou TSV) ou JSON
- Le fichier contient une ligne par clé primaire
- Les noms des colonnes du fichier correspondent aux noms des champs du schéma

>[!NOTE]
>
>Lorsque vous créez votre flux de données, gardez les éléments suivants à l’esprit :
>
>- Vous **devez** activer **[!UICONTROL Enable change data capture]**.
>- Vous **devez** sélectionner le jeu de données que vous avez précédemment créé.
>- Vous n’avez **besoin** mapper le champ `_change_request_type` dans votre flux de données.
>- La fréquence d’ingestion peut atteindre une fois toutes les 15 minutes.

Pour plus d’informations sur la création d’un flux de données, consultez le guide [Configurer un flux de données pour ingérer des données par lot à partir d’une source d’espace de stockage](/help/sources/tutorials/ui/dataflow/batch/cloud-storage.md).

## Utilisation d’un objet personnalisé dans le Créateur d’audience {#use-custom}

Maintenant que votre flux de données a été créé, vous pouvez utiliser les données d’objet personnalisées dans le Créateur d’audience. Ces données d’objet personnalisées peuvent être utilisées à la fois pour les audiences de personnes et les audiences de comptes.

L’objet personnalisé se trouve sous **[!UICONTROL Attributes]** dans le Créateur d’audience et suit le même chemin de relation qui a été créé pour votre schéma d’objet personnalisé.

![L’objet personnalisé est mis en surbrillance dans le Créateur d’audience.](/help/rtcdp/assets/segmentation/custom-objects/audience-builder.png)

## Étapes suivantes {#next-steps}

Ce guide explique comment ajouter des objets personnalisés de relation un-à-plusieurs à B2B CDP ainsi que la manière d’utiliser les données d’objet personnalisées dans les cas d’utilisation de segmentation.

Pour en savoir plus sur le Créateur d’audience, consultez le [guide du créateur d’audience](./audience-builder.md).
