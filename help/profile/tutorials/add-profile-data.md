---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Ajouter de données au Profil client en temps réel
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Ajouter de données au Profil client en temps réel

Ce didacticiel décrit les étapes nécessaires pour ajouter des données au Profil client en temps réel.

## Activation d’un schéma pour le Profil client en temps réel

Les données en cours d’assimilation dans la plate-forme d’expérience pour une utilisation par le Profil client en temps réel doivent être conformes à un schéma de modèle de données d’expérience (XDM) activé pour le Profil. Pour qu&#39;un schéma soit activé pour le Profil, il doit implémenter soit le Profil individuel XDM, soit la classe XDM ExperienceEvent.

Vous pouvez activer un schéma à utiliser dans le Profil client en temps réel à l’aide de l’API de registre de Schéma ou de l’interface utilisateur de l’éditeur de Schémas. Pour commencer, suivez les didacticiels de [création d’un schéma à l’aide d’API](../../xdm/tutorials/create-schema-api.md) ou de [création d’un schéma à l’aide de l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md)de l’éditeur de Schémas.

## Ajouter de données à l’aide de l’assimilation par lots

Toutes les données téléchargées sur la plate-forme à l’aide de l’assimilation par lot sont téléchargées dans des jeux de données individuels. Avant que ces données puissent être utilisées par le Profil client en temps réel, le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes, consultez le didacticiel sur la [configuration d&#39;un jeu de données pour le Profil et le service](dataset-configuration.md)d&#39;identité.

Une fois que le jeu de données a été configuré, vous pouvez y début l&#39;assimilation de données. Pour obtenir des instructions détaillées sur la façon de télécharger des fichiers dans différents formats, consultez le guide [du développeur d’assimilation](../../ingestion/batch-ingestion/api-overview.md) par lot.

## Ajouter de données à l’aide de l’assimilation en flux continu

Les données imbriquées dans un flux qui sont conformes à un schéma XDM compatible avec le Profil ajoutent ou remplacent automatiquement l’enregistrement approprié dans le Profil client en temps réel. Si plusieurs identités sont fournies dans l&#39;enregistrement ou si des données de série chronologique sont utilisées, ces identités sont mises en correspondance dans le graphique d&#39;identité sans configuration supplémentaire. Pour en savoir plus, consultez le guide [du développeur d’assimilation](../../ingestion/tutorials/streaming-record-data.md) en flux continu.

## Confirmer la réussite du téléchargement

Lors du premier chargement de données dans un nouveau jeu de données, ou dans le cadre d’un processus impliquant une nouvelle ETL ou une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement téléchargées.

A l’aide de l’API d’accès au Profil client en temps réel, vous pouvez récupérer des données de lot lors de leur chargement dans un jeu de données. Si vous ne parvenez pas à récupérer l&#39;une des entités attendues, il se peut que votre jeu de données ne soit pas activé pour le Profil. Après avoir confirmé que votre jeu de données a été activé, veillez à ce que le format et les identifiants de vos données source répondent à vos attentes.

Pour obtenir des instructions détaillées sur l&#39;accès aux entités à l&#39;aide de l&#39;API Profil client en temps réel, consultez le [sous-guide Entités, également appelé &quot;API d&#39;accès au Profil&quot;](../api/entities.md).