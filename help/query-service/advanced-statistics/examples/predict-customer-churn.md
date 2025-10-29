---
title: Prédire l’attrition client avec une régression logistique basée sur SQL
description: Découvrez comment prédire l’attrition des clients à l’aide d’une régression logistique SQL. Ce guide couvre l’ensemble du processus, de la création du modèle à l’évaluation et la prédiction. Obtenez des informations exploitables sur le comportement d’achat des clients pour mettre en œuvre des stratégies de rétention proactives et optimiser les décisions commerciales.
exl-id: 3b18870d-104c-4dce-8549-a6818dc40d24
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# Prédire l’attrition client avec une régression logistique basée sur SQL

La prévision de l’attrition des clients aide les entreprises à fidéliser leurs clients, à optimiser leurs ressources et à stimuler leur rentabilité en améliorant leur satisfaction et leur fidélité grâce à des informations exploitables.

Découvrez comment utiliser la régression logistique SQL pour prédire l’attrition client. Utilisez ce guide SQL complet pour transformer les données d’e-commerce brutes en informations client significatives basées sur les mesures comportementales clés (telles que la fréquence d’achat, la valeur moyenne de la commande et la récence du dernier achat). Le document couvre l’ensemble du processus, de la préparation des données à l’ingénierie des fonctionnalités, en passant par la création, l’évaluation et la prédiction de modèles.

Utilisez ce guide pour créer un modèle puissant de prédiction de l’attrition qui identifie les clients à risque, affine les stratégies de fidélisation et oriente de meilleures décisions commerciales. Il comprend des instructions détaillées, des requêtes SQL et des explications détaillées pour vous aider à appliquer en toute confiance des techniques de machine learning dans votre environnement de données.

## Commencer

Avant de créer le modèle d’attrition, il est important d’explorer les principales fonctionnalités du client et les exigences en matière de données. Les sections suivantes décrivent les attributs essentiels du client et les champs de données requis pour une formation de modèle précise.

### Définir les fonctionnalités du client {#define-customer-features}

Pour classer précisément l’attrition, le modèle analyse les habitudes et les tendances d’achat. Le tableau ci-dessous décrit les principales fonctionnalités de comportement des clients utilisées dans le modèle :

| Fonctionnalité | Description |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Nombre total d’achats effectués par le client. |
| `total_revenue` | Chiffre d’affaires total généré par les achats des clients. |
| `avg_order_value` | Valeur moyenne des achats d’un client. |
| `customer_lifetime` | Nombre de jours écoulés entre le premier et le dernier achat du client. |
| `days_since_last_purchase` | Nombre de jours écoulés depuis le dernier achat du client. |
| `purchase_frequency` | Nombre de mois distincts au cours desquels le client a effectué des achats. |

### Hypothèses et champs obligatoires {#assumptions-required-fields}

Pour générer des prédictions de résiliation client, le modèle dépend des champs clés de la table `webevents` qui capturent les détails des transactions client. Votre jeu de données doit inclure les champs suivants :

| Champ | Description |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Identifiant unique utilisé pour effectuer le suivi des clients entre les sessions. |
| `productListItems.priceTotal[0]` | Coût total des articles achetés par transaction. |
| `productListItems.quantity[0]` | Nombre total d’articles dans un achat. |
| `timestamp` | La date et l’heure exactes de chaque événement d’achat. |
| `commerce.order.purchaseID` | Valeur requise qui confirme un achat terminé. |

Le jeu de données doit contenir des enregistrements de transaction client historiques structurés, chaque ligne représentant un événement d’achat. Chaque événement doit inclure des horodatages dans un format date-heure approprié compatible avec la fonction SQL `DATEDIFF` (par exemple, AAAA-MM-JJ HH:MI:SS). En outre, chaque enregistrement doit contenir un Experience Cloud ID valide (`ECID`) dans le champ `identityMap` pour identifier les clients de manière unique.

>[!TIP]
>
>Le traitement de jeux de données volumineux contenant des millions d’enregistrements peut avoir un impact significatif sur les performances. Pour optimiser l’exécution des requêtes, partitionnez le jeu de données d’expérience par horodatage, effectuez un traitement incrémentiel à l’aide d’instantanés et appliquez des fonctions d’agrégation efficaces si nécessaire. En outre, filtrez les données avant l’agrégation pour réduire la surcharge de traitement.

## Créer modèle {#create-a-model}

Pour prédire l’attrition des clients, vous devez créer un modèle de régression logistique basé sur SQL qui analyse l’historique des achats des clients et les mesures comportementales. Le modèle classe les clients en tant que `churned` ou `not churned` en déterminant s’ils ont effectué un achat au cours des 90 derniers jours.

### Utilisation de SQL pour créer le modèle de prédiction de résiliation {#sql-create-model}

Le modèle SQL traite les données `webevents` en agrégeant les mesures clés et en attribuant des libellés d’attrition en fonction d’une règle d’inactivité de 90 jours. Cette approche distingue les clients actifs des clients à risque. La requête SQL effectue également une ingénierie des fonctionnalités pour améliorer la précision du modèle et la classification de perte de clientèle. Ces informations permettent à votre entreprise de mettre en œuvre des stratégies de rétention ciblées, de réduire le taux de perte et d’optimiser la valeur pour la durée de vie du client.

