---
title: Cas d’utilisation de la segmentation pour l’édition B2B de Real-time Customer Data Platform
description: Présentation des différents cas d’utilisation de l’édition B2B d’Adobe Real-time Customer Data Platform disponibles.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 1%

---

# Cas d’utilisation de la segmentation pour Real-time Customer Data Platform B2B Edition

Ce document fournit des exemples de définitions de segment dans Adobe Real-time Customer Data Platform Édition B2B et explique comment différents types d’attributs peuvent être combinés pour les cas d’utilisation B2B courants. Pour comprendre comment les destinations s’intègrent à votre workflow B2B, reportez-vous à la section [tutoriel de bout en bout](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Les attributs requis pour ces cas d’utilisation de segmentation ne sont disponibles que pour les clients de Real-time Customer Data Platform B2B Edition. Si vous n’utilisez pas Real-time Customer Data Platform B2B Edition, reportez-vous à la section [présentation de la segmentation](./segmentation-overview.md) au lieu de .

## Conditions préalables {#prerequisites}

Avant de pouvoir utiliser les attributs de segmentation pour les classes B2B, vous devez effectuer les étapes suivantes :

1. Créez des schémas qui utilisent les classes B2B. Les classes Édition B2B comprennent Compte, Campagne, Opportunité, Liste marketing, etc. Pour plus d’informations sur [Configuration de schémas à utiliser avec des classes B2B](../schemas/b2b.md) consultez la documentation du schéma.
1. Créez des relations entre vos schémas B2B de modèle de données d’expérience (XDM). Les segments basés sur les attributs de l’édition B2B nécessitent des relations entre les classes pour utiliser pleinement la fonctionnalité étendue de segmentation B2B. Consultez la documentation relative à [comment définir une relation entre deux schémas B2B](../../xdm/tutorials/relationship-b2b.md) pour plus d’informations.
1. Ingérez des données à l’aide de jeux de données basés sur vos schémas B2B. Consultez la documentation des sources pour [informations sur l’ingestion de données](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Lisez le [Guide d’utilisation du créateur de segments](../../segmentation/ui/segment-builder.md) pour obtenir des conseils plus détaillés sur la création de segments.

Une fois ces exigences respectées, vous pouvez combiner ces attributs pour les cas d’utilisation B2B courants.

## Prise en main {#getting-started}

Une fois que les relations des schémas d’union pour les classes B2B sont établies et ont été utilisées pour ingérer des données, leurs attributs sont disponibles dans le rail gauche du créateur de segments.

Les classes B2B et leurs attributs sont ajoutés à un `B2B` dans l’espace de travail Segmentation afin de les différencier de ceux disponibles en standard dans Real-time Customer Data Platform.

Afin de créer efficacement des segments pour les cas d’utilisation B2B, il est important de posséder une connaissance approfondie du schéma et de comprendre à quoi ressemble le modèle de données. Il est également utile de connaître le chemin que les données empruntent d’un objet de données à un autre.

L’image ci-dessous illustre les relations entre les classes B2B disponibles dans Real-Time CDP B2B Edition.

![ERD de classe B2B](../assets/segmentation/b2b-classes.png)

Comme votre modèle de données peut être complexe, vous pouvez utiliser l’interface utilisateur de Platform pour afficher une représentation visuelle plus détaillée de votre modèle de données afin de vous aider à trouver les attributs appropriés à votre cas d’utilisation. Pour commencer, accédez à l’interface utilisateur de Platform et sélectionnez Schémas dans le volet de navigation de gauche.

Sélectionnez le schéma approprié dans la liste disponible et sélectionnez la relation appropriée dans la [!UICONTROL Composition] rail latéral. Dans l’exemple ci-dessous, la sélection de la relation &quot;Personne&quot; révèle quel attribut du schéma actuel fait référence au schéma &quot;Personne&quot; associé (s’il s’agit du schéma source de la relation), ou est référencé par le schéma &quot;Personne&quot; (s’il s’agit du schéma de référence de la relation).

![exemple de clé source utilisant la relation personnes dans l’espace de travail du schéma](../assets/segmentation/source-key-schema-relationship-example.png)

Cette relation est reflétée dans le créateur de segments grâce à l’utilisation de la fonction `Key` comme illustré ci-dessous.

![exemple de la clé source à l’aide du créateur de segments dans l’espace de travail de segmentation](../assets/segmentation/source-key-segmentation-example.png)

Reportez-vous à la section [schémas dans la documentation de Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) pour plus d’informations sur les classes B2B disponibles.

Les cas d’utilisation ci-dessous fournissent des informations sur les classes utilisées pour établir des relations entre les différents schémas afin d’obtenir ces résultats. Ces exemples peuvent vous aider à créer vos propres segments.

## Exemples de différents cas d’utilisation de la segmentation {#use-cases}

Les cas d’utilisation suivants sont disponibles pour la segmentation avec l’édition B2B. Chaque exemple fournit une description des actions du segment et une description des classes utilisées pour les créer. Les images fournies mettent en surbrillance le chemin d’accès au fichier dans la variable [!UICONTROL Attributs] rail latéral qui reflète la structure du schéma. Le [!UICONTROL Propriétés du segment] à droite de l’affichage se trouve une ventilation écrite des attributs du segment.

### Exemple 1 : Trouver des &quot;décideurs&quot; pour les opportunités B2B {#find-decision-maker}

Trouvez toutes les personnes qui sont le &quot;décideur&quot; de toute opportunité. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] et la variable [!UICONTROL Relation de personne avec les opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples 1](../assets/segmentation/example-1.png)

### Exemple 2 : Recherche de profils B2B affectés à des opportunités pour une certaine somme en dollars {#find-opportunities-amount}

Recherchez toutes les personnes directement affectées à des opportunités dont le montant de l’opportunité est supérieur au montant donné (1 million de dollars). Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples 2](../assets/segmentation/example-2.png)

