---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configuration d’une instance d’API client
topic: Instance creation
description: Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 88%

---


# Configuration d’une instance d’API client

Dans le cadre d’Intelligent Services, Customer AI vous permet de générer des scores de propension personnalisés sans avoir à vous soucier de l’apprentissage automatique.

Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

## Configuration de votre instance {#set-up-your-instance}

Dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche tous les services disponibles. Dans le conteneur de Customer AI, cliquez sur **[!UICONTROL Ouvrir]**.

![](../images/user-guide/navigate-to-service.png)

L’écran *Customer AI* affiche toutes les instances de Customer AI existantes. Cliquez sur **[!UICONTROL Créer une instance]**.

![](../images/user-guide/dashboard.png)

Le workflow de création d’instance s’affiche à partir de l’étape *Configuration*.

Vous trouverez ci-dessous des informations importantes sur les valeurs que vous pouvez renseigner dans l’instance :

* Le nom de l’instance est utilisé partout où le score de Customer AI est affiché. Les noms doivent donc décrire ce que représentent les scores de prédiction, par exemple, « Likelihood to cancel magazine subscription » (Probabilité d’annuler l’abonnement au magazine).

* Le type de propension détermine l’intention de score et de polarité des mesures. You can either choose &quot;[!UICONTROL Churn]&quot; or &quot;[!UICONTROL Conversion]&quot;. Pour plus d’informations sur l’impact du type de propension sur votre instance, consultez la note située sous [résumé de notation](./discover-insights.md#scoring-summary) dans le document d’informations sur les découvertes.

* La source de données désigne l’endroit où se trouvent les données. Le jeu de données est le jeu de données d’entrée utilisé pour prévoir les scores. Par conception, Customer AI utilise des données d’événement d’expérience client pour calculer les scores de propension. Lors de la sélection d’un jeu de données à partir du sélecteur de liste déroulante, seuls les jeux compatibles avec Customer AI sont répertoriés.

* Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Indiquez les valeurs requises, puis cliquez sur **[!UICONTROL Suivant]**.

![](../images/user-guide/setup.png)

### Définition d’un objectif {#define-a-goal}

L’étape **[!UICONTROL Définir un objectif]** s’affiche et fournit un environnement interactif permettant de définir un objectif visuellement. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Cliquez sur **[!UICONTROL Saisir le nom du champ]** et sélectionnez un champ dans la liste déroulante. Cliquez sur la seconde entrée et sélectionnez une clause pour la condition de l’événement, puis indiquez la valeur cible pour terminer l’événement. D’autres événements peuvent être configurés en cliquant sur **[!UICONTROL Ajouter un événement]**. Enfin, atteignez l’objectif en appliquant une période de prédiction en nombre de jours, puis cliquez sur **[!UICONTROL Suivant]**.

![](../images/user-guide/goal.png)

### Configuration d’un planning *(facultatif)* {#configure-a-schedule}

The **[!UICONTROL Advanced]** step appears. Lors de cette étape facultative, vous pouvez configurer un planning pour automatiser les opérations de prédiction, définir les exclusions de prédiction pour filtrer certains événements ou cliquer sur **[!UICONTROL Terminer]** si aucune opération n’est requise.

Configurez un planning de notation en configurant la *Fréquence de notation*. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](../images/user-guide/schedule.png)

Sous la configuration du planning, vous pouvez définir des exclusions de prédiction afin d’empêcher que des événements répondant à certaines conditions soient évalués lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données non pertinentes.

Pour exclure certains événements, cliquez sur **[!UICONTROL Ajouter une exclusion]** et définissez l’événement de la même manière que l’objectif. Pour supprimer une exclusion, cliquez sur les points de suspension (**[!UICONTROL ...]**) en haut à droite du conteneur d’événements, puis cliquez sur **[!UICONTROL Supprimer le conteneur]**.

![](../images/user-guide/exclusion.png)

Excluez les événements selon les besoins, puis cliquez sur **[!UICONTROL Terminer]** pour créer l’instance.

![](../images/user-guide/advanced.png)

Si l’instance est créée avec succès, une opération de prédiction se déclenche immédiatement et les suivantes s’exécutent selon le planning défini.

>[!NOTE]
>
>Selon le volume des données d’entrée, les opérations de prédiction peuvent durer jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de Customer AI et exécuté une opération de prédiction. Une fois l’opération terminée, les insights notés génèrent automatiquement des profils avec les scores prévus. Veuillez patienter jusqu’à 24 heures avant de passer à la section suivante de ce tutoriel.

## Étapes suivantes {#next-steps}

En suivant ce didacticiel, vous avez correctement configuré une instance de l’IA du client et généré des scores de propension. Vous pouvez désormais choisir d’utiliser le créateur de segments pour [créer des segments de clients avec des scores](./create-segment.md) prédits ou [découvrir des statistiques avec l’IA](./discover-insights.md)du client.

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre le processus de configuration de l’API client. En outre, les meilleures pratiques et les exemples d’utilisation sont fournis.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

