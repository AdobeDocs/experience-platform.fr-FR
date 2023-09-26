---
title: Barrières de sécurité par défaut pour les données de profil client en temps réel
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel. Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données de profil afin d’optimiser les performances du système.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: d409c3f61824e77bfc26af577999d90d391f8a1b
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 78%

---

# Mécanismes de sécurisation par défaut pour les données [!DNL Real-Time Customer Profile]

Adobe Experience Platform vous permet de proposer des expériences cross-canal personnalisées basées sur des informations comportementales et des attributs du client sous la forme de profils client en temps réel. Pour prendre en charge cette nouvelle approche des profils, Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel.

Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données de profil afin d’optimiser les performances du système. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

>[!NOTE]
>
>La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Prise en main

Les services Experience Platform suivants sont impliqués dans la modélisation des données Real-Time Customer Profile :

* [[!DNL Real-Time Customer Profile]](home.md) : créez des profils clients unifiés à l’aide de données provenant de plusieurs sources.
* [Identités](../identity-service/home.md) : associez les identités à partir de sources de données disparates lors de leur ingestion dans Platform.
* [Schémas](../xdm/home.md) : les schémas du modèle de données d’expérience (XDM) sont le cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Audiences](../segmentation/home.md): le moteur de segmentation de Platform est utilisé pour créer des audiences à partir de vos profils clients en fonction des comportements et des attributs des clients.

## Types de limite

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.

* **Limite Hard :** une limite Hard fournit un maximum absolu.

>[!NOTE]
>
>Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Limites du modèle de données

Les barrières de sécurité suivantes fournissent des limites recommandées lors de la modélisation des données Real-Time Customer Profile. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

![Diagramme présentant les différentes barrières de sécurité pour les données de profil dans Adobe Experience Platform.](./images/guardrails/profile-guardrails.png)

