---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Tutoriels sur Real-time Customer Profile
topic: tutorial
description: Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 49%

---


# Configurer [!DNL Real-time Customer Profile] et [!DNL Identity Service]

In order to configure [!DNL Real-time Customer Profile] for your organization, you are required to complete multiple separate workflows. Ce document décrit les étapes à suivre et fournit des liens vers des tutoriels pour effectuer chaque workflow séparément. To learn more about [!DNL Real-time Customer Profile], begin by reading the [Profile overview](../profile/home.md).

## Enable schema for [!DNL Profile] and [!DNL Identity]

Before data can be ingested into Adobe Experience Platform and used in the creation of [!DNL Real-time Customer Profiles], a schema must be created to provide the structure for the data that will be ingested and that schema must be enabled for use in [!DNL Profile] and Adobe Experience Platform [!DNL Identity Service]. For step-by-step instructions on creating a schema that is enabled for both [!DNL Profile] and [!DNL Identity Service], please refer to the tutorials for [creating a schema using the Schema Registry API](../xdm/tutorials/create-schema-api.md) or [creating a schema using the Schema Builder UI](../xdm/tutorials/create-schema-ui.md).

## Configure a dataset for [!DNL Profile] and [!DNL Identity]

To begin ingesting data into [!DNL Profile], you must have a dataset that has been properly configured for use with [!DNL Real-time Customer Profile] and [!DNL Identity Service]. Pour commencer, suivez le [tutoriel consacré à la configuration d’un jeu de données pour Profile et Identity Service](../profile/tutorials/dataset-configuration.md).

## Configuration des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. To work with merge policies in the [!DNL Platform] UI, visit the [merge policies user guide](../profile/ui/merge-policies.md). Pour utiliser des stratégies de fusion à l’aide de l’API Real-time Customer Profile, consultez le [guide de développement sur les stratégies de fusion](../profile/api/merge-policies.md).

## Configuration des projections de périphérie

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. Adobe [!DNL Experience Platform] enables this real-time access to data through the use of what are known as edges. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. For more information and to begin working with edges, refer to the [!DNL Real-time Customer Profile] API [sub-guide on edge projections](../profile/api/edge-projections.md).

## Étapes suivantes

Once you have configured [!DNL Real-time Customer Profile] for your organization, you can begin adding data to individual customer profiles and creating audience segments based on specific customer attributes. Pour commencer, consultez les tutoriels suivants :

* [Ajout de données à Real-time Customer Profile](../profile/tutorials/add-profile-data.md)
* [Création d’un segment](../segmentation/tutorials/create-a-segment.md)