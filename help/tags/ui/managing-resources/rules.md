---
title: Règles
description: Découvrez le fonctionnement des extensions de balises dans Adobe Experience Platform.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: ht
source-wordcount: '1969'
ht-degree: 100%

---

# Règles

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans Adobe Experience Platform, les balises suivent un système basé sur des règles. Elles recherchent les interactions utilisateur et les données associées. Lorsque les critères définis dans votre règle sont satisfaits, la règle déclenche l’extension, le script ou le code côté client que vous avez identifié.

Créez des règles pour intégrer les données et les fonctionnalités du marketing, ainsi qu’une technologie d’annonces qui rassemble les produits disparates en une seule solution.

## Structure de règle

**Événements (If) :** l’événement est l’élément que la règle doit rechercher. Il est défini en sélectionnant un événement, toutes les conditions applicables et toutes les exceptions.

**Actions (Then) :** les déclencheurs surviennent après que les événements d’une règle ont lieu et que toutes les conditions sont satisfaites. Une règle de balise peut déclencher autant d’actions discrètes que vous souhaitez et vous pouvez contrôler l’ordre dans lequel elles se produisent. Par exemple, une règle unique pour une page de remerciements d’un site de commerce électronique peut déclencher vos outils d’analyse et balises tierces. Il n’est pas nécessaire de créer une règle distincte pour chaque extension ou balise.

Vous pouvez ajouter d’autres types d’événements. Plusieurs événements sont associés à l’aide d’un opérateur OR. Les conditions de la règle seront donc évaluées si l’un des événements est satisfait.

>[!IMPORTANT]
>
>Les modifications ne prennent effet que lorsqu’elles sont [publiées](../publishing/overview.md).

### Événements et conditions (if)

Les événements avec des conditions sont la composante *If* d’une règle.

Si un événement spécifié se produit, les conditions sont évaluées, puis les actions spécifiées ont lieu si nécessaire.

* **Événements** : indiquez un ou plusieurs événements devant avoir lieu pour déclencher la règle. Plusieurs événements sont unis par un opérateur OR. L’un des événements spécifiés va déclencher la règle.

* **Conditions** : circonscrivez l’événement en configurant les conditions qui doivent être vraies pour qu’un événement déclenche la règle. Une exception est définie comme une condition NOT. Plusieurs conditions sont réunies par un opérateur AND.

