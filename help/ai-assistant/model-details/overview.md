---
title: Cartes de modèles pour la transparence des modèles d’IA dans Adobe Experience Platform
description: En savoir plus sur les cartes modèles dans Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 74a8ef82-cff9-4a7e-95c8-f915eb664eda
source-git-commit: dddd699f231d54ee44b33f86a5c9e59c0aedc30c
workflow-type: tm+mt
source-wordcount: '3171'
ht-degree: 0%

---

# Cartes de modèle pour la transparence des modèles d’IA dans Adobe Experience Platform

Une carte de modèle d’IA est le format standard selon lequel la transparence du modèle d’IA est communiquée. Les cartes de modèle fournissent des informations complètes sur le modèle sous-jacent sur lequel un outil d’IA donné est basé. Les cartes modèles contiennent des informations telles que l’objectif d’un outil d’IA, les données de formation, les mesures de performance, les limites et les considérations éthiques. Vous pouvez utiliser la transparence fournie par les cartes modèles pour mieux comprendre les capacités et les limites du modèle, ainsi que pour mieux promouvoir une utilisation responsable et équitable de l’IA.

Les cartes de modèle sont publiques et sont destinées à améliorer la compréhension des clients existants et potentiels des modèles d’IA utilisés par Adobe. Les cartes modèles sont généralement statiques. Cependant, plusieurs aspects des modèles d’IA peuvent changer au fil du temps, notamment la parenté, le biais et d’autres attributs de transparence.

Lisez ce document pour en savoir plus sur les cartes modèles dans Adobe Experience Platform.

## Sections de la carte modèle {#model-card-sections}

Une carte modèle est composée de différentes sections, chacune se concentrant sur un aspect particulier du modèle d’IA.

Lisez ce qui suit pour obtenir un guide sur les différentes sections d&#39;une carte modèle, y compris des informations sur les questions qu&#39;elles abordent.

### Présentation du modèle {#model-overview}

La présentation du modèle contient des informations générales sur un modèle d’IA. Utilisez cette section pour fournir des informations telles que le nom, l’objectif et le type de votre modèle d’IA. De plus, vous pouvez utiliser cette section pour identifier les utilisateurs prévus et expliquer comment votre modèle s’intègre à Experience Platform.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quel est le nom du modèle ? | Nom officiel et version du modèle d’IA | **Modèle de score de propension CustomerAI v2.0** <br>CustomerAI est un modèle optimisé par l’IA conçu pour générer des scores de propension pour les utilisateurs en fonction de leurs comportements et interactions passés avec une entreprise. Il permet de prédire la probabilité qu’un client ou une cliente effectue des actions spécifiques, telles qu’effectuer un achat, interagir avec le contenu ou résilier le contrat. Ce modèle est déployé dans Adobe Experience Platform et s’intègre à divers workflows de marketing et d’analyse client.</br> |
| Quel est l’objectif du modèle ? | Brève description de l’objectif du modèle. | Le modèle est conçu pour fournir aux professionnels du marketing et aux équipes de l’engagement client des informations exploitables en prédisant la probabilité qu’un client effectue une action donnée, comme effectuer un achat, s’inscrire à un abonnement ou participer à une campagne par e-mail. Les sorties permettent aux entreprises d’optimiser la segmentation de l’audience et de personnaliser les interactions des clients en fonction des comportements prévus. |
| De quel type de modèle s&#39;agit-il ? | Type du modèle, tel que classification, régression, génératif, etc. | Il s’agit d’un modèle **classification d’apprentissage supervisé** qui prédit la probabilité qu’un événement se produise (par exemple, achat, résiliation, engagement) à partir des données client historiques. Il est entraîné à l’aide d’arbres de décision boostant le gradient (GBDT) avec une régression logistique pour modéliser les scores de propension. |
| Qui sont les utilisateurs prévus ? | Les groupes d’utilisateurs internes et externes auxquels le modèle est destiné. | Les principaux utilisateurs de ce modèle sont les professionnels du marketing, les analystes de données et les équipes d’engagement des clients qui tirent parti de Adobe Experience Platform pour piloter les stratégies marketing axées sur les données. |
| Comment ce modèle s’intègre-t-il à Adobe Experience Platform ? | Les détails sur l’intégration et les API utilisées, ainsi que leur compatibilité avec les workflows. | CustomerAI s’intègre directement dans les services d’IA de Adobe Experience Platform ****, ce qui permet aux utilisateurs d’accéder aux sorties du modèle par le biais d’API et de tableaux de bord préconfigurés. Les scores de propension générés par le modèle peuvent être utilisés dans **Adobe Journey Optimizer**, **et Adobe Real-Time CDP** afin d’affiner la segmentation de l’audience et d’adapter les stratégies marketing. |

