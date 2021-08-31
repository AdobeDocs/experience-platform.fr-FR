---
keywords: Experience Platform;guide de l’utilisateur;service clientèle;rubriques les plus consultées;configurer une instance;créer une instance ;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Configuration d’une instance Customer AI
topic-legacy: Instance creation
description: Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: b6fff24d6298bad968e16516f2e555927c3a4a12
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 26%

---

# Configuration d’une instance Customer AI

Dans le cadre d’Intelligent Services, Customer AI vous permet de générer des scores de propension personnalisés sans avoir à vous soucier de l’apprentissage automatique.

Intelligent Services fournit Customer AI en tant que service Adobe Sensei simple d’emploi pouvant être configuré pour de multiples cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

## Configuration de votre instance {#set-up-your-instance}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche tous les services disponibles. Dans le conteneur de Customer AI, sélectionnez **[!UICONTROL Ouvrir]**.

![](../images/user-guide/navigate-to-service.png)

L’interface utilisateur **Customer AI** s’affiche et affiche toutes vos instances de service.

- Vous trouverez la mesure **[!UICONTROL Nombre total de profils notés]** située dans le coin inférieur droit du conteneur **[!UICONTROL Créer une instance]**. Cette mesure effectue le suivi du nombre total de profils notés par Customer AI pour l’année civile en cours, y compris tous les environnements de test et toutes les instances de service supprimées.

![](../images/user-guide/total-profiles.png)

Les instances de service peuvent être modifiées, clonées et supprimées à l’aide des commandes situées dans la partie droite de l’interface utilisateur. Pour afficher ces contrôles, sélectionnez une instance parmi vos **[!UICONTROL instances de service]** existantes. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : Sélectionnez  **** Editer pour modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence de notation de l’instance.
- **[!UICONTROL Cloner]** : Sélectionnez  **** Clonecopies pour la configuration de l’instance de service actuellement sélectionnée. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]** : Vous pouvez supprimer une instance de service, y compris les exécutions historiques.
- **[!UICONTROL Source]** de données : Un lien vers le jeu de données utilisé par cette instance.
- **[!UICONTROL Détails]** de la dernière exécution : Cette option n’est affichée que lorsqu’une exécution échoue. Vous trouverez ici des informations sur les raisons de l’échec de l’exécution, telles que les codes d’erreur.
- **[!UICONTROL Définition de score]** : Aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

Pour créer une instance, sélectionnez **[!UICONTROL Créer une instance]**.

![](../images/user-guide/dashboard.png)

Le workflow de création d’instance s’affiche à partir de l’étape **[!UICONTROL Configuration]**.

Vous trouverez ci-dessous des informations importantes sur les valeurs que vous pouvez renseigner dans l’instance :

- Le nom de l’instance est utilisé à tous les endroits où les scores de Customer AI sont affichés. Les noms doivent donc décrire ce que représentent les scores de prédiction, par exemple, « Likelihood to cancel magazine subscription » (Probabilité d’annuler l’abonnement au magazine).

