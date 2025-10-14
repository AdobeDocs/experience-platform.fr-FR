---
keywords: Experience Platform;guide de l’utilisateur;attribution ai;rubriques populaires;région
feature: Attribution AI
title: Guide de l’interface utilisateur d’Attribution AI
description: Ce document sert de guide pour interagir avec l’IA dédiée à l’attribution dans l’interface utilisateur des services intelligents.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 29%

---

# Guide de l’interface utilisateur d’Attribution AI

Dans le cadre d’Intelligent Services, Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à l’IA dédiée à l’attribution, les professionnels du marketing peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase des parcours des clients.

Ce document sert de guide pour interagir avec l’IA dédiée à l’attribution dans l’interface utilisateur des services intelligents.

## Créer modèle

Dans l’interface utilisateur de [!DNL Adobe Experience Platform], sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche les services intelligents Adobe disponibles. Dans le conteneur d’IA dédiée à l’attribution, sélectionnez **[!UICONTROL Ouvrir]**.

![Accès à votre modèle](./images/user-guide/open_Attribution_ai.png)

La page de service d’Attribution AI s’affiche. Cette page répertorie les modèles de service de l’IA dédiée à l’attribution et affiche des informations à leur sujet, notamment le nom du modèle, les événements de conversion, la fréquence d’exécution du modèle et le statut de la dernière mise à jour.

La mesure **[!UICONTROL Nombre total d’événements de conversion notés]** se trouve dans le coin inférieur droit du conteneur **[!UICONTROL Créer un modèle]**. Cette mesure effectue le suivi du nombre total d’événements de conversion notés par l’IA dédiée à l’attribution pour l’année civile en cours, y compris tous les environnements de sandbox et tous les modèles de service supprimés.

![nombre total de conversions](./images/user-guide/total_conversions.png)

Les modèles de service peuvent être modifiés, clonés et supprimés à l’aide des commandes situées dans la partie droite de l’interface utilisateur. Pour afficher ces commandes, sélectionnez un modèle parmi vos **[!UICONTROL modèles de service]** existants. Les contrôles contiennent les informations suivantes :

- **[!UICONTROL Modifier]** : la sélection de **[!UICONTROL Modifier]** permet de modifier un modèle de service existant. Vous pouvez modifier le nom, la description, le statut, la fréquence de notation du modèle et les colonnes de jeux de données de notation supplémentaires.
- **[!UICONTROL Cloner]** : la sélection de l’option **[!UICONTROL Cloner]** permet de copier le modèle de service sélectionné. Vous pouvez ensuite modifier le workflow pour apporter des ajustements mineurs et le renommer en tant que nouveau modèle.
- **[!UICONTROL Supprimer]** : vous pouvez supprimer un modèle de service, y compris les exécutions historiques. Le jeu de données de sortie correspondant sera supprimé d’Experience Platform. Toutefois, les scores synchronisés avec le profil client en temps réel ne sont pas supprimés.
- **[!UICONTROL Source de données]** : lien vers le jeu de données utilisé. Si plusieurs jeux de données sont utilisés par l’IA dédiée à l’attribution, « Multiple » suivi du nombre de jeux de données s’affiche. Lorsque vous sélectionnez le lien hypertexte, la fenêtre contextuelle d’aperçu des jeux de données s’affiche.
- **[!UICONTROL Détails de la dernière exécution]** : ils s’affichent uniquement lorsqu’une exécution échoue. Des informations sur les raisons de l’échec de l’exécution, telles que des codes d’erreur, sont affichées ici.

![Volet latéral](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL Événements de conversion]** : aperçu rapide des événements de conversion configurés pour ce modèle.
- **[!UICONTROL Intervalle de recherche en amont]** : période que vous avez définie, indiquant le nombre de jours précédant l’inclusion des points de contact de l’événement de conversion.
- **[!UICONTROL Points de contact]** : liste de tous les points de contact que vous avez définis lors de la création de ce modèle.

![](./images/user-guide/side_panel_2.png)

Sélectionnez **[!UICONTROL Créer un modèle]** pour commencer.

![Créer un modèle](./images/user-guide/landing_page.png)

Ensuite, la page de configuration d’Attribution AI s’affiche et vous permet de fournir un nom et une description facultative de votre modèle de service.

