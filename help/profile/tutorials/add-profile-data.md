---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer le profil;Activer le profil
title: Ajout de données à Real-time Customer Profile
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes nécessaires à l’ajout de données dans Real-time Customer Profile.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 46%

---


# Ajout de données au [!DNL Real-time Customer Profile]

Ce tutoriel décrit les étapes nécessaires à l’ajout de données à [!DNL Real-time Customer Profile].

## Activation d’un schéma pour [!DNL Real-time Customer Profile]

Les données ingérées dans [!DNL Experience Platform] pour être utilisées par [!DNL Real-time Customer Profile] doivent être conformes à un schéma [!DNL Experience Data Model] (XDM) activé pour [!DNL Profile]. Pour qu’un schéma soit activé pour Profile, il doit mettre en oeuvre la classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Vous pouvez activer un schéma à utiliser dans [!DNL Real-time Customer Profile] à l’aide de l’API [!DNL Schema Registry] ou de l’interface utilisateur [!DNL Schema Editor]. Pour commencer, suivez les tutoriels de [Création d’un schéma à l’aide d’une API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

## Ajouter des données à l’aide de l’ingestion par lots

Toutes les données chargées dans [!DNL Platform] à l’aide de l’ingestion par lots sont chargées dans des jeux de données individuels. Avant que ces données puissent être utilisées par [!DNL Real-time Customer Profile], le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes, reportez-vous au tutoriel sur la [Configuration d’un jeu de données pour Profile et Identity Service](dataset-configuration.md).

Une fois que le jeu de données a été configuré, vous pouvez commencer l’ingestion de données. Pour obtenir des instructions détaillées sur la manière de charger des fichiers dans différents formats, reportez-vous au [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

## Ajouter des données à l’aide de l’ingestion par flux

Toutes les données ingérées par flux qui sont conformes à un schéma XDM compatible [!DNL Profile] ajouteront ou remplaceront automatiquement l’enregistrement approprié dans [!DNL Real-time Customer Profile]. Si plusieurs identités sont fournies dans l’enregistrement ou si des données de série temporelle sont utilisées, ces identités sont mises en correspondance dans le graphique d’identités sans configuration supplémentaire. Pour en savoir plus, consultez le [guide de développement de l’ingestion par flux](../../ingestion/tutorials/streaming-record-data.md).

## Confirmer la réussite du chargement

Lors du premier chargement de données dans un nouveau jeu de données ou dans le cadre d’un processus impliquant une nouvelle source de données ou ETL, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées.

À l’aide de l’API d’accès [!DNL Real-time Customer Profile], vous pouvez récupérer les données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes.

Pour obtenir des instructions détaillées sur la manière d’accéder aux entités à l’aide de l’API [!DNL Real-time Customer Profile], reportez-vous au [guide de point d’entrée des entités](../api/entities.md), également appelé API &quot;[!DNL Profile Access]&quot;.

## Mise à jour des données de banque de profils

Il peut parfois être nécessaire de mettre à jour les données dans la banque de profils de votre entreprise. Par exemple, vous devrez peut-être corriger des enregistrements ou modifier une valeur d’attribut. Pour ce faire, vous pouvez procéder à l’ingestion par lots ou par flux, ce qui nécessite un jeu de données activé par Profile configuré avec une balise upsert. Pour plus d’informations sur la configuration d’un jeu de données pour les mises à jour d’attributs, reportez-vous au tutoriel [Activation d’un jeu de données pour Profile et upsert](../../catalog/datasets/enable-upsert.md).