{style="table-layout:auto"}

+++

### Utilisation prévue {#intended-use}

La section d’utilisation prévue contient des informations sur les principaux cas d’utilisation de votre modèle d’IA. Vous pouvez utiliser cette section pour développer les problèmes que votre modèle vise à résoudre, les secteurs et/ou domaines pour lesquels votre modèle est pertinent, ainsi que les cas d’utilisation abusive à éviter lors de l’utilisation de votre modèle d’IA.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quels sont les principaux cas d’utilisation ? | Scénarios dans lesquels le modèle doit être utilisé. | Ce modèle est principalement utilisé pour la **segmentation de la clientèle, le marketing ciblé et la prédiction de l’attrition**. Les entreprises tirent parti de ce modèle pour **prédire les intentions d’achat des clients et clientes, optimiser les campagnes marketing et améliorer les efforts de personnalisation**. Par exemple, une société de commerce électronique peut utiliser le modèle pour identifier les acheteurs à forte intention et leur offrir des promotions exclusives. |
| Quels problèmes ce modèle résout-il ? | Principaux points faibles abordés par le modèle. | Les professionnels du marketing ont souvent du mal à **identifier les bons clients à cibler** et **optimiser les efforts d’engagement**. Ce modèle **réduit les conjectures** en offrant une **approche axée sur les données** au ciblage des clients et clientes, tout en s’assurant que les ressources marketing sont allouées efficacement. |
| Pour quels secteurs ou domaines ce modèle est-il pertinent ? | Liste des secteurs d’activité applicables. | Le modèle s’applique à plusieurs secteurs, notamment le commerce **, la vente au détail, les services financiers, les télécommunications et les médias**. Toute entreprise reposant sur l’engagement des clients et le marketing personnalisé peut bénéficier de ce modèle. |
| Comment ce modèle ne devrait-il pas être utilisé ? | Tout cas d’utilisation abusive à éviter. | Le modèle **ne doit pas être utilisé pour la prise de décision à haut risque** comme **la notation financière du crédit, les diagnostics médicaux ou les évaluations juridiques**. En outre, il n’est pas destiné à être utilisé pour **prédire les comportements personnellement sensibles** (tels que les problèmes de santé, les préférences politiques) en raison de préoccupations éthiques potentielles. |

{style="table-layout:auto"}

+++

### Entrées et sorties du modèle {#model-inputs-and-outputs}

La section entrées et sorties du modèle contient des informations sur les types de données pris en charge que votre modèle prend en entrée et renvoie en sortie. Vous pouvez utiliser cette section pour fournir des exemples d’entrées et de sorties de données pertinentes pour votre modèle d’IA.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quels types de données le modèle prend-il en entrée ? | Les types de données pris en entrée par le modèle sont les suivants : fonctionnalités de données, formats et sources. | Le modèle traite les **données comportementales des clients, attributs démographiques et interactions historiques**. Cela inclut des données telles que la fréquence des visites du site web, l’historique des achats précédents, l’engagement dans les e-mails marketing et des informations démographiques. |
| Quel format doivent prendre les entrées ? | Formats d’entrée acceptés. | Les données d’entrée doivent être structurées sous la forme d’objets **JSON** contenant des attributs du client et des signaux comportementaux. Pour le traitement par lots, le modèle accepte les fichiers **CSV** formatés conformément aux normes d’ingestion de données de Adobe Experience Platform. |
| Que produit le modèle ? | Type de sortie généré par le modèle. | Le modèle produit un score de propension compris entre 0 et 1, où des valeurs plus élevées indiquent une plus grande probabilité que l&#39;événement prédit se produise. En outre, il fournit des scores d’importance de la fonctionnalité, ce qui permet aux utilisateurs et utilisatrices de comprendre les facteurs qui ont influencé la prédiction. |
| Quels sont les exemples d’entrées et de sorties ? | Exemple d’entrée et sortie correspondante. | <ul><li>**Exemple d’entrée :** json { « customer_id »: 12345, « last_purchases »: 3, « last_visit_days »: 7, « email_click_rate »: 0.4 }</li><li>**Exemple de sortie :** json { « customer_id »: 12345, « propension_score »: 0.82 }</li></ul> |

