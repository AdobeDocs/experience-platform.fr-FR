---
title: Carte de modèle de score de propension à l’IA dédiée aux clients
description: Découvrez le modèle d’IA utilisé pour l’IA dédiée aux clients.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 63d95be281d1bc3867e4e24b9e7aadeecc64ac52
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 7%

---

# Carte de modèle de score de propension à l’IA dédiée aux clients

## Présentation du modèle {#model-overview}

* Le modèle de score de propension de l’IA dédiée aux clients est conçu pour fournir aux spécialistes marketing et aux équipes de l’engagement des clients des informations exploitables en prédisant la probabilité qu’un client effectue une action donnée, comme effectuer un achat, s’inscrire à une campagne par e-mail ou interagir avec une campagne par e-mail. Les sorties permettent aux entreprises d’optimiser la segmentation de l’audience et de personnaliser les interactions des clients en fonction des comportements prévus.
* Les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données et les équipes d’engagement des clients qui tirent parti de [Real-Time CDP](../../../rtcdp/home.md) pour piloter des stratégies marketing axées sur les données.
* Ce modèle est principalement utilisé pour la segmentation de la clientèle, le marketing ciblé et la prédiction de l’attrition. Les entreprises tirent parti de ce modèle pour prédire les intentions d’achat des clients, optimiser les campagnes marketing et améliorer les efforts de personnalisation. Par exemple, une société de commerce électronique peut utiliser le modèle pour identifier les acheteurs à forte intention et leur offrir des promotions exclusives.
* Les professionnels du marketing ont souvent du mal à identifier les bons clients à cibler et à optimiser les efforts d’engagement. Ce modèle réduit les hypothèses en offrant une approche axée sur les données au ciblage des clients, garantissant ainsi que les ressources marketing sont allouées efficacement.
* Le modèle ne doit pas être utilisé pour la prise de décision à haut risque, comme la notation du crédit financier, les diagnostics médicaux ou les évaluations juridiques. En outre, il n&#39;est pas destiné à être utilisé pour prédire les comportements personnellement sensibles (p. ex., les états de santé, les préférences politiques) en raison de préoccupations éthiques potentielles.

## Détails du modèle {#model-details}

* Il s’agit d’un modèle de classification d’apprentissage supervisé qui prédit la probabilité qu’un événement se produise (achat, résiliation, engagement) à partir des données client historiques. Il est entraîné à l’aide d’arbres de décision boostant le gradient (GBDT) avec une régression logistique pour modéliser les scores de propension.
* Le modèle traite les données comportementales des clients, les attributs démographiques et les interactions historiques. Cela inclut des données telles que la fréquence des visites du site web, l’historique des achats précédents, l’engagement dans les e-mails marketing et des informations démographiques.
* Le modèle produit un score compris entre 0 et 100, où des valeurs plus élevées indiquent une plus grande probabilité que l’événement prédit se produise dans la cohorte de population notée. En outre, il fournit des scores d’importance de la fonctionnalité, ce qui permet aux utilisateurs et utilisatrices de comprendre les facteurs qui ont influencé la prédiction.

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

* Le jeu de données de formation de chaque client est directement issu de ses propres données dans Experience Platform. Cela inclut les interactions historiques du client, les enregistrements transactionnels, les logs d’engagement comportemental et les informations démographiques telles que collectées et stockées dans son instance Experience Platform. Le jeu de données exploite les données spécifiques aux clients sur la période choisie, en capturant leurs tendances saisonnières uniques et leurs modèles d’engagement. Avant utilisation, le jeu de données de chaque client ou cliente subit un prétraitement adapté à ses caractéristiques de données, notamment la gestion des valeurs manquantes, le codage catégoriel, la mise à l’échelle des fonctionnalités, la détection des valeurs aberrantes et l’ingénierie des fonctionnalités afin d’assurer une qualité et une convivialité optimales pour son cas d’utilisation spécifique.
* Le modèle exploite les [!DNL LightGBM] à l’aide de [!DNL GBM], optimisées pour les données structurées. Il est entraîné sur des séquences d’événements client historiques pour identifier des modèles comportementaux prédictifs.
* Le modèle a été développé à l’aide de [!DNL LightGBM] et [!DNL scikit-learn], et est entraîné sur l’infrastructure cloud d’IA d’Adobe.
* Les ressources informatiques utilisées pour la formation des modèles sont des clusters [!DNL Databricks].

## Évaluation de modèles {#model-evaluation}

