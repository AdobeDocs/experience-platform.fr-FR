---
title: Présentation des cas d’utilisation de la segmentation pour l’édition B2B de la plateforme CDP en temps réel.
description: Présentation des différents cas d’utilisation de la plateforme CDP B2B en temps réel disponibles.
source-git-commit: e85d4b108e2d4a6a88772c071d9281603b695ada
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Présentation des cas d’utilisation de la segmentation pour la plateforme de données clients en temps réel B2B (version bêta)

<!-- This document relates to this [ticket](https://jira.corp.adobe.com/browse/PLAT-100468) -->

>[!IMPORTANT]
>
>La plateforme CDP B2B en temps réel est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Ce document fournit des exemples concernant la segmentation disponible pour l’édition B2B de la plateforme CDP en temps réel et la manière dont les différents types d’attributs peuvent être combinés pour les cas d’utilisation B2B courants.

>[!NOTE]
>
>Les attributs requis pour ces cas d’utilisation de segmentation ne sont disponibles que pour les clients de la plateforme de données clients en temps réel B2B Edition. Pour en savoir plus sur la plateforme des données clients en temps réel, y compris sur les fonctionnalités disponibles pour chaque type de licence, commencez par lire la [présentation de la plateforme des données clients en temps réel](../overview.md).

## Conditions préalables

Avant de pouvoir utiliser les attributs de segmentation pour les classes B2B, vous devez effectuer les étapes suivantes :

1. Créez des schémas qui utilisent les classes B2B. Les classes Édition B2B comprennent Compte, Campagne, Opportunité, Liste marketing, etc. Pour plus d’informations sur la [configuration des schémas à utiliser avec les classes B2B](../schemas/b2b.md), consultez la documentation sur les schémas.
1. Créez des relations entre vos schémas B2B de modèle de données d’expérience (XDM). Les segments basés sur les attributs de l’édition B2B nécessitent des relations entre les classes pour utiliser pleinement la fonctionnalité étendue de segmentation B2B. Pour plus d’informations, consultez la documentation sur la [définition d’une relation entre deux schémas B2B](../../xdm/tutorials/relationship-b2b.md) .
1. Ingérez des données à l’aide de jeux de données basés sur vos schémas B2B. Consultez la documentation des sources pour [plus d’informations sur l’ingestion de données](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Pour obtenir des instructions plus détaillées sur la création de segments, consultez le [guide d’utilisation du créateur de segments](../../segmentation/ui/segment-builder.md) .

Une fois ces exigences respectées, vous pouvez combiner ces attributs pour les cas d’utilisation B2B courants.

## Prise en main

Une fois que les relations des schémas d’union pour les classes B2B sont établies et ont été utilisées pour ingérer des données, leurs attributs sont disponibles dans le rail gauche du créateur de segments.

Les classes B2B et leurs attributs sont ajoutés avec une étiquette `B2B` dans l’espace de travail Segmentation afin de les différencier de celles disponibles en standard dans la plateforme de données clients en temps réel.

Afin de créer efficacement des segments pour les cas d’utilisation B2B, il est important de posséder une connaissance approfondie du schéma et de comprendre à quoi ressemble le modèle de données. Il est également utile de connaître le chemin que les données empruntent d’un objet de données à un autre.

L’image ci-dessous illustre les relations entre les classes B2B disponibles dans l’édition B2B de la plateforme CDP en temps réel.

![ERD de classe B2B](../assets/segmentation/b2b-classes.png)

Comme votre modèle de données peut être complexe, vous pouvez utiliser l’interface utilisateur de Platform pour afficher une représentation visuelle plus détaillée de votre modèle de données afin de vous aider à trouver les attributs appropriés à votre cas d’utilisation. Pour commencer, accédez à l’interface utilisateur de Platform et sélectionnez Schémas dans le volet de navigation de gauche.

Sélectionnez le schéma approprié dans la liste disponible et sélectionnez la relation appropriée dans le rail latéral [!UICONTROL Composition]. Dans l’exemple ci-dessous, la sélection de la relation &quot;Personne&quot; révèle quel attribut du schéma actuel fait référence au schéma &quot;Personne&quot; associé (s’il s’agit du schéma source de la relation), ou est référencé par le schéma &quot;Personne&quot; (s’il s’agit du schéma de destination de la relation).

![exemple de clé source utilisant la relation personnes dans l’espace de travail du schéma](../assets/segmentation/source-key-schema-relationship-example.png)

Cette relation est reflétée dans le Créateur de segments par l’utilisation de dossiers `Key` comme illustré dans l’image ci-dessous.

![exemple de la clé source à l’aide du créateur de segments dans l’espace de travail de segmentation](../assets/segmentation/source-key-segmentation-example.png)

Pour plus d’informations sur les classes B2B disponibles, reportez-vous aux [schémas de la documentation Édition B2B de la plateforme de données clients en temps réel](../schemas/b2b.md) .

Les cas d’utilisation ci-dessous fournissent des informations sur les classes utilisées pour établir des relations entre les différents schémas afin d’obtenir ces résultats. Ces exemples peuvent vous aider à créer vos propres segments.

## Exemples de différents cas d’utilisation

Les cas d’utilisation suivants sont disponibles pour la segmentation avec l’édition B2B. Chaque exemple fournit une description des actions du segment et une description des classes utilisées pour les créer. Les images fournies mettent en surbrillance le chemin d’accès au fichier dans le rail latéral [!UICONTROL Attributs] qui reflète la structure du schéma. La section [!UICONTROL Propriétés du segment] située à droite de l’affichage contient une ventilation écrite des attributs du segment.

### Exemple 1

Trouvez toutes les personnes qui sont le &quot;décideur&quot; de toute opportunité. Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile] et la classe [!UICONTROL XDM Business Opportunity Person Relation] .

![Interface utilisateur affichant les exemples 1](../assets/segmentation/example-1.png)

### Exemple 2

Recherchez toutes les personnes directement affectées à des opportunités dont le montant de l’opportunité est supérieur au montant donné (1 million de dollars). Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Opportunity Person Relation] et la classe [!UICONTROL XDM Business Opportunity].

