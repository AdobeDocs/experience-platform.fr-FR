---
keywords: Experience Platform;user guide;customer ai;popular topics
solution: Experience Platform
title: Guide de l’utilisateur de l’API client
topic: User guide
translation-type: tm+mt
source-git-commit: 7987cec12c22e9b48ddc9fdc263d7cd28bd172f2

---


# Guide de l’utilisateur de l’API client

L’IA du client, dans le cadre d’Intelligent Services, vous permet de générer des scores de propension personnalisés sans avoir à vous soucier de l’apprentissage automatique.

Ce guide décrit les étapes à suivre pour travailler avec l’API du client. Les étapes indiquées concernent les rubriques suivantes :

* [Configuration d’une instance](#configure-an-instance)
* [Création de segments client avec des scores prévus](#create-customer-segments-with-predicted-scores)

En outre, l’annexe de ce didacticiel fournit des informations sur la [sortie de l’IA](#customer-ai-output-data)du client.

## Configuration d’une instance

Les services intelligents fournissent l’API du client sous la forme d’un service Adobe Sensei simple d’utilisation qui peut être configuré pour différents cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

### Configuration de votre instance

Dans l’interface utilisateur de Platform, cliquez sur **Services** dans le volet de navigation de gauche. Le navigateur **Services** apparaît et affiche tous les services disponibles. Dans le conteneur de Customer AI, cliquez sur **Ouvrir**.

![](./images/user-guide/navigate-to-service.png)

L’écran *Customer AI* affiche toutes les instances de Customer AI existantes. Cliquez sur **Créer une instance**.

![](./images/user-guide/dashboard.png)

Le workflow de création d’instance s’affiche à partir de l’étape *Configuration*.

Vous trouverez ci-dessous des informations importantes sur les valeurs que vous devez fournir à l’instance :

* Le nom de l’instance est utilisé à tous les endroits où s’affiche le score de l’API du client. Par conséquent, les noms doivent décrire ce que les scores de prédiction représentent, par exemple, &quot;Probabilité d&#39;annuler le magazine  &quot;.

* Le type de propension détermine l’intention de score et de polarité des mesures. Vous pouvez choisir **Attrition** ou **Conversion**. Pour plus d&#39;informations sur l&#39;impact du type de propension sur votre instance, consultez la note sous le résumé [de](./discover-insights.md#scoring-summary) notation dans le d&#39;informations sur la découverte des .

* La source de données est l’emplacement des données. Le jeu de données est le jeu de données d’entrée utilisé pour prédire les scores. Par conception, Customer AI utilise des données d’événement d’expérience client pour calculer les scores de propension. Lors de la sélection d’un jeu de données dans le sélecteur déroulant, seules les données compatibles avec l’API du client sont répertoriées.

* Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Indiquez les valeurs requises, puis cliquez sur **Suivant**.

![](./images/user-guide/setup.png)

### Définition d’un objectif

L’étape *Définir un objectif* s’affiche et fournit un environnement interactif permettant de définir un objectif visuellement. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Cliquez sur **Saisir le nom du champ** et sélectionnez un champ dans la liste déroulante. Cliquez sur la seconde entrée et sélectionnez une clause pour la condition de l’événement, puis indiquez la valeur cible pour terminer l’événement. D’autres événements peuvent être configurés en cliquant sur **Ajouter un événement**. Enfin, atteignez l’objectif en appliquant une période de prédiction en nombre de jours, puis cliquez sur **Suivant**.

![](./images/user-guide/goal.png)

### Configuration d’un planning *(facultatif)*

L’étape *avancée* s’affiche. Lors de cette étape facultative, vous pouvez configurer un planning pour automatiser les opérations de prédiction, définir les exclusions de prédiction pour filtrer certains événements ou cliquer sur **Terminer** si aucune opération n’est requise.

Configurez un planning de notation en configurant la *Fréquence de notation*. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](./images/user-guide/schedule.png)

Sous la configuration du planning, vous pouvez définir des exclusions de prédiction afin d’empêcher que des événements répondant à certaines conditions soient évalués lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données non pertinentes.

Pour exclure certains événements, cliquez sur **Ajouter une exclusion** et définissez l’événement de la même manière que l’objectif. Pour supprimer une exclusion, cliquez sur les points de suspension (**...**) en haut à droite du conteneur d’événements, puis cliquez sur **Supprimer le conteneur**.

![](./images/user-guide/exclusion.png)

Excluez les événements selon les besoins, puis cliquez sur **Terminer** pour créer l’instance.

![](./images/user-guide/advanced.png)

Si l’instance est créée avec succès, une exécution de prédiction est immédiatement déclenchée et les exécutions suivantes s’exécutent conformément à la planification que vous avez définie.

>[!NOTE] Selon la taille des données d’entrée, l’exécution de la prédiction peut prendre jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de Customer AI et exécuté une opération de prédiction. Une fois la course terminée, les connaissances notées renseignent automatiquement les  avec des scores prédits. Veuillez patienter jusqu&#39;à 24 heures avant de passer à la section suivante de ce didacticiel.

## Création de segments client avec des scores prévus

Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des  avec des scores d’IA du client permet de créer des segments de clients pour trouver  en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments. Pour un tutoriel plus complet sur la création de segments, consultez le [guide d’utilisation du créateur de segments](../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Afin d’utiliser cette méthode, le  du client en temps réel doit être activé pour le jeu de données.

Dans l’interface utilisateur de Platform, cliquez sur **Segments** dans le volet de navigation de gauche, puis cliquez sur **Créer un segment**.

![](./images/user-guide/segments.png)

Le *créateur de segments* s’affiche. Dans la colonne *Champs* à gauche, sous l’onglet *Attributs*, cliquez sur le dossier nommé **XDM Individual Profile**, puis sur le dossier avec l’espace de noms de votre organisation. Le dossier nommé **Customer AI** contient les résultats des opérations de prédiction et est nommé d’après l’instance à laquelle sont associés les scores. Cliquez sur un dossier d’instance pour accéder aux résultats de l’instance souhaitée.

![](./images/user-guide/results.png)

Faites glisser l’attribut **Score** sur le *canevas du créateur de règles* situé au centre du créateur de segments pour définir une règle.

Sous la colonne de propriétés *de* segment de droite, attribuez un nom au segment.

![](./images/user-guide/properties.png)

Au-dessus de la colonne *Champs* de gauche, cliquez sur l’icône **engrenage** et sélectionnez une stratégie **de** fusion. Click **Save** to create the segment.

![](./images/user-guide/merge_policy.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez correctement configuré une instance de l’IA du client, généré des scores de propension et trouvé   en fonction de leurs scores de propension à l’aide du Créateur de segments. Vous pouvez désormais  votre  de en les activant vers des destinations. See the [destinations overview](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) for more information.

## Annexe

La section suivante fournit des informations supplémentaires sur la sortie de l’API du client.

### Données de sortie AI client

L’IA du client génère plusieurs attributs pour les  individuels qui sont considérés comme éligibles. Ces valeurs sont utilisées par le du client en temps réel, qui peut être utilisé pour créer et définir des segments. Le tableau ci-dessous décrit les différents attributs trouvés dans la sortie de l’API du client :

| Attribut | Description |
| ----- | ----------- |
| Score | probabilité relative pour un client d’atteindre l’objectif prévu dans le délai défini. Cette valeur ne doit pas être traitée comme un pourcentage de probabilité, mais plutôt comme la probabilité d&#39;un individu par rapport à la population globale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle d’un d’atteindre l’objectif prévu dans le délai défini. Lors de la comparaison de sorties entre différents objectifs, il est recommandé de prendre en compte la probabilité par rapport au percentile ou au score. La probabilité doit toujours être utilisée pour déterminer la probabilité moyenne dans la population admissible, car la probabilité tend à être la plus faible pour les  qui ne se produisent pas fréquemment. Les valeurs de probabilité sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations sur les performances d’un  par rapport à d’autres  de ayant obtenu les mêmes scores. Par exemple, un dont le rang de percentile est de 99 pour l’églises indique qu’il est plus susceptible de se produire que 99 % de tous les autres  qui ont été notés. Les centiles vont de 1 à 100. |
| Type de propension | Type de propension sélectionné. |
| Date de note | Date à laquelle la notation a eu lieu. |
| Facteurs influents | Raisons anticipées de la probabilité de conversion ou d’exécution d’un . Les facteurs comprennent les attributs suivants :<ul><li>Code : Attribut  ou comportemental qui influence positivement un  score prédit. </li><li>Valeur : Valeur de l’attribut  ou comportemental.</li><li>Importance : Indique le  de l’attribut de ou de comportement a sur le score prédit (faible, moyen, élevé)</li></ul> |