* L’efficacité du modèle est mesurée à l’aide de [!DNL AUC-ROC]. L’IA dédiée aux clients ciblant un très large éventail de cas d’utilisation client, sa plage d’exploitation ne peut pas être connue. Par conséquent, la mesure [!DNL AUC] est utilisée, car elle est indépendante de la portée et du budget.
* Les données d’évaluation comprennent les enregistrements de clients qui ne sont pas sélectionnés et sont prétraitées de la même manière que les données d’identification avec des étapes de normalisation, de codage et de nettoyage des fonctionnalités pour répondre aux attentes en matière de format d’entrée. Une fois la fenêtre de résultats dépassée, l’évaluation finale des performances peut être effectuée.

## Déploiement de modèles {#model-deployment}

* Le modèle est hébergé sur les services d’IA d’Experience Platform et intégré à diverses applications Adobe. Elle est disponible via des points d’entrée d’API, ce qui permet un accès transparent aux prédictions en temps réel et au traitement par lots dans les workflows de marketing et d’engagement client.
* Le modèle est surveillé en permanence par le biais de la surveillance du modèle pour voir la dérive de la configuration d’entraînement. Des remises à niveau périodiques (une fois tous les 3 mois) sont automatiquement effectuées.
* Le modèle est entraîné une fois tous les plusieurs mois (au maximum une fois tous les 6 mois) à l’aide de données d’interaction client mises à jour pour garantir une pertinence continue. Le recyclage périodique aide à atténuer la dérive des données et les fluctuations saisonnières qui pourraient avoir une incidence sur la précision prédictive.

## Explicabilité {#explainability}

Le modèle utilise [!DNL SHapley Additive Explanations] (SHAP) pour quantifier l’impact de chaque fonctionnalité d’entrée sur ses prédictions, ce qui permet d’évaluer de manière transparente la manière dont les attributs du client influencent les scores de propension. Les valeurs SHAP permettent à la fois l’interprétabilité globale, en identifiant les facteurs les plus influents dans toutes les prédictions, et l’interprétabilité locale, en expliquant les prédictions individuelles pour des clients spécifiques. Le modèle prend également en charge [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Équité et partialité {#fairness-and-bias}

* Ce modèle est entraîné sur des données comportementales anonymisées associées aux ID de cookie, sans accès aux attributs démographiques protégés tels que l’âge, le sexe ou l’origine ethnique. Par conséquent, il n’est pas possible de mesurer directement l’équité entre les groupes sensibles. Les efforts de réduction des biais comprennent la normalisation de la fréquence d’activité des utilisateurs, la suppression des caractéristiques trop dominantes et la réalisation de contrôles d’étalonnage des scores entre les cohortes.
* Le modèle tient compte du biais de récence et surveille le biais d&#39;exposition en évaluant les prédictions du modèle sur le trafic d&#39;exclusion randomisé. Des évaluations continues sont en place pour détecter et réduire l&#39;amplification des biais et les boucles de rétroaction pendant le déploiement du modèle.
* Le jeu de données est principalement fourni par des utilisateurs à fort engagement, ce qui peut introduire un biais de sélection. Pour atténuer ce problème, le modèle applique des stratégies d’échantillonnage.

## Solidité {#robustness}

Le modèle conserve une forte généralisation aux nouveaux enregistrements de clients. Les performances restent stables sur différents segments de clientèle, mais se dégradent légèrement lorsque le comportement des utilisateurs s’écarte considérablement des modèles historiques.

## Considérations relatives à la confidentialité et la sécurité {#privacy-and-security-considerations}

* Le modèle ne traite ni ne conserve aucune information d’identification personnelle (PII) et toutes les données utilisées pour la formation sont anonymisées et agrégées. Elle respecte strictement les politiques de confidentialité du RGPD, du CCPA et d’Adobe interne. Le modèle incorpore des techniques de confidentialité différentielles, de hachage, d’anonymisation et de tokenisation pour garantir la confidentialité.
* L’IA dédiée aux clients respecte vos préférences de consentement. Une fois que vous avez [configuré et activé votre politique de consentement](../../../data-governance/policies/user-guide.md#create-a-consent-policy), l’IA dédiée aux clients respecte les données de consentement collectées auprès de vous. Seules les données consenties sont utilisées pour évaluer le modèle lors des exécutions suivantes du modèle. Les nouveaux scores remplacent les anciens scores et peuvent être utilisés dans la segmentation. Actuellement, cette fonctionnalité n’est disponible que pour les clients et clientes de HealthCare Shield, ainsi que pour les clients Privacy and Security Shield.

## Considérations éthiques {#ethical-considerations}

Le modèle pourrait introduire un biais dans la prise de décision. Afin d’éviter cela, Experience Platform suit les directives d’IA responsable , en veillant à ce que les modèles soient soumis à des audits des préjugés, des tests d’équité et une supervision humaine avant leur déploiement.
