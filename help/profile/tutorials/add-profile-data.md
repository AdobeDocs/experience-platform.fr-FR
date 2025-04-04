---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer le profil;Activer le profil
title: Ajout de données au profil client en temps réel
type: Tutorial
description: Ce tutoriel décrit les étapes nécessaires pour ajouter des données au profil client en temps réel.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 59%

---


# Ajout de données aux [!DNL Real-Time Customer Profile]

Ce tutoriel décrit les étapes nécessaires pour ajouter des données à [!DNL Real-Time Customer Profile].

## Activation d’un schéma pour [!DNL Real-Time Customer Profile]

Les données en cours d’ingestion dans [!DNL Experience Platform] pour être utilisées par [!DNL Real-Time Customer Profile] doivent être conformes à un schéma [!DNL Experience Data Model] (XDM) activé pour [!DNL Profile]. Pour qu’un schéma soit activé pour Profile, il doit implémenter la classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Vous pouvez activer un schéma à utiliser dans [!DNL Real-Time Customer Profile] à l’aide de l’API [!DNL Schema Registry] ou de l’interface utilisateur [!DNL Schema Editor]. Pour commencer, suivez les tutoriels de [Création d’un schéma à l’aide d’une API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

## Ajouter des données à l’aide de l’ingestion par lots

Toutes les données chargées vers [!DNL Experience Platform] à l’aide de l’ingestion par lots sont chargées dans des jeux de données individuels. Avant que ces données puissent être utilisées par [!DNL Real-Time Customer Profile], le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes, reportez-vous au tutoriel sur la [Configuration d’un jeu de données pour le profil et le service d’identités](dataset-configuration.md).

Une fois que le jeu de données a été configuré, vous pouvez commencer l’ingestion de données. Pour obtenir des instructions détaillées sur la manière de charger des fichiers dans différents formats, reportez-vous au [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

## Ajouter des données à l’aide de l’ingestion par flux

Toutes les données ingérées par le flux conformes à un schéma XDM compatible avec le [!DNL Profile] ajouteront ou remplaceront automatiquement l’enregistrement approprié dans [!DNL Real-Time Customer Profile]. Si plusieurs identités sont fournies dans l’enregistrement ou si des données de série temporelle sont utilisées, ces identités sont mises en correspondance dans le graphique d’identités sans configuration supplémentaire. Pour en savoir plus, consultez le [guide de développement de l’ingestion par flux](../../ingestion/tutorials/streaming-record-data.md).

## Confirmer la réussite du chargement

Lors du premier chargement de données dans un nouveau jeu de données ou dans le cadre d’un processus impliquant une nouvelle source de données ou ETL, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées.

Grâce à l’API Access [!DNL Real-Time Customer Profile], vous pouvez récupérer des données de lots lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes.

Pour obtenir des instructions détaillées sur l’accès aux entités à l’aide de l’API [!DNL Real-Time Customer Profile], reportez-vous au guide de point d’entrée des [entités](../api/entities.md), également appelé « API [!DNL Profile Access] ».

## Mettre à jour les données du magasin de profils

Il peut parfois être nécessaire de mettre à jour les données du magasin de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../../catalog/datasets/enable-upsert.md).