>[!NOTE]
>
>Le modèle de prédiction de résiliation utilise un seuil par défaut de 90 jours pour classer les clients comme résiliés. Pour ajuster ce seuil afin qu’il s’aligne sur vos objectifs commerciaux et vos stratégies de rétention, modifiez la condition de `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` dans les requêtes SQL.

Utilisez l’instruction SQL suivante pour créer le modèle de `retention_model_logistic_reg` avec les fonctionnalités et les libellés spécifiés :

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Sortie du modèle {#model-output}

Le jeu de données de sortie contient des mesures liées aux clients et leur statut d’attrition. Chaque ligne représente un client, ses valeurs de fonction et son statut d’attrition. Vous pouvez utiliser cette sortie pour analyser le comportement des clients, entraîner des modèles prédictifs et développer des stratégies de fidélisation ciblées pour fidéliser les clients à risque. Un exemple de tableau de sortie est illustré ci-dessous :

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
|--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Colonne | Description |
|-----------|------------------------------------------------------------------------------------|
| `churned` | La valeur indique si le client a effectué un achat au cours des 90 derniers jours (0 = non résilié, 1 = résilié). |

## Utilisation de SQL pour évaluer le modèle {#model-evaluation}

Ensuite, évaluez le modèle de prédiction de l’attrition afin de déterminer son efficacité dans l’identification des clients à risque. Évaluez les performances du modèle à l’aide de mesures clés qui mesurent la précision et la fiabilité.

Pour mesurer la précision du modèle de `retention_model_logistic_reg` dans la prédiction de l’attrition client, utilisez la fonction `model_evaluate` . L’exemple SQL suivant évalue le modèle à l’aide d’un jeu de données structuré comme les données d’identification :

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Sortie d’évaluation de modèle

Le résultat de l’évaluation comprend des mesures de performances clés, telles que l’AUC-ROC, l’exactitude, la précision et le rappel. Ces mesures fournissent des informations sur l’efficacité des modèles que vous pouvez utiliser pour affiner les stratégies de rétention et prendre des décisions basées sur les données.

>[!NOTE]
>
>Les valeurs de performance vont de 0 à 1, où 1,0 représente une performance parfaite.

```console
 auc_roc | accuracy | precision | recall 
|---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Mesure | Description |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Cette mesure indique la capacité du modèle à faire la distinction entre les clients résiliés et non résiliés. Une valeur plus proche de 1 indique de meilleures performances. |
| `accuracy` | La mesure de précision représente la proportion de prédictions correctes, fournissant une mesure globale des performances du modèle. |
| `precision` | La précision indique la proportion de clients résiliés correctement identifiés et indique la fiabilité de la prédiction de résiliation. Une valeur élevée signifie moins de faux positifs. |
| `recall` | Le rappel mesure la capacité du modèle à identifier tous les clients réels résiliés. Une valeur de rappel élevée indique moins de clients de résiliation manqués. |

>[!NOTE]
>
>Les scores quasi parfaits dans cet exemple sont fournis à des fins de démonstration. Dans la pratique, les données réelles peuvent donner des valeurs inférieures en raison du bruit et de la variabilité.

## Prédiction de modèle {#model-prediction}

Une fois le modèle évalué, utilisez `model_predict` pour l’appliquer à un nouveau jeu de données et prévoir l’attrition du client. Vous pouvez utiliser ces prédictions pour identifier les clients à risque et mettre en œuvre des stratégies de fidélisation ciblées.

### Utilisation de SQL pour générer des prédictions de résiliation {#sql-model-predict}

La requête SQL ci-dessous utilise le modèle `retention_model_logistic_reg` pour prédire l’attrition du client avec un jeu de données structuré comme les données d’identification :

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Sortie de prédiction de modèle {#prediction-output}

Le jeu de données de sortie comprend les principales fonctionnalités client et leur statut de résiliation prédit, qui indique si un client est susceptible de résilier le contrat. Utilisez ces informations pour mettre en œuvre des stratégies de rétention proactives et réduire le taux de perte de clientèle.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
|-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Colonne | Description |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | Statut de résiliation prévu du client en fonction du modèle (0 = non résilié, 1 = résilié). |

## Étapes suivantes

Vous avez maintenant appris à créer, évaluer et utiliser un modèle SQL pour prédire l’attrition des clients. Grâce à cette base, vous pouvez analyser le comportement des clients, identifier les clients à risque et mettre en œuvre des stratégies de fidélisation proactives pour améliorer la fidélisation des clients. Pour améliorer et appliquer davantage votre modèle de prédiction de résiliation, tenez compte des étapes suivantes :

- Automatisez le processus : intégrez le modèle dans un pipeline de données pour une surveillance continue et des informations en temps réel. [Découvrez comment vérifier et traiter des jeux de données avec SQL](../../../dashboards/query.md).
- Surveiller les performances du modèle : évaluez continuellement le modèle avec de nouvelles données pour maintenir la précision et la pertinence.  Utilisez l’[assistant AI](../../../ai-assistant/landing.md) dans l’interface utilisateur de Adobe Experience Platform pour surveiller les modifications importantes des performances et [prévoir les tendances d’audience](../../../ai-assistant/new-features/audience-forecasting.md).