![Interface utilisateur affichant les exemples 2](../assets/segmentation/example-2.png)

### Exemple 3

Recherchez toutes les personnes directement affectées à des opportunités où se trouve le compte à un emplacement donné (Canada). Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] et la classe [!UICONTROL XDM Business Account].

![Interface utilisateur affichant les exemples de paramètres 3](../assets/segmentation/example-3.png)

### Exemple 4

Recherchez toutes les personnes qui sont un &quot;décideur&quot; de toutes les opportunités où le compte se trouve dans l’industrie &quot;financière&quot; et qui ont consulté la page des prix au cours des trois derniers jours. Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] et la classe [!UICONTROL XDM Business Account] et la classe [!UICONTROL XDM ExperienceEvent].

![Interface utilisateur affichant les exemples 4](../assets/segmentation/example-4.png)

### Exemple 5

Trouvez toutes les personnes qui travaillent dans un service des ressources humaines (HR) et qui sont liées à un compte ayant au moins une opportunité ouverte pour un montant donné (1 million de dollars) ou plus. Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Account] et la classe [!UICONTROL XDM Business Opportunity].

![Interface utilisateur affichant les exemples de paramètres 5](../assets/segmentation/example-5.png)

### Exemple 6

Recherchez toutes les personnes dont le titre de poste est Vice-président et qui sont liées à n’importe quel compte avec des recettes annuelles d’un montant donné (100 millions de dollars) ou plus et qui ont consulté la page des prix au moins 3 fois au cours du dernier mois. Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Account] et la classe [!UICONTROL XDM ExperienceEvent].

![Interface utilisateur affichant les exemples 6](../assets/segmentation/example-6.png)

### Exemple 7

Recherchez toutes les personnes qui sont un &quot;décideur&quot; d’une opportunité manquée fermée, et qui ont consulté la page des prix la semaine dernière. Ce segment nécessite un lien entre la classe [!UICONTROL XDM Individual Profile], la classe [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] et la classe [!UICONTROL XDM ExperienceEvent].

![Interface utilisateur affichant les exemples de paramètres 7](../assets/segmentation/example-7.png)

## Étapes suivantes

Après avoir lu cet aperçu, vous comprenez désormais les possibilités de segmentation disponibles à l’aide de la plateforme de données clients en temps réel, l’édition B2B. Pour plus d’informations sur Segmentation Service, consultez la [documentation sur la segmentation](../../segmentation/home.md).