### Exemple 3 : Recherche de profils B2B affectés aux opportunités par emplacement {#find-opportunities-location}

Recherchez toutes les personnes directement affectées à des opportunités où se trouve le compte à un emplacement donné (Canada). Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL Compte d’entreprise XDM] classe .

![Interface utilisateur affichant les exemples de paramètres 3](../assets/segmentation/example-3.png)

### Exemple 4 : Trouver des &quot;décideurs&quot; pour connaître les opportunités par secteur et les comportements de navigation {#find-industry-browsing-behavior}

Recherchez toutes les personnes qui sont un &quot;décideur&quot; de toutes les opportunités où le compte se trouve dans l’industrie &quot;financière&quot; et qui ont consulté la page des prix au cours des trois derniers jours. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL Compte d’entreprise XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples 4](../assets/segmentation/example-4.png)

### Exemple 5 : Recherche de profils B2B pour les opportunités par nom de département et montant des opportunités {#find-department-opportunity-amount}

Trouvez toutes les personnes qui travaillent dans un service des ressources humaines (HR) et qui sont liées à un compte ayant au moins une opportunité ouverte pour un montant donné (1 million de dollars) ou plus. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte d’entreprise XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples de paramètres 5](../assets/segmentation/example-5.png)

### Exemple 6 : Recherche de profils B2B par titre de traitement et chiffre d’affaires annuel {#find-by-job-title-and-revenue}

Recherchez toutes les personnes dont le titre de poste est Vice-président et qui sont liées à n’importe quel compte avec des recettes annuelles d’un montant donné (100 millions de dollars) ou plus et qui ont consulté la page des prix au moins 3 fois au cours du dernier mois. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte d’entreprise XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples 6](../assets/segmentation/example-6.png)

### Exemple 7 : Rechercher les &quot;décideurs&quot; par statut d’opportunité et comportement de navigation {#find-by-opportunity-status-and-browsing-behavior}

Recherchez toutes les personnes qui sont un &quot;décideur&quot; d’une opportunité manquée fermée, et qui ont consulté la page des prix la semaine dernière. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples de paramètres 7](../assets/segmentation/example-7.png)

### Exemple 8 : Utilisation de comptes liés pour étendre la portée de la segmentation {#related-accounts}

Recherchez toutes les personnes qui travaillent dans un service Ressources humaines (HR) et qui sont liées à n’importe quel compte. *ou l’un des comptes associés du compte ;* qui a au moins une opportunité ouverte pour le montant donné (1 million de dollars) ou plus. Ce segment nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte d’entreprise XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant la segmentation pour les comptes associés](../assets/segmentation/segmentation-related-accounts.png)

### Exemple 9 : Utilisation de scores de piste et/ou de scores de compte pour qualifier le profil {#account-scoring}

Recherchez tous les profils dont le score de piste est supérieur à 80.

![Interface utilisateur affichant la segmentation pour la notation prédictive de piste et de compte](../assets/segmentation/segmentation-predictive-lead-and-account-scoring.png)

## Étapes suivantes {#next-steps}

Après avoir lu cet aperçu, vous comprenez désormais les possibilités de segmentation disponibles avec Real-Time CDP, Edition B2B. Pour plus d’informations sur Segmentation Service, consultez la [documentation sur la segmentation](../../segmentation/home.md).
