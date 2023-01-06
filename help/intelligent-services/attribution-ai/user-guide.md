---
keywords: Experience Platform;guide de l’utilisateur;accès à l’attribution;rubriques les plus consultées;région
feature: Attribution AI
title: Guide de l’interface utilisateur Attribution AI
description: Ce document sert de guide pour interagir avec Attribution AI dans l’interface utilisateur d’Intelligent Services.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2960'
ht-degree: 35%

---

# Guide de l’interface utilisateur Attribution AI

Dans le cadre d’Intelligent Services, Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à Attribution AI, les marketeurs peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase du parcours des clients.

Ce document sert de guide pour interagir avec Attribution AI dans l’interface utilisateur d’Intelligent Services.

## Création d’une instance

Dans le [!DNL Adobe Experience Platform] Interface utilisateur, sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche les services intelligents Adobe disponibles. Dans le conteneur pour Attribution AI, sélectionnez **[!UICONTROL Ouvrir]**.

![Accès à votre instance](./images/user-guide/open_Attribution_ai.png)

La page de service d’Attribution AI s’affiche. Cette page répertorie les instances de service d’Attribution AI et affiche les informations les concernant, notamment le nom de l’instance, les événements de conversion, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour.

Vous trouverez la variable **[!UICONTROL Nombre total d’événements de conversion notés]** mesure située dans le coin inférieur droit de la **[!UICONTROL Créer une instance]** conteneur. Cette mesure effectue le suivi du nombre total d’événements de conversion marqués par Attribution AI pour l’année civile en cours, y compris tous les environnements de test et toutes les instances de service supprimées.

![total des conversions](./images/user-guide/total_conversions.png)

Les instances de service peuvent être modifiées, clonées et supprimées à l’aide des commandes situées dans la partie droite de l’interface utilisateur. Pour afficher ces commandes, sélectionnez une instance parmi les **[!UICONTROL Instances de service]**. Les contrôles contiennent les informations suivantes :

- **[!UICONTROL Modifier]**: Sélection **[!UICONTROL Modifier]** permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description, l’état et la fréquence de notation de l’instance.
- **[!UICONTROL Cloner]**: Sélection **[!UICONTROL Cloner]** copie l’instance de service sélectionnée. Vous pouvez ensuite modifier le workflow pour effectuer des ajustements mineurs et le renommer en nouvelle instance.
- **[!UICONTROL Supprimer]**: Vous pouvez supprimer une instance de service, y compris les exécutions historiques. Le jeu de données de sortie correspondant sera supprimé de Platform. Toutefois, les scores synchronisés dans Real-time Customer Profile ne sont pas supprimés.
- **[!UICONTROL Source de données]**: Lien vers le jeu de données utilisé. Si plusieurs jeux de données sont utilisés par Attribution AI, &quot;Multiple&quot; suivi du nombre de jeux de données s’affiche. Lorsque vous sélectionnez l’hyperlien, la fenêtre contextuelle d’aperçu des jeux de données s’affiche.
- **[!UICONTROL Détails de la dernière exécution]**: Cette option n’est affichée que lorsqu’une exécution échoue. Vous trouverez ici des informations sur les raisons pour lesquelles l’exécution a échoué, telles que les codes d’erreur.

![Volet latéral](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL Événements de conversion]**: Aperçu rapide des événements de conversion configurés pour cette instance.
- **[!UICONTROL Intervalle de recherche en amont]**: La période que vous avez définie indiquant le nombre de jours avant l’inclusion des points de contact de l’événement de conversion.
- **[!UICONTROL Points de contact]**: Liste de tous les points de contact que vous avez définis lors de la création de cette instance.

![](./images/user-guide/side_panel_2.png)

Sélectionner **[!UICONTROL Créer une instance]** pour commencer.

![Création d’une instance](./images/user-guide/landing_page.png)

Ensuite, la page de configuration d’Attribution AI s’affiche, où vous pouvez fournir un nom et une description facultative de votre instance de service.

![attribution d’un nom à une instance](./images/user-guide/naming_instance.png)

## Sélectionner les données {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

