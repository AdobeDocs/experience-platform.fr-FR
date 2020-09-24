---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
title: Ajout de données à Real-time Customer Profile
topic: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes nécessaires à l’ajout de données dans Real-time Customer Profile.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 58%

---


# Add data to [!DNL Real-time Customer Profile]

This tutorial outlines the steps necessary to add data to [!DNL Real-time Customer Profile].

## Enable a schema for [!DNL Real-time Customer Profile]

Les données ingérées [!DNL Experience Platform] pour être utilisées par [!DNL Real-time Customer Profile] doivent être conformes à un schéma [!DNL Experience Data Model] (XDM) activé pour [!DNL Profile]. In order for a schema to be enabled for Profile, it must implement either the [!DNL XDM Individual Profile] or [!DNL XDM ExperienceEvent] class.

You can enable a schema for use in [!DNL Real-time Customer Profile] using the [!DNL Schema Registry] API or the [!DNL Schema Editor] user interface. Pour commencer, suivez les tutoriels de [Création d’un schéma à l’aide d’une API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

## Ajouter des données à l’aide de l’ingestion par lots

All data uploaded to [!DNL Platform] using batch ingestion is uploaded to individual datasets. Before this data can be used by [!DNL Real-time Customer Profile], the dataset in question has to be specifically configured. Pour obtenir des instructions complètes, reportez-vous au tutoriel sur la [Configuration d’un jeu de données pour Profile et Identity Service](dataset-configuration.md).

Une fois que le jeu de données a été configuré, vous pouvez commencer l’ingestion de données. Pour obtenir des instructions détaillées sur la manière de charger des fichiers dans différents formats, reportez-vous au [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

## Ajouter des données à l’aide de l’ingestion par flux

Any stream-ingested data that is compliant with a [!DNL Profile]-enabled XDM schema will automatically add or overwrite the appropriate record in [!DNL Real-time Customer Profile]. Si plusieurs identités sont fournies dans l’enregistrement ou si des données de série temporelle sont utilisées, ces identités sont mises en correspondance dans le graphique d’identités sans configuration supplémentaire. Pour en savoir plus, consultez le [guide de développement de l’ingestion par flux](../../ingestion/tutorials/streaming-record-data.md).

## Confirmer la réussite du chargement

Lors du premier chargement de données dans un nouveau jeu de données ou dans le cadre d’un processus impliquant une nouvelle source de données ou ETL, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées.

Using the [!DNL Real-time Customer Profile] Access API, you can retrieve batch data as it gets loaded into a dataset. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes.

For detailed instructions on how to access entities using the [!DNL Real-time Customer Profile] API, please refer to the [entities endpoint guide](../api/entities.md), also known as the &quot;[!DNL Profile Access] API&quot;.