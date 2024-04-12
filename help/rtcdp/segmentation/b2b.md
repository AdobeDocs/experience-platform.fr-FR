---
title: Cas d’utilisation de la segmentation pour Real-time Customer Data Platform version B2B
description: Présentation des différents cas d’utilisation de l’édition B2B d’Adobe Real-time Customer Data Platform.
feature: Get Started, Audiences, Segments, B2B
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 8a487d948d2eb7db167298b61045ef8dd2099da6
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 1%

---

# Cas d’utilisation de la segmentation pour Real-time Customer Data Platform B2B Edition

Ce document fournit des exemples de définitions de segment dans l’édition B2B d’Adobe Real-time Customer Data Platform et explique comment différents types d’attributs peuvent être combinés pour les cas d’utilisation B2B courants. Pour comprendre comment les destinations s’intègrent à votre workflow B2B, reportez-vous à la section [tutoriel de bout en bout](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Les attributs requis pour ces cas d’utilisation de segmentation ne sont disponibles que pour les clients de Real-time Customer Data Platform B2B Edition. Si vous n’utilisez pas Real-time Customer Data Platform B2B Edition, reportez-vous à la section [présentation de la segmentation](./segmentation-overview.md) au lieu de .

## Conditions préalables {#prerequisites}

Avant de pouvoir utiliser les attributs de segmentation pour les classes B2B, vous devez effectuer les étapes suivantes :

1. Créez des schémas qui utilisent les classes B2B. Les classes Édition B2B comprennent Compte, Campagne, Opportunité, Liste marketing, etc. Pour plus d’informations sur [Configuration de schémas à utiliser avec des classes B2B](../schemas/b2b.md) consultez la documentation du schéma.
2. Créez des relations entre vos schémas B2B de modèle de données d’expérience (XDM). Les audiences basées sur les attributs de l’édition B2B nécessitent des relations entre les classes pour utiliser pleinement la fonctionnalité étendue de segmentation B2B. Consultez la documentation relative à [comment définir une relation entre deux schémas B2B](../../xdm/tutorials/relationship-b2b.md) pour plus d’informations.
3. Ingérez des données à l’aide de jeux de données basés sur vos schémas B2B. Consultez la documentation des sources pour [informations sur l’ingestion de données](../../sources/connectors/adobe-applications/marketo/marketo.md).
4. Lisez la section [Guide d’utilisation du créateur de segments](../../segmentation/ui/segment-builder.md) pour obtenir des conseils plus détaillés sur la création d’audiences.

Une fois ces exigences respectées, vous pouvez combiner ces attributs pour les cas d’utilisation B2B courants.

## Prise en main {#getting-started}

Une fois que les relations des schémas d’union pour les classes B2B sont établies et ont été utilisées pour ingérer des données, leurs attributs sont disponibles dans le rail gauche du créateur de segments.

Les classes B2B et leurs attributs sont ajoutés à un `B2B` dans l’espace de travail Segmentation afin de les différencier de ceux disponibles en standard dans Real-time Customer Data Platform.

Afin de créer efficacement des audiences pour les cas d’utilisation B2B, il est important d’avoir une connaissance approfondie du schéma et de comprendre à quoi ressemble le modèle de données. Il est également utile de connaître le chemin que les données empruntent d’un objet de données à un autre.

L’image ci-dessous illustre les relations entre les classes B2B disponibles dans Real-Time CDP B2B Edition.

![ERD de classe B2B](../assets/segmentation/b2b-classes.png)

Comme votre modèle de données peut être complexe, vous pouvez utiliser l’interface utilisateur de Platform pour afficher une représentation visuelle plus détaillée de votre modèle de données afin de vous aider à trouver les attributs appropriés à votre cas d’utilisation. Pour commencer, accédez à l’interface utilisateur de Platform et sélectionnez Schémas dans le volet de navigation de gauche.

Sélectionnez le schéma approprié dans la liste disponible et sélectionnez la relation appropriée dans la [!UICONTROL Composition] rail latéral. Dans l’exemple ci-dessous, la sélection de la relation &quot;Personne&quot; révèle quel attribut du schéma actuel fait référence au schéma &quot;Personne&quot; associé (s’il s’agit du schéma source de la relation), ou est référencé par le schéma &quot;Personne&quot; (s’il s’agit du schéma de référence de la relation).

![exemple de clé source utilisant la relation personnes dans l’espace de travail du schéma](../assets/segmentation/source-key-schema-relationship-example.png)

Cette relation est reflétée dans le créateur de segments grâce à l’utilisation de la fonction `Key` comme illustré ci-dessous.

![exemple de la clé source à l’aide du créateur de segments dans l’espace de travail de segmentation](../assets/segmentation/source-key-segmentation-example.png)

Reportez-vous à [schémas dans la documentation de Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) pour plus d’informations sur les classes B2B disponibles.

Les cas d’utilisation ci-dessous fournissent des informations sur les classes utilisées pour établir des relations entre les différents schémas afin d’obtenir ces résultats. Ces exemples peuvent vous aider à créer vos propres audiences.

## Exemples de différents cas d’utilisation de la segmentation {#use-cases}

Les cas d’utilisation suivants sont disponibles pour la segmentation avec l’édition B2B. Chaque exemple fournit une description de l’audience et une description des classes utilisées pour les créer. Les images fournies mettent en surbrillance le chemin du fichier dans la variable [!UICONTROL Attributs] rail latéral qui reflète la structure du schéma. La variable [!UICONTROL Propriétés du segment] à droite de l&#39;affichage se trouve une répartition écrite des attributs de l&#39;audience.

### Exemple 1 : rechercher des &quot;décideurs&quot; pour les opportunités B2B {#find-decision-maker}

Trouvez toutes les personnes qui sont le &quot;décideur&quot; de toute opportunité. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] et la variable [!UICONTROL Relation de personne avec les opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples 1 settings](../assets/segmentation/example-1.png)

