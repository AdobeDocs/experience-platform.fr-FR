---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Instructions pour les Experience Platform
topic: guide
translation-type: tm+mt
source-git-commit: d9e4812e3506de3082670a8afde5480cd8f865d6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 4%

---


# [!DNL Platform] garde [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] fournit des profils individuels qui vous permettent de fournir des expériences personnalisées sur plusieurs canaux en fonction d’informations comportementales et d’attributs du client. Pour atteindre ce ciblage, [!DNL Profile] et le moteur de segmentation de Adobe Experience Platform utilisent un modèle de données hybride fortement dénormalisé qui offre une nouvelle approche pour développer les profils clients. L’utilisation de ce modèle de données hybride rend extrêmement important que les données collectées soient modélisées correctement. Bien que la [!DNL Profile] banque de données qui gère les données de profil ne soit pas un magasin relationnel, [!DNL Profile] elle permet l’intégration à de petites entités de dimension afin de créer des segments de manière simplifiée et intuitive. Cette intégration est connue sous le nom de segmentation multientité.

Adobe Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des modèles de données qui [!DNL Real-time Customer Profile] ne peuvent pas être pris en charge. Ce document décrit les meilleures pratiques et les contraintes lors de l’utilisation d’entités de dimension, en particulier dans la segmentation par lots.

>[!NOTE]
>
>Les garde-fous et les limites décrits dans ce document sont constamment améliorés. Veuillez vérifier régulièrement les mises à jour.

## Prise en main

Il est recommandé de lire la documentation des services Experience Platform suivants avant de tenter de créer des modèles de données à utiliser dans [!DNL Real-time Customer Profile]. L&#39;utilisation des modèles de données et des garde-fous décrits dans le présent document exige une compréhension des divers services Experience Platform liés à la gestion des [!DNL Real-time Customer Profile] entités :