{style="table-layout:auto"}

+++

### Données d’apprentissage {#training-data}

La section Données d’entraînement contient des informations sur les jeux de données utilisés pour entraîner un modèle d’IA donné. Vous pouvez utiliser cette section pour en savoir plus sur la taille et la source des données d’identification, les biais identifiés dans le jeu de données et la manière dont les données ont été prétraitées.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quels jeux de données ont été utilisés pour entraîner le modèle ? | Description des sources de données. | Le modèle a été entraîné sur des données d’interaction client propriétaires et anonymes collectées via Adobe Experience Platform. Il comprend des données historiques sur le comportement des clients, des enregistrements de transactions, des interactions d’e-mails et des mesures d’engagement dans plusieurs secteurs d’activité. |
| Quelle est la taille et la source des données ? | Le volume et l’origine du jeu de données d’entraînement. | Le jeu de données de formation se compose de 10 millions d’enregistrements client provenant d’un ensemble diversifié de clients Adobe Experience Platform. Ces enregistrements comprennent l’historique des interactions client, les données transactionnelles, les logs d’engagement comportemental et les informations démographiques provenant de divers secteurs tels que la vente au détail, le commerce électronique, les télécommunications et la finance. Les données ont été recueillies sur une période de 24 mois, ce qui a permis d&#39;obtenir une représentation suffisante des tendances saisonnières et des modèles d&#39;engagement à long terme. |
| Y a-t-il des biais connus dans le jeu de données ? | Considérations relatives aux préjugés et efforts d’atténuation. | Le jeu de données est principalement fourni par des utilisateurs à fort engagement, ce qui peut introduire un biais de sélection. Pour atténuer ce problème, le modèle applique un échantillonnage stratifié, des techniques de vérification des biais et des stratégies d’augmentation des données. |
| Comment les données sont-elles prétraitées ? | Procédure de nettoyage et de préparation des données. | Le jeu de données subit un prétraitement complet pour garantir la cohérence, la qualité et la convivialité des données. <ol><li>**Gestion des valeurs manquantes** : les valeurs manquantes sont traitées à l’aide d’une combinaison d’imputation moyenne (pour les champs numériques), d’imputation de mode (pour les champs catégoriels) et de modélisation prédictive (pour les cas manquants complexes).</li><li>**Codage catégoriel :** les variables catégorielles telles que les segments de clients et de clientes et les catégories d’achat sont converties en représentations numériques par le biais de techniques de codage à accès unique et de codage cible.</li><li>**Mise à l’échelle et normalisation des caractéristiques :** la mise à l’échelle minimale et maximale est appliquée aux variables limitées (par exemple, l’âge, le revenu), tandis que la normalisation du score z est utilisée pour les caractéristiques normalement distribuées.</li><li>**Prétraitement supplémentaire :** le pipeline comprend la détection et la suppression des valeurs aberrantes, le filtrage des doublons, la normalisation de l’horodatage et l’ingénierie des fonctionnalités pour améliorer la prédiction.</li></ol> |

{style="table-layout:auto"}

+++

### Architecture du modèle et formation {#model-architecture-and-training}

La section Architecture du modèle et formation décrit le plan directeur de votre modèle d’IA. Cette section fait référence à la structure et à la conception du modèle d’IA, y compris des détails sur le type d’algorithme et les méthodes d’évaluation utilisées. Vous pouvez également utiliser cette section pour fournir des informations sur les structures d’entraînement utilisées, ainsi que sur les ressources de calcul utilisées dans l’entraînement.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quelle architecture le modèle utilise-t-il ? | Type de réseau neuronal, méthode d’ensemble, etc. | Le modèle exploite les arbres de décision à amplification de dégradé (GBDT) à l’aide de XGBoost, optimisé pour les données structurées. Il est entraîné sur des séquences d’événements client historiques pour identifier des modèles comportementaux prédictifs. |
| Quels algorithmes ont été appliqués ? | Techniques de machine learning utilisées. | Le modèle est construit à l&#39;aide d&#39;une approche d&#39;apprentissage supervisée, en utilisant des arbres de décision d&#39;amplification de gradient (GBDT) avec XGBoost comme algorithme d&#39;apprentissage principal. De plus, la régression logistique est incorporée comme modèle de référence pour l&#39;évaluation comparative de la précision prédictive. |
| Quels cadres de formation ont été utilisés ? | Bibliothèques ou plateformes utilisées pour la formation. | Le modèle a été développé en utilisant TensorFlow, XGBoost et scikit-learn. La formation s’exécute sur l’infrastructure cloud d’Adobe AI à l’aide des GPU NVIDIA V100, prenant en charge les jeux de données à grande échelle. |
| Quelles ressources informatiques ont été utilisées pour la formation ? | Ressources matérielles et cloud utilisées pour la formation. | GPU NVIDIA V100, entraînés sur les infrastructures cloud Google. |
| Quelles méthodes d&#39;évaluation ont été utilisées ? | Mesures et procédures de test utilisées pour l’évaluation. | AUC-ROC, precision-reminder et validation croisée. |

