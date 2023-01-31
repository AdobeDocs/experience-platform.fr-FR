---
title: Présentation de Data Distiller
description: Résumé des limites d’utilisation de Data Distiller pour les données de Query Service par rapport à vos droits de licence.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Présentation de Data Distiller

Data Distiller est une offre de package qui comprend un sous-ensemble des fonctionnalités de Adobe Experience Platform. Data Distiller vous permet d’effectuer une préparation des données post-ingestion (comme le nettoyage, la mise en forme et la manipulation) pour un profil client en temps réel ou des cas d’utilisation analytiques en exécutant des requêtes par lots dans Query Service. Votre utilisation de Data Distiller dépend de vos droits pour les applications basées sur Platform.

## Utilisation des licences {#license-usage}

Le  [Tableau de bord de l’utilisation des licences Data Distiller](./license-usage.md) est disponible une fois que vous avez acheté les heures de calcul de Data Distiller. Le tableau de bord de l’utilisation des licences vous permet de surveiller la consommation des heures de calcul autorisées. Voir [Document d’utilisation des licences Data Distiller](./license-usage.md) pour afficher des informations importantes sur l’utilisation des licences Query Service de votre entreprise.

## Paramètres de plage {#scoping-parameters}

Les paramètres de plage sont des limites d’utilisation liées à la portée de votre configuration requise et définies par votre capacité de licence. Sans modules complémentaires, les paramètres de portée du Distiller de données sont les suivants :

* **Heures de calcul**: Vous pouvez utiliser PSQL ou l’API Query Service pour exécuter des requêtes par lots exécutées dans n’importe quel environnement de test (planifié ou non) pour analyser et écrire des données. Cette opération utilise les heures calculées attribuées par an, telles qu’elles sont déterminées dans le processus de définition de la portée de votre contrat de licence. Total des heures de calcul est cumulé dans tous les environnements de test.
* **Données ingérées**: Les données ingérées dans Adobe Experience Platform qui peuvent être interrogées à l’aide de Data Distiller sont soumises aux limites décrites dans votre licence actuelle à Adobe Real-time Customer Data Platform, Customer Journey Analytics et/ou Adobe Journey Optimizer.
* **Stockage du lac de données**: Le stockage du lac de données fourni dans votre licence actuelle à Adobe Real-time Customer Data Platform, Customer Journey Analytics et/ou Adobe Journey Optimizer peut également être utilisé avec Data Distiller. Data Lake Storage est une fonctionnalité partagée.
* **Utilisateurs de Query Service**: Le nombre d’utilisateurs de Query Service décrit dans votre licence actuelle d’Adobe Real-time Customer Data Platform, de Customer Journey Analytics et/ou de Adobe Journey Optimizer peut également être utilisé avec Data Distiller. Les utilisateurs de Query Service sont une fonctionnalité partagée.

## Barrières de sécurité

Voir [Barrières de sécurité de Query Service](../guardrails.md) document concernant les limites d’utilisation par défaut des données de Query Service par rapport à vos droits de licence.

## Limites statiques

Une limite statique est la limite d’utilisation qui correspond aux limites fonctionnelles de l’activation de Adobe Experience Platform. [Informations supplémentaires sur l’activation de Adobe Experience Platform](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) se trouve dans les documents d’aide d’Adobe. Un résumé des limites statiques de Data Distiller est répertorié ci-dessous. Pour plus d’informations, reportez-vous au document de garde de Query Service.

* **Requêtes par lots**: Les requêtes par lots planifiées expirent au bout de 24 heures.
* **Query Service**: Vous pouvez utiliser Query Service aux fins suivantes :
   * Exécution de requêtes SQL pour l’analyse des données et la préparation des données après ingestion (nettoyage, mise en forme et manipulation).
   * Pour exécuter des requêtes SQL afin de créer des mesures de cumul à faire surface directement dans un outil de BI.
   * Pour inspecter rapidement les données dans Adobe Experience Platform.
   * Pour générer des informations significatives à partir de vos données.
* **Appel API de création de rapports**: Pour garantir que les requêtes s’exécutent sur des données agrégées à l’aide de l’API de création de rapports disposent de suffisamment de ressources pour s’exécuter efficacement. Cela inclut les requêtes qui améliorent les modèles de données existants tels que ceux fournis par Real-time Customer Data Platform. L’API de création de rapports effectue le suivi de l’utilisation des ressources en attribuant des emplacements simultanés à chaque requête. Au maximum 4 appels d’API de création de rapports sont disponibles simultanément. Si vous accédez à l’API de création de rapports par le biais d’un outil de BI et que vous avez besoin d’emplacements de simultanéité supplémentaires, un serveur de BI est requis.


