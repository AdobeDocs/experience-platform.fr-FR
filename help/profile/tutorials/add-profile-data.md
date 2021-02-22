---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API ; activer le profil ; Activer le profil
title: Ajouter les données au Profil client en temps réel
topic: didacticiel
type: Tutoriel
description: Ce tutoriel décrit les étapes nécessaires à l’ajout de données dans Real-time Customer Profile.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 54%

---


# Ajouter les données à [!DNL Real-time Customer Profile]

Ce didacticiel décrit les étapes nécessaires pour ajouter des données à [!DNL Real-time Customer Profile].

## Activer un schéma pour [!DNL Real-time Customer Profile]

Les données ingérées dans [!DNL Experience Platform] pour être utilisées par [!DNL Real-time Customer Profile] doivent être conformes à un schéma [!DNL Experience Data Model] (XDM) activé pour [!DNL Profile]. Pour qu&#39;un schéma soit activé pour le Profil, il doit implémenter la classe [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Vous pouvez activer un schéma à utiliser dans [!DNL Real-time Customer Profile] à l&#39;aide de l&#39;API [!DNL Schema Registry] ou de l&#39;interface utilisateur [!DNL Schema Editor]. Pour commencer, suivez les tutoriels de [Création d’un schéma à l’aide d’une API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un schéma à l’aide de l’interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

## Ajouter des données à l’aide de l’ingestion par lots

Toutes les données transférées vers [!DNL Platform] à l&#39;aide de l&#39;assimilation par lot sont transférées vers des jeux de données individuels. Pour que [!DNL Real-time Customer Profile] puisse utiliser ces données, le jeu de données en question doit être configuré spécifiquement. Pour obtenir des instructions complètes, reportez-vous au tutoriel sur la [Configuration d’un jeu de données pour Profile et Identity Service](dataset-configuration.md).

Une fois que le jeu de données a été configuré, vous pouvez commencer l’ingestion de données. Pour obtenir des instructions détaillées sur la manière de charger des fichiers dans différents formats, reportez-vous au [guide de développement de l’ingestion par lots](../../ingestion/batch-ingestion/api-overview.md).

## Ajouter des données à l’aide de l’ingestion par flux

Toute donnée imbriquée dans un flux qui est conforme à un schéma XDM compatible [!DNL Profile] ajoute ou remplace automatiquement l&#39;enregistrement approprié dans [!DNL Real-time Customer Profile]. Si plusieurs identités sont fournies dans l’enregistrement ou si des données de série temporelle sont utilisées, ces identités sont mises en correspondance dans le graphique d’identités sans configuration supplémentaire. Pour en savoir plus, consultez le [guide de développement de l’ingestion par flux](../../ingestion/tutorials/streaming-record-data.md).

## Confirmer la réussite du chargement

Lors du premier chargement de données dans un nouveau jeu de données ou dans le cadre d’un processus impliquant une nouvelle source de données ou ETL, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées.

L&#39;API d&#39;accès [!DNL Real-time Customer Profile] vous permet de récupérer des données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités attendues, il se peut que votre jeu de données ne soit pas activé pour [!DNL Profile]. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données sources répondent à vos attentes.

Pour obtenir des instructions détaillées sur la façon d&#39;accéder aux entités à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], consultez le [guide des points de terminaison des entités](../api/entities.md), également appelé &quot;[!DNL Profile Access] API&quot;.