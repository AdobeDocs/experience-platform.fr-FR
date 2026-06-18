---
title: Cas D’Utilisation De La Configuration De Flux De Données Dynamiques
description: Découvrez comment utiliser pour séparer  [!DNL Dynamic Datastream Configurations]  événements par valeur, gérer la conservation des données, supprimer les événements système et filtrer le trafic de robots.
source-git-commit: 19e297602d67a360a3b6bcdd6d5403fb6090de7f
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 2%

---


# Cas d’utilisation de la configuration dynamique des trains de données

Cette page présente six cas d’utilisation courants pour [!DNL Dynamic Datastream Configurations] : séparation des événements par valeur, stratégie de conservation des données hiérarchisée, suppression des événements système, filtrage du trafic de robots, routage sélectif des solutions Experience Cloud et migration du connecteur source Analytics.

Chaque cas d’utilisation est indépendant. Implémentez uniquement celles qui s’appliquent à votre implémentation .

Avant de configurer des règles, complétez la [liste de contrôle des conditions préalables et de la planification](/help/datastreams/dynamic-configurations/prerequisites.md) et passez en revue les [modèles de configuration](/help/datastreams/dynamic-configurations/configuration-patterns.md) pour choisir la stratégie de jeu de données principale appropriée pour votre implémentation.

## Cas d’utilisation 1 : séparer les événements exploitables des événements analytiques {#uc1}

**Objectif :** Optimisez l’utilisation de la boutique de profils et réduisez le volume total de données en acheminant uniquement les événements **exploitables** vers la [!DNL Real-Time Customer Profile] tout en conservant les événements **analytiques** disponibles pour [!DNL Customer Journey Analytics].

**Utilisation :** vous ingérez des événements Web SDK ou Mobile SDK dans des [!DNL Adobe Experience Platform] et constatez des dépassements de profil, des dépassements de volume total de données ou une pression de mécanisme de sécurisation de l’ingestion en flux continu, car tous les événements se retrouvent dans un jeu de données activé pour les profils.

### Stratégie du jeu de données {#uc1-dataset-strategy}

La structure de deux jeux de données suivante sépare les événements en fonction de leur valeur de profil.

| Jeu de données | Activé pour Profil | Événements |
|---------|----------------|--------|
| `Web Events - Profile` | Oui | Achats, ajout au panier, envois de formulaire, conversions clés |
| `Web Events - Analytics` | Non | Pages vues, événements de défilement, clics sur les liens, navigation générale |

### Configuration des règles {#uc1-rule-config}

