---
keywords: Experience Platform ; guide de l’utilisateur ; assistance client ; rubriques populaires ; configurer l’instance ; créer l’instance ;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Configuration d’une instance d’API client
topic: Création d’instances
description: Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 34%

---

# Configuration d’une instance d’API client

Dans le cadre d’Intelligent Services, Customer AI vous permet de générer des scores de propension personnalisés sans avoir à vous soucier de l’apprentissage automatique.

Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

## Configuration de votre instance {#set-up-your-instance}

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche tous les services disponibles. Dans le conteneur de l’API client, sélectionnez **[!UICONTROL Ouvrir]**.

![](../images/user-guide/navigate-to-service.png)

L&#39;interface utilisateur **Customer AI** s&#39;affiche et affiche toutes vos instances de service.

- Vous pouvez trouver la mesure **[!UICONTROL Nombre total de profils marqués]** située dans le coin inférieur droit du conteneur **[!UICONTROL Créer une instance]**. Cette mesure suit le nombre total de profils marqués par l’IA du client pour l’année civile en cours, y compris tous les environnements de sandbox et toutes les instances de service supprimées.

![](../images/user-guide/total-profiles.png)

Les instances de service peuvent être modifiées, clonées et supprimées à l’aide des commandes situées sur le côté droit de l’interface utilisateur. Pour afficher ces contrôles, sélectionnez une instance de vos instances **[!UICONTROL Service existantes]**. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : Le fait de sélectionner  **** Modifier vous permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence d’évaluation de l’instance.
- **[!UICONTROL Cloner]** : La sélection de  **** Clonecopies copie la configuration de l’instance de service actuellement sélectionnée. Vous pouvez ensuite modifier le processus pour effectuer des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]** : Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
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

- La source de données désigne l’endroit où se trouvent les données. Le jeu de données est le jeu de données d’entrée utilisé pour prévoir les scores. Par conception, l’IA du client utilise les données du Événement d’expérience du client, Adobe Analytics et Adobe Audience Manager pour calculer les scores de propension. Lors de la sélection d’un jeu de données à partir du sélecteur de liste déroulante, seuls les jeux compatibles avec Customer AI sont répertoriés.

- Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Indiquez les valeurs requises, puis sélectionnez **[!UICONTROL Suivant]**.

![](../images/user-guide/setup.png)

### Définition d’un objectif {#define-a-goal}

L’étape **[!UICONTROL Définir l’objectif]** s’affiche et fournit un environnement interactif vous permettant de définir visuellement un objectif de prédiction. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Pour créer un objectif, sélectionnez **[!UICONTROL Entrer le nom du champ]** et sélectionnez un champ dans la liste déroulante. Sélectionnez la deuxième entrée et sélectionnez une clause pour la condition événement, puis indiquez la valeur de cible pour terminer le événement. Vous pouvez configurer d&#39;autres événements en sélectionnant **[!UICONTROL événement d&#39;Ajoute]**. Enfin, terminez l’objectif en appliquant une période de prédiction en nombre de jours, puis sélectionnez **[!UICONTROL Suivant]**.

![](../images/user-guide/goal.png)

#### Se produira et ne se produira pas

Lors de la définition de votre objectif, vous avez la possibilité de sélectionner **[!UICONTROL Se produira]** ou **[!UICONTROL ne se produira pas]**. La sélection de **[!UICONTROL Se produit]** signifie que les conditions de événement que vous définissez doivent être remplies pour que les données de événement d&#39;un client soient incluses dans l&#39;interface utilisateur des statistiques.

Par exemple, si vous souhaitez configurer une application pour prédire si un client effectuera un achat, vous pouvez sélectionner **[!UICONTROL Se produira]** suivi de **[!UICONTROL Tous]**, puis entrer **commerce.purchase.id** et **existe** en tant qu&#39;opérateur.

![se produira](../images/user-guide/occur.png)

Cependant, il peut arriver que vous souhaitiez prédire si un certain événement ne se produira pas dans un certain délai. Pour configurer un objectif avec cette option, sélectionnez **[!UICONTROL Ne se produira pas]** dans la liste déroulante de niveau supérieur.

