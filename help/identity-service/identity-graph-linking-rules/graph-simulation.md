---
title: Simulation de graphique
description: Découvrez comment utiliser la simulation graphique dans l’interface utilisateur d’Identity Service.
hide: true
hidefromtoc: true
badge: Version bêta
source-git-commit: 2afdfd54b420bcf59423ea64048d928422ea61c9
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 5%

---

# Simulation de graphique

La simulation graphique est un outil de l’interface utilisateur d’Identity Service que vous pouvez utiliser pour simuler le comportement d’un graphique d’identités en fonction d’une combinaison particulière d’identités et de la manière dont vous configurez la variable [algorithme d’optimisation des identités](./identity-optimization-algorithm.md).

Lisez ce document pour découvrir comment utiliser la simulation graphique afin de mieux comprendre le comportement du graphique d’identités et le fonctionnement de l’algorithme graphique.

## Découvrez l’interface de simulation graphique

Vous pouvez accéder à la simulation graphique dans l’interface utilisateur de Adobe Experience Platform. Sélectionner **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Simulation graphique]** dans l’en-tête supérieur.

![Interface de simulation graphique de l’interface utilisateur de Adobe Experience Platform.](../images/graph-simulation/graph-simulation.png)

L’interface de simulation graphique peut être divisée en trois sections :

* Événements : utilisez la variable **[!UICONTROL Événements]** pour ajouter des identités afin de simuler un graphique. Une identité entièrement qualifiée doit comporter un espace de noms d’identité et sa valeur d’identité correspondante. Vous devez ajouter au moins deux identités pour simuler un graphique. Vous pouvez également sélectionner **[!UICONTROL Exemple de chargement]** pour saisir un événement et une configuration d’algorithme préconfigurés.

![Panneau Événements de l’outil Simulation de graphique.](../images/graph-simulation/events.png)

* Configuration d’algorithme : utilisez la variable **[!UICONTROL Configuration d’algorithme]** pour ajouter et configurer l’algorithme d’optimisation des espaces de noms. Vous pouvez faire glisser et déposer un espace de noms pour modifier leur rang de priorité respectif. Vous pouvez également sélectionner **[!UICONTROL Unique par graphique]** pour déterminer si un espace de noms est unique.

![Configuration de l’algorithme de l’outil Simulation de graphique.](../images/graph-simulation/algorithm-configuration.png)

* Visionneuse de graphiques simulée : la visionneuse de graphiques simulée affiche le graphique obtenu en fonction des événements que vous avez ajoutés et de l’algorithme que vous avez configuré. Une ligne droite entre deux noeuds signifie qu’un lien est établi. Une ligne pointillée indique qu’un lien a été supprimé.


![Panneau de la visionneuse de graphiques simulée, avec un exemple de graphique simulé.](../images/graph-simulation/simulated-graph.png)

## Ajouter des événements

Pour commencer, sélectionnez **[!UICONTROL Ajout d’événements]**.

![Bouton Ajouter des événements sélectionné.](../images/graph-simulation/add-events.png)

