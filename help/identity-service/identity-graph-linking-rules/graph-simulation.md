---
title: Guide de l’interface utilisateur de simulation graphique
description: Découvrez comment utiliser la simulation graphique dans l’interface utilisateur d’Identity Service.
badge: Version bêta
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 4c49bec7974dafe18d18deded6ddc936ece47dc3
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 1%

---

# Guide de l’interface utilisateur de [!DNL Graph Simulation]

>[!AVAILABILITY]
>
>Cette fonctionnalité n’est pas encore disponible ; le programme bêta pour les règles de liaison de graphiques d’identités devrait commencer en juillet sur les environnements de test de développement. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation.

[!DNL Graph Simulation] est un outil de l’interface utilisateur d’Identity Service que vous pouvez utiliser pour simuler le comportement d’un graphique d’identités en fonction d’une combinaison particulière d’identités et de la manière dont vous configurez la variable [algorithme d’optimisation des identités](./identity-optimization-algorithm.md).

Lisez ce document pour découvrir comment utiliser [!DNL Graph Simulation] pour mieux comprendre le comportement du graphique d’identités et le fonctionnement de l’algorithme graphique.

## Connaître le [!DNL Graph Simulation] interface {#interface}

Vous pouvez accéder à [!DNL Graph Simulation] dans l’interface utilisateur de Adobe Experience Platform. Sélectionner **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Simulation graphique]** dans l’en-tête supérieur.

![Interface de simulation graphique de l’interface utilisateur de Adobe Experience Platform.](../images/graph-simulation/graph-simulation.png)

La variable [!DNL Graph Simulation] peut être divisée en trois sections :

>[!BEGINTABS]

>[!TAB Événements]

Événements : utilisez la variable **[!UICONTROL Événements]** pour ajouter des identités afin de simuler un graphique. Une identité entièrement qualifiée doit comporter un espace de noms d’identité et sa valeur d’identité correspondante. Vous devez ajouter au moins deux identités pour simuler un graphique. Vous pouvez également sélectionner **[!UICONTROL Exemple de chargement]** pour saisir un événement et une configuration d’algorithme préconfigurés.

![Panneau Événements de l’outil Simulation de graphique.](../images/graph-simulation/events.png)

>[!TAB Configuration d’algorithme]

Configuration de l’algorithme : utilisez la méthode **[!UICONTROL Configuration d’algorithme]** pour ajouter et configurer l’algorithme d’optimisation des espaces de noms. Vous pouvez faire glisser et déposer un espace de noms pour modifier leur rang de priorité respectif. Vous pouvez également sélectionner **[!UICONTROL Unique par graphique]** pour déterminer si un espace de noms est unique.

![Configuration de l’algorithme de l’outil Simulation de graphique.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Visionneuse de graphiques simulée]

Visionneuse de graphiques simulée : la visionneuse de graphiques simulée affiche le graphique obtenu en fonction des événements que vous avez ajoutés et de l’algorithme que vous avez configuré. Une ligne droite entre deux identités signifie qu’un lien est établi. Une ligne pointillée indique qu’un lien a été supprimé.

