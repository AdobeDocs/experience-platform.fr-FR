---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 'Ajouter les données au client en temps réel '
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# Ajouter les données au client en temps réel 

Ce didacticiel décrit les étapes nécessaires à l’ajout de données aux  de clients en temps réel.

## Activation d’un  pour le client en temps réel 

Les données en cours d’assimilation dans la plate-forme d’expérience pour une utilisation par le client en temps réel doivent être conformes à un de modèle de données d’expérience (XDM) qui est activé pour l’ de l’expérience. Pour qu’un soit activé pour l’ de, il doit implémenter la classe XDM Individuel ou XDM ExperienceEvent.

Vous pouvez activer un pour une utilisation dans le client en temps réel  à l’aide de l’API de registre de l’ ou de l’interface utilisateur de l’éditeur de. Pour commencer, suivez les didacticiels de [création d’un à l’aide d’API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un  à l’aide de l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md)de l’éditeur d’ deformulaire.

## Ajouter de données à l’aide de l’assimilation par lot

Toutes les données téléchargées sur la plate-forme à l’aide de l’assimilation par lot sont téléchargées dans des jeux de données individuels. Avant que ces données puissent être utilisées par le du client en temps réel, le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes, reportez-vous au didacticiel sur la [configuration d&#39;un jeu de données pour les  de et le service](dataset-configuration.md)d&#39;identité.

Une fois que le jeu de données a été configuré, vous pouvez à y importer des données. Pour obtenir des instructions détaillées sur la manière de télécharger des fichiers dans différents formats, reportez-vous au guide [du développeur d’assimilation de](../../ingestion/batch-ingestion/api-overview.md) lots.

## Ajouter de données à l’aide de l’assimilation en flux continu

Toute donnée imbriquée en flux continu et compatible avec un XDM compatible avec les   automatiquement ajouter ou remplacer l’enregistrement approprié dans lejournal en temps réel du client. Si plusieurs identités sont fournies dans l’enregistrement ou si des données de série chronologique sont utilisées, ces identités sont mises en correspondance dans le graphique d’identité sans configuration supplémentaire. Pour en savoir plus, consultez le guide [du développeur d’assimilation de](../../ingestion/tutorials/streaming-record-data.md) flux continu.

## Confirmer la réussite du transfert

Lors du premier chargement de données dans un nouveau jeu de données ou dans le cadre d’un processus impliquant une nouvelle ETL ou source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement téléchargées.

Grâce à l’API d’accès aux en temps réel, vous pouvez récupérer des données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer les entités que vous attendez, il se peut que votre jeu de données ne soit pas activé pour les  de. Une fois que vous avez confirmé que votre jeu de données a été activé, assurez-vous que le format et les identifiants des données source répondent à vos attentes.

Pour obtenir des instructions détaillées sur la façon d&#39;accéder aux entités à l&#39;aide de l&#39;API  client en temps réel, reportez-vous au [sous-guide sur les entités, également appelé &quot;API d&#39;accès &quot;](../api/entities.md).