{style="table-layout:auto"}

+++

### Performance et évaluation {#performance-and-evaluation}

La section Performances et évaluation contient des informations sur les mesures et les méthodes utilisées pour évaluer la façon dont le modèle effectue les tâches prévues. Vous pouvez utiliser cette section pour fournir des informations sur les mesures d’évaluation utilisées, ainsi que les faiblesses identifiées ou les cas d’échec.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Comment le modèle a-t-il été testé ? | Méthodes utilisées pour valider les performances. | Le modèle a été testé en utilisant une approche de validation d’exclusion, où 80 % des données ont été utilisées pour la formation et 20 % ont été réservées à l’évaluation. |
| Quelles mesures d’évaluation ont été utilisées ? | Les indicateurs clés de performance. | L&#39;efficacité du modèle est mesurée en utilisant **AUC-ROC (0,85)**, **précision-rappel (0,78)** et **score F1 (0,80)**. Ces mesures permettent d’évaluer la puissance prédictive du modèle sur différents segments. |
| Comment les performances varient-elles selon les différents scénarios ? | Variations de performances spécifiques au contexte. | Précision moindre pour les nouveaux segments de clientèle avec des données historiques limitées. |
| Existe-t-il des faiblesses ou des cas d’échec connus ? | Toute limite ou point d’échec. | Le modèle peut être sous-performant pour les clients avec des données historiques limitées (problème de démarrage à froid). En outre, les effets de saisonnalité, tels que les tendances des achats de vacances, peuvent nécessiter un recyclage fréquent pour maintenir la précision. |

{style="table-layout:auto"}

+++

### Équité et partialité {#fairness-and-bias}

La section sur l’équité et les préjugés contient des informations sur la performance du modèle d’IA en ce qui concerne les mesures d’équité et de préjugés. L&#39;équité fait référence à la capacité du modèle à fournir des résultats équitables entre différents groupes démographiques et cas d&#39;utilisation, tandis que le biais fait référence aux erreurs systématiques qui entraînent des résultats injustes. Utilisez cette section pour élaborer sur les contrôles d’équité effectués et pour discuter de la manière dont le modèle atténue les biais.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quels contrôles d’équité ont été effectués ? | Les processus d&#39;analyse et d&#39;atténuation des biais qui ont été effectués. | Le modèle a été soumis à des tests de parité démographique et à des évaluations contradictoires de l’équité afin de détecter les disparités de rendement entre les différents segments d’utilisateurs. |
| Le modèle touche-t-il de façon disproportionnée certains groupes? | Toute disparité dans les performances qui a été identifiée. | L’analyse a révélé une baisse de performances de 5 % pour les utilisateurs disposant de faibles données historiques d’interaction. Pour y remédier, le modèle incorpore des techniques de repondération pendant la formation. |
| Comment le modèle atténue-t-il les biais ? | Techniques utilisées pour traiter les biais. | L’ensemble de données est stratifié afin d’assurer une représentation proportionnelle des différentes données démographiques des clients, et des contraintes d’équité sont introduites au cours de la formation afin d’empêcher le modèle de favoriser un groupe particulier. Des vérifications régulières des biais sont effectuées à l’aide d’une analyse de parité démographique, permettant des ajustements si des disparités de rendement sont détectées. |

{style="table-layout:auto"}

+++

### Explicabilité et interprétabilité {#explainability-and-interpretability}