![Panneau de la visionneuse de graphiques simulée, avec un exemple de graphique simulé.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Ajouter des événements {#add-events}

Pour commencer, sélectionnez **[!UICONTROL Ajout d’événements]**.

![Le bouton Ajouter des événements est sélectionné.](../images/graph-simulation/add-events.png)

Une fenêtre contextuelle s’affiche pour [!UICONTROL #1 d’événement]. À partir de là, saisissez votre combinaison d’espace de noms d’identité et de valeurs d’identité. Vous pouvez utiliser le menu déroulant pour sélectionner un espace de noms d’identité. Vous pouvez également saisir les premières lettres d’un espace de noms, puis sélectionner les options fournies dans le menu déroulant. Une fois que vous avez sélectionné votre espace de noms, fournissez une valeur d’identité qui correspond à votre espace de noms.

![La fenêtre #1 de l&#39;événement avec une interface vide.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Valeur d’identité que vous saisissez lors de la [!DNL Graph Simulation] Les exercices ne doivent pas nécessairement être de vraies valeurs d’identité et peuvent être de simples espaces réservés.

Une fois votre première identité terminée, sélectionnez l’icône d’ajout (**`+`**) pour ajouter une seconde identité.

![La première identité complète de {Email: tom@acme.com} est saisie dans le panneau Événements de la simulation graphique.](../images/graph-simulation/event-one-added.png)

Répétez ensuite les mêmes étapes et ajoutez une seconde identité. Deux identités entièrement qualifiées sont nécessaires pour générer un graphique d’identités. Dans l’exemple ci-dessous, un ECID est ajouté en tant qu’espace de noms et reçoit la valeur `111`. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Une seconde identité de {ECID : 111} est ajouté à la #1 d’événement.](../images/graph-simulation/first-event.png)

La variable [!UICONTROL Événements] mises à jour de l’interface pour afficher votre premier événement, qui, dans ce cas, est : `{Email: tom@acme.com, ECID: 111}`.

![Interface d’événements mise à jour avec {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Répétez ensuite les mêmes étapes pour ajouter un second événement. Pour #2 d’événement, ajoutez `{Email: summer@acme.com}` comme votre première identité, puis ajoutez la même `{ECID: 111}` comme seconde identité, créant ainsi un deuxième événement de : `{Email: summer@acme.com}, {ECID: 111}`. Une fois que vous avez terminé, vous devriez avoir deux événements, l’un pour `{Email: tom@acme.com, ECID: 111}` et un pour `{Email: summer@acme.com}, {ECID: 111}`.

![Interface d’événements mise à jour avec deux événements.](../images/graph-simulation/two-events.png)

### Charger l’exemple {#load-example}

Sélectionner **[!UICONTROL Exemple de chargement]** pour configurer un exemple de graphique avec un algorithme prédéfini et une configuration d’événement.

![L&#39;option Exemple de chargement est sélectionnée.](../images/graph-simulation/load-example.png)

Une fenêtre contextuelle s’affiche, vous indiquant les scénarios de graphiques disponibles parmi lesquels vous pouvez effectuer un choix :

| Exemple de graphique | Description | Exemple |
| --- | --- | --- |
| Appareil partagé | L’appareil partagé fait référence à des scénarios où deux utilisateurs différents se connectent au même appareil. | Un mari et une femme partagent une iPad pour la navigation sur Internet et le commerce électronique. |
| Téléphone non valide (non unique) | Un numéro de téléphone non valide ou non unique fait référence à des scénarios où deux utilisateurs différents utilisent le même numéro de téléphone pour créer un compte. | Une mère et sa fille utilisent leur numéro de téléphone commun pour s&#39;inscrire à n&#39;importe quel compte de commerce électronique. |
| Valeurs d’identité « incorrectes » | Les &quot;mauvaises&quot; valeurs d’identité se rapportent aux scénarios où Identity Service génère des IDFA non uniques en raison d’une mise en oeuvre erronée. | WebSDK envoie une `user_null` pour chaque événement en raison de problèmes d’implémentation du code. |

![Fenêtre présentant les exemples préconfigurés disponibles : appareil partagé, téléphone non valide et valeurs d’identité incorrectes.](../images/graph-simulation/example-options.png)

Sélectionnez l’une des options à charger. [!DNL Graph Simulation] avec des événements et un algorithme préconfigurés. Vous pouvez toujours effectuer d’autres configurations dans les exemples de scénario de graphique préchargés.

![Événements et algorithme configurés pour un téléphone non valide.](../images/graph-simulation/example-loaded.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Simuler]**.

![Exemple de graphique simulé pour un téléphone non valide.](../images/graph-simulation/example-simulated.png)

### Utiliser la version texte {#use-text-version}

Vous pouvez également utiliser le mode texte pour configurer des événements. Pour utiliser le mode texte, cliquez sur l’icône de paramètres, puis sélectionnez **[!UICONTROL Texte (utilisateurs avancés)]**.

![Icône Paramètres sélectionnée.](../images/graph-simulation/settings.png)

Vous pouvez saisir vos identités manuellement en mode texte. Utilisez deux-points (`:`) pour distinguer la valeur d’identité qui correspond à l’espace de noms que vous avez saisi, puis utilisez une virgule (`,`) pour séparer vos identités. Pour distinguer différents événements les uns des autres, utilisez une nouvelle ligne pour chaque événement.

![Panneau Événements utilisant la version du mode texte.](../images/graph-simulation/text-version.png)

### Modifier l’événement {#edit-event}

Pour modifier un événement, sélectionnez les ellipses (`...`) en regard d’un événement donné, puis sélectionnez **[!UICONTROL Modifier]**.

![Icône Modifier l’événement sélectionnée.](../images/graph-simulation/edit.png)

### Supprimer un événement {#delete-event}

Pour supprimer un événement, sélectionnez les ellipses (`...`) en regard d’un événement donné, puis sélectionnez **[!UICONTROL Supprimer]**.

![Icône de suppression d’événement sélectionnée.](../images/graph-simulation/delete.png)

## Configuration de l’algorithme {#configure-algorithm}

>[!IMPORTANT]
>
>L’algorithme que vous configurez détermine la manière dont Identity Service traite les espaces de noms que vous avez saisis dans vos événements. Toute configuration que vous associez dans la variable [!DNL Graph Simulation UI] ne sont pas enregistrées dans les paramètres d’identité.

Une fois que vous avez ajouté vos événements, vous pouvez configurer l’algorithme qui sera utilisé pour simuler votre graphique. Pour commencer, sélectionnez **[!UICONTROL Ajouter une configuration]**.

![Panneau de configuration des algorithmes.](../images/graph-simulation/add-config.png)

Une ligne de configuration vide s’affiche. Tout d’abord, saisissez le même espace de noms que celui utilisé pour vos événements. Dans ce cas, commencez par saisir Email. Une fois que vous avez saisi l’espace de noms, les colonnes pour [!UICONTROL Symbole d’identité] et [!UICONTROL Type d’identité] auto-renseigne.

![Première entrée de configuration.](../images/graph-simulation/add-namespace.png)

Répétez ensuite les mêmes étapes et ajoutez votre second espace de noms, qui est ici l’ECID. Une fois tous vos espaces de noms renseignés, vous pouvez commencer à configurer leurs priorités et leur unicité.

* **Priorité d’espace de noms**: la priorité d’un espace de noms détermine son importance relative par rapport aux autres espaces de noms d’un graphique d’identités donné. Par exemple, si votre graphique d’identités comporte quatre espaces de noms différents : ID CRM, ECID, Email et Apple IDFA, vous pouvez configurer des priorités afin de déterminer un ordre d’importance pour les quatre espaces de noms.
* **Espace de noms unique**: si un espace de noms est désigné comme unique, Identity Service génère des graphiques avec l’avertissement qu’une seule identité avec un espace de noms unique donné peut exister. Par exemple, si l’espace de noms Email est désigné comme un espace de noms unique, un graphique ne peut avoir qu’une seule identité avec Email. S’il existe plusieurs identités avec l’espace de noms Email, le lien le plus ancien est supprimé.

Pour configurer la priorité des espaces de noms, sélectionnez les rangées d’espaces de noms et faites-les glisser selon l’ordre de priorité souhaité, la rangée supérieure représentant la priorité la plus élevée et la rangée inférieure la priorité la plus faible. Pour désigner un espace de noms unique, sélectionnez la variable **[!UICONTROL Unique par graphique]** .

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Simuler]**.

![Tous les espaces de noms configurés.](../images/graph-simulation/all-namespaces.png)

## Afficher le graphique simulé

La variable [!UICONTROL Graphique simulé] affiche le ou les graphiques d’identités générés en fonction des événements que vous avez ajoutés et de l’algorithme que vous avez configuré.

| Icônes de graphique | Description |
| --- | --- |
| Ligne pleine | Une ligne pleine représente un lien établi entre deux identités. |
| Ligne en pointillé | Une ligne pointillée représente un lien supprimé entre deux identités. |
| Nombre en ligne | Un nombre sur une ligne représente l’horodatage de la génération de ce lien donné. Le nombre le plus bas (1) représente le lien le plus ancien établi. |

Dans l’exemple de graphique ci-dessous, il existe une ligne pointillée entre `{Email: tom@acme.com}` et `{ECID: 111}` pour les raisons suivantes :

* Le courrier électronique a été désigné comme unique au cours de l’étape de configuration de l’algorithme. Par conséquent, une seule identité avec un espace de noms Email peut exister dans un graphique.
* Le lien entre `{Email: tom@acme.com}` et `{ECID: 111}` était la première identité établie (événement #1). Il s’agit du lien le plus ancien et il est donc supprimé.

![Panneau de la visionneuse de graphiques simulée, avec un exemple de graphique simulé.](../images/graph-simulation/simulated-graph.png)

## Étapes suivantes

En lisant ce document, vous savez maintenant comment utiliser le [!DNL Graph Simulation] pour mieux comprendre comment vos données d’identité sont traitées selon un ensemble spécifique de règles et de configurations. Pour plus d’informations, lisez les documents suivants :

* [Règles de liaison de graphiques d’identités](overview.md)
* [Algorithme d’optimisation des identités](identity-optimization-algorithm.md)
* [Priorité d’espace de noms](namespace-priority.md)
