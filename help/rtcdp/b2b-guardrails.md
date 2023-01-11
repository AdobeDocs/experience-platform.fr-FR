---
keywords: profil;profil client en temps réel;dépannage;garde-fous;directives;limite;entité;entité Principale;entité de dimension;RTCDP;CDP;Édition B2B;Real-time Customer Data Platform;plateforme de données client en temps réel;cdp en temps réel;b2b;cdp;
title: Barrières de sécurité par défaut pour Real-time Customer Data Platform version B2B
type: Documentation
description: Adobe Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel. Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données pour optimiser les performances du système à l’aide de l’édition B2B d’Adobe Real-time Customer Data Platform.
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '1651'
ht-degree: 59%

---

# Barrières de sécurité par défaut pour Real-time Customer Data Platform version B2B

>[!NOTE]
>
>Les limites décrites dans ce document représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

L’édition B2B de Real-time Customer Data Platform vous permet de proposer des expériences cross-canal personnalisées basées sur des informations comportementales et des attributs du client sous la forme de profils client et de profils de compte en temps réel. Pour prendre en charge cette nouvelle approche des profils, Experience Platform utilise un modèle de données hybride fortement dénormalisé qui diffère du modèle de données relationnelles traditionnel.

Ce document fournit des limites d’utilisation et de débit par défaut pour vous aider à modéliser vos données pour optimiser les performances du système. Lors de la révision des barrières de sécurité suivantes, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

>[!INFO]
>
>La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Types de limite

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.

* **Limite Hard :** une limite Hard fournit un maximum absolu.

>[!INFO]
>
>Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.

## Limites du modèle de données

Les barrières de sécurité suivantes fournissent des limites recommandées lors de la modélisation des données Real-Time Customer Profile. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

### Barrières de sécurité pour les entités principales

>[!NOTE]
>
>Les limites de modèle de données décrites dans cette section représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Jeux de données de classe XDM standard Real-Time CDP B2B Edition | 60 | Soft | Il est recommandé d’utiliser un maximum de 60 jeux de données qui utilisent les classes XDM (Experience Data Model) standard fournies par Real-Time CDP B2B Edition. Pour obtenir la liste complète des classes XDM standard pour les cas d’utilisation B2B, reportez-vous à la section [schémas dans la documentation de Real-Time CDP B2B Edition](schemas/b2b.md). <br/><br/>*Remarque : en raison de la nature du modèle de données hybride dénormalisé d’Experience Platform, la plupart des clients ne dépasse pas cette limite. Pour toute question sur la manière de modéliser vos données ou pour en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.* |
| Anciennes relations à entités multiples | 20 | Soft | Il est recommandé d’établir au maximum 20 relations à entités multiples définies entre des entités principales et des entités de dimension. D’autres mappages de relation ne doivent pas être effectués tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Relations multiples-à-un par classe XDM | 2 | Soft | Il est recommandé de définir au maximum 2 relations multiples-à-un par classe XDM. Une relation supplémentaire ne doit pas être établie tant qu’une relation existante n’a pas été supprimée ou désactivée. Pour savoir comment créer une relation entre deux schémas, reportez-vous au tutoriel sur la [définition des relations de schéma B2B](../xdm/tutorials/relationship-b2b.md). |

### Barrières de sécurité de l’entité de dimension

>[!NOTE]
>
>Les limites de modèle de données décrites dans cette section représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune relation héritée imbriquée | 0 | Soft | Vous ne devez pas créer de relation entre deux schémas non-[!DNL XDM Individual Profile]. La possibilité de créer des relations n’est pas recommandée pour les schémas qui ne font pas partie du schéma d’union [!DNL Profile]. |
| Seuls les objets B2B peuvent participer à des relations multiples-à-un | 0 | Hard | Le système ne prend en charge que les relations multiples-à-un entre les objets B2B. Pour plus d’informations sur les relations multiples-à-un, consultez le tutoriel sur la [définition des relations de schéma B2B](../xdm/tutorials/relationship-b2b.md). |
| Profondeur maximale des relations imbriquées entre les objets B2B | 3 | Hard | La profondeur maximale des relations imbriquées entre les objets B2B est de 3. Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas avoir de relation entre des objets B2B imbriqués à plus de 3 niveaux. |

## Limites de taille des données