La section explicabilité et interprétabilité contient des informations sur la capacité d’un modèle d’IA à fournir des explications claires et compréhensibles et sur la facilité avec laquelle un utilisateur humain peut comprendre comment les fonctionnalités d’entrée affectent les prédictions et les réponses. Utilisez cette section pour expliquer comment les utilisateurs peuvent mieux comprendre pourquoi votre modèle prend certaines décisions et quels outils ou techniques sont disponibles pour une meilleure interprétabilité.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Les utilisateurs peuvent-ils comprendre pourquoi le modèle prend certaines décisions ? | Méthodes d’interprétabilité utilisées par le modèle. | Le modèle utilise **SHAP (SHapley Additive Explanations)** pour quantifier l’impact de chaque fonctionnalité d’entrée sur ses prédictions, ce qui permet d’évaluer de manière transparente la manière dont les attributs du client influencent les scores de propension. Les valeurs SHAP permettent à la fois l’interprétabilité globale, en identifiant les facteurs les plus influents dans toutes les prédictions, et l’interprétabilité locale, en expliquant les prédictions individuelles pour des clients spécifiques. |
| Quels outils ou techniques sont disponibles pour l’interprétabilité ? | Outils d’explicabilité disponibles. | Le modèle prend en charge **Local Interpretable Model-Agnostic Explanations (LIME))** et SHAP pour fournir des informations sur la manière dont les fonctionnalités d’entrée influencent les prédictions. LIME génère des explications locales en créant des versions perturbées des données d&#39;entrée et en observant les changements dans les prédictions, tandis que SHAP attribue des valeurs de contribution à chaque caractéristique, offrant à la fois une interprétabilité globale et locale des décisions de modèle. |

{style="table-layout:auto"}

+++

### Robustesse et généralisation {#robustness-and-generalization}

La section robustesse et généralisation contient des informations sur les performances de votre modèle d’IA sur les données non vues. De plus, vous pouvez utiliser cette section pour expliquer comment votre modèle maintient ses performances et sa précision en cas d’entrées inattendues ou difficiles.

>[!TIP]
>
>Dans l’IA, les « données non vues » font référence à des données différentes des données sur lesquelles un modèle donné a été entraîné.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quelle est la performance du modèle sur les données non vues ? | Résultats des tests de performance de généralisation. | Le modèle conserve **80 % de l’AUC-ROC** lorsqu’il est testé sur des jeux de données invisibles, ce qui démontre une forte généralisation aux nouveaux enregistrements de clients. Les performances restent stables sur différents segments de clientèle, mais se dégradent légèrement lorsque le comportement des utilisateurs s’écarte considérablement des modèles historiques. |
| Le modèle a-t-il été soumis à des tests de résistance pour les intrants contradictoires ? | Détails de l’évaluation de la robustesse. | Le modèle a été évalué par rapport à des entrées perturbées et antagonistes, y compris des données manquantes, une injection aberrante et un étiquetage erroné intentionnel. Bien que la performance reste robuste dans des conditions normales, une légère dégradation de la précision (environ 3-5 %) a été observée dans des modifications extrêmes de l&#39;antagonisme. |

{style="table-layout:auto"}

+++

### Considérations relatives à la sécurité et à la confidentialité {#security-and-privacy-considerations}

La section Considérations relatives à la sécurité et à la confidentialité contient des informations sur les mesures et pratiques mises en œuvre pour protéger les données sensibles et assurer l’utilisation sécurisée de votre modèle. Vous pouvez utiliser cette section pour répondre aux questions sur la manière dont votre modèle gère les données sensibles.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Le modèle gère-t-il des données sensibles ? | Toute conformité des informations avec les lois sur la confidentialité. | Le modèle ne traite ni ne conserve aucune information d’identification personnelle (PII) et toutes les données utilisées pour la formation sont anonymisées et agrégées. Elle se conforme strictement au RGPD, au CCPA et aux politiques de confidentialité internes d’Adobe afin d’assurer une utilisation responsable des données. |
| Quelles techniques de protection de la vie privée ont été utilisées ? | Techniques utilisées pour garantir les mesures de confidentialité. | Le modèle intègre des techniques de confidentialité différentielle pour ajouter un bruit contrôlé aux données, empêchant ainsi la ré-identification des individus. En outre, des méthodes de hachage, d’anonymisation et de tokenisation sont utilisées pour supprimer les informations d’identification personnelles avant l’entraînement et l’inférence du modèle. |

{style="table-layout:auto"}

+++

### Surveillance et maintenance {#monitoring-and-maintenance}

