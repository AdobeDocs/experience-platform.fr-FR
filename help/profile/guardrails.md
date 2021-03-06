---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;garde-fous;consignes;limite;entité;entité Principale;entité de dimension;
title: Barrières de sécurité par défaut pour les données de profil client en temps réel
solution: Experience Platform
product: experience platform
type: Documentation
description: 'Adobe Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel. Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données Profile afin d’optimiser les performances du système. '
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 8a343ad275dcfc33eb304e3fc19d375b81277448
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 49%

---

# Barrières de sécurité par défaut pour [!DNL Real-time Customer Profile] data

Adobe Experience Platform vous permet de proposer des expériences cross-canal personnalisées basées sur des informations comportementales et des attributs du client sous la forme de profils client en temps réel. Pour prendre en charge cette nouvelle approche des profils, Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel.

Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données Profile afin d’optimiser les performances du système. Lors de la révision des barrières de sécurité suivantes, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

>[!NOTE]
>
>La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Prise en main

Les services Experience Platform suivants sont impliqués dans la modélisation des données Real-time Customer Profile :

* [[!DNL Real-time Customer Profile]](home.md): Créez des profils consommateurs unifiés à l’aide de données provenant de plusieurs sources.
* [Identités](../identity-service/home.md): Associez les identités à partir de sources de données disparates lors de leur ingestion dans Platform.
* [Schémas](../xdm/home.md): Les schémas de modèle de données d’expérience (XDM) sont le cadre normalisé selon lequel Platform organise les données d’expérience client.
* [Segments](../segmentation/home.md): Le moteur de segmentation de Platform est utilisé pour créer des segments à partir de vos profils clients en fonction des comportements et des attributs des clients.

## Types de limite

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.

* **Limite Hard :** une limite Hard fournit un maximum absolu.

>[!NOTE]
>
>Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Limites du modèle de données

Les barrières de sécurité suivantes fournissent des limites recommandées lors de la modélisation des données Real-time Customer Profile. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

