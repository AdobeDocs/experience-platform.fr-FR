---
title: Carte de modèle de score de propension à l’IA dédiée aux clients
description: Découvrez le modèle d’IA utilisé pour l’IA dédiée aux clients.
hide: true
hidefromtoc: true
source-git-commit: 21a95bd678cf83c72a08213b647ef778cfb49cfc
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# Carte de modèle de score de propension à l’IA dédiée aux clients

Dans le cadre des [Services intelligents dans Adobe Experience Platform](../../../intelligent-services/home.md), vous pouvez utiliser [IA dédiée aux clients](../../../intelligent-services/customer-ai/overview.md) pour générer des prédictions et des explications des clients au niveau individuel.

À l’aide de facteurs d’influence, vous pouvez utiliser Customer AI pour savoir ce qu’un client est susceptible de faire et pourquoi. En outre, vous pouvez tirer parti des prédictions et des informations de l’IA dédiée aux clients pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés.

Lisez cette carte modèle pour plus d’informations sur le modèle d’IA utilisé pour alimenter l’IA dédiée aux clients.

## Présentation du modèle {#model-overview}

* L’IA dédiée aux clients est un modèle optimisé par l’IA conçu pour générer des scores de propension pour les utilisateurs en fonction de leurs comportements et interactions passés avec une entreprise. Utilisez l’IA dédiée aux clients pour prédire la probabilité qu’un client ou une cliente effectue des actions spécifiques, telles qu’un achat, interagisse avec le contenu ou la résiliation. Ce modèle est déployé dans Experience Platform et s’intègre à divers workflows de marketing et d’analyse client.
* Le modèle est conçu pour fournir aux professionnels du marketing et aux équipes de l’engagement client des informations exploitables en prédisant la probabilité qu’un client effectue une action donnée, comme effectuer un achat, s’inscrire à un abonnement ou participer à une campagne par e-mail. Les sorties permettent aux entreprises d’optimiser la segmentation de l’audience et de personnaliser les interactions des clients en fonction des comportements prévus.
* Il s’agit d’un **modèle de classification d’apprentissage supervisé** qui prédit la probabilité qu’un événement se produise (achat, perte, engagement) à partir des données client historiques. Il est entraîné à l’aide d’arbres de décision boostant le gradient (GBDT) avec une régression logistique pour modéliser les scores de propension.
* Les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données et les équipes d’engagement des clients qui tirent parti d’Experience Platform pour piloter les stratégies marketing axées sur les données.
* L’IA dédiée aux clients s’intègre directement aux services d’IA d’Experience Platform, ce qui permet aux utilisateurs d’accéder aux sorties du modèle par le biais d’API et de tableaux de bord préconfigurés. Les scores de propension générés par le modèle peuvent être utilisés dans [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) et [Real-Time CDP](../../../rtcdp/home.md) afin d’affiner la segmentation de l’audience et d’adapter les stratégies marketing.

## Utilisation prévue {#intended-use}

* Ce modèle est principalement utilisé pour la **segmentation de la clientèle, le marketing ciblé et la prédiction de l’attrition**. Les entreprises tirent parti de ce modèle pour **prédire les intentions d’achat des clients et clientes, optimiser les campagnes marketing et améliorer les efforts de personnalisation**. Par exemple, une société de commerce électronique peut utiliser le modèle pour identifier les acheteurs à forte intention et leur offrir des promotions exclusives.
* Les professionnels du marketing ont souvent du mal à **identifier les bons clients à cibler** et **optimiser les efforts d’engagement**. Ce modèle **réduit les conjectures** en offrant une approche axée sur les données au ciblage des clients et clientes, tout en s’assurant que les ressources marketing sont allouées efficacement.
* Le modèle s’applique à plusieurs secteurs, notamment le commerce électronique, la vente au détail, les services financiers, les télécommunications et les médias. Toute entreprise reposant sur l’engagement des clients et le marketing personnalisé peut bénéficier de ce modèle.
* Le modèle **ne doit pas être utilisé pour la prise de décision à haut risque** comme la notation financière du crédit, les diagnostics médicaux ou les évaluations juridiques. En outre, il n&#39;est pas destiné à être utilisé pour prédire les comportements personnellement sensibles (état de santé, préférences politiques) en raison de préoccupations éthiques potentielles.

