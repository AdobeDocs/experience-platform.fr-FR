---
title: Détails du modèle de score de propension de l’IA dédiée aux clients
description: Découvrez le modèle d’IA utilisé pour l’IA dédiée aux clients.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: a7b69cd11ccbd9950cafa73dba51be1d67924bfe
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Détails du modèle de score de propension de l’IA dédiée aux clients

## Présentation du modèle {#model-overview}

* **Nom et version du modèle** : modèle de score de propension de l’IA dédiée aux clients
* **Objectif du modèle** : le modèle est conçu pour fournir aux spécialistes du marketing et aux équipes de l’engagement des clients des informations exploitables en prédisant la probabilité qu’un client effectue une action donnée, comme effectuer un achat, s’abonner ou participer à une campagne par e-mail. Les sorties permettent aux entreprises d’optimiser la segmentation de l’audience et de personnaliser les interactions des consommateurs en fonction des comportements prévus.
* **Utilisateurs prévus** : les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données et les équipes d’engagement des clients qui tirent parti de [Real-Time CDP](../../../rtcdp/home.md) pour piloter les stratégies marketing axées sur les données.
* **Cas d’utilisation** : ce modèle est principalement utilisé pour la segmentation des consommateurs, le marketing ciblé et la prédiction de l’attrition. Les entreprises tirent parti de ce modèle pour prédire les intentions d’achat des consommateurs, optimiser les campagnes marketing et améliorer les efforts de personnalisation. Par exemple, une société de commerce électronique peut utiliser le modèle pour identifier les acheteurs à forte intention et leur offrir des promotions exclusives.
* **Problèmes** : les professionnels du marketing ont souvent du mal à identifier les bons consommateurs à cibler et à optimiser les efforts d’engagement. Ce modèle réduit les conjectures en fournissant une approche axée sur les données au ciblage des consommateurs et consommatrices, tout en s’assurant que les ressources marketing sont allouées efficacement.
* **Mauvaise utilisation potentielle** : le modèle ne doit pas être utilisé pour les cas d’utilisation à haut risque, tels que la notation de crédit financier, les diagnostics médicaux ou les évaluations juridiques. En outre, le modèle ne doit pas être utilisé pour prédire les comportements personnellement sensibles (tels que les problèmes de santé, les préférences politiques).

## Détails du modèle {#model-details}

* **Type de modèle** : il s’agit d’un modèle de classification d’apprentissage supervisé qui prédit la probabilité qu’un événement se produise (tel que l’achat, l’attrition, l’engagement) à partir des données historiques du consommateur. Il est entraîné à l’aide d’arbres de décision boostant le gradient (GBDT) avec une régression logistique pour modéliser les scores de propension.
* **Entrée** : le modèle traite les données comportementales des consommateurs, les attributs démographiques et les interactions historiques. Cela inclut des données telles que la fréquence des visites du site web, l’historique des achats précédents, l’engagement dans les e-mails marketing et des informations démographiques.
* **Résultat** : le modèle génère un score compris entre 0 et 100, où des valeurs plus élevées indiquent une plus grande probabilité que l’événement prévu se produise dans la cohorte de population notée. En outre, il fournit des scores d’importance des fonctionnalités, ce qui permet aux spécialistes marketing de comprendre les facteurs qui ont influencé la prédiction.

**Exemple d’entrée**

```json
{ 
  "customer_id": 12345, 
  "past_purchases": 3, 
  "last_visit_days": 7,
  "email_click_rate": 0.4 
}
```

**Exemple de sortie**

```json
{ 
  "customer_id": 12345,
  "SCORE": 89 
}
```

## Modèle de formation {#model-training}

* **Entraînement des données et prétraitement** : le jeu de données d’entraînement de chaque client est directement issu de ses propres données dans Adobe Experience Platform. Cela inclut l’historique des interactions du client, les enregistrements transactionnels, les journaux d’engagement comportemental, ainsi que les informations démographiques telles que collectées et stockées dans son instance Adobe Experience Platform. Le jeu de données exploite les données spécifiques aux clients sur la période choisie, en capturant leurs tendances saisonnières uniques et leurs modèles d’engagement. Avant utilisation, le jeu de données de chaque client ou cliente subit un prétraitement adapté à ses caractéristiques de données, notamment la gestion des valeurs manquantes, le codage catégoriel, la mise à l’échelle des fonctionnalités, la détection des valeurs aberrantes et l’ingénierie des fonctionnalités afin d’assurer une qualité et une convivialité optimales pour son cas d’utilisation spécifique.
   * Les données client utilisées pour la formation ne sont pas utilisées entre les clients.
* **Spécifications de formation** : le modèle utilise des [!DNL LightGBM] à l’aide de [!DNL GBM], optimisées pour les données structurées. Il est entraîné sur des séquences d’événements client historiques pour identifier des modèles comportementaux prédictifs.
* **Framework de formation** : le modèle a été développé à l’aide de [!DNL LightGBM] et [!DNL scikit-learn], et est formé sur l’infrastructure cloud d’IA d’Adobe.
* **Infrastructures de formation** : clusters [!DNL Databricks].

