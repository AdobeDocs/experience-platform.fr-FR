---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: Configuration d’une instance d’API client
topic: Instance creation
description: Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.
translation-type: tm+mt
source-git-commit: 0b92346065b7c9615d8aef4c9b13c84e0383b4b9
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 35%

---


# Configuration d’une instance d’API client

Dans le cadre d’Intelligent Services, Customer AI vous permet de générer des scores de propension personnalisés sans avoir à vous soucier de l’apprentissage automatique.

Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

## Configuration de votre instance {#set-up-your-instance}

In the Platform UI, select **[!UICONTROL Services]** in the left navigation. Le navigateur **[!UICONTROL Services]** apparaît et affiche tous les services disponibles. In the container for Customer AI, select **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

L’interface utilisateur **Customer AI** s’affiche et affiche toutes les instances de service.

- La mesure **[!UICONTROL Total profils notés]** se trouve dans le coin inférieur droit du conteneur d’instance **** Créer. Cette mesure suit le nombre total de profils marqués par l’IA du client pour l’année civile en cours, y compris tous les environnements de sandbox et toutes les instances de service supprimées.

![](../images/user-guide/total-profiles.png)

Les instances de service peuvent être modifiées, clonées et supprimées à l’aide des commandes situées sur le côté droit de l’interface utilisateur. Pour afficher ces contrôles, sélectionnez une instance parmi les instances **[!UICONTROL de]** service existantes. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]**: La sélection de **[!UICONTROL Modifier]** vous permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence d’évaluation de l’instance.
- **[!UICONTROL Cloner]**: Si vous sélectionnez **[!UICONTROL Cloner]** , la configuration de l’instance de service sélectionnée est copiée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]**: Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
- **[!UICONTROL Source]** de données : Lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Détails]** de la dernière exécution : Ceci s’affiche uniquement en cas d’échec d’une exécution. Les informations sur les raisons de l’échec de l’exécution, telles que les codes d’erreur, s’affichent ici.
- **[!UICONTROL Définition]** de note : Aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

Pour créer une instance, sélectionnez **[!UICONTROL Créer une instance]**.

![](../images/user-guide/dashboard.png)

Le workflow de création d’instance s’affiche à partir de l’étape **[!UICONTROL Configuration]**.

Vous trouverez ci-dessous des informations importantes sur les valeurs que vous pouvez renseigner dans l’instance :

- Le nom de l’instance est utilisé à tous les endroits où les scores d’IA du client sont affichés. Les noms doivent donc décrire ce que représentent les scores de prédiction, par exemple, « Likelihood to cancel magazine subscription » (Probabilité d’annuler l’abonnement au magazine).