## Entrées et sorties du modèle {#model-inputs-and-outputs}

* Le modèle traite les données comportementales des clients, les attributs démographiques et les interactions historiques. Cela inclut des données telles que la fréquence des visites du site web, l’historique des achats précédents, l’engagement dans les e-mails marketing et des informations démographiques.
* Les données d’entrée doivent être structurées en tant qu’objets JSON contenant des attributs du client et des signaux comportementaux. Pour le traitement par lots, le modèle accepte les fichiers CSV formatés conformément aux normes d’ingestion de données d’Experience Platform.
* Le modèle produit un score de propension compris entre 0 et 1, où des valeurs plus élevées indiquent une plus grande probabilité que l&#39;événement prédit se produise. En outre, il fournit des scores d’importance de la fonctionnalité, ce qui permet aux utilisateurs et utilisatrices de comprendre les facteurs qui ont influencé la prédiction.

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
  "propensity_score": 0.82
}
```

## Données d’apprentissage

* Le modèle a été entraîné sur des **données d’interaction client propriétaires et anonymes** collectées via Experience Platform. Il comprend des données historiques sur les clients **données comportementales, enregistrements de transactions, interactions d’e-mails et mesures d’engagement** dans plusieurs secteurs d’activité.
* Le jeu de données de formation se compose de 10 millions d’enregistrements client **** provenant d’un ensemble diversifié de clients Experience Platform. Ces enregistrements comprennent les **interactions client historiques, données transactionnelles, journaux d’engagement comportemental et informations démographiques** provenant de divers secteurs tels que la vente au détail, le commerce électronique, les télécommunications et la finance. Les données ont été recueillies sur une période de 24 mois, ce qui a permis d&#39;obtenir une représentation suffisante des tendances saisonnières et des modèles d&#39;engagement à long terme.
* Le jeu de données est principalement fourni par des utilisateurs à fort engagement, ce qui peut introduire un biais de sélection. Pour atténuer ce problème, le modèle applique un échantillonnage stratifié, des techniques de vérification des biais et des stratégies d’augmentation des données.
* Le jeu de données subit un prétraitement complet pour garantir la cohérence, la qualité et la convivialité des données.
   * **Gestion des valeurs manquantes** : les valeurs manquantes sont traitées à l’aide d’une combinaison d’imputation moyenne (pour les champs numériques), d’imputation de mode (pour les champs catégoriels) et de modélisation prédictive (pour les cas manquants complexes).
   * **Codage catégoriel** : les variables catégorielles telles que les segments de clients et de clientes et les catégories d’achat sont converties en représentations numériques par le biais de techniques de codage à accès unique et de codage cible.
   * **Mise à l’échelle et normalisation des caractéristiques** : la mise à l’échelle minimale et maximale est appliquée aux variables limitées (âge, revenu), tandis que la normalisation du score z est utilisée pour les caractéristiques normalement distribuées.
   * **Prétraitement supplémentaire** : le pipeline comprend la détection et la suppression des valeurs aberrantes, le filtrage des doublons, la normalisation de l’horodatage et l’ingénierie des fonctionnalités pour améliorer la modélisation prédictive.

## Architecture du modèle et formation

* Le modèle exploite **[!DNL Gradient Boosting Decision Trees](GBDT) à l’aide de[!DNL XGBoost]**, optimisées pour les données structurées. Il est entraîné sur des séquences d’événements client historiques pour identifier des modèles comportementaux prédictifs.
* Le modèle est construit à l&#39;aide d&#39;une approche d&#39;apprentissage supervisée, en utilisant le GBDT avec le [!DNL XGBoost] comme algorithme d&#39;apprentissage primaire. De plus, la régression logistique est incorporée comme modèle de référence pour l&#39;évaluation comparative de la précision prédictive.
* Le modèle a été développé à l’aide de **[!DNL TensorFlow]**, **[!DNL XGBoost]** et **[!DNL scikit-learn]**. La formation s’exécute sur l’infrastructure cloud d’Adobe AI à l’aide de GPU **[!DNL NVIDIA V100]** prenant en charge les jeux de données à grande échelle.
* [!DNL NVIDIA V100 GPUs], formé sur l’infrastructure cloud de Google.
* [!DNL AUC-ROC], rappel de précision et validation croisée.

## Performance et évaluation

* Le modèle a été testé en utilisant une approche de validation d’exclusion, où 80 % des données ont été utilisées pour la formation et 20 % ont été réservées à l’évaluation.
* L&#39;efficacité du modèle est mesurée à l&#39;aide de [!DNL AUC-ROC] (0,85), précision-rappel (0,78) et score F1 (0,80). Ces mesures permettent d’évaluer la puissance prédictive du modèle sur différents segments.
* Précision moindre pour les nouveaux segments de clientèle avec des données historiques limitées.
* Le modèle peut être sous-performant pour les clients avec des données historiques limitées (problème de démarrage à froid). En outre, les effets de saisonnalité (tendances des achats de vacances) peuvent nécessiter un recyclage fréquent pour maintenir la précision.

## Équité et partialité

* Le modèle a été soumis à des **tests de parité démographique** et **évaluations de l’équité contradictoires** afin de détecter les disparités de rendement entre les différents segments d’utilisateurs.
* L’analyse a révélé une baisse de performances de **5 % pour les utilisateurs disposant de faibles données historiques d’interaction**. Pour y remédier, le modèle incorpore des techniques de repondération pendant la formation.
* L’ensemble de données est stratifié afin d’assurer une représentation proportionnelle des différentes données démographiques des clients, et des contraintes d’équité sont introduites au cours de la formation afin d’empêcher le modèle de favoriser un groupe particulier. Des vérifications régulières des biais sont effectuées à l’aide d’une analyse de parité démographique, permettant des ajustements si des disparités de rendement sont détectées.

## Explicabilité et interprétabilité

* Le modèle utilise **[!DNL SHapley Additive Explanations](SHAP)** pour quantifier l’impact de chaque fonctionnalité d’entrée sur ses prédictions, ce qui permet d’évaluer de manière transparente la manière dont les attributs du client influencent les scores de propension. Les valeurs SHAP permettent à la fois l’interprétabilité globale, en identifiant les facteurs les plus influents dans toutes les prédictions, et l’interprétabilité locale, en expliquant les prédictions individuelles pour des clients spécifiques.
* Le modèle prend en charge **[!DNL Local Interpretable Model-Agnostic Explanations](LIME)** et SHAP pour fournir des informations sur la manière dont les fonctionnalités d’entrée influencent les prédictions. LIME génère des explications locales en créant des versions perturbées des données d&#39;entrée et en observant les changements dans les prédictions, tandis que SHAP attribue des valeurs de contribution à chaque caractéristique, offrant à la fois une interprétabilité globale et locale des décisions de modèle.

## Robustesse et généralisation

* Le modèle conserve une [!DNL AUC-ROC] de 80 % lorsqu’il est testé sur des jeux de données invisibles, ce qui démontre une forte généralisation aux nouveaux enregistrements de clients. Les performances restent stables sur différents segments de clientèle, mais se dégradent légèrement lorsque le comportement des utilisateurs s’écarte considérablement des modèles historiques.
* Le modèle a été évalué par rapport à des entrées perturbées et antagonistes, y compris des données manquantes, une injection aberrante et un étiquetage erroné intentionnel. Bien que la performance reste robuste dans des conditions normales, une légère dégradation de la précision (environ 3-5 %) a été observée dans des modifications extrêmes de l&#39;antagonisme.

## Considérations relatives à la sécurité et à la confidentialité

* Le modèle **ne traite ni ne conserve aucune information d’identification personnelle)** et toutes les données utilisées pour la formation sont rendues anonymes et agrégées. Elle se conforme strictement au RGPD, au CCPA et aux politiques de confidentialité internes d’Adobe afin d’assurer une utilisation responsable des données.
* Le modèle intègre des techniques de confidentialité différentielle pour ajouter un bruit contrôlé aux données, empêchant ainsi la ré-identification des individus. En outre, des méthodes **hachage, anonymisation et tokenisation sont utilisées pour supprimer les informations d’identification personnelles** avant l’entraînement et l’inférence des modèles.

## Déploiement et intégration

* Le modèle est hébergé sur les services d’IA de Adobe Experience Platform et intégré à diverses applications Adobe. Elle est disponible via des points d’entrée d’API, ce qui permet un accès transparent aux prédictions en temps réel et au traitement par lots dans les workflows de marketing et d’engagement client.
* Le modèle s’exécute sur un déploiement basé sur **[!DNL Kubernetes]** avec des fonctionnalités de mise à l’échelle automatique pour gérer efficacement différentes charges de travail. Les ressources de calcul incluent des GPU [!DNL NVIDIA V100] pour l’entraînement et une inférence optimisée basée sur CPU pour une évolutivité en temps réel.

## Surveillance et maintenance

* Le modèle est surveillé en permanence **par le biais de[!DNL WatsonX]**, en suivant des indicateurs de performances clés tels que la dérive de précision, les changements d’importance des fonctionnalités et la stabilité des prévisions. Les mécanismes de détection et d’alerte des anomalies avertissent l’équipe lorsque des écarts importants par rapport au comportement attendu se produisent.
* Le modèle est recyclé chaque mois à l’aide de données d’interaction client mises à jour afin d’assurer une pertinence continue. Le recyclage périodique aide à atténuer la dérive des données et les fluctuations saisonnières qui pourraient avoir une incidence sur la précision prédictive

## Préoccupations éthiques et intelligence artificielle responsable

* Le modèle pourrait introduire un biais dans la prise de décision s&#39;il n&#39;est pas correctement suivi. Par exemple, si certaines données démographiques sont surreprésentées dans les données de formation, le modèle pourrait favoriser injustement des groupes de clients spécifiques.
* Experience Platform suit des directives d’IA responsables, en veillant à ce que les modèles soient soumis à des audits **biais, des tests d’équité et une supervision humaine** avant leur déploiement.

## Limites connues

* Le modèle peut avoir du mal à prédire avec précision les résultats pour les produits nouvellement lancés ou les segments de clients pour lesquels les données historiques disponibles sont insuffisantes. De plus, les variations saisonnières du comportement des clients peuvent causer des fluctuations dans la précision prédictive si elles ne sont pas prises en compte lors du recyclage.
* Les performances diminuent lorsque l’historique du client est clairsemé, par exemple pour les nouveaux acheteurs ou les utilisateurs avec des données d’engagement minimales. En outre, si les comportements des clients **changements dus à des facteurs externes tels que les ralentissements économiques ou les tendances du secteur** changent, le modèle peut nécessiter une adaptation rapide pour maintenir la précision.

## Améliorations futures

* Les itérations futures incluront des techniques d’apprentissage de transfert pour améliorer les performances des utilisateurs démarrés à froid et améliorer leur adaptabilité aux changements de comportement des clients. En outre, l’intégration de données en temps réel sera introduite pour améliorer la réactivité et la précision des modèles dans les environnements de marketing dynamique.