Par conception, Attribution AI peut utiliser les données Adobe Analytics, Evénement d’expérience et Événement d’expérience client pour calculer les scores d’attribution. Lors de la sélection d’un jeu de données, seuls les jeux compatibles avec Attribution AI sont répertoriés. Pour sélectionner un jeu de données, sélectionnez (**+**) en regard du nom du jeu de données ou cochez la case pour ajouter plusieurs jeux de données à la fois. Vous pouvez également utiliser l’option de recherche pour trouver rapidement les jeux de données qui vous intéressent.

Après avoir sélectionné les jeux de données que vous souhaitez utiliser, sélectionnez la variable **[!UICONTROL Ajouter]** pour ajouter les jeux de données au volet d’aperçu du jeu de données.

![Sélectionner des jeux de données](./images/user-guide/select-datasets.png)

Icône Sélectionner l’information ![icône info](./images/user-guide/info-icon.png) en regard d’un jeu de données, la fenêtre contextuelle d’aperçu du jeu de données s’ouvre.

![Sélection et recherche d’un jeu de données](./images/user-guide/dataset-preview.png)

L’aperçu du jeu de données contient des données telles que l’heure de la dernière mise à jour, le schéma source et un aperçu des dix premières colonnes.

Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer vos brouillons au fur et à mesure que vous vous déplacez dans le workflow. Vous pouvez également enregistrer les configurations de modèle de brouillon et passer à l’étape suivante du workflow. Utilisation **[!UICONTROL Enregistrer et continuer]** pour créer et enregistrer des brouillons lors des configurations de modèle. Cette fonctionnalité vous permet de créer et d’enregistrer des brouillons de la configuration du modèle. Elle est particulièrement utile lorsque vous devez définir de nombreux champs dans le workflow de configuration.

![Le workflow Créer de l’onglet Attribution AI Data Science Services avec Enregistrer et enregistrer et continuer est mis en surbrillance.](./images/user-guide/aai-save-save-&-exit.png)

### Complétude du jeu de données {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

Dans l’aperçu du jeu de données, il existe une valeur en pourcentage d’exhaustivité du jeu de données. Cette valeur fournit un instantané du nombre de colonnes vides/nulles de votre jeu de données. Si un jeu de données contient de nombreuses valeurs manquantes et que ces valeurs sont capturées ailleurs, il est vivement recommandé d’inclure le jeu de données contenant les valeurs manquantes.

>[!NOTE]
>
>L’exhaustivité des jeux de données est calculée à l’aide de la période de formation maximale pour Attribution AI (un an). Cela signifie que les données de plus d’un an ne sont pas prises en compte lors de l’affichage de la valeur d’exhaustivité de votre jeu de données.

![Complétude du jeu de données](./images/user-guide/dataset-completeness.png)

### Sélection d’une identité {#identity}

