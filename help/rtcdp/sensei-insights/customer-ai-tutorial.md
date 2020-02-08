---
title: Prévoyez les scores de propension des clients à l’aide de l’API client (alpha).
seo-title: Prévoyez les scores de propension des clients à l’aide de l’API client (alpha).
description: Ce didacticiel explique comment utiliser l’API client (alpha).
seo-description: Ce didacticiel explique comment utiliser l’API client (alpha).
index: false
translation-type: tm+mt
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Prévoyez les scores de propension des clients à l’aide de l’API client (alpha).

>[!NOTE]
>La fonctionnalité d’IA du client décrite dans ce document est en alpha. La documentation et la fonctionnalité peuvent être modifiées.

Créé et optimisé par Adobe Sensei, l’API client dans Adobe Experience Platform vous permet de générer des scores de propension personnalisés sans avoir à vous soucier des aspects d’apprentissage automatique.

Ce didacticiel décrit les étapes à suivre pour travailler avec l’API client à l’aide de l’interface utilisateur de la plateforme d’expérience. Les étapes sont fournies pour les rubriques suivantes :

* [Configuration d’une instance](#configure-an-instance)
* [Créer des segments de clients avec des scores prédéfinis](#create-customer-segments-with-predicted-scores)

## Prise en main

Ce guide nécessite une compréhension pratique des différents services de plateforme impliqués dans l’utilisation de l’IA du client. Avant de commencer ce didacticiel, consultez les documents suivants :

* [Présentation du profil du client en temps réel](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)
* [Présentation du service de segmentation](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md)
* [Guide de l’utilisateur du créateur de segments](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segment-builder-guide.md)

## Configuration d’une instance

Experience Platform fournit l’API client en tant que service Adobe Sensei simple d’utilisation pouvant être configuré pour différents cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de l’API client.

### Configuration de votre instance

Dans l’interface utilisateur de la plateforme, cliquez sur **Services** dans le volet de navigation de gauche. Le navigateur **Services** apparaît et affiche tous les services disponibles à votre disposition. Dans le conteneur de l’API client, cliquez sur **Ouvrir**.

![](./images/service.png)

L’écran Informations *sur le* client affiche toutes les instances d’Informations sur le client existantes. Cliquez sur **Créer une instance**.

![](./images/customer_ai.png)

Le processus de création d’instance s’affiche, à partir de l’étape *Configuration* .

Vous trouverez ci-dessous des informations importantes sur les valeurs pour lesquelles vous devez fournir à l’instance :

* Le nom de l’instance est utilisé à tous les endroits où le score d’intelligence artificielle du client est affiché. Les noms doivent donc décrire ce que les scores de prédiction représentent, par exemple, &quot;Probabilité d’annuler l’abonnement au magazine&quot;.

* Le type de propension détermine l’intention du score et de la polarité des mesures. Vous pouvez choisir **Égalité** ou **Conversion**.

* La source de données fait référence au jeu de données d’entrée qui sera utilisé pour prédire les scores. Par conception, l’API du client utilise les données d’événement d’expérience du consommateur pour calculer les scores de propension. Lors de la sélection d’un jeu de données dans le sélecteur déroulant, seuls ceux qui sont compatibles avec l’API du client sont répertoriés.

* Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Indiquez les valeurs requises, puis cliquez sur **Suivant**.

![](./images/setup.png)

### Définir un objectif

L’étape *Définir l’objectif* s’affiche et fournit un environnement interactif vous permettant de définir visuellement un objectif. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance d’intelligence artificielle du client est de déterminer la probabilité d’atteindre son objectif au cours d’une période donnée.

Cliquez sur **Saisir le nom** du champ et sélectionnez un champ dans la liste déroulante. Cliquez sur la seconde entrée et sélectionnez une clause pour la condition de l’événement, puis indiquez la valeur cible pour terminer l’événement. D’autres événements peuvent être configurés en cliquant sur **Ajouter un événement**. Enfin, terminez l’objectif en appliquant une période de prédiction en nombre de jours, puis cliquez sur **Suivant**.

![](./images/goal.png)

### Configuration d’un calendrier *(facultatif)*

L’étape *avancée* s’affiche. Cette étape facultative vous permet de configurer un calendrier pour automatiser les exécutions de prédiction, de définir des exclusions de prédiction pour filtrer certains événements ou de cliquer sur **Terminer** si rien n’est nécessaire.

Configurez un calendrier de notation en configurant la fréquence de *notation*. Les exécutions de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](./images/schedule.png)

Sous la configuration de planification, vous pouvez définir des exclusions de prédiction afin d’empêcher que des événements répondant à certaines conditions ne soient évalués lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données non pertinentes.

Pour exclure certains événements, cliquez sur **Ajouter une exclusion** et définissez l’événement de la même manière que la définition de l’objectif. Pour supprimer une exclusion, cliquez sur les ellipses (**...**) en haut à droite du conteneur d’événements, puis cliquez sur **Supprimer le conteneur**.

![](./images/exclusion.png)

Exclure les événements selon les besoins, puis cliquez sur **Terminer** pour créer l’instance.

![](./images/advanced.png)

Si l’instance est créée avec succès, une exécution de prédiction est immédiatement déclenchée et les suivantes s’exécutent selon votre planification définie.

>   **** Remarque : Selon la taille des données d’entrée, l’exécution de la prédiction peut prendre jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de l’API client et une exécution de prédiction a été exécutée. Une fois la course terminée, les connaissances notées hydratent automatiquement les profils avec les scores prévus. Veuillez patienter 24 heures avant de passer à la section suivante de ce didacticiel.

## Créer des segments de clients avec des scores prédéfinis

Lorsqu’une exécution de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les profils. L’enrichissement des profils avec des scores AI du client permet de créer des segments de clients basés sur des scores de propension. Cette section décrit la procédure à suivre pour créer des segments à l’aide du créateur de segments. Pour un didacticiel plus robuste sur la création de segments, consultez le guide [d’utilisation du créateur de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segment-builder-guide.md)segments.

Dans l’interface utilisateur de la plateforme, cliquez sur **Segments** dans le volet de navigation de gauche, puis cliquez sur **Créer un segment**.

![](./images/segments.png)

Le créateur *de* segments s’affiche. Dans la colonne *Champs* de gauche et sous l’onglet *Attributs* , cliquez sur le dossier nommé Profil **** XDM individuel, puis sur le dossier contenant l’espace de noms de votre organisation. Le dossier nommé **Customer AI** contient les résultats des exécutions de prédiction et est nommé d’après l’instance à laquelle appartiennent les scores. Cliquez sur et accédez aux résultats de l’instance souhaitée.

![](./images/results.png)

Situé au centre du créateur de segments, faites glisser l’attribut **Score** sur le canevas *du créateur de* règles pour définir une règle.

Dans la colonne de propriétés *de* segment de droite, sélectionnez une stratégie *de* fusion et attribuez un nom au segment, puis cliquez sur **Enregistrer** pour créer le segment.

![](./images/properties.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez correctement configuré une instance de l’IA du client, généré des scores de propension et créé un segment appliqué par des scores de propension à l’aide du créateur de segments. Votre segment de client peut désormais être utilisé par les destinations activées pour cibler vos audiences. Pour plus d’informations, consultez l’aperçu [des](../destinations/destinations-overview.md) Destinations.