Par exemple, si vous souhaitez prédire quels clients sont moins engagés et ne pas consulter la page de connexion à votre compte au cours du mois suivant, Sélectionnez **[!UICONTROL Ne se produira pas]** suivi de **[!UICONTROL Tous]**, puis entrez **web.webInteraction.URL** et **[!UICONTROL est égal]** comme opérateur avec **account-login** comme valeur.

![ne se produira pas](../images/user-guide/not-occur.png)

#### Tout et n’importe lequel des

Dans certains cas, vous pouvez vouloir prédire si une combinaison de événements se produira et, dans d’autres cas, vous pouvez prédire l’occurrence d’un événement à partir d’un ensemble prédéfini. Pour prédire si un client aura une combinaison de événements, sélectionnez l&#39;option **[!UICONTROL Tous]** dans la liste déroulante de deuxième niveau de la page **[!UICONTROL Définir l&#39;objectif]**.

Par exemple, vous pouvez vouloir prédire si un client achète un produit particulier. Cet objectif de prédiction est défini par deux conditions : a `commerce.order.purchaseID` **existe** et `productListItems.SKU` **est égal à** une valeur spécifique.

![Tous les exemples](../images/user-guide/all-of.png)

Pour prédire si un client aura un événement d&#39;un ensemble donné, vous pouvez utiliser l&#39;option **[!UICONTROL N&#39;importe lequel de]**.

Vous pouvez, par exemple, prévoir si un client visite une certaine URL ou une page Web portant un nom particulier. Cet objectif de prédiction est défini par deux conditions : `web.webPageDetails.URL` **débuts avec** une valeur particulière et `web.webPageDetails.name` **débuts avec** une valeur particulière.

![N’importe quel exemple](../images/user-guide/any-of.png)

### Configuration d’un planning *(facultatif)* {#configure-a-schedule}

L&#39;étape **[!UICONTROL Advanced]** s&#39;affiche. Cette étape facultative vous permet de configurer un calendrier pour automatiser les exécutions de prédiction, de définir des exclusions de prédiction pour filtrer certains événements ou de sélectionner **[!UICONTROL Terminer]** si rien n&#39;est nécessaire.

Configurez un planning de notation en configurant la **[!UICONTROL Fréquence de notation]**. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](../images/user-guide/schedule.png)

Sous la configuration du planning, vous pouvez définir des exclusions de prédiction afin d’empêcher que des événements répondant à certaines conditions soient évalués lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données non pertinentes.

Pour exclure certains événements, sélectionnez **[!UICONTROL Ajouter l’exclusion]** et définissez le événement de la même manière que la définition de l’objectif. Pour supprimer une exclusion, sélectionnez les ellipses (**[!UICONTROL ...]**) en haut à droite du conteneur de événement, puis sélectionnez **[!UICONTROL Supprimer le Conteneur]**.

![](../images/user-guide/exclusion.png)

Exclure les événements si nécessaire, puis sélectionnez **[!UICONTROL Terminer]** pour créer l’instance.

![](../images/user-guide/advanced.png)

Si l’instance est créée avec succès, une opération de prédiction se déclenche immédiatement et les suivantes s’exécutent selon le planning défini.

>[!NOTE]
>
>Selon le volume des données d’entrée, les opérations de prédiction peuvent durer jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de Customer AI et exécuté une opération de prédiction. Une fois l’opération terminée, les insights notés génèrent automatiquement des profils avec les scores prévus. Veuillez patienter jusqu’à 24 heures avant de passer à la section suivante de ce tutoriel.

## Étapes suivantes {#next-steps}

En suivant ce didacticiel, vous avez correctement configuré une instance de l’IA du client et généré des scores de propension. Vous pouvez désormais choisir d’utiliser le créateur de segments pour [créer des segments de clients avec des scores prédits](./create-segment.md) ou [découvrir des statistiques avec l’IA du client](./discover-insights.md).

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre le processus de configuration de l’API client. En outre, les meilleures pratiques et les exemples d’utilisation sont fournis.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