Les événements disponibles dépendent des extensions installées. Pour plus d’informations sur les événements dans l’extension Core, reportez-vous à [Types d’événements de l’extension Core](../../extensions/web/core/overview.md#core-extension-event-types).

### Actions (Then)

Les actions sont la partie *Then* d’une règle. Elles définissent ce que vous voulez qu’il se passe lorsque la règle s’exécute. Lorsqu’un événement est déclenché, si les conditions prennent la valeur true (vrai) et si les exceptions prennent la valeur false (faux), les actions sont effectuées. Vous pouvez faire glisser et déposer des actions pour les organiser selon vos besoins.

## Créez une règle

Créez une règle en indiquant les actions qui se produisent si une condition est remplie.

1. Ouvrez lʼonglet [!UICONTROL Règles], puis sélectionnez **[!UICONTROL Créer une règle]**.

   ![](../../images/launch-rule-builder.jpg)

1. Attribuez un nom à la règle.
1. Cliquez sur lʼicône **[!UICONTROL Ajouter]** sous Événements.
1. Sélectionnez votre extension et l’un des types d’événements disponibles pour cette extension, puis configurez les paramètres de l’événement.

   ![](../../images/rule-event-config.png)

   Les types d’événement disponibles dépendent de l’extension sélectionnée. Les paramètres de l’événement diffèrent en fonction du type d’événement. Certains événements ne comportent aucun paramètre à configurer.

   >[!IMPORTANT]
   >
   >Dans une règle côté client, les éléments de données sont segmentés en unités lexicales avec un `%` au début et à la fin du nom de l’élément de données. Par exemple : `%viewportHeight%`. Dans une règle de transfert d’événements, les éléments de données sont segmentés en unités lexicales avec `{{` au début et `}}` à la fin du nom de l’élément de données. Par exemple : `{{viewportHeight}}`.

   Pour référencer des données à partir du réseau Edge, le chemin d’accès de l’élément de données doit être `arc.event._<element>_`.

   `arc` désigne Adobe Response Context.

   Par exemple : `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Si ce chemin d’accès n’est pas spécifié correctement, les données ne sont pas collectées.

1. Définissez le paramètre Ordre, puis cliquez sur **[!UICONTROL Conserver les modifications]**.

   L’ordre par défaut pour tous les composants de règle est 50. Si vous souhaitez l’exécuter plus tôt, attribuez-lui un nombre inférieur à 50.

   * L’ordre d’exécution est l’ordre des nombres. 1 vient avant 3. 3 vient avant 10. 10 vient avant 100, etc.
   * Les règles qui ont le même ordre s’exécutent sans ordre particulier.
   * Les règles sont déclenchées dans l’ordre, mais pas nécessairement dans le même ordre. Si Règle A et Règle B partagent un événement et que vous attribuez un ordre pour que cette Règle A vienne en premier lieu, alors si Règle A fait quelque chose de manière asynchrone, il n’est pas garanti que Règle A se termine avant que Règle B ne commence.

      Si vous souhaitez qu’elle s’exécute plus tard, attribuez-lui un nombre supérieur à 50. Pour plus d’informations sur l’ordre, reportez-vous à [Ordre des règles](rules.md#rule-ordering).

1. Cliquez sur lʼicône **[!UICONTROL Ajouter]** sous Conditions, puis sélectionnez un type de logique, une extension, un type de condition et configurez les paramètres de votre condition. Sélectionnez ensuite **[!UICONTROL Conserver les modifications]**.

   ![](../../images/condition-settings.png)

   Les types de conditions disponibles dépendent de l’extension sélectionnée. Les paramètres de conditions diffèrent en fonction du type de condition.

   Type de logique :

   * Le type de logique normal permet l’exécution d’actions si la condition est remplie.
   * Le type de logique exceptionnel empêche l’exécution d’actions si la condition est remplie.

   (Avancé) Délai d’expiration : Cette option est disponible lorsque le séquencement des composants de règle est activé sur votre propriété. Cet attribut définit la durée maximale autorisée pour l’exécution de la condition. Si le délai d’expiration est atteint, la condition échoue et le reste des conditions et actions de la règle est supprimé de la file d’attente de traitement. La valeur par défaut est de 2 000 ms.

   Vous pouvez ajouter autant de conditions que vous le souhaitez. Plusieurs conditions dans la même règle sont jointes avec AND.

1. Cliquez sur lʼicône **[!UICONTROL Ajouter]** sous Actions, puis sélectionnez votre extension et lʼun des types dʼactions disponibles pour cette extension, configurez les paramètres de lʼaction, puis cliquez sur **[!UICONTROL Conserver les modifications]**.

   ![](../../images/action-settings.png)

   Les types d’action disponibles dépendent de l’extension que vous avez sélectionnée. Les paramètres d’action diffèrent selon le type d’action.

   (Avancé) Attendre avant d’exécuter l’action suivante : Cette option est disponible lorsque le séquencement des composants de règle est activé sur votre propriété. Lorsque cette option est cochée, les balises n’appellent pas l’action suivante tant que celle-ci n’est pas terminée. Lorsque cette option est désactivée, l’action suivante commence à s’exécuter immédiatement. La valeur par défaut est **[!UICONTROL Activé]**.

   (Avancé) Délai d’expiration : Cette option est disponible lorsque le séquencement des composants de règle est activé sur votre propriété. Il définit la durée maximale autorisée pour l’achèvement de l’action. Si le délai d’expiration est atteint, l’action échoue et toutes les actions suivantes de cette règle sont supprimées de la file d’attente de traitement. La valeur par défaut est de 2 000 ms.


1. Vérifiez votre règle, puis sélectionnez **[!UICONTROL Enregistrer la règle]**.

   Ultérieurement, lorsque vous [publierez](../publishing/overview.md), vous ajouterez cette règle à une bibliothèque et vous la déploierez.

Lors de la création ou de la modification de règles, vous pouvez enregistrer et créer une [bibliothèque active](../publishing/libraries.md#active-library). Cette opération enregistre immédiatement votre modification dans votre bibliothèque et exécute une version. Le statut de la version s’affiche.

## Ordre des règles {#rule-ordering}

L’ordre des règles vous permet de contrôler l’ordre d’exécution des règles qui partagent un événement.

Il est souvent important que vos règles se déclenchent dans un ordre spécifique. Exemples : (1) vous avez plusieurs règles qui définissent de manière conditionnelle des variables [!DNL Analytics] et vous devez vous assurer que la règle avec Send Beacon (Envoyer la balise) passe en dernier lieu. (2) vous avez une règle qui déclenche [!DNL Target] et une autre règle déclenche [!DNL Analytics], et vous souhaitez que la règle [!DNL Target] s’exécute en premier lieu.

En fin de compte, la responsabilité d’exécuter les actions dans l’ordre repose sur le développeur d’extensions du type d’événement que vous utilisez. Les développeurs d’extensions Adobe s’assurent que leurs extensions fonctionnent comme prévu. En ce qui concerne les extensions tierces, Adobe fournit des conseils aux développeurs d’extensions pour leur permettre d’effectuer cette implémentation correctement, mais c’est à eux de le faire.

Adobe vous recommande vivement de classer vos règles avec des nombres positifs compris entre 1 et 100 (la valeur par défaut est 50). Au plus simple, au mieux. Rappelez-vous que vous devez conserver votre ordre. Toutefois, Adobe admet qu’il peut y avoir des cas dans lesquels cet ordre s’avère contraignant. Dès lors, d’autres nombres sont autorisés. Les balises prennent en charge les nombres compris entre +/- 2 147 483 648. Vous pouvez également utiliser une douzaine de décimales. Cependant, si vous pensez que vous devez y avoir recours, vous devez repenser certaines des décisions que vous avez prises pour arriver à la situation actuelle.

>[!IMPORTANT]
>
>Dans la section Action d’une règle, les règles côté serveur sont exécutées de manière séquentielle. Assurez-vous que l’ordre est correct lorsque vous créez la règle.

### Scénarios

* Cinq règles partagent un événement. Elles ont toutes une priorité par défaut. Je souhaite que l’une d’elles s’exécute en dernier lieu. Il me suffit de modifier ce composant de règle et de lui attribuer un nombre supérieur à 50 (60 par exemple).
* Cinq règles partagent un événement. Elles ont toutes une priorité par défaut. Je souhaite que l’une d’elles s’exécute en premier lieu. Il me suffit de modifier ce composant de règle et de lui attribuer un nombre inférieur à 50 (40 par exemple).

### Gestion des règles côté client

L’ordre de chargement des règles varie selon que l’action de règle est configurée avec JavaScript, HTML ou un autre code côté client, et que les règles utilisent un événement de haut ou de bas de page ou un type d’événement différent.

Vous pouvez utiliser `document.write` dans vos scripts personnalisés, quels que soient les événements configurés pour la règle.

Vous pouvez agencer différents types de code personnalisé les uns par rapport aux autres. Vous pouvez, par exemple, avoir une action de code personnalisé JavaScript, puis une action de code personnalisé HTML, et enfin une action de code personnalisé JavaScript. Les balises garantissent leur exécution dans cet ordre.

## Regroupement de règles

Les événements et conditions des règles sont toujours regroupés dans la bibliothèque de balises principale. Les actions peuvent être regroupées dans la bibliothèque principale ou chargées plus tard en tant que sous-ressources, si nécessaire. Le type d’événement de la règle détermine si les actions sont regroupées ou non.

### Règles avec événements « Core - Library Loaded » (Core - Bibliothèque chargée) ou « Core - Page Top » (Core - Haut de page)

Ces événements doivent être presque toujours exécutés (à moins que les conditions n’aient la valeur false). Par souci d’efficacité, ils sont donc regroupés dans la bibliothèque principale, le fichier référencé par votre code incorporé.

* **Javascript :** le code JavaScript est intégré à la bibliothèque de balises principale. Le script personnalisé est encapsulé dans une balise de script et écrit dans le document à l’aide de `document.write`. Si la règle comporte plusieurs scripts personnalisés, ils sont écrits dans l’ordre.

* **HTML :** le code HTML est intégré à la bibliothèque de balises principale. `document.write` est utilisée pour écrire le code HTML dans le document. Si la règle comporte plusieurs scripts personnalisés, ils sont écrits dans l’ordre.

### Règles avec tout autre événement

Adobe ne peut garantir qu’aucune autre règle sera réellement déclenchée et que son code d’action sera nécessaire. Pour cette raison, les actions de tous les types d’événement qui ne sont pas répertoriés ci-dessus ne sont pas incluses dans la bibliothèque principale. Ils sont à la place stockés sous forme de sous-ressources et référencés par la bibliothèque principale si nécessaire.

* **JavaScript :** le code JavaScript est chargé à partir du serveur sous forme de texte normal, encapsulé dans une balise de script et ajouté au document à l’aide de Postscribe. Si la règle comporte plusieurs scripts personnalisés JavaScript, ils sont chargés en parallèle à partir du serveur, mais exécutés dans le même ordre que celui qui a été configuré dans la règle.
* **HTML :** le code HTML est chargé à partir du serveur et ajouté au document à l’aide de Postscribe. Si la règle comporte plusieurs scripts HTML personnalisés, ils sont chargés en parallèle à partir du serveur, mais exécutés dans le même ordre que celui qui a été configuré dans la règle.

## Séquencement des composants de règle {#sequencing}

Le comportement de lʼenvironnement dʼexécution des balises dépend de si **[!UICONTROL Exécuter les composants de règle en séquence]** est activé ou non pour votre propriété.

### Activé

Si cette option est activée, lorsqu’un événement est déclenché au moment de l’exécution, les conditions et actions de la règle sont ajoutées à une file d’attente de traitement (selon l’ordre que vous avez défini) et traitées une par une sur une base FIFO. La balise attend l’achèvement du composant avant de passer au suivant.

Si une condition est évaluée comme false ou atteint son délai d’expiration défini, les conditions et actions suivantes de cette règle sont supprimées de la file d’attente.

Si une action échoue ou atteint son délai d’expiration défini, les actions suivantes de cette règle sont supprimées de la file d’attente. 

>[!NOTE]
>
>Lorsque ce paramètre est activé, toutes les conditions et actions sont exécutées de manière asynchrone, et ce, même si vous avez chargé la bibliothèque de balises de manière synchrone.

### Désactivé

Si cette option est désactivée, lorsqu’un événement est déclenché au moment de l’exécution, les conditions de la règle sont immédiatement évaluées. Plusieurs conditions sont évaluées en parallèle.

Si toutes les conditions renvoient la valeur true (et que les exceptions renvoient la valeur false), les actions de la règle sont immédiatement exécutées. Les actions sont appelées dans l’ordre, mais les balises n’attendent pas qu’une action soit achevée avant d’appeler la suivante. Si vos actions sont synchrones, elles sont tout de même exécutées dans l’ordre. Si une ou plusieurs actions sont asynchrones, certaines actions s’exécutent en parallèle.