![nommer un modèle](./images/user-guide/naming_instance.png)

## Sélectionner les données {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

Par défaut, l’IA dédiée à l’attribution peut utiliser les données Adobe Analytics, d’événement d’expérience et d’événement d’expérience client pour calculer les scores d’attribution. Lors de la sélection d’un jeu de données, seuls les jeux compatibles avec l’IA dédiée à l’attribution sont répertoriés. Pour sélectionner un jeu de données, sélectionnez le symbole (**+**) en regard du nom du jeu de données ou cochez la case pour ajouter plusieurs jeux de données à la fois. Vous pouvez également utiliser l’option de recherche pour trouver rapidement les jeux de données qui vous intéressent.

Après avoir sélectionné les jeux de données que vous souhaitez utiliser, cliquez sur le bouton **[!UICONTROL Ajouter]** pour ajouter les jeux de données au volet d’aperçu du jeu de données.

![Sélectionner des jeux de données](./images/user-guide/select-datasets.png)

Si vous sélectionnez l’icône d’informations ![icône d’informations](/help/images/icons/info.png) en regard d’un jeu de données, la fenêtre contextuelle d’aperçu du jeu de données s’ouvre.

![Sélectionner et rechercher un jeu de données](./images/user-guide/dataset-preview.png)

L’aperçu du jeu de données contient des données telles que l’heure de la dernière mise à jour, le schéma source et un aperçu des dix premières colonnes.

Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer les brouillons tout au long du workflow. Vous pouvez également enregistrer les configurations de modèle de brouillon et passer à l’étape suivante du workflow. Utilisez **[!UICONTROL Enregistrer et continuer]** pour créer et enregistrer des brouillons lors des configurations de modèle. La fonction vous permet de créer et d&#39;enregistrer des brouillons de la configuration du modèle. Elle est particulièrement utile lorsque vous devez définir de nombreux champs dans le processus de configuration.

![Le workflow Créer de l’onglet IA dédiée à l’attribution des services de science des données avec Enregistrer et Enregistrer et continuer en surbrillance.](./images/user-guide/aai-save-save-&-exit.png)

### Exhaustivité du jeu de données {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

Dans l’aperçu du jeu de données se trouve une valeur de pourcentage d’exhaustivité du jeu de données. Cette valeur fournit un instantané rapide du nombre de colonnes vides/nulles de votre jeu de données. Si un jeu de données contient de nombreuses valeurs manquantes et que ces valeurs sont capturées ailleurs, il est vivement recommandé d’inclure le jeu de données contenant les valeurs manquantes.

>[!NOTE]
>
>L’exhaustivité des jeux de données est calculée à l’aide de la fenêtre d’entraînement maximale pour Attribution AI (un an). Cela signifie que les données de plus d’un an ne sont pas prises en compte lors de l’affichage de la valeur d’exhaustivité de votre jeu de données.