Une fenêtre contextuelle s’affiche pour [!UICONTROL #1 d’événement]. À partir de là, saisissez votre combinaison d’espace de noms d’identité et de valeurs d’identité. Vous pouvez utiliser le menu déroulant pour sélectionner un espace de noms d’identité. Vous pouvez également saisir les premières lettres d’un espace de noms, puis sélectionner les options fournies dans le menu déroulant. Une fois que vous avez sélectionné votre espace de noms, fournissez une valeur d’identité qui correspond à votre espace de noms.

![](../images/graph-simulation/event-one.png)

>[!TIP]
>
>La valeur d’identité que vous saisissez lors des exercices de simulation graphique n’a pas besoin d’être de vraies valeurs d’identité et peut être de simples espaces réservés.

Une fois votre première identité terminée, sélectionnez l’icône d’ajout (**`+`**) pour ajouter une seconde identité.

![La première identité complète de {Email: tom@acme.com} est saisie dans le panneau Événements de la simulation graphique.](../images/graph-simulation/event-one-added.png)

Répétez ensuite les mêmes étapes et ajoutez une seconde identité. Deux identités entièrement qualifiées sont nécessaires pour générer un graphique d’identités. Dans l’exemple ci-dessous, un ECID est ajouté en tant qu’espace de noms et reçoit la valeur `111`. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Une seconde identité de {ECID : 111} est ajouté à la #1 d’événement.](../images/graph-simulation/first-event.png)

La variable [!UICONTROL Événements] mises à jour de l’interface pour afficher votre premier événement, qui, dans ce cas, est : `{Email: tom@acme.com, ECID: 111}`.

![Interface d’événements mise à jour avec {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Répétez ensuite les mêmes étapes pour ajouter un second événement. Pour #2 d’événement, ajoutez `{Email: summer@acme.com}` comme votre première identité, puis ajoutez la même `{ECID: 111}` comme seconde identité, créant ainsi un deuxième événement de : `{Email: summer@acme.com}, {ECID: 111}`. Une fois que vous avez terminé, vous devriez avoir deux événements, l’un pour `{Email: tom@acme.com, ECID: 111}` et un pour `{Email: summer@acme.com}, {ECID: 111}`.

![Interface d’événements mise à jour avec deux événements.](../images/graph-simulation/two-events.png)

### Charger l’exemple

+++Sélectionner pour afficher les étapes d’utilisation d’exemples de graphiques préchargés

Pour configurer un exemple de graphique avec un algorithme préconfiguré, sélectionnez **[!UICONTROL Exemple de chargement]**. Une fenêtre contextuelle s’affiche, vous indiquant les scénarios de graphiques disponibles parmi lesquels vous pouvez effectuer un choix :

| Exemple de graphique | Description | Exemple |
| --- | --- | --- |
| Appareil partagé | L’appareil partagé fait référence à des scénarios où deux utilisateurs différents se connectent au même appareil. | Un mari et une femme partagent une iPad pour la navigation sur Internet et le commerce électronique. |
| Téléphone non valide (non unique) | Un numéro de téléphone non valide ou non unique fait référence à des scénarios où deux utilisateurs différents utilisent le même numéro de téléphone pour créer un compte. | Une mère et sa fille utilisent leur numéro de téléphone commun pour s&#39;inscrire à n&#39;importe quel compte de commerce électronique. |
| Valeurs d’identité « incorrectes » | Les &quot;mauvaises&quot; valeurs d’identité se rapportent aux scénarios où Identity Service génère des IDFA non uniques en raison d’une mise en oeuvre erronée. | WebSDK envoie une `user_null` pour chaque événement en raison de problèmes d’implémentation du code. |

Sélectionnez l’une des options pour charger la simulation graphique avec des événements et un algorithme préconfigurés. Vous pouvez toujours effectuer d’autres configurations dans les exemples de scénario de graphique préchargés.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Simuler]**.

+++

### Utiliser la version texte

+++Sélectionnez cette option pour afficher les étapes d’utilisation de la version texte.

Vous pouvez également utiliser le mode texte pour configurer des événements. Pour utiliser le mode texte, sélectionnez l’engrenage (?) puis sélectionnez **[!UICONTROL Texte (utilisateurs avancés)]**.

Vous pouvez saisir vos identités manuellement en mode texte. Utilisez deux-points (`:`) pour distinguer la valeur d’identité qui correspond à l’espace de noms que vous avez saisi, puis utilisez une virgule (`,`) pour séparer vos identités. Pour distinguer différents événements les uns des autres, utilisez une nouvelle ligne pour chaque événement.

+++

### Modifier l’événement

Pour modifier un événement, sélectionnez les ellipses (`...`) en regard d’un événement donné, puis sélectionnez **[!UICONTROL Modifier]**.

### Supprimer un événement

Pour supprimer un événement, sélectionnez les ellipses (`...`) en regard d’un événement donné, puis sélectionnez **[!UICONTROL Supprimer]**.

## Configuration de l’algorithme

L’algorithme que vous configurez détermine la manière dont Identity Service traite les espaces de noms que vous avez saisis dans vos événements. Les configurations que vous associez dans l’interface utilisateur de simulation graphique ne sont pas enregistrées dans les paramètres d’identité.

Pour commencer, sélectionnez Ajouter (`+`) dans le coin inférieur du panneau de configuration de l’algorithme.



Une ligne de configuration vide s’affiche. Tout d’abord, saisissez le même espace de noms que celui utilisé pour vos événements. Dans ce cas, commencez par saisir l’identifiant CRM. Une fois que vous avez saisi l’espace de noms, les colonnes pour [!UICONTROL Symbole d’identité] et [!UICONTROL Type d’identité] auto-renseigne.



Répétez ensuite les mêmes étapes et ajoutez votre second espace de noms, qui est ici l’ECID. Une fois tous vos espaces de noms renseignés, vous pouvez commencer à configurer leurs priorités et leur unicité.

* **Priorité d’espace de noms**: la priorité d’un espace de noms détermine son importance relative par rapport aux autres espaces de noms d’un graphique d’identités donné. Par exemple, si votre graphique d’identités comporte quatre espaces de noms différents : ID CRM, ECID, Email et Apple IDFA, vous pouvez configurer des priorités afin de déterminer un ordre d’importance pour les quatre espaces de noms. (AJOUTER POURQUOI)
* **Espace de noms unique**: si un espace de noms est désigné comme unique, Identity Service génère des graphiques avec l’avertissement qu’une seule identité avec un espace de noms unique donné peut exister. Par exemple, si l’identifiant CRM est désigné comme un espace de noms unique, un graphique ne peut avoir qu’une seule identité avec l’identifiant CRM. S’il existe plusieurs identités avec l’espace de noms de l’identifiant CRM, le lien le plus ancien est supprimé.

Pour configurer la priorité des espaces de noms, sélectionnez les rangées d’espaces de noms et faites-les glisser selon l’ordre de priorité souhaité, la rangée supérieure représentant la priorité la plus élevée et la rangée inférieure la priorité la plus faible. Pour désigner un espace de noms unique, sélectionnez la variable **[!UICONTROL Unique par graphique]** .



Lorsque vous avez terminé, sélectionnez **[!UICONTROL Simuler]**.

## Afficher le graphique simulé

La variable [!UICONTROL Graphique simulé] affiche le ou les graphiques d’identités générés en fonction des événements que vous avez ajoutés et de l’algorithme que vous avez configuré.

| Icônes de graphique | Description |
| --- | --- |
| Ligne pleine | Une ligne pleine représente un lien établi entre deux identités. |
| Ligne en pointillé | Une ligne pointillée représente un lien supprimé entre deux identités. |
| Nombre en ligne | Un nombre sur une ligne représente l’horodatage de la génération de ce lien donné. Le nombre le plus bas (1) représente le lien le plus ancien établi. |

Dans l’exemple de graphique ci-dessous, il existe une ligne pointillée entre `{CRM ID: Tom}` et `{ECID: 111}` pour les raisons suivantes :

* L’identifiant CRM a été désigné comme unique lors de l’étape de configuration de l’algorithme. Par conséquent, une seule identité avec un espace de noms d’ID de gestion de la relation client peut exister dans un graphique.
* Le lien entre `{CRM ID: Tom}` et `{ECID: 111}` était la première identité établie (événement #1). Il s’agit du lien le plus ancien et il est donc supprimé.

## Exemples de scénarios graphiques

>[!NOTE]
>
>&quot;Identifiant CRM&quot; est un espace de noms personnalisé. Par conséquent, les exemples ci-dessous vous demandent de créer un espace de noms personnalisé avec un nom d’affichage et un symbole d’identité &quot;Identifiant CRM&quot;.

La section suivante présente des exemples de scénarios graphiques que vous pouvez rencontrer avec la simulation graphique.

### Identifiant CRM uniquement

Événements :

* Identifiant CRM : Tom, ECID : 111

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++

### Identifiant CRM avec courrier électronique haché

Dans ce scénario, un identifiant CRM est ingéré et représente à la fois des données en ligne (événement d’expérience) et hors ligne (enregistrement de profil). Ce scénario implique également l’ingestion d’un email haché, qui représente un autre espace de noms envoyé dans le jeu de données d’enregistrement CRM avec l’identifiant CRM.

Événements :

* Identifiant CRM : Tom, Email_LC_SHA256 : tom<span>@acme.com
* Identifiant CRM : Tom, ECID : 111
* Identifiant CRM : Summer, Email_LC_SHA256 : summer<span>@acme.com
* Identifiant CRM : été, ECID : 222

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | Email_LC_SHA256 | E-mail | NON |
| 3 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++

### Identifiant CRM avec courrier électronique haché, téléphone haché, GAID et IDFA

Événements :

* Identifiant CRM : Tom, Email_LC_SHA256 : aabbcc, Phone_SHA256: 123-4567
* Identifiant CRM : Tom, ECID : 111
* Identifiant CRM : Tom, ECID : 222, IDFA : A-A-A
* ID de gestion de la relation client : Summer, Email_LC_SHA256: deeff, Phone_SHA256: 765-4321
* Identifiant CRM : été, ECID : 333
* Identifiant CRM : Summer, ECID : 444, GAID:B-B-B

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | Email_LC_SHA256 | E-mail | NON |
| 3 | Téléphone (SHA256) | Phone_SHA256 | Téléphone | NON |
| 4 | Google Ad ID (GAID) | GAID | DEVICE | NON |
| 5 | Apple IDFA (ID pour Apple) | IDFA | DEVICE | NON |
| 6 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++