### Barrières de sécurité pour les entités principales

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Jeux de données de classe XDM Individual Profile | 20 | Soft | Il est recommandé d’utiliser au maximum 20 jeux de données qui exploitent la classe XDM Individual Profile. |
| Jeux de données de classe XDM ExperienceEvent | 20 | Soft | Il est recommandé d’utiliser au maximum 20 jeux de données qui utilisent la classe XDM ExperienceEvent. |
| Jeux de données de suites de rapports Adobe Analytics activés pour Profile | 1 | Soft | Un (1) jeu de données de suite de rapports Analytics doit être activé au maximum pour Profile. Toute tentative d’activation de plusieurs jeux de données de suite de rapports Analytics pour Profile peut avoir des conséquences imprévues sur la qualité des données. Pour plus d’informations, voir la section sur [Jeux de données Adobe Analytics](#aa-datasets) dans l’ Annexe . |
| Relations multi-entités | 5 | Soft | Il est recommandé d’établir au maximum 5 relations à entités multiples définies entre des entités principales et des entités de dimension. D’autres mappages de relation ne doivent pas être effectués tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Profondeur JSON du champ d’ID utilisé dans les relations entre plusieurs entités | 4 | Soft | La profondeur maximale recommandée pour un champ d’ID utilisé dans les relations multi-entités est de 4. Cela signifie que dans un schéma fortement imbriqué, les champs imbriqués de plus de 4 niveaux de profondeur ne doivent pas être utilisés comme champ d’identifiant dans une relation. |
| Cardinalité d’un tableau dans un fragment de profil | &lt;=500 | Soft | La cardinalité optimale du tableau dans un fragment de profil (données indépendantes du temps) est &lt;=500. |
| Cardinalité des tableaux dans ExperienceEvent | &lt;=10 | Soft | La cardinalité optimale des tableaux dans un ExperienceEvent (données de série temporelle) est &lt;=10. |
| Nombre d’identités pour le graphique d’identités d’un profil individuel | 50 | Hard | **Le nombre maximal d’identités dans un graphique d’identités pour un profil individuel est de 50.** Les profils comportant plus de 50 identités sont exclus de la segmentation, des exportations et des recherches. |

{style=&quot;table-layout:auto&quot;}

### Barrières de sécurité de l’entité de dimension

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune donnée de série temporelle n’est autorisée pour les variables[!DNL XDM Individual Profile] entities | 0 | Hard | **Les données de série temporelle ne sont pas autorisées pour les variables[!DNL XDM Individual Profile] entités dans le service de profil.** Si un jeu de données de série temporelle est associé à un événement[!DNL XDM Individual Profile] Identifiant, le jeu de données ne doit pas être activé pour [!DNL Profile]. |
| Aucune relation imbriquée | 0 | Soft | Vous ne devez pas créer de relation entre deux schémas non-[!DNL XDM Individual Profile]. La possibilité de créer des relations n’est pas recommandée pour les schémas qui ne font pas partie du schéma d’union [!DNL Profile]. |
| Profondeur JSON du champ d’identifiant Principal | 4 | Soft | La profondeur maximale recommandée pour le champ d’identifiant Principal est de 4. Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas sélectionner un champ comme identifiant Principal s’il est imbriqué à plus de 4 niveaux de profondeur. Un champ situé au quatrième niveau imbriqué peut être utilisé comme Principal ID. |

{style=&quot;table-layout:auto&quot;}

## Limites de taille des données

Les barrières de sécurité suivantes se rapportent à la taille des données et fournissent des limites recommandées pour les données qui peuvent être ingérées, stockées et interrogées comme prévu. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

>[!NOTE]
>
>La taille des données est mesurée en tant que données non compressées dans JSON au moment de l’ingestion.

### Barrières de sécurité pour les entités principales

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille maximale d’ExperienceEvent | 10 Ko | Hard | **La taille maximale d’un événement est de 10 Ko.** L’ingestion se poursuit, mais tous les événements de plus de 10 Ko seront ignorés. |
| Taille maximale d’enregistrement de profil | 100 Ko | Hard | **La taille maximale d’un enregistrement de profil est de 100 Ko.** L’ingestion se poursuit, mais les enregistrements de profil supérieurs à 100 Ko seront supprimés. |
| Taille maximale du fragment de profil | 50 Mo | Hard | **La taille maximale d’un fragment de profil unique est de 50 Mo.** La segmentation, les exportations et les recherches peuvent échouer pour toutes les [fragment de profil](#profile-fragments) qui dépasse 50 Mo. |
| Taille maximale de stockage du profil | 50 Mo | Soft | **La taille maximale d’un profil stocké est de 50 Mo.** Ajouter de nouvelles [fragments de profil](#profile-fragments) dans un profil de plus de 50 Mo affecte les performances du système. Par exemple, un profil peut contenir un fragment unique de 50 Mo ou plusieurs fragments répartis dans plusieurs jeux de données avec une taille totale combinée de 50 Mo. Toute tentative de stockage d’un profil avec un fragment unique de plus de 50 Mo ou plusieurs fragments dont la taille combinée est supérieure à 50 Mo aura une incidence sur les performances du système. |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | 90 | Soft | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. |

{style=&quot;table-layout:auto&quot;}

### Barrières de sécurité de l’entité de dimension

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale pour toutes les entités de dimension | 5 Go | Soft | La taille totale recommandée pour toutes les entités dimensionnelles est de 5 Go. L’ingestion d’entités de dimension volumineuses peut affecter les performances du système. Par exemple, il n’est pas recommandé de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeux de données par schéma d’entité dimensionnelle | 5 | Soft | Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle. Par exemple, si vous créez un schéma pour les « produits » et ajoutez cinq jeux de données de contribution, vous ne devez pas créer un sixième jeu de données lié au schéma de produits. |
| Lots d’entités de dimension ingérés par jour | 4 par entité | Soft | Le nombre maximal recommandé de lots d’entités de dimension ingérés par jour est de 4 par entité. Par exemple, vous pouvez ingérer des mises à jour à un catalogue de produits jusqu’à 4 fois par jour. L’ingestion de lots d’entités de dimension supplémentaires pour la même entité peut affecter les performances du système. |

{style=&quot;table-layout:auto&quot;}

## Barrières de sécurité de la segmentation

Les barrières de sécurité décrites dans cette section font référence au nombre et à la nature des segments qu’une organisation peut créer dans Experience Platform, ainsi qu’au mappage et à l’activation de segments vers des destinations.

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Segments par environnement de test | 10 000 | Soft | Une organisation peut avoir plus de 10,000 segments au total, à condition qu’il y ait moins de 10,000 segments dans chaque sandbox individuelle. Toute tentative de création de segments supplémentaires peut affecter les performances du système. |
| Segments de diffusion en continu par environnement de test | 500 | Soft | Une organisation peut avoir plus de 500 segments en flux continu au total, à condition qu’il y ait moins de 500 segments en flux continu dans chaque environnement de test individuel. Toute tentative de création de segments de diffusion en continu supplémentaires peut affecter les performances du système. |
| Segments par lot par environnement de test | 10 000 | Soft | Une organisation peut avoir plus de 10 000 segments par lot au total, à condition qu’il y ait moins de 10 000 segments par lot dans chaque environnement de test individuel. Toute tentative de création de segments par lot supplémentaires peut affecter les performances du système. |

{style=&quot;table-layout:auto&quot;}

## Annexe

Cette section fournit des détails supplémentaires sur les limites de ce document.

### Types d’entités

Le modèle de la banque de données [!DNL Profile] se compose de deux types d’entités principales :

* **Entité principal :** une entité principale, ou entité de profil, fusionne les données pour former une « source unique de vérité » pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrège les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d’union pour [!DNL Real-time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme un conteneur pour tous les attributs de profil et événements comportementaux.

   Les attributs indépendants du temps, également appelés « données d’enregistrement », sont modélisés à l’aide de [!DNL XDM Individual Profile], tandis que les données de série temporelle, également appelées « données d’événement », sont modélisées à l’aide de [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série temporelle sont ingérées dans Adobe Experience Platform, [!DNL Real-time Customer Profile] commence à ingérer les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

   ![](images/guardrails/profile-entity.png)

* **Entité de dimension :** bien que la banque de données de profil conservant les données de profil ne soit pas un magasin relationnel, Profile permet l’intégration à de petites entités de dimension afin de créer des segments d’une manière simplifiée et intuitive. Cette intégration est connue sous le nom de [segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md). Votre entreprise peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces schémas non-[!DNL XDM Individual Profile] sont appelés « entités de dimension » et ne contiennent pas de données de série temporelle. Les entités de dimension fournissent des données de recherche qui aident et simplifient les définitions de segment multi-entités. Elles doivent être suffisamment petites pour que le moteur de segmentation puisse charger l’ensemble des données en mémoire pour un traitement optimal (recherche de point rapide).

   ![](images/guardrails/profile-and-dimension-entities.png)

### Fragments de profil

Dans ce document, plusieurs barrières de sécurité font référence à des &quot;fragments de profil&quot;. Dans Experience Platform, plusieurs fragments de profil sont fusionnés pour former Real-time Customer Profile. Chaque fragment représente une identité Principale unique et les données d’enregistrement ou d’événement correspondantes pour cet identifiant dans un jeu de données donné. Pour en savoir plus sur les fragments de profil, reportez-vous à la section [Présentation des profils](home.md#profile-fragments-vs-merged-profiles).

### Stratégies de fusion {#merge-policies}

Lorsque vous rassemblez des données provenant de plusieurs sources, les stratégies de fusion sont les règles utilisées par Platform pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer cette vue unifiée. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client. Lorsque les données provenant de plusieurs sources entrent en conflit, la stratégie de fusion détermine les informations à inclure dans le profil de l’individu. Pour en savoir plus sur les stratégies de fusion, commencez par lire la [présentation des stratégies de fusion](merge-policies/overview.md).

### Jeux de données de suite de rapports Adobe Analytics dans Platform {#aa-datasets}

Un (1) jeu de données de suite de rapports Adobe Analytics maximum doit être activé pour Profile. Il s’agit d’une limite soft, ce qui signifie que vous pouvez activer plusieurs jeux de données Analytics pour Profile, mais elle n’est pas recommandée, car elle peut avoir des conséquences inattendues sur vos données. Cela est dû aux différences entre les schémas du modèle de données d’expérience (XDM), qui fournissent la structure sémantique des données dans Experience Platform et permettent une cohérence dans l’interprétation des données, ainsi que la nature personnalisable des eVars et des variables de conversion dans Adobe Analytics.

Par exemple, dans Adobe Analytics, une seule organisation peut avoir plusieurs suites de rapports. Si la suite de rapports A désigne l’eVar 4 comme &quot;terme de recherche interne&quot; et que la suite de rapports B désigne l’eVar 4 comme &quot;domaine référent&quot;, ces valeurs seront toutes deux ingérées dans le même champ de Profile, ce qui entraînera une confusion et dégradera la qualité des données.