![&#x200B; Exhaustivité du jeu de données &#x200B;](./images/user-guide/dataset-completeness.png)

### Sélectionner une identité {#identity}

Vous pouvez désormais joindre plusieurs jeux de données les uns aux autres en fonction du mappage d’identité (champ). Vous devez sélectionner un type d’identité (également appelé « espace de noms d’identité ») et une valeur d’identité dans cet espace de noms. Si vous avez affecté plusieurs champs en tant qu’identité dans votre schéma sous le même espace de noms, toutes les valeurs d’identité affectées apparaissent dans la liste déroulante d’identités précédée de l’espace de noms, par exemple `EMAIL (personalEmail.address)` ou `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>Le même type d’identité (espace de noms) doit être utilisé pour chaque jeu de données que vous sélectionnez. Une coche verte apparaît en regard du type d’identité dans la colonne d’identité, indiquant que les jeux de données sont compatibles. Par exemple, lors de l’utilisation de l’espace de noms Téléphone et `mobilePhone.number` comme identifiant, tous les identifiants des jeux de données restants doivent contenir et utiliser l’espace de noms Téléphone .

Pour sélectionner une identité, sélectionnez la valeur soulignée située dans la colonne d’identité. La fenêtre contextuelle de sélection d’une identité s’affiche.

![sélectionner le même espace de noms](./images/user-guide/aai-identity-map-save-and-exit.png)

Dans le cas où plusieurs identités sont disponibles dans un espace de noms, veillez à sélectionner le champ d’identité approprié à votre cas d’utilisation. Par exemple, deux identités d’e-mail sont disponibles dans l’espace de noms e-mail, une adresse e-mail professionnelle et une adresse e-mail personnelle. Selon le cas d’utilisation, un e-mail personnel est plus susceptible d’être renseigné et plus utile dans les prédictions individuelles. Cela signifie que vous devez sélectionner `EMAIL (personalEmail.address)` comme identité.

![Clé du jeu de données non sélectionnée](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> S’il n’existe aucun type d’identité valide (espace de noms) pour un jeu de données, vous devez définir une identité principale et l’affecter à un espace de noms d’identité à l’aide de l’[éditeur de schéma](../../xdm/schema/composition.md#identity). Pour en savoir plus sur les espaces de noms et les identités, consultez la documentation [&#x200B; Espaces de noms du service d’identités &#x200B;](../../identity-service/features/namespaces.md).

## Mappage des champs de canal média et de campagne {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

Une fois la sélection et l’ajout des jeux de données terminés, l’étape de configuration **Map** s’affiche. L’IA dédiée à l’attribution nécessite de mapper le champ Canal multimédia pour chaque jeu de données que vous avez sélectionné à l’étape précédente. En effet, sans mappage du canal média entre les jeux de données, les informations dérivées de l’IA dédiée à l’attribution peuvent ne pas s’afficher correctement, ce qui rend la page d’informations difficile à interpréter. Bien que seul le canal média soit requis, il est vivement recommandé de mapper certains des champs facultatifs tels que l’action du média, le nom de la campagne, le groupe de la campagne et la balise de la campagne. Cela permet à l’IA dédiée à l’attribution de fournir des informations plus claires et des résultats optimaux.

![mappage](./images/user-guide/mapping-save-&-exit.png)

## Définition des événements {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

Il existe trois types différents de données d’entrée utilisées pour définir les événements :

- **Événements de conversion :** objectifs professionnels qui identifient l’impact des activités marketing, comme les commandes e-commerce, les achats en magasin et les visites sur le site web.
- **Intervalle de recherche en amont :** fournit une période indiquant le nombre de jours avant l’inclusion des points de contact de l’événement de conversion.
- **Points de contact :** événements marketing au niveau des bénéficiaires, des individus ou des cookies utilisés pour évaluer l’impact numérique ou basé sur les recettes des conversions.

### Définition des événements de conversion {#define-conversion-events}

Pour définir un événement de conversion, vous devez donner un nom à l’événement et sélectionner le type d’événement en sélectionnant le jeu de données et le champ dans le menu déroulant **Sélectionner un jeu de données et un champ**.

![menu déroulant oui](./images/user-guide/define-conversion-events.png)

Une fois qu’un événement est sélectionné, un nouveau menu déroulant s’affiche à sa droite. Le second menu déroulant est utilisé pour fournir davantage de contexte à votre événement grâce à l’utilisation des opérations. Pour cet événement de conversion, l’opération par défaut *exists* est utilisée.

>[!NOTE]
>
>Une chaîne sous votre *nom de conversion* est mise à jour au fur et à mesure que vous définissez votre événement.

![aucun menu déroulant](./images/user-guide/conversion_event_1.png)

Vous pouvez ensuite sélectionner un jeu de données combiné qui est généré en combinant tous les jeux de données d’entrée de l’étape précédente. Vous pouvez également sélectionner une colonne en fonction de jeux de données individuels dans le menu déroulant **Sélectionner un jeu de données et un champ**.

Les boutons **[!UICONTROL Ajouter un événement]** et **[!UICONTROL Ajouter un groupe]** permettent de définir plus précisément votre conversion. En fonction de la conversion que vous définissez, vous devrez peut-être utiliser les boutons **[!UICONTROL Ajouter un événement]** et **[!UICONTROL Ajouter un groupe]** pour fournir davantage de contexte.

![ajouter un événement](./images/user-guide/add_event.png)

Sélectionnez **[!UICONTROL Ajouter un événement]** pour créer des champs supplémentaires qui peuvent être remplis en utilisant la même méthode que celle décrite ci-dessus. Cela permet d’ajouter une instruction AND à la définition de chaîne sous le nom de la conversion. Sélectionnez la **x** pour supprimer un événement qui a été ajouté.

![menu ajouter un événement](./images/user-guide/add_event_result.png)

Sélectionner **[!UICONTROL Ajouter un groupe]** permet de créer des champs supplémentaires distincts du champ d’origine. Avec l’ajout de groupes, un bouton bleu *Et* apparaît. Si vous sélectionnez **Et**, vous avez la possibilité de modifier le paramètre pour qu’il contienne « Ou ». « Ou » est utilisé pour définir plusieurs chemins de conversion performants. « Et » prolonge le chemin de conversion pour inclure des conditions supplémentaires.

![utilisation de et/ou](./images/user-guide/and_or.png)

Si vous avez besoin de plusieurs conversions, sélectionnez **Ajouter une conversion** pour créer une carte de conversion. Vous pouvez répéter la procédure ci-dessus pour définir plusieurs conversions.

![ajouter une conversion](./images/user-guide/add_conversion.png)

### Définition de l’intervalle de recherche en amont {#lookback-window}

Une fois la conversion définie, vous devez confirmer votre intervalle de recherche en amont. À l’aide des touches fléchées ou en sélectionnant la valeur par défaut (56), indiquez le nombre de jours précédant l’événement de conversion depuis lequel vous souhaitez inclure des points de contact. Les points de contact sont définis à l’étape suivante.

![recherche en amont](./images/user-guide/lookback_window.png)

### Définition des points de contact

La définition des points de contact suit un workflow similaire à celui de la [définition des conversions](#define-conversion-events). Dans un premier temps, vous devez nommer votre point de contact et sélectionner une valeur de point de contact dans le menu déroulant *Saisir le nom du champ*. Une fois sélectionné, le menu déroulant de l’opérateur s’affiche avec la valeur par défaut « exists ». Sélectionnez la liste déroulante pour afficher la liste des opérateurs.

![opérateurs](./images/user-guide/operators.png)

Pour ce point de contact, sélectionnez **equals**.

![étape 1](./images/user-guide/touchpoint_step1.png)

Une fois qu’un opérateur pour un point de contact est sélectionné, *Saisir la valeur du champ* est mis à disposition. Les valeurs du menu déroulant pour *Saisir la valeur du champ* reposent sur l’opérateur et la valeur du point de contact que vous avez sélectionnés précédemment. Si une valeur n’apparaît pas dans le menu déroulant, vous pouvez la saisir manuellement. Sélectionnez la liste déroulante, puis sélectionnez **CLIQUER**.

>[!NOTE]
>
>Les opérateurs « existe » et « n’existe pas » ne sont pas associés à des valeurs de champ.

![menu déroulant du point de contact](./images/user-guide/touchpoint_dropdown.png)

Les boutons **Ajouter un événement** et **Ajouter un groupe** permettent de définir plus précisément votre point de contact. En raison de la nature complexe des points de contact, il n’est pas rare d’avoir plusieurs événements et groupes pour un seul point de contact.

Lorsque cette option est sélectionnée, **Ajouter un événement** permet d’ajouter des champs supplémentaires. sélectionnez la **x** pour supprimer un événement qui a été ajouté.

![ajouter un événement](./images/user-guide/touchpoint_add_event.png)

Sélectionner **Ajouter un groupe** permet de créer des champs supplémentaires distincts du champ d’origine. Avec l’ajout de groupes, un bouton bleu *Et* apparaît. Sélectionnez **Et** pour modifier le paramètre, le nouveau paramètre « Ou » est utilisé pour définir plusieurs chemins d’accès réussis. Ce point de contact particulier n’a qu’un seul chemin performant. Par conséquent, « Ou » n’est pas nécessaire.

![présentation du point de contact](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Utilisez la chaîne sous *Nom du point de contact* pour obtenir un aperçu rapide de votre point de contact. Notez que la chaîne correspond au nom du point de contact.

![](./images/user-guide/touchpoint_string.png)

Vous pouvez ajouter des points de contact supplémentaires en sélectionnant **Ajouter un point de contact** et en répétant le processus ci-dessus.

![ajouter un point de contact](./images/user-guide/add_touchpoint.png)

Une fois que vous avez terminé de définir tous les points de contact nécessaires, faites défiler l’écran vers le haut et sélectionnez **Suivant** dans le coin supérieur droit pour passer à l’étape finale.

![définition terminée](./images/user-guide/define_event_save_and_exit.png)

## Configuration de la formation et de la notation avancées

La dernière page d’Attribution AI est la page **[!UICONTROL Avancé]** utilisée pour configurer la formation et la notation.

![nouvelles options d’ensemble de pages](./images/user-guide/advanced_settings_set_options.png)

### Planification de la formation

À l’aide du *planning*, vous pouvez sélectionner le jour et l’heure de la semaine où vous souhaitez que la notation soit effectuée.

Sélectionnez la liste déroulante sous *Fréquence de notation* pour effectuer une sélection entre les scores quotidien, hebdomadaire et mensuel. Ensuite, sélectionnez les jours de la semaine où vous souhaitez que la notation soit effectuée. Vous pouvez sélectionner plusieurs jours. La sélection du même jour la désélectionne à nouveau.

![Planification de la formation](./images/user-guide/schedule_training.png)

Pour modifier l’heure à laquelle vous souhaitez que la notation se produise, sélectionnez l’icône d’horloge. Dans la nouvelle fenêtre qui s’affiche, saisissez l’heure de la journée à laquelle vous souhaitez que la notation soit effectuée. Sélectionnez à l’extérieur du recouvrement pour le fermer.

>[!NOTE]
>
>Chaque processus de notation peut prendre jusqu’à 24 heures.

![icône de l’horloge](./images/user-guide/time_of_day.png)

### Colonnes supplémentaires du jeu de données de note (facultatif)

Par défaut, un jeu de données de note est créé pour chaque modèle de service dans un schéma standard. Vous pouvez choisir d’ajouter des colonnes supplémentaires en fonction de vos configurations Événement de conversion et Point de contact à la sortie du jeu de données de notation. Commencez par sélectionner des colonnes à partir de votre jeu de données d’entrée, puis faites-les glisser et déposez-les pour modifier l’ordre en maintenant le bouton gauche de la souris enfoncé sur l’icône hamburger.

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
>Les codes pays comportent deux caractères. Vous trouverez ci-contre une liste complète de ces codes [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![région](./images/user-guide/region-based.png)

### Période de formation {#training-window}

Pour vous assurer d’obtenir le modèle le plus précis possible, il est important de former votre modèle avec des données historiques qui représentent votre entreprise. Par défaut, le modèle est entraîné à l’aide de 2 trimestres (6 mois) de données d’événements de conversion. Sélectionnez le menu déroulant pour modifier la valeur par défaut. Vous pouvez opter pour une formation basée sur un à quatre trimestres de données (3 à 12 mois).

>[!NOTE]
>
>Un créneau de formation réduit est plus sensible aux tendances récentes, tandis qu’un créneau de formation plus étendu crée un modèle plus robuste qui est moins sensible aux tendances récentes.

![période de formation](./images/user-guide/training_window.png)

Une fois la fenêtre de formation sélectionnée, cliquez sur **[!UICONTROL Terminer]** dans le coin supérieur droit. Prévoyez un certain temps pour le traitement des données. Une fois cette opération terminée, une boîte de dialogue s’affiche, confirmant que la configuration de l’instance est terminée. Sélectionnez **[!UICONTROL Ok]** pour être redirigé vers la page **[!UICONTROL Instances de service]** où vous pouvez voir votre instance de service.

![configuration terminée](./images/user-guide/instance_setup_complete.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une instance de service dans Attribution AI. Une fois la notation de l’instance terminée (patientez jusqu’à 24 heures), vous êtes prêt à [découvrir les informations de l’IA dédiée à l’attribution](./discover-insights.md). De plus, si vous souhaitez télécharger vos résultats de notation, consultez la documentation [téléchargement des notes](./download-scores.md).

## Ressources supplémentaires

La vidéo suivante décrit un workflow de bout en bout pour la création d’une instance dans Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/36546?learn=on&quality=12&captions=fre_fr)
