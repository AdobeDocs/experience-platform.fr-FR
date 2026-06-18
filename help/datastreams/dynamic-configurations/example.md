---
title: Exemple de configuration de flux de données dynamique de bout en bout
description: Découvrez comment combiner des cas  [!DNL Dynamic Datastream Configuration] ’utilisation dans un seul flux de données pour une implémentation d’e-commerce à l’aide du premier modèle Analytics.
source-git-commit: 738597c837440cb66aa80b24f1f877c9c4cb758b
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 6%

---


# Exemple complet de [!DNL Dynamic Datastream Configuration]

Cette page montre comment combiner plusieurs cas d’utilisation de [!DNL Dynamic Datastream Configuration] en une seule configuration prête pour la production. L’exemple utilise le modèle [Analytique en premier](/help/datastreams/dynamic-configurations/configuration-patterns.md#analytical-first) et s’applique à un scénario d’e-commerce courant.

## Scénario {#scenario}

Un retailer d’e-commerce utilise Web SDK avec des [!DNL Adobe Target] de personnalisation, de [!DNL Adobe Analytics], de [!DNL Customer Journey Analytics] et de [!DNL Adobe Real-Time CDP]. Le retailer conserve actuellement trois flux de données distincts : un pour [!DNL Adobe Analytics] et [!DNL Adobe Target], un pour [!DNL Customer Journey Analytics] et un pour [!DNL Adobe Journey Optimizer]. L’objectif est de consolider en un seul flux de données et de :

- Filtrer le trafic de robots avant qu’il n’atteigne un service ([cas d’utilisation 4](/help/datastreams/dynamic-configurations/use-cases.md#uc4))
- Supprimer les événements système `decisioning.propositionFetch` de [!DNL Adobe Experience Platform] ([cas d’utilisation 3](/help/datastreams/dynamic-configurations/use-cases.md#uc3))
- Acheminer les achats et les interactions de produits vers le [!DNL Real-Time Customer Profile] pour la segmentation et les parcours de [!DNL Adobe Journey Optimizer] ([cas d’utilisation 1](/help/datastreams/dynamic-configurations/use-cases.md#uc1) et [cas d’utilisation 2](/help/datastreams/dynamic-configurations/use-cases.md#uc2))
- Conserver les pages vues dans le lac de données pour les [!DNL Customer Journey Analytics] uniquement

Comme la plupart des événements sont des pages vues (**Analytique**), le retailer choisit **Analytique en premier** : le jeu de données principal n’est pas activé pour les profils et les règles promeuvent les événements **Exploitables** vers les profils.

## Stratégie du jeu de données {#dataset-strategy}

Créez ces jeux de données avant de configurer des règles. Pour obtenir des conseils sur la configuration de la conservation des données, consultez le [&#x200B; Guide de conservation des jeux de données des événements Experience &#x200B;](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md).

| Jeu de données | Activé pour Profil | Rétention | Rôle |
|---------|----------------|-----|---------|
| `Bot Traffic - Quarantine` | Non | 30 jours | Isoler les événements de robots pour analyse avant de les ignorer |
| `System Events - Quarantine` | Non | 30 jours | Isolation d’événements `propositionFetch` pour le débogage |
| `Purchases` | Oui | 3 mois | Conversions à forte valeur ajoutée pour le profil, la [!UICONTROL segmentation &#x200B;] et [!DNL Adobe Journey Optimizer] |
| `Product Interactions` | Oui | 30 jours | Consultations de produits et ajout au panier pour le profil et la [!UICONTROL segmentation &#x200B;] |
| `Browsing - General` **(principal)** | Non | 12 mois | Pages vues et recherche de site pour la création de rapports [!DNL Customer Journey Analytics] |

`Browsing - General` est le jeu de données principal du flux de données. Tous les événements qui ne correspondent à aucune règle reviennent à ce jeu de données.

## Règles de service Experience Platform {#aep-rules}

Le tableau suivant présente l’ensemble complet des règles pour le service [!DNL Adobe Experience Platform]. Edge Network évalue les règles dans l’ordre indiqué.

| Règle | Nom | Conditions | [!DNL Adobe Experience Platform] | Remplacement du jeu de données | [!UICONTROL Segmentation &#x200B;] | [!DNL Adobe Journey Optimizer] | Cas d’utilisation |
|------|------|-----------|------------|-----------------|-------------------|-------------------------------|----------|
| 1 | Trafic de robots | `botDetection.score` est égal à `1` | Activé | `Bot Traffic - Quarantine` | Désactivé | Désactivé | [UC 4](/help/datastreams/dynamic-configurations/use-cases.md#uc4) |
| 2 | Événements système | `eventType` est égal à `decisioning.propositionFetch` [!DNL OR] `eventType` est égal à `personalization.request` | Activé | `System Events - Quarantine` | Désactivé | Désactivé | [UC 3](/help/datastreams/dynamic-configurations/use-cases.md#uc3) |
| 3 | Achats | `eventType` est égal à `commerce.purchases` | Activé | `Purchases` | Activé | Activé | [UC 1](/help/datastreams/dynamic-configurations/use-cases.md#uc1), [UC 2](/help/datastreams/dynamic-configurations/use-cases.md#uc2) |
| 4 | Interactions avec les produits | `eventType` est égal à `commerce.productViews` [!DNL OR] `eventType` est égal à `commerce.productListAdds` | Activé | `Product Interactions` | Activé | Désactivé | [UC 1](/help/datastreams/dynamic-configurations/use-cases.md#uc1), [UC 2](/help/datastreams/dynamic-configurations/use-cases.md#uc2) |
| Par défaut | Valeur par défaut (aucune correspondance) | Tout le reste | Activé (principal) | `Browsing - General` | Désactivé | Désactivé | [UC 1](/help/datastreams/dynamic-configurations/use-cases.md#uc1) |

## Pourquoi cet ordre des règles {#rule-order}

1. **Trafic de robots en premier (règle 1).** Mettre en quarantaine les événements détectés par les robots avant l’exécution d’une logique de routage. Un événement de robot correspondant à une règle ultérieure gaspillerait la capacité du magasin de profils.

2. **Deuxième événement système (règle 2).** `decisioning.propositionFetch` événements se déclenchent à chaque chargement de page et n’ont aucune valeur analytique. Les intercepter précocement les empêche de correspondre accidentellement à une règle **utilisable**.

3. **Achats tiers (règle 3).** Les événements exploitables bénéficient d’un traitement [!DNL Adobe Experience Platform] complet : profil, segmentation Edge et [!DNL Adobe Journey Optimizer] pour la personnalisation entrante déclenchée.

4. **Interactions de produit quatrième (règle 4).** Activation du profil pour la segmentation, mais [!DNL Adobe Journey Optimizer] désactivation. Cette implémentation ne récupère pas la personnalisation entrante à partir de [!DNL Adobe Journey Optimizer] sur le comportement de navigation.

5. **Dernière valeur par défaut.** Toutes les autres informations (pages vues, événements de défilement, recherche de site) entrent dans le jeu de données principal hors profil pour les rapports [!DNL Customer Journey Analytics] uniquement.

## Analyse du budget de la règle {#rule-budget}

Cette configuration utilise des règles explicites **4** sur la limite de 5 règles par service pour [!DNL Adobe Experience Platform]. Un emplacement de règle reste disponible pour les besoins futurs. Par exemple, le filtrage du trafic interne par domaine d’e-mail ou le routage d’un nouveau type d’événement.

Pour obtenir la liste complète des mécanismes de sécurisation, voir [Création de configurations de flux de données dynamiques](/help/datastreams/configure-dynamic-datastream.md#guardrails).

Si vous avez besoin d’une granularité plus élevée, combinez d’autres types d’événements en tant que conditions [!DNL OR] dans une règle existante. Par exemple, la règle 4 combine déjà `commerce.productViews` et `commerce.productListAdds`. Vous pouvez ajouter des `commerce.productListOpens` ou des `commerce.saveForLaters` à la même règle sans utiliser d’emplacement de règle supplémentaire. Chaque règle prend en charge jusqu’à 100 conditions.

## Règles au niveau de la solution {#solution-rules}

Les règles de service Experience Platform de la section précédente sont indépendantes des règles pour d’autres services. Vous pouvez configurer jusqu’à 5 règles supplémentaires pour chacune des [!DNL Adobe Analytics], [!DNL Adobe Target], [!DNL Adobe Audience Manager] et [!DNL Event Forwarding], indépendamment des règles d’Experience Platform.

| Service | Règle | Condition | Action |
|---------|------|-----------|--------|
| [!DNL Adobe Analytics] | Contournement des robots | `botDetection.score` est égal à `1` | [!DNL Adobe Analytics] : désactivé |
| [!DNL Adobe Analytics] | Suite de rapports Commerce | `eventType` commence par `commerce.` | Remplacement de la suite de rapports : `rsid-commerce` |
| [!DNL Adobe Target] | Contournement des robots | `botDetection.score` est égal à `1` | [!DNL Adobe Target] : désactivé |

## Validation d’Assurance {#assurance-validation}

Après avoir enregistré vos règles, attendez 15 minutes que les modifications se propagent dans Edge Network. Validez ensuite chaque chemin d’accès à l’aide de [&#128279;](/help/assurance/home.md).

Pour une présentation complète du processus de validation, voir [Tester et valider [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/testing.md).

| Événement de test | Correspondance de règle attendue | Jeu de données attendu | Profil ingéré |
|-----------|--------------------|-----------------|--------------------|
| Page vue à partir d’un agent-utilisateur de robot | Règle 1 : trafic de robots | `Bot Traffic - Quarantine` | Non |
| Déclenchement du chargement de page [!DNL Adobe Target] personnalisation | Règle 2 : Événements système | `System Events - Quarantine` | Non |
| Achat terminé | Règle 3 : Achats | `Purchases` | Oui |
| Page de détails du produit vue | Règle 4 : Interactions de produits | `Product Interactions` | Oui |
| Page d’accueil vue | Valeur par défaut (aucune correspondance) | `Browsing - General` | Non |

## Étapes suivantes

- Suivez les étapes de la section [Tester et valider [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/testing.md) pour vérifier chaque chemin d’accès à l’événement avant le déploiement en production.
- Lisez [bonnes pratiques pour [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/best-practices.md) pour obtenir des conseils opérationnels permanents.
- Voir la [FAQ](/help/datastreams/dynamic-configurations/faq.md) si vous rencontrez un comportement de routage inattendu.
