---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; garde-fous ; directives ; limite ; entité ; Principale ; entité de dimension ;
title: Garanties pour les données de Profil client en temps réel
solution: Experience Platform
product: experience platform
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des modèles de données que le Profil client en temps réel ne peut pas prendre en charge. Ce document décrit les meilleures pratiques et les contraintes à garder à l’esprit lors de la modélisation des données de Profil.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 5%

---

# Gardiens des données [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fournit des profils individuels qui vous permettent de fournir des expériences personnalisées sur plusieurs canaux en fonction d’informations comportementales et d’attributs du client. Pour atteindre ce ciblage, [!DNL Profile] et le moteur de segmentation de Adobe Experience Platform utilisent un modèle de données hybrides fortement dénormalisé qui offre une nouvelle approche de développement des profils clients. L’utilisation de ce modèle de données hybride rend extrêmement important que les données collectées soient modélisées correctement. Bien que le magasin de données [!DNL Profile] qui gère les données de profil ne soit pas un magasin relationnel, [!DNL Profile] permet l&#39;intégration à des entités de petite dimension afin de créer des segments de manière simplifiée et intuitive. Cette intégration est connue sous le nom de segmentation multientité.

Adobe Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des modèles de données que [!DNL Real-time Customer Profile] ne peut pas prendre en charge. Ce document décrit ces garde-fous ainsi que les meilleures pratiques et contraintes lors de l’utilisation des données de Profil à des fins de segmentation.

>[!NOTE]
>
>Les garde-fous et les limites décrits dans ce document sont constamment améliorés. Veuillez vérifier régulièrement les mises à jour.

## Prise en main

Il est recommandé de lire la documentation des services Experience Platform suivants avant de tenter de créer des modèles de données à utiliser dans [!DNL Real-time Customer Profile]. L&#39;utilisation des modèles de données et des garde-fous décrits dans le présent document exige une compréhension des divers services Experience Platform liés à la gestion des entités [!DNL Real-time Customer Profile] :

* [[!DNL Real-time Customer Profile]](home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service](../identity-service/home.md) d&#39;identité Adobe Experience Platform : Prend en charge la création d&#39;une &quot;vue unique du client&quot; en rapprochant les identités de sources de données disparates au fur et à mesure qu&#39;elles sont ingérées  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
   * [Principes de base de la composition](../xdm/schema/composition.md) des schémas : Cette section présente les schémas et la modélisation des données dans l’Experience Platform.