### Exemple 2 : recherche de profils B2B affectés à des opportunités pour une certaine somme en dollars {#find-opportunities-amount}

Recherchez toutes les personnes directement affectées à des opportunités dont le montant de l’opportunité est supérieur au montant donné (1 million de dollars). Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples 2](../assets/segmentation/example-2.png)

### Exemple 3 : recherche de profils B2B affectés à des opportunités par emplacement {#find-opportunities-location}

Recherchez toutes les personnes directement affectées à des opportunités où se trouve le compte à un emplacement donné (Canada). Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL Compte commercial XDM] classe .

![Interface utilisateur affichant les exemples de paramètres 3](../assets/segmentation/example-3.png)

### Exemple 4 : rechercher des &quot;décideurs&quot; pour les opportunités par secteur et le comportement de navigation {#find-industry-browsing-behavior}

Recherchez toutes les personnes qui sont un &quot;décideur&quot; de toutes les opportunités où le compte se trouve dans l’industrie &quot;financière&quot; et qui ont consulté la page des prix au cours des trois derniers jours. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL Compte commercial XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples 4](../assets/segmentation/example-4.png)

### Exemple 5 : recherche de profils B2B pour les opportunités par nom de département et montant des opportunités {#find-department-opportunity-amount}

Trouvez toutes les personnes qui travaillent dans un service des ressources humaines (HR) et qui possèdent un compte ayant au moins une opportunité ouverte pour un montant donné (1 million de dollars) ou plus. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte commercial XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant les exemples de paramètres 5](../assets/segmentation/example-5.png)

### Exemple 6 : recherche de profils B2B par titre de poste et chiffre d’affaires annuel du compte {#find-by-job-title-and-revenue}

Recherchez toutes les personnes dont le titre de poste est Vice-président et qui ont un compte quelconque avec des recettes annuelles d’un montant donné (100 millions de dollars) ou plus et qui ont consulté la page des prix au moins 3 fois le mois dernier. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte commercial XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples 6](../assets/segmentation/example-6.png)

### Exemple 7 : rechercher des &quot;décideurs&quot; par statut d’opportunité et comportement de navigation {#find-by-opportunity-status-and-browsing-behavior}

Recherchez toutes les personnes qui sont un &quot;décideur&quot; d’une opportunité manquée fermée, et qui ont consulté la page des prix la semaine dernière. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Relation de personne avec les opportunités commerciales XDM] Classe, [!UICONTROL Opportunités commerciales XDM] et [!UICONTROL XDM ExperienceEvent] classe .

![Interface utilisateur affichant les exemples de paramètres 7](../assets/segmentation/example-7.png)

### Exemple 8 : utilisation de comptes connexes pour étendre la portée de la segmentation {#related-accounts}

Recherchez toutes les personnes qui travaillent dans un service Ressources humaines (HR) et qui sont liées à n’importe quel compte. *ou l’un des comptes associés du compte ;* qui a au moins une opportunité ouverte pour le montant donné (1 million de dollars) ou plus. Cette audience nécessite un lien entre la variable [!UICONTROL XDM Individual Profile] Classe, [!UICONTROL Compte commercial XDM] et [!UICONTROL Opportunités commerciales XDM] classe .

![Interface utilisateur affichant la segmentation pour les comptes associés](../assets/segmentation/example-8.png)

### Exemple 9 : utilisation de scores de piste et/ou de scores de compte pour qualifier un profil {#account-scoring}

Recherchez tous les profils dont le score de piste est supérieur à 80.

![Interface utilisateur affichant la segmentation pour la notation prédictive de piste et de compte](../assets/segmentation/example-9.png)

### Exemple 10 : Recherchez les profils B2B associés à des comptes dont l’organisation parent génère des recettes supérieures à un certain montant en dollars. {#find-parent-org-amount}

Recherchez toutes les personnes associées à des comptes dont l’organisation parente a des recettes supérieures au montant donné (100 000 000 $).

![Interface utilisateur affichant l’organisation parente de segmentation](../assets/segmentation/example-10.png)

### Exemple 11 : rechercher des profils B2B par titre de tâche et nom de compte avec une relation active {#find-by-job-title-and-account-name}

Recherchez toutes les personnes qui sont un &quot;responsable&quot; sur le compte &quot;Acme&quot;, où la relation de compte est &quot;active&quot;.

![Interface utilisateur affichant l’organisation parente de segmentation](../assets/segmentation/example-11.png)

### Exemple 12 : Recherchez les profils B2B ciblés pour les campagnes dont le coût réel dépasse le coût budgété. {#find-actualcost-exceed-budgetcost}

Recherchez toutes les personnes ciblées pour les campagnes où le coût réel a dépassé le coût budgété.

![Interface utilisateur affichant l’organisation parente de segmentation](../assets/segmentation/example-12.png)

### Exemple 13 : recherche de profils B2B appartenant à une liste statique Marketo et isDeleted=false {#find-marketo-static-list}

Recherchez toutes les personnes appartenant à la liste statique Marketo &quot;Anniversaires users&quot; où isDeleted=false.

![Interface utilisateur affichant l’organisation parente de segmentation](../assets/segmentation/example-13.png)

## Étapes suivantes {#next-steps}

Après avoir lu cet aperçu, vous comprenez désormais les possibilités de segmentation disponibles à l’aide de Real-Time CDP, Édition B2B. Pour plus d’informations sur Segmentation Service, consultez la [documentation sur la segmentation](../../segmentation/home.md).