### Mécanismes de sécurisation pour les entités principales

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Jeux de données de classe XDM Indivdual Profile | 20 | Soft | Il est recommandé d’utiliser au maximum 20 jeux de données qui exploitent la classe XDM Individual Profile. |
| Jeux de données de classe XDM ExperienceEvent | 20 | Soft | Il est recommandé d’utiliser au maximum 20 jeux de données qui exploitent la classe XDM ExperienceEvent. |
| Jeux de données de suites de rapports Adobe Analytics activés pour Profil | 1 | Soft | Un (1) jeu de données de suite de rapports Analytics maximum doit être activé pour Profil. Toute tentative d’activation de plusieurs jeux de données de suite de rapports Analytics pour Profil peut avoir des conséquences imprévues sur la qualité des données. Pour plus d’informations, voir la section sur les [Jeux de données Adobe Analytics](#aa-datasets) dans l’Annexe. |
| Relations à entités multiples | 5 | Soft | Il est recommandé d’établir au maximum 5 relations à entités multiples définies entre des entités principales et des entités de dimension. D’autres mappages de relation ne doivent pas être effectués tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Profondeur JSON du champ d’ID utilisé dans les relations à entités multiples | 4 | Soft | La profondeur JSON maximale recommandée pour un champ d’ID utilisé dans les relations à entités multiples est de 4. Cela signifie que dans un schéma fortement imbriqué, les champs imbriqués de plus de 4 niveaux de profondeur ne doivent pas être utilisés comme champ d’ID dans une relation. |
| Cardinalité de tableau dans un fragment de profil | &lt;=500 | Soft | La cardinalité de tableau optimale dans un fragment de profil (données indépendantes du temps) est &lt;=500. |
| Cardinalité de tableau dans ExperienceEvent | &lt;=10 | Soft | La cardinalité optimale des tableaux dans un ExperienceEvent (données de série temporelle) est &lt;=10. |
| Nombre d’identités pour le graphique d’identités d’un profil individuel | 50 | Hard | **Le nombre maximal d’identités dans un graphique d’identités pour un profil individuel est de 50.** Les profils comportant plus de 50 identités sont exclus de la segmentation, des exportations et des recherches. |

{style="table-layout:auto"}

### Mécanismes de sécurisation de l’entité de dimension

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune donnée de série temporelle n’est autorisée pour les entités non [!DNL XDM Individual Profile]. | 0 | Hard | **Les données de série temporelle ne sont pas autorisées pour les entités non [!DNL XDM Individual Profile] dans le service Profil.** Si un jeu de données de série temporelle est associé à un ID non [!DNL XDM Individual Profile], le jeu de données ne doit pas être activé pour [!DNL Profile]. |
| Aucune relation imbriquée | 0 | Soft | Vous ne devez pas créer de relation entre deux schémas non-[!DNL XDM Individual Profile]. La possibilité de créer des relations n’est pas recommandée pour les schémas qui ne font pas partie du schéma d’union [!DNL Profile]. |
| Profondeur JSON du champ de l’ID principal | 4 | Soft | La profondeur JSON maximale recommandée pour le champ de l’ID principal est de 4. Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas choisir un champ comme identifiant principal qui est imbriqué à plus de 4 niveaux de profondeur. Un champ qui est au quatrième niveau d’imbrication peut être utilisé comme ID principal. |

{style="table-layout:auto"}

## Limites de taille des données

Les mécanismes de sécurisation suivants se rapportent à la taille des données et fournissent des limites recommandées pour les données qui peuvent être ingérées, stockées et interrogées comme prévu. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

>[!NOTE]
>
>La taille des données est mesurée en tant que données non compressées dans JSON au moment de l’ingestion.

### Mécanismes de sécurisation pour les entités principales

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille maximale d’ExperienceEvent | 10 Ko | Hard | **La taille maximale d’un événement est de 10 Ko.** L’ingestion se poursuit, mais tous les événements de plus de 10 Ko seront ignorés. |
| Taille maximale d’enregistrement de profil | 100 Ko | Hard | **La taille maximale d’un enregistrement de profil est de 100 Mo.** L’ingestion se poursuit, mais les enregistrements de profil supérieurs à 100 Ko seront ignorés. |
| Taille maximale du fragment de profil | 50 Mo | Hard | **La taille maximale d’un fragment de profil est de 50 Mo.** La segmentation, les exportations et les recherches peuvent échouer pour tout [fragment de profil](#profile-fragments) qui dépasse 50 Mo. |
| Taille maximale de stockage du profil | 50 Mo | Soft | **La taille maximale d’un profil stocké est de 50 Mo.** Ajouter de nouveaux [fragments de profil](#profile-fragments) dans un profil de plus de 50 Mo affecte les performances du système. Par exemple, un profil peut contenir un fragment unique de 50 Mo ou plusieurs fragments répartis sur plusieurs jeux de données avec une taille totale de 50 Mo. Toute tentative de stockage d’un profil avec un fragment de plus de 50 Mo ou plusieurs fragments dont la taille totale est supérieure à 50 Mo aura une incidence sur les performances du système. |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | 90 | Soft | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. |
| Nombre d’ExperienceEvents par enregistrement de profil | 5000 | Soft | **Le nombre maximal d’ExperienceEvents par enregistrement de profil est de 5 000.** Les profils comportant plus de 5 000 ExperienceEvents **not** être pris en compte pour la segmentation ; |

{style="table-layout:auto"}

### Mécanismes de sécurisation de l’entité de dimension

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale pour toutes les entités de dimension | 5 Go | Soft | La taille totale recommandée pour toutes les entités dimensionnelles est de 5 Go. L’ingestion d’entités de dimension volumineuses peut affecter les performances du système. Par exemple, il n’est pas recommandé de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeux de données par schéma d’entité dimensionnelle | 5 | Soft | Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle. Par exemple, si vous créez un schéma pour les « produits » et ajoutez cinq jeux de données de contribution, vous ne devez pas créer un sixième jeu de données lié au schéma de produits. |
| Lots d’entités de dimension ingérés par jour | 4 par entité | Soft | Le nombre maximal recommandé de lots d’entités de dimension ingérés par jour est de 4 par entité. Par exemple, vous pouvez ingérer des mises à jour à un catalogue de produits jusqu’à 4 fois par jour. L’ingestion de lots d’entités de dimension supplémentaires pour la même entité peut affecter les performances du système. |

{style="table-layout:auto"}

## Mécanismes de sécurisation de la segmentation

Les barrières de sécurité décrites dans cette section font référence au nombre et à la nature des audiences qu’une organisation peut créer dans un Experience Platform, ainsi qu’au mappage et à l’activation d’audiences vers des destinations.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Audiences par environnement de test | 4 000 | Soft | Une organisation peut avoir plus de 4 000 audiences au total, à condition qu’il y ait moins de 4 000 audiences dans chaque environnement de test individuel. Toute tentative de création d’audiences supplémentaires peut affecter les performances du système. |
| Audiences Edge par environnement de test | 150 | Soft | Une organisation peut avoir plus de 150 audiences de périphérie au total, à condition qu’il y ait moins de 150 audiences de périphérie dans chaque environnement de test individuel. Toute tentative de création d’audiences Edge supplémentaires peut avoir une incidence sur les performances du système. |
| Audiences par environnement de test en flux continu | 500 | Soft | Une organisation peut avoir plus de 500 audiences en continu au total, à condition qu’il y ait moins de 500 audiences en continu dans chaque environnement de test individuel. Toute tentative de création d’audiences en continu supplémentaires peut affecter les performances du système. |
| Audiences par environnement de test par lot | 4 000 | Soft | Une organisation peut avoir plus de 4 000 audiences par lots au total, à condition qu’il y ait moins de 4 000 audiences par lots dans chaque environnement de test individuel. Toute tentative de création d’audiences par lots supplémentaires peut affecter les performances du système. |

{style="table-layout:auto"}

## Annexe

Cette section fournit des détails supplémentaires sur les limites de ce document.

### Types d’entités

Le modèle de la banque de données [!DNL Profile] se compose de deux types d’entités principales : [entités primaires](#primary-entity) et [entités de dimension](#dimension-entity).

#### Entité de Principal

Une entité principale, ou entité de profil, fusionne les données pour former une &quot;source unique de vérité&quot; pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrège les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d’union pour [!DNL Real-Time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme un conteneur pour tous les attributs de profil et événements comportementaux.

Les attributs indépendants du temps, également appelés « données d’enregistrement », sont modélisés à l’aide de [!DNL XDM Individual Profile], tandis que les données de série temporelle, également appelées « données d’événement », sont modélisées à l’aide de [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série temporelle sont ingérées dans Adobe Experience Platform, [!DNL Real-Time Customer Profile] commence à ingérer les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

![Infographie présentant les différences entre les données d’enregistrement et les données de série temporelle.](images/guardrails/profile-entity.png)

#### Entité de Dimension

Bien que la banque de données de profil conservant les données de profil ne soit pas une banque de données relationnelle, Profile permet l’intégration à de petites entités de dimension afin de créer des audiences d’une manière simplifiée et intuitive. Cette intégration est connue sous le nom de [segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md).

Votre entreprise peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces variables[!DNL XDM Individual Profile] Les schémas sont appelés &quot;entités de dimension&quot; (également appelées &quot;entités de recherche&quot;) et ne contiennent pas de données de série temporelle. Les schémas qui représentent des entités de dimension sont liés à des entités de profil grâce à l’utilisation de [relations de schéma](../xdm/tutorials/relationship-ui.md).

Les entités de dimension fournissent des données de recherche qui aident et simplifient les définitions de segment multi-entités. Elles doivent être suffisamment petites pour que le moteur de segmentation puisse charger l’ensemble des données en mémoire pour un traitement optimal (recherche de point rapide).

![Infographie montrant qu’une entité de profil est composée d’entités de dimension.](images/guardrails/profile-and-dimension-entities.png)

### Fragments de profil

Dans ce document, plusieurs mécanismes de sécurisation font référence à des « fragments de profil ». Dans Experience Platform, plusieurs fragments de profil sont fusionnés pour former le profil client en temps réel. Chaque fragment représente une identité principale unique et l’enregistrement correspondant ou l’ensemble complet de données d’événement pour cet identifiant, dans un jeu de données déterminé. Pour en savoir plus sur les fragments de profil, consultez la section [Présentation des profils](home.md#profile-fragments-vs-merged-profiles).

### Politiques de fusion {#merge-policies}

Lorsque des données sont extraites de plusieurs sources, les politiques de fusion sont les règles utilisées par Platform pour déterminer la hiérachisation et le choix des données à combiner pour créer cette vue unifiée. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client. Quand les données provenant de plusieurs sources entrent en conflit, la politique de fusion détermine les informations à inclure dans le profil de la personne. Au maximum, cinq (5) politiques de fusion sont autorisées par organisation. Pour en savoir plus sur les politiques de fusion, consultez la section [présentation des politiques de fusion](merge-policies/overview.md).

### Jeux de données de la suite de rapports Adobe Analytics dans Platform {#aa-datasets}

Plusieurs suites de rapports peuvent être activées pour Profil si tous les conflits de données sont résolus. Vous pouvez utiliser la fonctionnalité Préparation de données pour résoudre les conflits de données entre les eVar, les listes et les props. Pour en savoir plus sur l’utilisation de la fonctionnalité Préparation des données, consultez le [Guide de l’interface utilisateur du connecteur Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).