* [Service](../segmentation/home.md) de segmentation Adobe Experience Platform : Moteur de segmentation  [!DNL Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.
   * [Segmentation](../segmentation/multi-entity-segmentation.md) multientité : Guide de création de segments qui intègrent des entités de dimension aux données de profil.

## Types d’entité

Le modèle de données de stockage [!DNL Profile] comprend deux types d&#39;entité principaux :

* **Entité Principal :** Une entité Principale, ou entité profil, fusionne les données pour former une &quot;source unique de vérité&quot; pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrégat les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d&#39;union pour [!DNL Real-time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme conteneur pour tous les attributs de profil et événements comportementaux.

   Les attributs indépendants du temps, également appelés &quot;données d’enregistrement&quot;, sont modélisés à l’aide de [!DNL XDM Individual Profile], tandis que les données de série chronologique, également connues sous le nom de &quot;données d’événement&quot;, sont modélisées à l’aide de [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série chronologique sont ingérées dans Adobe Experience Platform, [!DNL Real-time Customer Profile] commence à ingérer les données qui ont été activées pour leur utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

   ![](images/guardrails/profile-entity.png)

* **Entité de Dimension :** Votre organisation peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces schémas non[!DNL XDM Individual Profile] sont appelés &quot;entités de dimension&quot; et ne contiennent pas de données de série chronologique. Les entités de Dimension fournissent des données de recherche qui facilitent et simplifient les définitions de segment à plusieurs entités et doivent être suffisamment petites pour que le moteur de segmentation puisse charger l&#39;ensemble des données en mémoire pour un traitement optimal (recherche rapide).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Types de limite

Lors de la définition de votre modèle de données, il est recommandé de rester dans les garde-fous fournis afin d’assurer des performances appropriées et d’éviter les erreurs système. Les garde-fous fournis dans ce document comprennent deux types de limite :

* **Limite de douceur :** une limite de souplesse fournit un maximum recommandé pour des performances système optimales. Il est possible d&#39;aller au-delà d&#39;une limite souple sans casser le système ou recevoir de messages d&#39;erreur, mais aller au-delà d&#39;une limite souple entraînera une dégradation des performances. Il est recommandé de rester dans la limite souple afin d’éviter toute diminution des performances globales.

* **Limite stricte :** une limite stricte fournit un maximum absolu au système. Dépasser une limite stricte entraînera des pannes et des erreurs, ce qui empêchera le système de fonctionner comme prévu.

## Gardiens des modèles de données

Il est recommandé d’adhérer aux garde-fous suivants lors de la création d’un modèle de données à utiliser avec [!DNL Real-time Customer Profile].

### Gardiens d&#39;entité Principal

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre de jeux de données recommandés pour contribuer au schéma d&#39;union [!DNL Profile] | 20 | Soft | **Il est recommandé d’utiliser un maximum de 20 jeux de données  [!DNL Profile]activés.** Pour activer un autre jeu de données pour  [!DNL Profile], un jeu de données existant doit d&#39;abord être supprimé ou désactivé. |
| Nombre de relations multientités recommandé | 5 | Doux | **Il est recommandé de définir un maximum de 5 relations multientités entre entités Principales et entités de dimension.** Les correspondances de relations supplémentaires ne doivent pas être effectuées tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Profondeur JSON maximale pour le champ ID utilisé dans la relation multientité | 4 | Doux | **La profondeur maximale recommandée de JSON pour un champ d’ID utilisé dans les relations multientités est 4.** Cela signifie que dans un schéma fortement imbriqué, les champs qui sont imbriqués à plus de 4 niveaux de profondeur ne doivent pas être utilisés comme champ d’identifiant dans une relation. |
| Cardinalité de tableau dans un fragment de profil | &lt;=500 | Doux | **La cardinalité optimale de la baie dans un fragment de profil (données horodatées) est  &lt;>** |
| Cardinalité de la baie dans ExperienceEvent | &lt;=10 | Doux | **La cardinalité optimale de la baie dans un ExperienceEvent (données de série chronologique) est  &lt;>** |

### Gardiens des entités de Dimension

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune donnée de série chronologique n&#39;est autorisée pour les entités non [!DNL XDM Individual Profile] | 0 | Hard | **Les données de séries chronologiques ne sont pas autorisées pour les non-[!DNL XDM Individual Profile] entités dans Profil Service.** Si un jeu de données de séries chronologiques est associé à un [!DNL XDM Individual Profile] identifiant non valide, le jeu de données ne doit pas être activé pour  [!DNL Profile]. |
| Aucune relation imbriquée | 0 | Doux | **Vous ne devez pas créer de relation entre deux non-[!DNL XDM Individual Profile] schémas.** La possibilité de créer des relations n&#39;est pas recommandée pour les schémas qui ne font pas partie du schéma d&#39; [!DNL Profile] union. |
| Profondeur JSON maximale pour le champ ID Principal | 4 | Doux | **La profondeur maximale recommandée pour le champ d’ID Principal est 4.** Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas sélectionner un champ comme identifiant Principal s’il est imbriqué à plus de 4 niveaux. Un champ situé au quatrième niveau imbriqué peut être utilisé comme Principal ID. |

## Gardiens de taille de données

Les garde-fous suivants se rapportent à la taille des données et sont recommandés pour s’assurer que les données peuvent être ingérées, stockées et interrogées comme prévu.

>[!NOTE]
>
>La taille des données sera mesurée sous forme de données non compressées dans JSON au moment de l’assimilation.

### Gardiens d&#39;entité Principal

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille maximale par fragment de profil | 10 Ko | Doux | **La taille maximale recommandée d’un fragment de profil est de 10 Ko.** L&#39;insertion de fragments de profil plus volumineux affectera les performances du système. Par exemple, le chargement d’un jeu de données CRM lourd dont la taille de certains fragments de profil est de 50 kB entraîne une dégradation des performances du système. |
| Taille maximale absolue par fragment de profil | 1 Mo | dur | **La taille maximale absolue d’un fragment de profil est de 1 Mo.** L&#39;importation échoue lorsque vous tentez de télécharger un fragment de profil de plus de 1 Mo. |

### Gardiens des entités de Dimension

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale maximale pour toutes les entités dimensionnelles | 5 Go | Doux | **La taille totale maximale recommandée pour toutes les entités dimensionnelles est de 5 Go.** L&#39;insertion d&#39;entités de grande dimension entraîne une dégradation des performances du système. Par exemple, il n’est pas recommandé de tenter de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeu de données par schéma d&#39;entité dimensionnelle | 5 | Doux | **Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle.** Par exemple, si vous créez un schéma pour &quot;produits&quot; et ajoutez cinq jeux de données de contribution, vous ne devriez pas créer un sixième jeu de données lié au schéma de produits. |

## Gardiens de segmentation

Les garde-fous décrits dans cette section font référence au nombre et à la nature de segments qu’une organisation peut créer dans un Experience Platform, ainsi qu’au mappage et à l’activation de segments vers des destinations.

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de segments par sandbox | 10 000 | Doux | **Le nombre maximal de segments qu’une entreprise peut créer est de 10 000 par sandbox.** Une entreprise peut avoir plus de 10 000 segments au total, pour autant qu’il y ait moins de 10 000 segments dans chaque sandbox individuel. Si vous tentez de créer des segments supplémentaires, les performances du système seront amoindries. |
| Nombre maximal de segments de diffusion en continu par sandbox | 500 | Doux | **Le nombre maximal de segments en flux continu qu’une entreprise peut créer est de 500 par sandbox.** Une entreprise peut avoir plus de 500 segments en flux continu au total, pour autant qu’il y ait moins de 500 segments en flux continu dans chaque sandbox individuel. La tentative de création de segments de diffusion en continu supplémentaires entraînera une dégradation des performances du système. |
| Nombre maximal de segments de lot par sandbox | 10 000 | Doux | **Le nombre maximal de segments par lot qu’une entreprise peut créer est de 10 000 par sandbox.** Une entreprise peut avoir plus de 10 000 segments de lot au total, à condition qu’il y ait moins de 10 000 segments de lot dans chaque sandbox individuel. Toute tentative de création de segments de lots supplémentaires entraîne une dégradation des performances du système. |