- Le type de propension détermine l’intention de score et de polarité des mesures. Vous pouvez choisir **[!UICONTROL Attrition]** ou **[!UICONTROL Conversion]**. Pour plus d’informations sur l’impact du type de propension sur votre instance, consultez la note située sous [résumé de notation](./discover-insights.md#scoring-summary) dans le document d’informations sur les découvertes.

- La source de données désigne l’endroit où se trouvent les données. Le jeu de données est le jeu de données d’entrée utilisé pour prévoir les scores. Par conception, Customer AI utilise les données Événement d’expérience client, Adobe Analytics et Adobe Audience Manager pour calculer les scores de propension. Lors de la sélection d’un jeu de données à partir du sélecteur de liste déroulante, seuls les jeux compatibles avec Customer AI sont répertoriés.

- Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

Indiquez les valeurs requises, puis sélectionnez **[!UICONTROL Suivant]**.

![](../images/user-guide/setup.png)

### Définition d’un objectif {#define-a-goal}

L’étape **[!UICONTROL Définir l’objectif]** s’affiche et vous permet de définir visuellement un objectif de prédiction dans un environnement interactif. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Pour créer un objectif, sélectionnez **[!UICONTROL Saisir le nom du champ]** et sélectionnez un champ dans la liste déroulante. Sélectionnez la seconde entrée et sélectionnez une clause pour la condition de l’événement, puis fournissez la valeur cible pour terminer l’événement. Vous pouvez configurer d’autres événements en sélectionnant **[!UICONTROL Ajouter un événement]**. Enfin, atteignez l’objectif en appliquant une période de prédiction en nombre de jours, puis sélectionnez **[!UICONTROL Suivant]**.

![](../images/user-guide/goal.png)

#### Se produira et ne se produira pas

Lors de la définition de votre objectif, vous avez la possibilité de sélectionner **[!UICONTROL Se produira]** ou **[!UICONTROL ne se produira pas]**. La sélection de **[!UICONTROL Se produit]** signifie que les conditions d’événement que vous définissez doivent être remplies pour que les données d’événement d’un client soient incluses dans l’interface utilisateur d’insights.

Par exemple, si vous souhaitez configurer une application pour prédire si un client effectuera un achat, vous pouvez sélectionner **[!UICONTROL Se produira]** suivi de **[!UICONTROL Tous]**, puis saisir **commerce.achats.id** et **existe** comme opérateur.

![se produit](../images/user-guide/occur.png)

Cependant, il peut arriver que vous souhaitiez prédire si un événement ne se produira pas dans un certain délai. Pour configurer un objectif avec cette option, sélectionnez **[!UICONTROL Ne se produira pas]** dans la liste déroulante de niveau supérieur.

Par exemple, si vous souhaitez prédire quels clients sont les moins engagés et ne consultez pas la page de connexion de votre compte au cours du mois suivant. Sélectionnez **[!UICONTROL Ne se produira pas]** suivi de **[!UICONTROL Tous]**, puis saisissez **web.webInteraction.URL** et **[!UICONTROL est égal à]** comme opérateur avec **account-login** comme valeur.

![ne se produira pas](../images/user-guide/not-occur.png)

#### Tout et n’importe lequel de

Dans certains cas, vous pouvez vouloir prédire si une combinaison d’événements se produira. Dans d’autres cas, vous pouvez vouloir prédire l’occurrence de tout événement d’un ensemble prédéfini. Pour prédire si un client aura une combinaison d’événements, sélectionnez l’option **[!UICONTROL Tous]** dans la liste déroulante de deuxième niveau de la page **[!UICONTROL Définir l’objectif]**.

Vous pouvez, par exemple, prédire si un client achète un produit particulier. Cet objectif de prédiction est défini par deux conditions : a `commerce.order.purchaseID` **exists** et `productListItems.SKU` **est égal à** une valeur spécifique.

![Tous les exemples](../images/user-guide/all-of.png)

Pour prédire si un client aura un événement d’un ensemble donné, vous pouvez utiliser l’option **[!UICONTROL Any of]** .

Vous pouvez, par exemple, prédire si un client visite une certaine URL ou une page web portant un nom particulier. Cet objectif de prédiction est défini par deux conditions : `web.webPageDetails.URL` **commence par** une valeur particulière et `web.webPageDetails.name` **commence par** une valeur particulière.

![N’importe quel exemple](../images/user-guide/any-of.png)

### Événements personnalisés (*facultatif*) {#custom-events}

Si vous disposez d’informations supplémentaires en plus des [champs d’événement standard](../input-output.md#standard-events) utilisés par Customer AI pour générer des scores de propension, une option d’événement personnalisé est fournie. Si le jeu de données que vous avez sélectionné inclut des événements personnalisés définis dans votre schéma, vous pouvez les ajouter à votre instance.

![fonction d’événement](../images/user-guide/event-feature.png)

Pour ajouter un événement personnalisé, sélectionnez **[!UICONTROL Ajouter un événement personnalisé]**. Ensuite, saisissez un nom d’événement personnalisé, puis mappez-le au champ d’événement de votre schéma. Les noms d’événement personnalisés s’affichent à la place de la valeur des champs lorsque vous examinez les facteurs d’influence et d’autres informations. Cela signifie que les identifiants d’utilisateur, de réservation, les informations sur l’appareil et d’autres valeurs personnalisées sont répertoriés avec le nom de l’événement personnalisé au lieu de l’identifiant/de la valeur de l’événement. Ces événements personnalisés supplémentaires sont utilisés par Customer AI pour améliorer la qualité de votre modèle et fournir des résultats plus précis.

![Champ Événement personnalisé](../images/user-guide/custom-event.png)

Sélectionnez ensuite l&#39;opérateur que vous souhaitez utiliser dans la liste déroulante des opérateurs disponibles. Seuls les opérateurs compatibles avec l&#39;événement sont répertoriés.

![Opérateur Événement personnalisé](../images/user-guide/custom-operator.png)

Enfin, saisissez la ou les valeurs du champ si l&#39;opérateur sélectionné en requiert une. Dans cet exemple, il suffit de vérifier s’il existe une réservation d’hôtel ou de restaurant. Cependant, si nous voulions être plus précis, nous pourrions utiliser l’opérateur égal et saisir une valeur exacte dans l’invite de valeur.

![Valeur du champ Événement personnalisé](../images/user-guide/custom-value.png)

Une fois l’opération terminée, sélectionnez **[!UICONTROL Suivant]** en haut à droite pour continuer.

### Configuration d’un planning *(facultatif)* {#configure-a-schedule}

L’étape **[!UICONTROL Avancé]** s’affiche. Cette étape facultative vous permet de configurer un planning pour automatiser les opérations de prédiction, de définir des exclusions de prédiction pour filtrer certains événements, ou de sélectionner **[!UICONTROL Terminer]** si rien n’est nécessaire.

Configurez un planning de notation en configurant la **[!UICONTROL Fréquence de notation]**. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](../images/user-guide/schedule.png)

### Exclusions de prédiction

Si votre jeu de données contenait des colonnes ajoutées en tant que données de test, vous pouvez ajouter cette colonne ou cet événement à une liste d’exclusion en sélectionnant **Ajouter une exclusion**, puis en entrant le champ que vous souhaitez exclure. Cela empêche l’évaluation des événements répondant à certaines conditions lors de la génération de scores. Cette fonction peut être utilisée pour filtrer les entrées de données non pertinentes ou certaines promotions.

Pour exclure un événement, sélectionnez **[!UICONTROL Ajouter l’exclusion]** et définissez l’événement. Pour supprimer une exclusion, sélectionnez les ellipses (**[!UICONTROL ...]**) en haut à droite du conteneur d’événements, puis sélectionnez **[!UICONTROL Supprimer le conteneur]**.

![](../images/user-guide/exclusion.png)

Excluez les événements selon les besoins, puis sélectionnez **[!UICONTROL Terminer]** pour créer l’instance.

![](../images/user-guide/advanced.png)

Si l’instance est créée avec succès, une opération de prédiction se déclenche immédiatement et les suivantes s’exécutent selon le planning défini.

>[!NOTE]
>
>Selon le volume des données d’entrée, les opérations de prédiction peuvent durer jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de Customer AI et exécuté une opération de prédiction. Une fois l’opération terminée, les insights notés génèrent automatiquement des profils avec les scores prévus. Veuillez patienter jusqu’à 24 heures avant de passer à la section suivante de ce tutoriel.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez correctement configuré une instance de Customer AI et généré des scores de propension. Vous pouvez désormais choisir d’utiliser le créateur de segments pour [créer des segments clients avec les scores prévus](./create-segment.md) ou [découvrir des insights avec Customer AI](./discover-insights.md).

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre le processus de configuration de Customer AI. De plus, des bonnes pratiques et des exemples de cas d’utilisation sont fournis.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