La section surveillance et maintenance contient des informations sur la manière dont les performances de votre modèle sont surveillées au fil du temps et sur la fréquence de recyclage du modèle. Vous pouvez utiliser cette section pour fournir des informations sur la manière dont les mesures telles que la précision, la précision, le rappel et la latence sont suivies.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Comment les performances du modèle sont-elles surveillées au fil du temps ? | Détails sur les mécanismes de tracking utilisés pour le modèle. | Le modèle est surveillé en permanence via WatsonX, suivant des indicateurs de performances clés tels que la dérive de précision, les changements d&#39;importance des fonctionnalités et la stabilité des prévisions. Les mécanismes de détection et d’alerte des anomalies avertissent l’équipe lorsque des écarts importants par rapport au comportement attendu se produisent. |
| À quelle fréquence le modèle est-il recyclé ? | Fréquence des mises à jour sur le modèle. | Le modèle est recyclé chaque mois à l’aide de données d’interaction client mises à jour afin d’assurer une pertinence continue. Le recyclage périodique aide à atténuer la dérive des données et les fluctuations saisonnières qui pourraient avoir une incidence sur la précision prédictive. |

{style="table-layout:auto"}

+++

### Considérations éthiques et IA responsable {#ethical-considerations-and-responsible-ai}

La section Considérations éthiques et IA responsable contient des informations sur les préoccupations éthiques associées à votre modèle d’IA. Cette section décrit également dans quelle mesure votre modèle s’aligne sur les principes de l’IA responsable. Utilisez cette section pour fournir des informations sur les impacts éthiques potentiels de l’utilisation de votre modèle, y compris la reconnaissance des préjugés, l’assurance de l’équité et la prévention des dommages causés aux individus ou aux groupes.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quelles sont les préoccupations éthiques associées à ce modèle ? | Les risques potentiels qui ont été identifiés. | Le modèle pourrait introduire un biais dans la prise de décision s&#39;il n&#39;est pas correctement suivi. Par exemple, si certaines données démographiques sont surreprésentées dans les données de formation, le modèle pourrait favoriser injustement des groupes de clients spécifiques. |
| Comment le modèle s’aligne-t-il sur les principes de l’IA responsable ? | Informations sur la manière dont le modèle se conforme aux directives d’éthique de l’IA. | Adobe Experience Platform suit des directives d’IA responsable, en s’assurant que les modèles subissent des audits de biais, des tests d’équité et une supervision humaine avant leur déploiement. |

{style="table-layout:auto"}

+++

### Limites connues {#known-limitations}

La section limitations connues contient des informations sur les limitations existantes qui ont été identifiées pour votre modèle d’IA. Utilisez cette section pour souligner les conditions dans lesquelles votre modèle d’IA peut mal fonctionner et pour souligner toutes les limites que les utilisateurs doivent connaître.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quelles sont les limites connues du modèle ? | Toute contrainte de performances ou de cas d’utilisation identifiée. | Le modèle peut avoir du mal à prédire avec précision les résultats pour les produits nouvellement lancés ou les segments de clients pour lesquels les données historiques disponibles sont insuffisantes. De plus, les variations saisonnières du comportement des clients peuvent causer des fluctuations dans la précision prédictive si elles ne sont pas prises en compte lors du recyclage. |
| Dans quelles conditions le modèle est-il peu performant ? | Toutes les faiblesses identifiées concernant le modèle. | Les performances diminuent lorsque l’historique du client est clairsemé, par exemple pour les nouveaux acheteurs ou les utilisateurs avec des données d’engagement minimales. En outre, si les comportements des clients changent en raison de facteurs externes tels que les ralentissements économiques ou les tendances du secteur, le modèle peut nécessiter une adaptation rapide pour maintenir la précision. |

{style="table-layout:auto"}

+++

### Améliorations futures {#future-improvements}

La section améliorations futures contient des informations sur les mises à jour de fonctionnalités prévues pour votre modèle d’IA. Utilisez cette section pour élaborer votre feuille de route d’amélioration.

+++Afficher les questions et les exemples de réponses

| Question | Informations nécessaires | Exemple de réponse |
| --- | --- | --- |
| Quelles améliorations sont prévues pour les itérations futures ? | Feuille de route des améliorations. | Les itérations futures incluront des techniques d’apprentissage de transfert pour améliorer les performances des utilisateurs démarrés à froid et améliorer leur adaptabilité aux changements de comportement des clients. En outre, l’intégration de données en temps réel sera introduite pour améliorer la réactivité et la précision des modèles dans les environnements de marketing dynamique. |

{style="table-layout:auto"}

+++