## Évaluation de modèles {#model-evaluation}

* **Mesures et procédures d’évaluation** : l’efficacité du modèle est mesurée à l’aide de [!DNL AUC-ROC]. L’IA dédiée aux clients ciblant un très large éventail de cas d’utilisation client, sa plage d’exploitation ne peut pas être connue. Nous utilisons donc une [!DNL AUC] métrique indépendante de la portée et du budget.
* **Données d’évaluation et prétraitement** : les données d’évaluation comprennent les enregistrements de consommateurs retenues et sont prétraitées de la même manière que les données d’entraînement avec des étapes de normalisation des fonctionnalités, de codage et de nettoyage pour répondre aux attentes en matière de format d’entrée. Une fois la fenêtre de résultats dépassée, nous pouvons effectuer une évaluation finale des performances.

## Déploiement de modèles {#model-deployment}

* **Déploiement du modèle** : le modèle est hébergé sur les services d’IA de Adobe Experience Platform et intégré à diverses applications Adobe. Elle est disponible via des points d’entrée d’API, ce qui permet un accès transparent aux prédictions en temps réel et au traitement par lots dans les workflows de marketing et d’engagement des consommateurs.
* **Surveillance du modèle** : le modèle est surveillé en permanence via la surveillance du modèle pour voir la dérive par rapport à la configuration d’entraînement. Des remises à niveau périodiques (une fois tous les 3 mois) sont automatiquement exécutées.
* **Mise à jour du modèle** : le modèle est recyclé une fois par mois (le plus souvent une fois par mois) à l’aide de données d’interaction client mises à jour afin de garantir une pertinence continue. Le recyclage périodique aide à atténuer la dérive des données et les fluctuations saisonnières qui pourraient avoir une incidence sur la précision prédictive.

## Explicabilité {#explainability}

**Explicabilité du modèle** : le modèle utilise [!DNL SHapley Additive Explanations] (SHAP) pour quantifier l’impact de chaque fonctionnalité d’entrée sur ses prédictions, ce qui permet d’évaluer de manière transparente la manière dont les attributs du client influencent les scores de propension. Les valeurs SHAP permettent à la fois une interprétabilité globale, identifiant les facteurs les plus influents dans toutes les prédictions, et une interprétabilité locale, expliquant les prédictions individuelles pour des consommateurs spécifiques. Le modèle prend également en charge [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Équité et partialité {#fairness-and-bias}

* **Équité du modèle** : ce modèle est entraîné sur des données comportementales anonymisées associées aux ID de cookie, sans accès aux attributs démographiques protégés tels que l’âge, le sexe ou l’origine ethnique. Par conséquent, il n’est pas possible de mesurer directement l’équité entre les groupes sensibles. Les efforts de réduction des biais comprennent la normalisation de la fréquence d’activité des utilisateurs, la suppression des caractéristiques trop dominantes et la réalisation de contrôles d’étalonnage des scores entre les cohortes. Nous tenons compte du biais de récence et surveillons le biais d&#39;exposition en évaluant les prédictions du modèle sur le trafic d&#39;exclusion randomisé. Des évaluations continues sont en place pour détecter et réduire l&#39;amplification des biais et les boucles de rétroaction pendant le déploiement du modèle.
* **Biais de données** : le jeu de données est principalement issu d’utilisateurs à fort engagement, ce qui peut introduire un biais de sélection. Pour atténuer ce problème, le modèle applique des stratégies d’échantillonnage. Selon le cas d’utilisation, les clients doivent examiner la manière dont les biais potentiels dans les sorties du modèle peuvent s’aligner sur leur application prévue ou avoir une incidence sur celle-ci.

## Solidité {#robustness}

**Robustesse du modèle** : le modèle maintient une forte généralisation aux nouveaux enregistrements de consommateurs. Les performances restent stables sur différents segments de consommateurs, mais se dégradent légèrement lorsque le comportement des utilisateurs s’écarte considérablement des modèles historiques.

## Considérations éthiques {#ethical-considerations}

**Considérations éthiques associées au modèle** : ce modèle est destiné aux cas d’utilisation marketing. Les clients doivent donc faire preuve d’une prudence accrue s’ils l’appliquent à des domaines sensibles ou réglementés tels que le crédit ou l’emploi. Les extrants sont probabilistes et dérivés de données comportementales, qui peuvent refléter des biais historiques ou de représentation. Les clients sont encouragés à appliquer une supervision humaine. Adobe Experience Platform suit des directives d’IA responsable, en s’assurant que les modèles subissent des audits de biais, des tests d’équité et une supervision humaine avant leur déploiement. Pour plus d’informations, consultez les [Principes d’éthique de l’IA dans Adobe](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).