---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;garde-fous;consignes;limite;entité;entité Principale;entité de dimension;
title: Barrières de sécurité pour les données de profil client en temps réel
solution: Experience Platform
product: experience platform
type: Documentation
description: Adobe Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des modèles de données que Real-time Customer Profile ne peut pas prendre en charge. Ce document décrit les bonnes pratiques et les contraintes à garder à l’esprit lors de la modélisation des données de profil.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 441c2978b90a4703874787b3ed8b94c4a7779aa8
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 6%

---

# Barrières de sécurité pour les données [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fournit des profils individuels qui vous permettent de proposer des expériences cross-canal personnalisées en fonction des informations comportementales et des attributs du client. Pour atteindre ce ciblage, [!DNL Profile] et le moteur de segmentation dans Adobe Experience Platform utilisent un modèle de données hybride fortement dénormalisé qui offre une nouvelle approche pour développer les profils client. L’utilisation de ce modèle de données hybride rend important le fait que les données collectées soient correctement modélisées. Bien que la [!DNL Profile] banque de données conservant les données de profil ne soit pas un magasin relationnel, [!DNL Profile] permet l’intégration à de petites entités de dimension afin de créer des segments de manière simplifiée et intuitive. Cette intégration est connue sous le nom de segmentation d’entités multiples.

Adobe Experience Platform fournit une série de barrières de sécurité pour vous aider à éviter de créer des modèles de données que [!DNL Real-time Customer Profile] ne peut pas prendre en charge. Ce document décrit ces barrières de sécurité, les bonnes pratiques et les contraintes lors de l’utilisation des données de profil pour la segmentation.

>[!NOTE]
>
>Les barrières de sécurité et les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.

## Prise en main

Il est recommandé de lire la documentation des services Experience Platform ci-après avant de tenter de créer des modèles de données à utiliser dans [!DNL Real-time Customer Profile]. L’utilisation des modèles de données et des barrières de sécurité décrites dans ce document nécessite une compréhension des différents services Experience Platform impliqués dans la gestion des entités [!DNL Real-time Customer Profile] :