Avant de configurer des règles, décidez d’utiliser la stratégie de jeu de données [Exploitable en premier ou Analytique en premier](/help/datastreams/dynamic-configurations/configuration-patterns.md#aep-patterns). Ce choix détermine le jeu de données que vous définissez comme principal sur votre flux de données.

**Exemple 1 : Analytique en premier — Règle des événements exploitables**

Jeu de données par Principal : `Web Events - Analytics` (non activé pour profile, secours par défaut)
Jeu de données Secondaire : `Web Events - Profile` (activé pour profile)

Créez une règle pour promouvoir des événements **exploitables** dans le jeu de données activé pour le profil. Tous les événements **analytiques** sont automatiquement rattachés au jeu de données principal.

**Règle : événements activables**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `commerce.purchases` |

Ajoutez des conditions supplémentaires à l’aide de la logique [!DNL OR] pour d’autres types d’événements **exploitables** tels que `commerce.productListAdds` ou `leadGeneration.formComplete`.

- Service **[!DNL Adobe Experience Platform]:** activé
- **Remplacement du jeu de données d’événement :** `Web Events - Profile`
- **Services Edge :** activez [!DNL Adobe Journey Optimizer], [!UICONTROL Segmentation Edge] ou [!UICONTROL Gestion des décisions] selon les besoins pour vos cas d’utilisation de personnalisation. Voir [Paramètres ](/help/datastreams/configure.md#aep).

**Exemple 2 : utilisable en premier — règle des événements analytiques**

Jeu de données par Principal : `Web Events - Profile` (activé pour le profil, secours par défaut)
Jeu de données Secondaire : `Web Events - Analytics` (non activé pour le profil)

Écrivez une règle pour acheminer les événements **Analytics** en dehors du jeu de données activé pour le profil. Tous les événements **pouvant faire l’objet d’une action** sont automatiquement intégrés au jeu de données principal.

**Règle : événements analytiques**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `web.webpagedetails.pageViews` |

Ajoutez des conditions supplémentaires pour d’autres types d’événements **Analytics**.

- Service **[!DNL Adobe Experience Platform]:** activé
- **Remplacement du jeu de données d’événement :** `Web Events - Analytics`
- **[!DNL Adobe Journey Optimizer]/ [!UICONTROL Segmentation Edge] / [!UICONTROL Gestion Des Décisions]:** Désactivé

## Cas d’utilisation 2 : stratégie de conservation des données à plusieurs niveaux {#uc2}

**Objectif :** gérer les coûts de conservation des données en acheminant les événements vers des jeux de données avec différentes fenêtres de conservation en fonction de la valeur commerciale à long terme.

**Utilisation :** vous avez besoin de différentes fenêtres de conservation pour différents types d’événements. Par exemple, une rétention plus longue pour les données d’achat et une rétention plus courte pour les interactions de produits dans [!DNL Adobe Real-Time CDP].

Pour plus d’informations sur la configuration de la conservation des jeux de données, consultez le [ Guide de conservation des jeux de données des événements Experience ](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md).

### Stratégie du jeu de données {#uc2-dataset-strategy}

La structure à trois niveaux suivante attribue des fenêtres de rétention en fonction de la valeur de l’événement.

| Jeu de données | Activé pour Profil | Rétention | Événements |
|---------|----------------|-----|--------|
| `Purchases` | Oui | 3 mois | Achats en ligne consentis |
| `Product Interactions` | Oui | 30 jours | Consultations de produits, ajout au panier, pages vues avec paramètres UTM |
| `Browsing - General` | Non | 12 mois | Pages vues générales, recherche de site, impressions de composant |

>[!IMPORTANT]
>
>Vous définissez la conservation des données au niveau du jeu de données dans [!DNL Adobe Experience Platform], et non dans le [!DNL Dynamic Datastream Configuration]. Voir [Définir ou mettre à jour la conservation d’un jeu de données](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md#set-update-ttl). Les configurations de train de données dynamiques acheminent les événements vers le jeu de données correct. Le paramètre de conservation du jeu de données contrôle la durée de conservation des données. Créez vos jeux de données avec la fenêtre de conservation appropriée avant de configurer des règles.

### Configuration des règles {#uc2-rule-config}

Définissez le jeu de données principal de votre flux de données sur `Browsing - General` afin que les événements non correspondants se retrouvent par défaut dans le jeu de données hors profil plutôt que de gonfler la banque de profils. Vous n’avez pas besoin d’une règle pour les événements de navigation généraux ; ils sont automatiquement intégrés au jeu de données principal.

**Règle 1 : Achats**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `commerce.purchases` |

- **Remplacement du jeu de données d’événement :** `Purchases`
- **Services Edge :** activés si nécessaire ([!UICONTROL Segmentation Edge], [!DNL Adobe Journey Optimizer], [!UICONTROL Gestion des décisions])

**Règle 2 : interactions de produits**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `commerce.productViews` |

Ajoutez des conditions supplémentaires avec des [!DNL OR] pour les `commerce.productListAdds`, les pages vues avec des paramètres UTM et d’autres événements d’interaction de produit.

- **Remplacement du jeu de données d’événement :** `Product Interactions`
- **Services Edge :** activés si nécessaire

## Cas d’utilisation 3 : suppression des événements système de personnalisation {#uc3}

**Objectif :** tenir les événements `decisioning.propositionFetch` et `personalization.request` hors de la [!DNL Customer Journey Analytics] et de la [!DNL Real-Time Customer Profile]. Ces événements système se déclenchent à chaque chargement de page lorsque [!DNL Adobe Target] ou [!DNL Adobe Journey Optimizer] récupère des décisions de personnalisation. Il s’agit d’événements **utilisables** sans valeur d’analyse ou de profil.

**Utilisation :** vous utilisez des [!DNL Adobe Target] ou des [!DNL Adobe Journey Optimizer] pour la personnalisation avec des [!DNL Customer Journey Analytics] ou des [!DNL Adobe Real-Time CDP]. Ces événements système gonflent le nombre de lignes facturables, consomment la capacité de la boutique de profils ou consomment le débit d’ingestion en flux continu.

### Configuration des règles {#uc3-rule-config}

Acheminez les événements du système vers un jeu de données de quarantaine dédié plutôt que de désactiver entièrement le service [!DNL Adobe Experience Platform]. Cela permet de conserver les événements à des fins de débogage avant de confirmer qu’ils ne comportent aucune valeur.

**Règle : événements système**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `decisioning.propositionFetch` |

Ajoutez une condition de [!DNL OR] pour les `personalization.request` et tout autre type d&#39;événement système que vous souhaitez supprimer.

- Service **[!DNL Adobe Experience Platform]:** activé
- **Remplacement du jeu de données d’événement :** `System Events - Quarantine` (jeu de données non activé pour un profil avec une fenêtre de conservation de 30 jours, à des fins de débogage et d’audit)
- **[!UICONTROL Segmentation ] / [!DNL Adobe Journey Optimizer] / [!UICONTROL Gestion des décisions]:** Activé si nécessaire

Après avoir acheminé ces événements vers le jeu de données de quarantaine, assurez-vous qu’il est exclu de votre connexion [!DNL Customer Journey Analytics].

>[!NOTE]
>
>La suppression des événements de `decisioning.propositionFetch` de [!DNL Adobe Experience Platform] ingestion ne désactive pas l’appel de personnalisation lui-même. [!DNL Adobe Target] et [!DNL Adobe Journey Optimizer] évaluent et renvoient toujours les décisions de personnalisation. Cette règle contrôle uniquement si [!DNL Adobe Experience Platform] stocke l’enregistrement d’événement système dans ses jeux de données.

## Cas pratique 4 : filtrage du trafic de robots {#uc4}

**Objectif :** empêcher les événements générés par les robots d’entrer dans le [!DNL Real-Time Customer Profile], de gonfler les mesures de [!DNL Customer Journey Analytics] ou d’utiliser le débit d’ingestion en flux continu.

**Utilisation :** vous avez activé la détection de robots sur votre flux de données et souhaitez agir sur les scores de robots affectés aux événements.

### Conditions préalables {#uc4-prerequisites}

Avant de configurer cette règle, effectuez la configuration de détection des robots décrite dans la [liste de contrôle des conditions préalables et de la planification](/help/datastreams/dynamic-configurations/prerequisites.md#schema-dataset) :

1. Activez la [détection de robots](/help/datastreams/bot-detection.md) sur le flux de données.
2. Ajoutez le groupe de champs **Informations de détection des robots** à votre schéma XDM.
3. Patientez jusqu’à 15 minutes pour que les règles de détection des robots se propagent avant le test.

### Configuration des règles {#uc4-rule-config}

Commencez toujours par mettre en quarantaine les événements de robots pour analyse. Après avoir vérifié que le score du robot est correct, vous pouvez continuer la mise en quarantaine ou choisir d’ignorer entièrement ces événements.

**Règle : trafic de robots**

| Champ | Opérateur | Valeur |
| ----- | -------- | ----- |
| `botDetection.score` | est égal à | `1` |

**Option A : Quarantaine pour analyse (recommandée initialement)**

- Service **[!DNL Adobe Experience Platform]:** activé
- **Remplacement du jeu de données d’événement :** `Bot Traffic - Quarantine` (hors profil, conservation de 30 jours)
- **Services Edge :** désactivé

Assurez-vous que ce jeu de données est exclu de votre connexion [!DNL Customer Journey Analytics].

**Option B : Ignorer complètement (après validation de l’option A)**

- Service **[!DNL Adobe Experience Platform]:** désactivé

Après avoir validé le jeu de données de quarantaine et confirmé que le score du robot est exact, désactivez le service [!DNL Adobe Experience Platform] dans la règle pour empêcher ces événements d’atteindre [!DNL Adobe Experience Platform].

Vous pouvez également désactiver d’autres services pour le trafic de robots dans des règles distinctes :

- **[!DNL Adobe Analytics]:** Désactivé. Cela empêche les deux accès de gonfler les mesures des suites de rapports.
- **[!DNL Adobe Target]:** Désactivé. Cela empêche les robots de fausser les résultats des tests A/B.

>[!NOTE]
>
>[!DNL Adobe Analytics] possède ses propres fonctionnalités de filtrage des robots. La désactivation des [!DNL Adobe Analytics] par le biais d’une règle de [!DNL Dynamic Datastream Configuration] pour le trafic de robots est une approche complémentaire. Demandez à votre équipe Analytics si le filtrage au niveau des trains de données et/ou Analytics est adapté à votre implémentation.

### Ordre des règles {#uc4-rule-ordering}

Placez la règle de filtrage des robots **en premier** dans votre liste de règles, avant toute règle **exploitable** ou **analytique**. Étant donné que l’Edge Network utilise une évaluation first-match-wins, le fait de placer cette règle en premier garantit qu’Edge Network intercepte et ignore le trafic de robots avant l’exécution de toute autre logique de routage. Le routage d’un événement de robot vers un jeu de données activé pour un profil consomme une capacité inutile de magasin de profils.

## Cas d’utilisation 5 : routage sélectif de la solution Experience Cloud {#uc5}

**Objectif :** contrôler quelles solutions Experience Cloud ([!DNL Adobe Analytics], [!DNL Adobe Target], [!DNL Adobe Audience Manager]) reçoivent des types d’événements spécifiques et remplacent les paramètres au niveau de la solution tels que les suites de rapports ou les jetons de propriété en fonction des conditions d’événement.

**Utilisation :** si vous souhaitez consolider plusieurs flux de données en un seul, différents types d’événements doivent accéder à différentes suites de rapports [!DNL Adobe Analytics], ou certains événements ne doivent pas atteindre les [!DNL Adobe Target] ou les [!DNL Adobe Audience Manager].

### Exemple A : remplacement des suites de rapports Analytics par type d’événement {#uc5-example-a}

Un seul flux de données desservant plusieurs sections du site qui dépendent de différentes suites de rapports :

**Règle 1 : Événements e-commerce**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | commence par | `commerce.` |

- **[!DNL Adobe Analytics]:** activé
- **Remplacement de la suite de rapports :** `rsid-commerce`

**Règle 2 : Événements de contenu**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `web.webpagedetails.pageViews` |

- **[!DNL Adobe Analytics]:** activé
- **Remplacement de la suite de rapports :** `rsid-content`

### Exemple B : désactivation de Target pour les événements Analytics {#uc5-example-b}

Empêchez les événements **analytiques** d’atteindre les [!DNL Adobe Target] afin de réduire le nombre de requêtes Target par seconde et les traitements inutiles :

**Règle : événements analytiques**

| Champ | Opérateur | Valeur |
|-------|----------|-------|
| `eventType` | est égal à | `web.webpagedetails.pageViews` |

- **[!DNL Adobe Target]:** désactivé
- **[!DNL Adobe Analytics]:** activé (suite de rapports par défaut)

### Exemple C : consolidation de plusieurs flux de données {#uc5-example-c}

Si vous conservez actuellement des flux de données distincts pour [!DNL Adobe Analytics] et [!DNL Adobe Target], [!DNL Event Forwarding], [!DNL Adobe Journey Optimizer] et [!DNL Customer Journey Analytics], vous pouvez les consolider en un seul flux de données :

1. [Activer tous les services](/help/datastreams/configure.md#add-services) sur un flux de données.
2. Utilisez des règles de [!DNL Dynamic Datastream Configuration] pour contrôler quels événements atteignent quels services.
3. Supprimez les événements `decisioning.propositionFetch` de [!DNL Adobe Experience Platform] (voir [cas d’utilisation 3](#uc3)).
4. Filtrez le trafic de robots avant qu’il n’atteigne un service (voir [cas d’utilisation 4](#uc4)).
5. Acheminer les événements **exploitables** et les événements **analytiques** vers les jeux de données appropriés (voir [cas d’utilisation 1](#uc1)).

Cela réduit la surcharge de gestion des flux de données et élimine la nécessité d’une logique côté client pour sélectionner des flux de données.

Pour obtenir un exemple complet de consolidation avec des tables de règles et une logique d&#39;ordre des règles, reportez-vous à l&#39;exemple [de bout en bout](/help/datastreams/dynamic-configurations/example.md).

## Cas d’utilisation 6 : migration à partir du connecteur source Analytics {#uc6}

**Objectif :** remplacer le [connecteur source Adobe Analytics](/help/sources/connectors/adobe-applications/analytics.md) par [collecte de données Web SDK](/help/collection/js/js-overview.md) tout en conservant le filtrage au niveau des lignes du connecteur source fourni.

**Utilisation :** vous effectuez une migration du connecteur source [!DNL Adobe Analytics] vers la collecte de données Web SDK dans [!DNL Adobe Experience Platform] et vous vous êtes fié au connecteur source pour filtrer les événements reçus par le profil.

### Approche de la migration {#uc6-migration}

Suivez ces étapes dans l’ordre. Les étapes 1 et 2 sont des étapes de planification que vous effectuez avant de toucher le flux de données.

**Étape 1 : Inventaire de vos filtres de connecteur source**

Documentez les événements que le connecteur source exclut actuellement de l’ingestion :

- Types d’événements exclus du profil (par exemple, pages vues, appels de liens personnalisés)
- Filtres de ligne basés sur des conditions spécifiques (par exemple, exclure le trafic interne)

**Étape 2 : Mapper les filtres du connecteur source aux règles**

| Filtre du connecteur Source | Équivalent de configuration de train de données dynamique |
| ---------------------- | ------------------------------------------- |
| Filtre de ligne : exclure le type d’événement X du profil | Règle : achemine les événements où `eventType` est égal à X vers un jeu de données ne concernant pas les profils |
| Filtre de ligne : exclure le trafic interne | Règle : achemine les événements où `email` contient des `@yourcompany.com` vers un jeu de données ne concernant pas les profils ou les ignore |

**Étape 3 : créer votre stratégie de jeu de données**

Suivez [cas d’utilisation 1](#uc1) ou [cas d’utilisation 2](#uc2) en fonction de vos besoins de conservation.

**Étape 4 : configurer des règles**

Implémentez les règles mappées à l’étape 2. Choisissez entre un modèle [Analytique en premier ou Exploitable en premier](/help/datastreams/dynamic-configurations/configuration-patterns.md#aep-patterns). Hiérarchisez d’abord les règles qui affectent le plus grand nombre d’événements et laissez tous les autres événements sur la version de secours par défaut.

**Étape 5 : exécution de l’ingestion parallèle**

Pendant la migration, exécutez en parallèle le connecteur source et l’ingestion Web SDK pour une fenêtre de validation. Comparer :

- Volumes d’événements par jeu de données
- Nombre de profils et volume total de données
- [!DNL Customer Journey Analytics] le nombre de lignes

Après avoir validé les résultats, désactivez le connecteur source.

>[!WARNING]
>
>Ne réutilisez pas les mêmes jeux de données pour le connecteur source [!DNL Adobe Analytics] et l’ingestion Web SDK. L’ingestion de deux sources dans le même jeu de données duplique vos données. Utilisez des jeux de données distincts pour chaque chemin d’ingestion et n’activez pas le jeu de données d’ingestion Web SDK pour le profil tant que la validation n’est pas terminée.

>[!NOTE]
>
>[!DNL Dynamic Datastream Configurations] fonctionnent au niveau du routage de l’événement et ne peuvent pas filtrer les champs individuels au sein d’un événement. Pour le contrôle au niveau du champ (au niveau des colonnes), concevez vos schémas XDM de manière à n’inclure que les champs dont chaque jeu de données a besoin et utilisez les mappages [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) pour contrôler quels champs sont mappés depuis votre couche de données brutes dans la payload XDM.

## Étapes suivantes

- Consultez l’[exemple complet](/help/datastreams/dynamic-configurations/example.md) pour voir plusieurs cas d’utilisation combinés dans une configuration de flux de données unique.
- Lisez [ Bonnes pratiques relatives à  [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/best-practices.md) avant de procéder au déploiement en production.
- Suivez les étapes de la section [Tester et valider [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/testing.md) pour vérifier que vos règles s’appliquent correctement au routage.