- Le type de propension détermine l’intention de score et de polarité des mesures. Vous pouvez choisir **[!UICONTROL Attrition]** ou **[!UICONTROL Conversion]**. Pour plus d’informations sur l’impact du type de propension sur votre instance, consultez la note située sous [résumé de notation](./discover-insights.md#scoring-summary) dans le document d’informations sur les découvertes.

- La source de données désigne l’endroit où se trouvent les données. Le jeu de données est le jeu de données d’entrée utilisé pour prévoir les scores. Par conception, Customer AI utilise des données d’événement d’expérience client pour calculer les scores de propension. Lors de la sélection d’un jeu de données à partir du sélecteur de liste déroulante, seuls les jeux compatibles avec Customer AI sont répertoriés.

- Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Provide the required values and then select **[!UICONTROL Next]**.

![](../images/user-guide/setup.png)

### Définition d’un objectif {#define-a-goal}

The **[!UICONTROL Define goal]** step appears and it provides an interactive environment for you to visually define a prediction goal. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Pour créer un objectif, sélectionnez **[!UICONTROL Entrer le nom]** du champ et sélectionnez un champ dans la liste déroulante. Sélectionnez la deuxième entrée et sélectionnez une clause pour la condition événement, puis indiquez la valeur de cible pour terminer le événement. Additional events can be configured by selecting **[!UICONTROL Add event]**. Lastly, complete the goal by applying a prediction time frame in number of days, then select **[!UICONTROL Next]**.

![](../images/user-guide/goal.png)

#### Se produira et ne se produira pas

Lors de la définition de votre objectif, vous avez la possibilité de sélectionner **[!UICONTROL Se produira]** ou **[!UICONTROL Ne se produira]** pas. Si vous sélectionnez **[!UICONTROL Cette option se produit]** , les conditions de événement que vous définissez doivent être remplies pour que les données de événement d’un client soient incluses dans l’interface utilisateur des statistiques.

Par exemple, si vous souhaitez configurer une application pour prédire si un client effectuera un achat, vous pouvez sélectionner **[!UICONTROL Se produira]** , suivi de **[!UICONTROL Tout]** , puis entrer **commerce.achats.id** et **existe en tant qu’opérateur.**

![se produira](../images/user-guide/occur.png)

Cependant, il peut arriver que vous souhaitiez prédire si un certain événement ne se produira pas dans un certain délai. Pour configurer un objectif avec cette option, sélectionnez **[!UICONTROL Ne se produira]** pas dans la liste déroulante de niveau supérieur.

Par exemple, si vous souhaitez prédire quels clients sont moins engagés et ne pas consulter la page de connexion à votre compte au cours du mois suivant, Sélectionnez **[!UICONTROL Ne se produira]** pas, suivi de **[!UICONTROL Tout]** , puis saisissez **web.webInteraction.URL** et **[!UICONTROL est égal comme opérateur avec account-login comme valeur.]******

![ne se produira pas](../images/user-guide/not-occur.png)

#### Tout et n’importe lequel des

Dans certains cas, vous pouvez vouloir prédire si une combinaison de événements se produira et, dans d’autres cas, vous pouvez prédire l’occurrence d’un événement à partir d’un ensemble prédéfini. Pour prédire si un client aura une combinaison de événements, sélectionnez l’option **[!UICONTROL Tout]** dans la liste déroulante de second niveau sur la page **[!UICONTROL Définir l’objectif]** .

Par exemple, vous pouvez vouloir prédire si un client achète un produit particulier. Cet objectif de prédiction est défini par deux conditions : a `commerce.order.purchaseID` existe **et la valeur** est `productListItems.SKU` **** égale à une valeur spécifique.

![Tous les exemples](../images/user-guide/all-of.png)

Pour prédire si un client aura un événement d’un ensemble donné, vous pouvez utiliser l’option **[!UICONTROL N’importe lequel des]** .

Vous pouvez, par exemple, prévoir si un client visite une certaine URL ou une page Web portant un nom particulier. Cet objectif de prédiction est défini par deux conditions : `web.webPageDetails.URL` **débuts avec** une valeur particulière et `web.webPageDetails.name` débuts avec **** une valeur particulière.

![N’importe quel exemple](../images/user-guide/any-of.png)

### Configuration d’un planning *(facultatif)* {#configure-a-schedule}

The **[!UICONTROL Advanced]** step appears. This optional step allows you to configure a schedule to automate prediction runs, define prediction exclusions to filter certain events, or select **[!UICONTROL Finish]** if nothing is needed.

Configurez un planning de notation en configurant la **[!UICONTROL Fréquence de notation]**. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](../images/user-guide/schedule.png)

Sous la configuration du planning, vous pouvez définir des exclusions de prédiction afin d’empêcher que des événements répondant à certaines conditions soient évalués lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données non pertinentes.

To exclude certain events, select **[!UICONTROL Add exclusion]** and define the event in the same fashion as to how the goal is defined. To remove an exclusion, select the ellipses (**[!UICONTROL ...]**) to the top-right of the event container and then select **[!UICONTROL Remove Container]**.

![](../images/user-guide/exclusion.png)

Exclude events as needed and then select **[!UICONTROL Finish]** to create the instance.

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