* [[ !Profil client en temps réel DNL]](home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Service](../identity-service/home.md)d&#39;identité Adobe Experience Platform : Prend en charge la création d&#39;une &quot;vue unique du client&quot; en rapprochant les identités de sources de données disparates au fur et à mesure qu&#39;elles sont ingérées [!DNL Platform].
* [[ ! Modèle de données d’expérience DNL (XDM)]](../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
   * [Principes de base de la composition](../xdm/schema/composition.md)des schémas : Cette section présente les schémas et la modélisation des données dans l’Experience Platform.
* [Service](../segmentation/home.md)de segmentation Adobe Experience Platform : Moteur de segmentation utilisé [!DNL Platform] pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.
   * [Segmentation](../segmentation/multi-entity-segmentation.md)multientité : Guide de création de segments qui intègrent des entités de dimension aux données de profil.

## Types d’entité

Le modèle de données de [!DNL Profile] stockage est constitué de deux types d’entité principaux :

* **Entité Principal :** Une Principale entité, ou entité de profil, fusionne les données pour former une &quot;source unique de vérité&quot; pour un individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrégat les champs de tous les schémas qui implémentent la même classe dans un seul schéma d’union. Le schéma d&#39;union pour [!DNL Real-time Customer Profile] est un modèle de données hybride dénormalisé qui agit comme conteneur pour tous les attributs de profil et événements comportementaux.

   Les attributs indépendants du temps, également appelés &quot;données d’enregistrement&quot;, sont modélisés à l’aide de [!DNL XDM Individual Profile]la modélisation, tandis que les données de série chronologique, également appelées &quot;données d’événement&quot;, sont modélisées à l’aide [!DNL XDM ExperienceEvent]. Comme les données d’enregistrement et de série chronologique sont ingérées dans Adobe Experience Platform, il se déclenche [!DNL Real-time Customer Profile] pour commencer à ingérer les données qui ont été activées pour leur utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

   ![](images/guardrails/profile-entity.png)

* **Entité de Dimension :** Votre entreprise peut également définir des classes XDM pour décrire des éléments autres que des individus, tels que des magasins, des produits ou des propriétés. Ces non-[!DNL XDM Individual Profile] schémas sont appelés &quot;entités de dimension&quot; et ne contiennent pas de données de série chronologique. Les entités de Dimension fournissent des données de recherche qui facilitent et simplifient les définitions de segment à plusieurs entités et doivent être suffisamment petites pour que le moteur de segmentation puisse charger l&#39;ensemble des données en mémoire pour un traitement optimal (recherche rapide).

   ![](images/guardrails/profile-and-dimension-entities.png)

## Types de limite

Lors de la définition de votre modèle de données, il est recommandé de rester dans les garde-fous fournis afin d’assurer des performances appropriées et d’éviter les erreurs système. Les garde-fous fournis dans ce document comprennent deux types de limite :

* **Limite de douceur :** Une limite souple offre un maximum recommandé pour des performances système optimales. Il est possible d&#39;aller au-delà d&#39;une limite souple sans casser le système ou recevoir de messages d&#39;erreur, mais aller au-delà d&#39;une limite souple entraînera une dégradation des performances. Il est recommandé de rester dans la limite souple afin d’éviter toute diminution des performances globales.

* **Limite stricte :** Une limite stricte fournit un maximum absolu au système. Dépasser une limite stricte entraînera des pannes et des erreurs, ce qui empêchera le système de fonctionner comme prévu.

## Gardiens des modèles de données

Il est recommandé de respecter les garde-fous suivants lors de la création d&#39;un modèle de données à utiliser avec [!DNL Real-time Customer Profile].

### Gardiens d&#39;entité Principal

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre de jeux de données recommandés pour contribuer au schéma [!DNL Profile] d&#39;union | 20 | Soft | **Il est recommandé d’utiliser un maximum de 20 jeux de données[!DNL Profile]activés.** Pour activer un autre jeu de données pour [!DNL Profile], un jeu de données existant doit d&#39;abord être supprimé ou désactivé. |
| Nombre de relations multientités recommandé | 5 | Soft | **Il est recommandé de définir un maximum de 5 relations multientités entre entités Principales et entités de dimension.** Les correspondances de relations supplémentaires ne doivent pas être effectuées tant qu’une relation existante n’est pas supprimée ou désactivée. |
| Profondeur JSON maximale pour le champ ID utilisé dans la relation multientité | 4 | Soft | **La profondeur maximale recommandée de JSON pour un champ d’ID utilisé dans les relations multientités est 4.** Cela signifie que dans un schéma fortement imbriqué, les champs qui sont imbriqués à plus de 4 niveaux de profondeur ne doivent pas être utilisés comme champ d’identifiant dans une relation. |
| Cardinalité de tableau dans un fragment de profil | &lt;=500 | Soft | **La cardinalité optimale de la baie dans un fragment de profil (données horodatées) est &lt;=500.** |
| Cardinalité de la baie dans ExperienceEvent | &lt;=10 | Soft | **La cardinalité optimale de la baie dans un ExperienceEvent (données de série chronologique) est &lt;=10.** |

### Gardiens des entités de Dimension

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Aucune donnée de série chronologique n&#39;est autorisée pour les non-[!DNL XDM Individual Profile] entités | 0 | Hard | **Les données de séries chronologiques ne sont pas autorisées pour les entités non[!DNL XDM Individual Profile]autorisées dans Profil Service.** Si un jeu de données de série chronologique est associé à un autre type d’[!DNL XDM Individual Profile] ID, le jeu de données ne doit pas être activé pour [!DNL Profile]. |
| Aucune relation imbriquée | 0 | Soft | **Vous ne devez pas créer de relation entre deux non-[!DNL XDM Individual Profile]-schémas.** La possibilité de créer des relations n&#39;est pas recommandée pour les schémas qui ne font pas partie du schéma d&#39; [!DNL Profile] union. |
| Profondeur JSON maximale pour le champ ID Principal | 4 | Soft | **La profondeur maximale recommandée pour le champ d’ID Principal est 4.** Cela signifie que dans un schéma fortement imbriqué, vous ne devez pas sélectionner un champ comme identifiant Principal s’il est imbriqué à plus de 4 niveaux. Un champ situé au quatrième niveau imbriqué peut être utilisé comme Principal ID. |

## Gardiens de taille de données

Les garde-fous suivants se rapportent à la taille des données et sont recommandés pour s’assurer que les données peuvent être ingérées, stockées et interrogées comme prévu.

>[!NOTE]
>
>La taille des données sera mesurée sous forme de données non compressées dans JSON au moment de l’assimilation.

### Gardiens d&#39;entité Principal

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille maximale par fragment de profil | 10 Ko | Soft | **La taille maximale recommandée d’un fragment de profil est de 10 Ko.** L&#39;insertion de fragments de profil plus volumineux affectera les performances du système. Par exemple, le chargement d’un jeu de données CRM lourd dont la taille de certains fragments de profil est de 50 kB entraîne une dégradation des performances du système. |
| Taille maximale absolue par fragment de profil | 1MB | Hard | **La taille maximale absolue d’un fragment de profil est de 1 Mo.** L&#39;importation échoue lorsque vous tentez de télécharger un fragment de profil de plus de 1 Mo. |

### Gardiens des entités de Dimension

| Gardrail | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille totale maximale par entité dimensionnelle | 1 Go   | Soft | **La taille totale maximale recommandée pour une entité de dimension est de 1 Go.** L&#39;insertion d&#39;entités de grande dimension entraîne une dégradation des performances du système. Par exemple, il n’est pas recommandé de tenter de charger un catalogue de produits de 10 Go en tant qu’entité de dimension. |
| Jeu de données par schéma d&#39;entité dimensionnelle | 5 | Soft | **Il est recommandé d’associer un maximum de 5 jeux de données à chaque schéma d’entité dimensionnelle.** Par exemple, si vous créez un schéma pour &quot;produits&quot; et ajoutez cinq jeux de données de contribution, vous ne devriez pas créer un sixième jeu de données lié au schéma de produits. |