Vous pouvez désormais joindre plusieurs jeux de données les uns aux autres en fonction de la carte d’identité (champ). Vous devez sélectionner un type d’identité (également appelé &quot;espace de noms d’identité&quot;) et une valeur d’identité dans cet espace de noms. Si vous avez affecté plusieurs champs en tant qu’identité dans votre schéma sous le même espace de noms, toutes les valeurs d’identité attribuées apparaissent dans la liste déroulante d’identité précédée de l’espace de noms tel que `EMAIL (personalEmail.address)` ou `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>Le même type d’identité (espace de noms) doit être utilisé pour chaque jeu de données sélectionné. Une coche verte s’affiche en regard du type d’identité dans la colonne d’identité pour indiquer que les jeux de données sont compatibles. Par exemple, lors de l’utilisation de l’espace de noms Phone et `mobilePhone.number` comme identifiant, tous les identifiants des jeux de données restants doivent contenir et utiliser l’espace de noms Phone.

Pour sélectionner une identité, sélectionnez la valeur soulignée située dans la colonne d’identité. La fenêtre contextuelle Sélectionner une identité s’affiche.

![sélectionner le même espace de noms](./images/user-guide/aai-identity-map-save-and-exit.png)

Dans le cas où plusieurs identités sont disponibles dans un espace de noms, veillez à sélectionner le champ d’identité approprié à votre cas d’utilisation. Par exemple, deux identités de courrier électronique sont disponibles dans l’espace de noms de courrier électronique, un courrier électronique professionnel et un courrier électronique personnel. Selon le cas d’utilisation, un email personnel est plus susceptible d’être renseigné et plus utile dans les prédictions individuelles. Cela signifie que vous pouvez sélectionner `EMAIL (personalEmail.address)` comme votre identité.

![Clé de jeu de données non sélectionnée](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> S’il n’existe aucun type d’identité (espace de noms) valide pour un jeu de données, vous devez définir une identité Principale et l’affecter à un espace de noms d’identité à l’aide de la variable [éditeur de schéma](../../xdm/schema/composition.md#identity). Pour en savoir plus sur les espaces de noms et les identités, rendez-vous sur la page [Espaces de noms Identity Service](../../identity-service/namespaces.md) documentation.

## Mappage du canal média et des champs de campagne {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

Une fois que vous avez fini de sélectionner et d’ajouter des jeux de données, la variable **Carte** l’étape de configuration s’affiche. Attribution AI exige que vous mappez le champ Canal multimédia pour chaque jeu de données sélectionné à l’étape précédente. En effet, sans le mappage du canal Media entre les jeux de données, les informations dérivées d’Attribution AI peuvent ne pas s’afficher correctement, ce qui rend la page d’informations difficile à interpréter. Bien que seul le canal Média soit requis, il est vivement recommandé de mapper certains des champs facultatifs tels que l’action Média, le nom de la campagne, le groupe Campagne et la balise Campagne. Cela permet à Attribution AI de fournir des informations plus claires et des résultats optimaux.

![mappage](./images/user-guide/mapping-save-&-exit.png)

## Définition des événements {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

Il existe trois types différents de données d’entrée utilisées pour définir les événements :

- **Événements de conversion :** objectifs professionnels qui identifient l’impact des activités marketing, comme les commandes e-commerce, les achats en magasin et les visites sur le site web.
- **Intervalle de recherche en amont :** fournit une période indiquant le nombre de jours avant l’inclusion des points de contact de l’événement de conversion.
- **Points de contact :** événements marketing au niveau des bénéficiaires, des individus ou des cookies utilisés pour évaluer l’impact numérique ou basé sur les recettes des conversions.

### Définition des événements de conversion {#define-conversion-events}

Pour définir un événement de conversion, vous devez donner un nom à l’événement et sélectionner le type d’événement en sélectionnant le jeu de données et le champ dans la variable **Sélection d’un jeu de données et d’un champ** menu déroulant.

![menu déroulant oui](./images/user-guide/define-conversion-events.png)

Une fois qu’un événement est sélectionné, un nouveau menu déroulant s’affiche à sa droite. Le second menu déroulant est utilisé pour fournir davantage de contexte à votre événement grâce à l’utilisation des opérations. Pour cet événement de conversion, l’opération par défaut *exists* est utilisée.

>[!NOTE]
>
>Une chaîne sous votre *nom de conversion* est mise à jour au fur et à mesure que vous définissez votre événement.

![aucun menu déroulant](./images/user-guide/conversion_event_1.png)

Vous pouvez ensuite sélectionner un jeu de données combiné généré en combinant tous les jeux de données d’entrée à l’étape précédente. Vous pouvez également sélectionner une colonne en fonction de jeux de données individuels dans la variable **Sélection d’un jeu de données et d’un champ** menu déroulant.

Les boutons **[!UICONTROL Ajouter un événement]** et **[!UICONTROL Ajouter un groupe]** permettent de définir plus précisément votre conversion. En fonction de la conversion que vous définissez, vous devrez peut-être utiliser les boutons **[!UICONTROL Ajouter un événement]** et **[!UICONTROL Ajouter un groupe]** pour fournir davantage de contexte.

![ajouter un événement](./images/user-guide/add_event.png)

Sélection **[!UICONTROL Ajouter un événement]** crée des champs supplémentaires qui peuvent être remplis en utilisant la même méthode que celle décrite ci-dessus. Cela permet d’ajouter une instruction ET à la définition de la chaîne sous le nom de la conversion. Sélectionnez la **x** pour supprimer un événement qui a été ajouté.

![menu ajouter un événement](./images/user-guide/add_event_result.png)

Sélection **[!UICONTROL Ajouter un groupe]** permet de créer des champs supplémentaires distincts de l’original. Avec l’ajout de groupes, un bouton bleu *Et* apparaît. Sélection **Et** permet de modifier le paramètre pour qu’il contienne &quot;Ou&quot;. « Ou » est utilisé pour définir plusieurs chemins de conversion performants. « Et » prolonge le chemin de conversion pour inclure des conditions supplémentaires.

![utilisation de et/ou](./images/user-guide/and_or.png)

Si vous avez besoin de plusieurs conversions, sélectionnez **Ajouter une conversion** pour créer une carte de conversion. Vous pouvez répéter la procédure ci-dessus pour définir plusieurs conversions.

![ajouter une conversion](./images/user-guide/add_conversion.png)

### Définition de l’intervalle de recherche en amont {#lookback-window}

Une fois la conversion définie, vous devez confirmer votre intervalle de recherche en amont. À l’aide des touches fléchées ou en sélectionnant la valeur par défaut (56), indiquez le nombre de jours avant votre événement de conversion à partir duquel vous souhaitez inclure des points de contact. Les points de contact sont définis à l’étape suivante.

![recherche en amont](./images/user-guide/lookback_window.png)

### Définition des points de contact

La définition des points de contact suit un workflow similaire à celui de la [définition des conversions](#define-conversion-events). Dans un premier temps, vous devez nommer votre point de contact et sélectionner une valeur de point de contact dans le menu déroulant *Saisir le nom du champ*. Une fois sélectionné, le menu déroulant de l’opérateur s’affiche avec la valeur par défaut « exists ». Sélectionnez la liste déroulante pour afficher une liste d’opérateurs.

![opérateurs](./images/user-guide/operators.png)

Pour ce point de contact, sélectionnez **equals**.

![étape 1](./images/user-guide/touchpoint_step1.png)

Une fois qu’un opérateur pour un point de contact est sélectionné, *Saisir la valeur du champ* est mis à disposition. Les valeurs du menu déroulant pour *Saisir la valeur du champ* reposent sur l’opérateur et la valeur du point de contact que vous avez sélectionnés précédemment. Si une valeur n’apparaît pas dans le menu déroulant, vous pouvez la saisir manuellement. Sélectionnez la liste déroulante, puis sélectionnez **CLIQUEZ**.

>[!NOTE]
>
>Les opérateurs « exists » et « not exists » ne sont pas associés à des valeurs de champ.

![menu déroulant du point de contact](./images/user-guide/touchpoint_dropdown.png)

Les boutons **Ajouter un événement** et **Ajouter un groupe** permettent de définir plus précisément votre point de contact. En raison de la nature complexe des points de contact, il n’est pas rare d’avoir plusieurs événements et groupes pour un seul point de contact.

Lorsque cette option est sélectionnée, **Ajouter un événement** permet d’ajouter des champs supplémentaires. sélectionnez la variable **x** pour supprimer un événement qui a été ajouté.

![ajouter un événement](./images/user-guide/touchpoint_add_event.png)

Sélection **Ajouter un groupe** permet de créer des champs supplémentaires distincts de l’original. Avec l’ajout de groupes, un bouton bleu *Et* apparaît. Sélectionner **Et** pour modifier le paramètre, le nouveau paramètre &quot;Ou&quot; est utilisé pour définir plusieurs chemins performants. Ce point de contact particulier n’a qu’un seul chemin performant. Par conséquent, « Ou » n’est pas nécessaire.

![présentation du point de contact](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Utilisez la chaîne sous le *nom du point de contact* pour avoir un aperçu rapide de votre point de contact. Notez que la chaîne correspond au nom du point de contact.

![](./images/user-guide/touchpoint_string.png)

Vous pouvez ajouter d’autres points de contact en sélectionnant **Ajouter un point de contact** et répétant le processus ci-dessus.

![ajouter un point de contact](./images/user-guide/add_touchpoint.png)

Une fois que vous avez défini tous les points de contact nécessaires, faites défiler la page vers le haut et sélectionnez **Suivant** dans le coin supérieur droit pour passer à l’étape finale.

![définition terminée](./images/user-guide/define_event_save_and_exit.png)

## Configuration de la formation et de la notation avancées

La dernière page d’Attribution AI est la page **[!UICONTROL Avancé]** utilisée pour configurer la formation et la notation.

![nouvelles options de jeu de pages](./images/user-guide/advanced_settings_set_options.png)

### Planification de la formation

À l’aide du *planning*, vous pouvez sélectionner le jour et l’heure de la semaine où vous souhaitez que la notation soit effectuée.

Sélectionnez la liste déroulante sous *Fréquence de notation* pour choisir entre une notation quotidienne, hebdomadaire et mensuelle. Ensuite, sélectionnez les jours de la semaine où vous souhaitez que la notation soit effectuée. Vous pouvez sélectionner plusieurs jours. Si vous sélectionnez à nouveau le même jour, il est désélectionné.

![Planification de la formation](./images/user-guide/schedule_training.png)

Pour modifier l’heure de la journée où vous souhaitez que la notation soit effectuée, cliquez sur l’icône de l’horloge. Dans la nouvelle fenêtre qui s’affiche, saisissez l’heure de la journée à laquelle vous souhaitez que la notation soit effectuée. Sélectionnez en dehors de la superposition pour la fermer.

>[!NOTE]
>
>Chaque processus de notation peut prendre jusqu’à 24 heures.

![icône de l’horloge](./images/user-guide/time_of_day.png)

### Colonnes de jeu de données de score supplémentaires (facultatif)

Par défaut, un jeu de données de score est créé pour chaque instance de service dans un schéma standard. Vous pouvez choisir d’ajouter des colonnes supplémentaires en fonction de vos configurations Événement de conversion et Point de contact à la sortie du jeu de données de notation. Commencez par sélectionner des colonnes dans votre jeu de données d’entrée, puis faites-les glisser et déposez-les pour modifier l’ordre en maintenant le bouton gauche de la souris enfoncé sur l’icône de hamburger.

![ajout de colonne de jeu de données de score](./images/user-guide/Add-score-dataset.png)

### Modélisation basée sur la région (facultative) {#region-based-modeling-optional}

Le comportement de vos clients peut varier considérablement selon le pays et la région géographique. Pour les entreprises mondiales, l’utilisation de modèles basés sur les pays ou les régions peut accroître la précision de l’attribution. Chaque région ajoutée crée un nouveau modèle avec les données de cette région.

Pour définir une nouvelle région, commencez par sélectionner **[!UICONTROL Ajouter une région]**. Dans le conteneur qui s’affiche, attribuez un nom à la région. Une seule valeur (« placeContext.geo.countryCode ») s’affiche dans le menu déroulant **[!UICONTROL Saisir le nom du champ]**. Sélectionnez cette valeur.

![Sélectionner l’attribution de la région](./images/user-guide/select_region_att.png)

Sélectionnez ensuite un opérateur.

![opérateur de région](./images/user-guide/region_operators.png)

Pour finir, saisissez le code pays dans le menu déroulant **[!UICONTROL Saisir la valeur du champ]**.

>[!NOTE]
>
>Les codes pays se composent de deux caractères. Vous trouverez ci-contre une liste complète de ces codes [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![région](./images/user-guide/region-based.png)

### Période de formation {#training-window}

Pour vous assurer d’obtenir le modèle le plus précis possible, il est important de former votre modèle avec des données historiques qui représentent votre entreprise. Par défaut, le modèle est formé à l’aide de 2 trimestres (6 mois) de données d’événements de conversion. Sélectionnez le menu déroulant pour modifier la valeur par défaut. Vous pouvez opter pour une formation basée sur un à quatre trimestres de données (3 à 12 mois).

>[!NOTE]
>
>Une période de formation plus courte est plus réceptive aux tendances récentes, tandis qu’une période de formation plus longue crée un modèle plus robuste et est moins sensible aux tendances récentes.

![période de formation](./images/user-guide/training_window.png)

Une fois la fenêtre de formation sélectionnée, sélectionnez **[!UICONTROL Terminer]** dans le coin supérieur droit. Prévoyez un certain temps pour le traitement des données. Une fois cette opération terminée, une boîte de dialogue s’affiche, confirmant que la configuration de l’instance est terminée. Sélectionner **[!UICONTROL Ok]** pour être redirigé vers le **[!UICONTROL Instances de service]** où vous pouvez voir votre instance de service.

![configuration terminée](./images/user-guide/instance_setup_complete.png)

## Politiques de gouvernance

Une fois que vous avez parcouru le workflow pour créer une instance et envoyer la configuration du modèle, la variable [application des stratégies](/help/data-governance/enforcement/auto-enforcement.md) vérifie s’il existe des violations. Si une violation de stratégie se produit, une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs stratégies ont été violées. Cela permet de vous assurer que vos opérations de données et vos actions marketing dans Platform sont conformes aux politiques d’utilisation des données.

![fenêtre contextuelle affichant une violation de stratégie](./images/user-guide/policy-violation-popover-aai.png)

La fenêtre contextuelle fournit des informations spécifiques sur la violation. Vous pouvez résoudre ces violations par le biais de paramètres de stratégie et d’autres mesures qui ne sont pas directement liés au workflow de configuration. Par exemple, vous pouvez modifier les étiquettes afin que certains champs soient autorisés à être utilisés à des fins de science des données. Vous pouvez également modifier la configuration de modèle elle-même afin qu’elle n’utilise rien avec un libellé. Consultez la documentation pour en savoir plus sur la configuration [policies](/help/data-governance/policies/overview.md).

## Contrôle d’accès basé sur attribut

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée uniquement.

[Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.](../../../help/access-control/abac/overview.md) Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma d’un modèle de données d’expérience (XDM) avec des libellés définissant l’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD) et aux informations d’identification personnelle (PII) sur l’ensemble des workflows et ressources de Platform. Les administrateurs peuvent définir des rôles utilisateur ayant accès uniquement à des champs et données spécifiques qui correspondent à ces champs.

En raison du contrôle d’accès basé sur les attributs, certains champs et certaines fonctionnalités peuvent avoir un accès limité et ne pas être disponibles pour certaines instances de service Attribution AI. Par exemple, &quot;Identité&quot;, &quot;Définition de score&quot; et &quot;Cloner&quot;.

En haut de l’espace de travail Attribution AI **page insights**, les détails affichés dans la barre latérale ont un accès restreint.

![Espace de travail Attribution AI avec les champs de schéma restreints mis en surbrillance.](./images/user-guide/access-restricted.png)

Si vous sélectionnez des jeux de données avec des schémas restreints sur la variable **[!UICONTROL Workflow Créer une instance]** , un signe d’avertissement s’affiche en regard du nom du jeu de données avec le message : [!UICONTROL Les informations restreintes sont exclues].

![Espace de travail Attribution AI avec les champs de jeu de données restreint mis en surbrillance.](./images/user-guide/restricted-info-excluded.png)

Lorsque vous prévisualisez des jeux de données avec un schéma limité sur l’objet **[!UICONTROL Workflow Créer une instance]** , un avertissement s’affiche pour vous informer que [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans l’aperçu du jeu de données.]

![L’espace de travail Attribution AI avec les résultats des champs de schéma prévisualisés restreints est mis en surbrillance.](./images/user-guide/restricted-dataset-preview.png)

Après avoir créé une instance contenant des informations restreintes, passez à la **[!UICONTROL Définition d’un objectif]** , un avertissement s’affiche en haut de l’écran : [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans la configuration.]

![Espace de travail Attribution AI avec les champs restreints des résultats de l’instance mis en surbrillance.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une instance de service dans Attribution AI. Une fois que la notation avec l’instance est terminée (compter jusqu’à 24 heures), vous êtes prêt à [découvrir les insights d’Attribution AI](./discover-insights.md). De plus, si vous souhaitez télécharger les résultats de la notation, rendez-vous sur la page [téléchargement de scores](./download-scores.md) documentation.

## Ressources supplémentaires

La vidéo suivante présente un processus de bout en bout pour créer une instance dans Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