* [[!DNL Real-time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service Adobe Experience Platform Identity](../identity-service/home.md) : Prend en charge la création d’une &quot;vue unique du client&quot; en rapprochant les identités de sources de données disparates lors de leur ingestion dans  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
   * [Principes de base de la composition](../xdm/schema/composition.md) des schémas : Cette section présente les schémas et la modélisation des données dans Experience Platform.
* [Service de segmentation Adobe Experience Platform](../segmentation/home.md) : moteur de segmentation de [!DNL Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.
   * [Segmentation d’entités multiples](../segmentation/multi-entity-segmentation.md) : Guide de création de segments qui intègrent des entités de dimension aux données de profil.

## Types d’entité

Le modèle de données de magasin [!DNL Profile] se compose de deux types d’entité principaux :

* **Entité Principal :** une entité Principale, ou entité de profil, fusionne les données pour former une &quot;source unique de vérité&quot; pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrège les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d’union pour [!DNL Real-time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme un conteneur pour tous les attributs de profil et événements comportementaux.

   Les attributs indépendants du temps, également appelés &quot;données d’enregistrement&quot;, sont modélisés à l’aide de [!DNL XDM Individual Profile], tandis que les données de série temporelle, également appelées &quot;données d’événement&quot;, sont modélisées à l’aide de [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série temporelle sont ingérées dans Adobe Experience Platform, [!DNL Real-time Customer Profile] commence à ingérer les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

   ![](images/guardrails/profile-entity.png)

* **Entité de Dimension :** votre entreprise peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces schémas non-[!DNL XDM Individual Profile] sont appelés &quot;entités de dimension&quot; et ne contiennent pas de données de série temporelle. Les entités de Dimension fournissent des données de recherche qui aident et simplifient les définitions de segment multi-entités. Elles doivent être suffisamment petites pour que le moteur de segmentation puisse charger l’ensemble des données en mémoire pour un traitement optimal (recherche de point rapide).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Fragments de profil

Ce document comporte plusieurs barrières de sécurité faisant référence à des &quot;fragments de profil&quot;. Le profil client en temps réel est composé de plusieurs fragments de profil. Chaque fragment représente les données de l’identité d’un jeu de données où il s’agit de l’identité Principale. Cela signifie qu’un fragment peut contenir un identifiant Principal et des données d’événement (série temporelle) dans un jeu de données XDM ExperienceEvent ou qu’il peut être composé d’un identifiant Principal et de données d’enregistrement (attributs indépendants du temps) dans un jeu de données XDM Individual Profile.

## Types de limite

Lors de la définition de votre modèle de données, il est recommandé de rester dans les barrières de sécurité fournies pour garantir des performances correctes et éviter les erreurs système.

Les barrières de sécurité fournies dans ce document incluent deux types de limites :

* **Limite de soft :** une limite de soft offre un maximum recommandé pour des performances optimales du système. Il est possible d’aller au-delà d’une limite souple sans endommager le système ni recevoir de messages d’erreur, mais dépasser cette limite entraînera une dégradation des performances. Il est recommandé de rester dans les limites de soft afin d’éviter des baisses de performances globales.

* **Limite stricte :** une limite stricte fournit un maximum absolu au système. Si vous dépassez cette limite, des pannes et des erreurs s’affichent, ce qui empêche le système de fonctionner comme prévu.

## Barrières de sécurité du modèle de données

Il est recommandé de respecter les barrières de sécurité suivantes lors de la création d’un modèle de données à utiliser avec [!DNL Real-time Customer Profile].

### Barrières de sécurité Principales pour les entités

| Guardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre de jeux de données recommandés pour contribuer au schéma d’union [!DNL Profile] | 20 | Soft | **Il est recommandé d’utiliser un maximum de 20 jeux de données  [!DNL Profile]activés.** Pour activer un autre jeu de données pour  [!DNL Profile], un jeu de données existant doit d’abord être supprimé ou désactivé. |
| Nombre de relations multi-entités recommandé | 5 | Soft | **Il est recommandé d’établir au maximum 5 relations multientités définies entre des entités Principales et des entités de dimension.** D’autres mappages de relation ne doivent pas être effectués tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Profondeur JSON maximale pour le champ d’ID utilisé dans les relations entre entités multiples | 4 | Soft | **La profondeur maximale recommandée pour un champ d’ID utilisé dans les relations multi-entités est de 4.** Cela signifie que dans un schéma fortement imbriqué, les champs imbriqués de plus de 4 niveaux de profondeur ne doivent pas être utilisés comme champ d’identifiant dans une relation. |
| Cardinalité d’un tableau dans un fragment de profil | &lt;=500 | Soft | **La cardinalité optimale du tableau dans un fragment de profil (données indépendantes du temps) est la suivante :  &lt;>** |
| Cardinalité des tableaux dans ExperienceEvent | &lt;=10 | Soft | **La cardinalité optimale du tableau dans un ExperienceEvent (données de série temporelle) est :  &lt;>** |

### Protections des entités de Dimension

| Guardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune donnée de série temporelle n’est autorisée pour les entités non-[!DNL XDM Individual Profile] | 0 | Hard | **Les données de série temporelle ne sont pas autorisées pour les non-[!DNL XDM Individual Profile] entités dans le service de profil.** Si un jeu de données de série temporelle est associé à un non-[!DNL XDM Individual Profile] ID, le jeu de données ne doit pas être activé pour  [!DNL Profile]. |
| Aucune relation imbriquée | 0 | Soft | **Vous ne devez pas créer de relation entre deux non-[!DNL XDM Individual Profile] schémas.** La possibilité de créer des relations n’est pas recommandée pour les schémas qui ne font pas partie du schéma d’ [!DNL Profile] union. |
| Profondeur JSON maximale pour le champ d’identifiant Principal | 4 | Soft | **La profondeur maximale recommandée pour le champ d’identifiant Principal est de 4.** Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas sélectionner un champ comme identifiant Principal s’il est imbriqué à plus de 4 niveaux de profondeur. Un champ situé au quatrième niveau imbriqué peut être utilisé comme Principal ID. |

## Barrières de sécurité de la taille des données

Les barrières de sécurité suivantes se rapportent à la taille des données et sont recommandées pour s’assurer que les données peuvent être ingérées, stockées et interrogées comme prévu.

>[!NOTE]
>
>La taille des données est mesurée en tant que données non compressées dans JSON au moment de l’ingestion.

### Barrières de sécurité Principales pour les entités

| Guardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille maximale d’ExperienceEvent | 10 Ko | Hard | **La taille maximale d’un événement est de 10 Ko.** L’ingestion se poursuit, mais tous les événements de plus de 10 Ko seront ignorés. |
| Taille maximale d’enregistrement de profil | 100 Ko | Hard | **La taille maximale d’un enregistrement de profil est de 100 Ko.** L’ingestion se poursuit, mais les enregistrements de profil supérieurs à 100 Ko seront supprimés. |
| Taille maximale du fragment de profil | 50 Mo | Hard | **La taille maximale d’un fragment de profil est de 50 Mo.** La segmentation, les exportations et les recherches peuvent échouer pour tout  [ ](#profile-fragments) fragment de profil supérieur à 50 Mo. |
| Taille maximale de stockage du profil | 50 Mo | Soft | **La taille maximale d’un profil stocké est de 50 Mo.** L’ajout de nouveaux  [fragments de ](#profile-fragments) profil dans un profil supérieur à 50 Mo affecte les performances du système. |
| Nombre de lots Profile ou ExperienceEvent ingérés par jour | 90 | Soft | **Le nombre maximal de lots Profile ou ExperienceEvent ingérés par jour est de 90.** Cela signifie que le total combiné des lots Profile et ExperienceEvent ingérés chaque jour ne peut pas dépasser 90. L’ingestion de lots supplémentaires affectera les performances du système. |

### Protections des entités de Dimension

| Guardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale maximale pour toutes les entités dimensionnelles | 5 Go | Soft | **La taille totale maximale recommandée pour toutes les entités dimensionnelles est de 5 Go.** L’ingestion d’entités de dimension volumineuses entraîne une dégradation des performances du système. Par exemple, il n’est pas recommandé de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeux de données par schéma d’entité dimensionnelle | 5 | Soft | **Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle.** Par exemple, si vous créez un schéma pour &quot;products&quot; et ajoutez cinq jeux de données de contribution, vous ne devez pas créer un sixième jeu de données lié au schéma de produits. |
| Nombre de lots d’entités de dimension ingérés par jour | 4 par entité | Soft | **Le nombre maximal de lots d’entités de dimension ingérés par jour est de 4 par entité.** Par exemple, vous pouvez ingérer des mises à jour à un catalogue de produits jusqu’à 4 fois par jour. L’ingestion de lots d’entités de dimension supplémentaires pour la même entité affectera les performances du système. |

## Protections de la segmentation

Les barrières de sécurité décrites dans cette section font référence au nombre et à la nature des segments qu’une organisation peut créer dans Experience Platform, ainsi qu’au mappage et à l’activation de segments vers des destinations.

| Guardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de segments par environnement de test | 10 000 | Soft | **Le nombre maximal de segments qu’une organisation peut créer est de 10 000 par environnement de test.** Une organisation peut avoir plus de 10 000 segments au total, à condition qu’il y ait moins de 10 000 segments dans chaque environnement de test individuel. Toute tentative de création de segments supplémentaires entraînera une dégradation des performances du système. |
| Nombre maximal de segments de diffusion en continu par environnement de test | 500 | Soft | **Le nombre maximal de segments en flux continu qu’une organisation peut créer est de 500 par environnement de test.** Une organisation peut avoir plus de 500 segments en flux continu au total, à condition qu’il y ait moins de 500 segments en flux continu dans chaque environnement de test individuel. Toute tentative de création de segments de diffusion en continu supplémentaires entraînera une dégradation des performances du système. |
| Nombre maximal de segments par lot par environnement de test | 10 000 | Soft | **Le nombre maximal de segments par lot qu’une organisation peut créer est de 10 000 par environnement de test.** Une organisation peut avoir plus de 10 000 segments par lot au total, à condition qu’il y ait moins de 10 000 segments par lot dans chaque environnement de test individuel. Toute tentative de création de segments par lot supplémentaires entraînera une dégradation des performances du système. |
