---
keywords: Experience Platform;query service;Query service;requête
title: Prise en main de Adobe Experience Platform Query Service
description: Une explication des étapes nécessaires pour utiliser entièrement Adobe Experience Platform Query Service
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---

# Prise en main de Adobe Experience Platform [!DNL Query Service] {#getting-started}

Utilisez Adobe Experience Platform Query Service pour exécuter des requêtes SQL sur des jeux de données ingérés, joindre des données provenant de plusieurs sources et générer des jeux de données dérivés pour les analyses, les workflows de machine learning ou le profil client en temps réel. Après l’ingestion de données, accédez à Query Service par le biais de l’interface utilisateur pour une analyse et une collaboration interactives ou par le biais de l’API pour une exécution de requête automatisée et programmatique.

## Conditions préalables {#prerequisites}

Avant de commencer à interroger des données, vérifiez que vous disposez des éléments suivants :

- **Autorisations requises** : votre compte utilisateur a accès à Query Service dans Experience Platform. Si le service n’est pas disponible dans l’interface utilisateur, consultez la [documentation sur les autorisations](../../access-control/home.md#permissions) et contactez votre administrateur système.
- **Ingestion des données** : vous avez ingéré des données dans Experience Platform.

Si vous devez ingérer des données, consultez le tutoriel vidéo [ingestion de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) pour obtenir un aperçu de la création de jeux de données, du mappage de schéma, de l’ingestion et de la validation. Lisez la [documentation de présentation de l’ingestion](../../ingestion/home.md) pour obtenir des informations plus détaillées et des liens vers d’autres ressources d’apprentissage.

## Chemins de démarrage rapide

Après avoir ingéré vos données dans Experience Platform, vous pouvez commencer à utiliser Query Service à l’aide de l’[!DNL Query Editor] d’Experience Platform ou de l’API Query Service.

### [!DNL Query Editor]

Utilisez le [!DNL Query Editor] pour l’analyse, l’exploration des données et le développement collaboratif de requêtes. Pour une présentation de la fonctionnalité de l’interface utilisateur, consultez la [documentation de l’interface utilisateur de Query Service](../ui/overview.md). Pour en savoir plus sur l’écriture et l’exécution de requêtes dans l’interface utilisateur, lisez la [[!DNL Query Editor user guide]](../ui/user-guide.md).

### API Query Service

Utilisez l’API Query Service pour les workflows automatisés, la gestion des modèles de requête et les intégrations de programmes. Reportez-vous au [guide de développement de Query Service](../api/getting-started.md) pour obtenir des instructions détaillées sur l’utilisation de l’API Query Service.

## Étapes suivantes

Ce document couvrait les conditions préalables requises pour utiliser les fonctionnalités de [!DNL Query Service] dans Experience Platform. Pour commencer rapidement à utiliser les fonctionnalités de Query Service, nous vous recommandons de lire les documents suivants :

- [Directives générales pour l’exécution des requêtes](../best-practices/writing-queries.md)
- [Syntaxe SQL dans Query Service](../sql/syntax.md)
- [Créer des jeux de données dérivés avec SQL](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

Vous pouvez également consulter la présentation du cas d’utilisation de navigation abandonnée [&#x200B; pour en savoir plus sur les avantages du traitement des données par Query Service dans Experience Platform](../use-cases/abandoned-browse.md#video-example).

Les ressources suivantes sont utiles pour améliorer votre compréhension des [!DNL Query Service] :

- [Présentation de l’interface utilisateur de [!DNL Query Service]](../ui/overview.md)
- [[!DNL Query Service] des informations d’identification](../ui/credentials.md)
- [Présentation des connexions client](../clients/overview.md)