Les barrières de sécurité suivantes se rapportent à la taille des données et fournissent des limites recommandées pour les données qui peuvent être ingérées, stockées et interrogées comme prévu. Pour en savoir plus sur les entités principales et les entités de dimension, consultez la section sur les [types d’entités](#entity-types) dans l’Annexe.

>[!INFO]
>
>La taille des données est mesurée en tant que données non compressées dans JSON au moment de l’ingestion.

### Barrières de sécurité pour les entités principales

>[!NOTE]
>
>Les limites de taille des données décrites dans cette section représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Lots ingérés par classe XDM par jour | 45 | Soft | Le nombre total de lots ingérés chaque jour par classe XDM ne doit pas dépasser 45. L’ingestion de lots supplémentaires peut empêcher une performance optimale. |

### Barrières de sécurité de l’entité de dimension

>[!NOTE]
>
>Les limites de taille des données décrites dans cette section représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale pour toutes les entités de dimension | 5 Go | Soft | La taille totale recommandée pour toutes les entités dimensionnelles est de 5 Go. L’ingestion d’entités de dimension volumineuses peut affecter les performances du système. Par exemple, il n’est pas recommandé de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeux de données par schéma d’entité dimensionnelle | 5 | Soft | Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle. Par exemple, si vous créez un schéma pour les « produits » et ajoutez cinq jeux de données de contribution, vous ne devez pas créer un sixième jeu de données lié au schéma de produits. |
| Lots d’entités de dimension ingérés par jour | 4 par entité | Soft | Le nombre maximal recommandé de lots d’entités de dimension ingérés par jour est de 4 par entité. Par exemple, vous pouvez ingérer des mises à jour à un catalogue de produits jusqu’à 4 fois par jour. L’ingestion de lots d’entités de dimension supplémentaires pour la même entité peut affecter les performances du système. |

## Barrières de sécurité de la segmentation

Les barrières de sécurité décrites dans cette section font référence au nombre et à la nature des segments qu’une organisation peut créer dans Experience Platform, ainsi qu’au mappage et à l’activation de segments vers des destinations.

>[!NOTE]
>
>Les limites de segmentation décrites dans cette section représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Segments par sandbox B2B | 400 | Soft | Une organisation peut avoir plus de 400 segments au total, à condition qu’il y ait moins de 400 segments dans chaque sandbox B2B individuelle. Toute tentative de création de segments supplémentaires peut affecter les performances du système. |

## Étapes suivantes

Les limites décrites dans ce document représentent les modifications activées par Real-time Customer Data Platform B2B Edition. Pour obtenir une liste complète des limites par défaut de l’édition B2B de Real-Time CDP, combinez ces limites aux limites générales de Adobe Experience Platform décrites dans la section [Barrières de sécurité de la documentation sur les données Real-time Customer Profile](../profile/guardrails.md).

## Annexe

Cette section fournit des détails supplémentaires sur les limites de ce document.

### Types d’entités

Le modèle de la banque de données [!DNL Profile] se compose de deux types d’entités principales : [Principales entités](#primary-entity) et [entités de dimension](#dimension-entity).

#### Entité Principal

Une entité Principale, ou entité de profil, fusionne les données pour former une &quot;source unique de vérité&quot; pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrège les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d’union pour [!DNL Real-Time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme un conteneur pour tous les attributs de profil et événements comportementaux.

Les attributs indépendants du temps, également appelés « données d’enregistrement », sont modélisés à l’aide de [!DNL XDM Individual Profile], tandis que les données de série temporelle, également appelées « données d’événement », sont modélisées à l’aide de [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série temporelle sont ingérées dans Adobe Experience Platform, [!DNL Real-Time Customer Profile] commence à ingérer les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

![Infographie présentant les différences entre les données d’enregistrement et les données de série temporelle.](../profile/images/guardrails/profile-entity.png)

#### Entité de Dimension

Bien que la banque de données de profil conservant les données de profil ne soit pas un magasin relationnel, Profile permet l’intégration à de petites entités de dimension afin de créer des segments d’une manière simplifiée et intuitive. Cette intégration est connue sous le nom de [segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md).

Votre entreprise peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces[!DNL XDM Individual Profile] Les schémas sont appelés &quot;entités de dimension&quot; (également appelées &quot;entités de recherche&quot;) et ne contiennent pas de données de série temporelle. Les schémas qui représentent des entités de dimension sont liés à des entités de profil grâce à l’utilisation de [relations de schéma](../xdm/tutorials/relationship-ui.md).

Les entités de dimension fournissent des données de recherche qui aident et simplifient les définitions de segment multi-entités. Elles doivent être suffisamment petites pour que le moteur de segmentation puisse charger l’ensemble des données en mémoire pour un traitement optimal (recherche de point rapide).

![Infographie montrant qu’une entité de profil est composée d’entités de dimension.](../profile/images/guardrails/profile-and-dimension-entities.png)