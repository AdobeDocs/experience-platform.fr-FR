---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’interface utilisateur du créateur de segments
topic: ui guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '2745'
ht-degree: 57%

---


# [!DNL Segment Builder] guide de l&#39;utilisateur

[!DNL Adobe Experience Platform Segmentation Service] fournit une API RESTful et une interface utilisateur pour créer des définitions de segment à partir de [!DNL Real-time Customer Profile] données.

## Prise en main

Working with segment definitions requires an understanding of the various [!DNL Experience Platform] services involved with segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [!DNL Segmentation Service](../home.md): [!DNL Segmentation Service] vous permet de diviser les données stockées dans [!DNL Experience Platform] des rapports avec des individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits qui partagent des caractéristiques similaires et réagissent de la même manière aux stratégies marketing.
- [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [!DNL Identity Service](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et qui sont incorporées [!DNL Platform]dans.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Accès aux définitions de segment

To begin working with segment definitions in [!DNL Adobe Experience Platform], click **[!UICONTROL Segments]** in the left navigation. Pour afficher toutes les définitions de segment pour votre organisation, cliquez sur l’onglet *[!UICONTROL Parcourir]*. Cette vue contient des informations sur la définition de segment, y compris la méthode d’évaluation, la date de création et la date de dernière modification.

La méthode d’évaluation peut être soit par flux, soit par lot. Les segments par flux sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi.

Les segments par lot affichent des informations supplémentaires, indiquant à la fois la dernière date d’évaluation et la prochaine date d’évaluation du lot.

Cliquez sur **[!UICONTROL Créer un segment]** dans le coin supérieur droit pour ouvrir l’espace de travail du créateur de segments, où vous pouvez commencer à créer une définition de segment.

![](../images/segment-builder/segment-browse.png)

## [!DNL Segment Builder] espace de travail

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] des éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

![](../images/segment-builder/segment-builder.png)

## Blocs de création de définitions de segment

Les blocs de création de base des définitions de segment sont les **[!UICONTROL Attributs]** et les **[!UICONTROL Événements]**. En outre, les attributs et les événements contenus dans les **[!UICONTROL Audiences]** existantes peuvent également être utilisés comme éléments de nouvelles définitions.

You can see these building blocks in the *[!UICONTROL Fields]* section on the left side of the [!DNL Segment Builder] workspace. Les *[!UICONTROL champs]* contiennent un onglet pour chacun des blocs de création principaux : **[!UICONTROL Attributs]**, **[!UICONTROL Événements]** et **[!UICONTROL Audiences]**.

![](../images/segment-builder/segment-fields.png)

### Attributs

The **[!UICONTROL Attributes]** tab allows you to browse [!DNL Profile] attributes belonging to the [!DNL XDM Individual Profile] class. Chaque dossier peut être développé pour afficher des attributs supplémentaires, où chaque attribut est une mosaïque qui peut être glissée sur le canevas du créateur de règles au centre de l’espace de travail. Le [canevas du créateur de règles](#rule-builder-canvas) est abordé plus en détail dans la suite de ce guide.

![](../images/segment-builder/attributes.png)

### Événements

L’onglet **[!UICONTROL Événements]** vous permet de créer une audience basée sur des événements ou des actions qui ont eu lieu en utilisant des éléments de données [!DNL XDM ExperienceEvent] Vous pouvez également trouver les types d’événements dans l’onglet **[!UICONTROL Événements]**, qui sont une collection d’événements couramment utilisés pour vous permettre de créer vos segments plus rapidement.

In addition to being able to browse for [!DNL ExperienceEvent] elements, you can also search for Event Types. Event Types use the same coding logic as [!DNL ExperienceEvents], without requiring you to search through the [!DNL XDM ExperienceEvent] class looking for the correct event. For example, using the search bar to search &quot;cart&quot; returns the Event Types &quot;[!UICONTROL AddCart]&quot; and &quot;[!UICONTROL RemoveCart]&quot;, which are two very commonly used cart actions when building segment definitions.

Vous pouvez rechercher n’importe quel type de composant en tapant son nom dans la barre de recherche, qui utilise la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Les résultats de la recherche commencent à s’afficher au fur et à mesure que des mots entiers sont saisis. Par exemple, pour créer une règle basée sur le champ XDM `ExperienceEvent.commerce.productViews`, commencez à saisir « product views » dans le champ de recherche. Une fois le mot « product » saisi, les résultats de la recherche commencent à s’afficher. Chaque résultat inclut la hiérarchie d’objets à laquelle il appartient.

>[!NOTE]
>
>Les champs de schéma personnalisés définis par votre organisation peuvent mettre jusqu’à 24 heures pour s’afficher et être utilisables dans les règles de création.

You can then easily drag and drop [!DNL ExperienceEvents] and [!UICONTROL Event Types] into your segment definition.

![](../images/segment-builder/events-eventTypes.png)

Par défaut, seuls les champs de schéma renseignés de votre banque de données s’affichent. This includes [!UICONTROL Event Types]. If the [!UICONTROL Event Types] list is not visible, or you are only able to select &quot;[!UICONTROL Any]&quot; as an [!UICONTROL Event Type], click the gear icon next to *[!UICONTROL Fields]*, then select **[!UICONTROL Show full XDM schema]** under *[!UICONTROL Available Fields]*. Cliquez à nouveau sur l’icône en forme d’engrenage pour revenir à l’onglet *[!UICONTROL Champs]*. Vous devriez maintenant pouvoir afficher plusieurs types d’événements et champs de schéma, qu’ils contiennent des données ou non.

![](../images/segment-builder/show-populated.png)

### Audiences

L’onglet **[!UICONTROL Audiences]** répertorie toutes les audiences importées de sources externes, telles qu’Adobe Audience Manager, ainsi que les audiences créées dans [!DNL Experience Platform].

On the [!UICONTROL Audiences] tab, you can see all of the available sources as a group of folders. En cliquant dans ces dossiers, vous pouvez voir les sous-dossiers et les audiences disponibles. De plus, vous pouvez cliquer sur l’icône du dossier (comme indiqué dans l’image située à l’extrême droite) afin de visualiser la structure des dossiers (une coche indique le dossier dans lequel vous vous trouvez actuellement) et de parcourir facilement les dossiers en cliquant sur le nom d’un dossier dans l’arborescence.

Vous pouvez passer la souris sur l’option ⓘ située à côté d’une audience pour afficher des informations sur cette dernière, notamment son identifiant, sa description et la hiérarchie des dossiers permettant de la localiser.

![](../images/segment-builder/audience-folder-structure.png)

You can also search for [!UICONTROL Audiences] using the search bar, which utilizes [Lucene&#39;s search syntax](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Dans l’onglet *[!UICONTROL Audiences]*, si vous sélectionnez un dossier de niveau supérieur, la barre de recherche s’affiche et vous permet de faire une recherche dans ce dossier. Les résultats de la recherche ne commencent à s’afficher que lorsque des mots entiers sont saisis. For example, to find an [!UICONTROL Audience] named `Online Shoppers`, start typing &quot;Online&quot; in the search bar. Une fois que le mot « Online » a été complètement saisi, les résultats de la recherche contenant ce mot apparaissent.

## Canevas du créateur de règles {#rule-builder-canvas}

Une définition de segment est un ensemble de règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible. These rules are created using the *[!UICONTROL rule builder canvas]*, located in the center of [!DNL Segment Builder].

Pour ajouter une nouvelle règle à votre définition de segment, faites glisser une mosaïque depuis l’onglet *[!UICONTROL Champs]* et déposez-la sur le canevas du créateur de règles. Des options spécifiques au contexte vous seront ensuite présentées en fonction du type de données ajouté. Available data types include: strings, dates, [!DNL ExperienceEvents], [!UICONTROL Event Types], and [!UICONTROL Audiences].

![](../images/segment-builder/rule-builder-canvas.png)

### Ajout d’audiences

Vous pouvez faire glisser une audience depuis l’onglet *[!UICONTROL Audience]* sur le canevas du créateur de règles pour référencer l’appartenance à l’audience dans la nouvelle définition de segment. Cela vous permet d’inclure ou d’exclure l’appartenance à une audience en tant qu’attribut dans la nouvelle règle de segmentation.

For [!DNL Platform] audiences created using [!DNL Segment Builder], you are given the option to convert the audience into the set of rules that were used in the segment definition for that audience. Cette conversion effectue une copie de la logique de règle, qui peut ensuite être modifiée sans affecter la définition de segment d’origine. Assurez-vous d’avoir enregistré les dernières modifications apportées à votre définition de segment avant de la convertir en logique de règle.

>[!NOTE]
>
>Lors de l’ajout d’une audience provenant d’une source externe, seule l’appartenance à l’audience est référencée. Vous ne pouvez pas convertir l’audience en règles. Par conséquent, les règles utilisées pour créer l’audience originale ne peuvent pas être modifiées dans la nouvelle définition de segment.

![](../images/segment-builder/add-audience-to-segment.png)

Si des conflits surviennent lors de la conversion d’audiences en règles, [!DNL Segment Builder] tentera de préserver les options existantes au mieux de ses capacités.

### vue de code

Vous pouvez également vue une version basée sur un code d’une règle créée dans le [!DNL Segment Builder]. Une fois que vous avez créé votre règle dans le canevas du créateur de règles, vous pouvez sélectionner vue **[!UICONTROL de]** code pour voir votre segment comme étant PQL.

![](../images/segment-builder/code-view.png)

La vue de code fournit un bouton qui vous permet de copier la valeur du segment à utiliser dans les appels d’API. Pour obtenir la dernière version du segment, veillez à enregistrer vos dernières modifications dans le segment.

![](../images/segment-builder/copy-code.png)

## Conteneurs

Les règles de segmentation sont évaluées dans l’ordre dans lequel elles sont répertoriées. Les conteneurs permettent de contrôler l’ordre d’exécution grâce à l’utilisation de requêtes imbriquées.

Une fois que vous avez ajouté au moins une mosaïque au canevas du créateur de règles, vous pouvez commencer à ajouter des conteneurs. Pour créer un nouveau conteneur, cliquez sur les points de suspension (...) dans le coin supérieur droit de la mosaïque, puis sur **[!UICONTROL Ajouter un conteneur]**.

![](../images/segment-builder/add-container.png)

Un nouveau conteneur apparaît comme la descendance du premier conteneur, mais vous pouvez réorganiser la hiérarchie en faisant glisser et en déplaçant les conteneurs. The default behavior of a container is to &quot;[!UICONTROL Include]&quot; the attribute, event, or audience provided. You can set the rule to &quot;[!UICONTROL Exclude]&quot; profiles that match the container criteria by clicking **[!UICONTROL Include]** in the top-left corner of the tile and selecting &quot;[!UICONTROL Exclude]&quot;.

Un conteneur enfant peut également être extrait et ajouté en ligne au conteneur parent en cliquant sur « Extraire le conteneur » dans le conteneur enfant. Cliquez sur les points de suspension (...) dans le coin supérieur droit du conteneur enfant pour accéder à cette option.

![](../images/segment-builder/include-exclude.png)

Une fois que vous avez cliqué sur **[!UICONTROL Extraire le conteneur]**, le conteneur enfant est supprimé et les critères apparaissent en ligne.

>[!NOTE]
>
>Lorsque vous extrayez des conteneurs, veillez à ce que la logique continue de correspondre à la définition de segment souhaitée.

![](../images/segment-builder/unwrapped-container-inline.png)

## Stratégies de fusion

[!DNL Experience Platform] permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create a profile.

Vous pouvez sélectionner une stratégie de fusion qui correspond à votre objectif marketing pour cette audience ou utiliser la stratégie de fusion par défaut fournie par [!DNL Platform]. Vous pouvez créer plusieurs stratégies de fusion propres à votre organisation, y compris créer votre propre stratégie de fusion par défaut. Pour obtenir des instructions détaillées sur la création de stratégies de fusion pour votre organisation, consultez le tutoriel sur l’[utilisation des stratégies de fusion à l’aide de l’interface utilisateur](../../profile/ui/merge-policies.md).

Pour sélectionner une stratégie de fusion pour votre définition de segment, cliquez sur l’icône en forme d’engrenage dans l’onglet *[!UICONTROL Champs]*, puis utilisez le *menu déroulant Stratégie de fusion *pour sélectionner la stratégie de fusion à utiliser.

![](../images/segment-builder/merge-policy-selector.png)

## Propriétés du segment

Lors de la création d’une définition de segment, la section *[!UICONTROL Propriétés du segment]* située dans la partie droite de l’espace de travail affiche une estimation de la taille du segment obtenu, ce qui vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même.

La section *[!UICONTROL Propriétés du segment]* vous permet également de spécifier des informations importantes sur votre définition de segment, y compris son *[!UICONTROL nom]* et sa *[!UICONTROL description]*. Les noms des définitions de segment sont utilisés pour identifier votre segment parmi ceux définis par votre organisation et doivent donc être descriptifs, concis et uniques.

Au fur et à mesure que vous continuez à créer votre définition de segment, vous pouvez visualiser un aperçu paginé de l’audience en sélectionnant **[!UICONTROL Afficher les profils]**.

![](../images/segment-builder/segment-properties.png)

>[!NOTE]
>
>Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

## Activation de la segmentation planifiée {#enable-scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). Evaluation means moving [!DNL Real-time Customer Profile] data through segment definitions in order to produce corresponding audiences. Once created, the audiences are saved and stored so that they can be exported using [!DNL Experience Platform] APIs.

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet *[!UICONTROL Parcourir]* dans **[!UICONTROL Segments]** et activez l’option **[!UICONTROL Évaluer tous les segments]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Segmentation par flux {#streaming-segmentation}

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, le client doit activer la segmentation planifiée pour l’entreprise. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à [la section précédente de ce guide d’utilisation](#enable-scheduled-segmentation).

Une requête sera automatiquement évaluée avec la segmentation en flux continu si elle répond à l’un des critères suivants :

| Type de requête | Détails | Exemple |
| ---------- | ------- | ------- |
| Accès entrant | Toute définition de segment faisant référence à un seul événement entrant sans restriction de temps. | ![](../images/segment-builder/incoming-hit.png) |
| Accès entrant dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant **au cours des sept derniers jours**. | ![](../images/segment-builder/relative-hit-success.png) |
| Accès entrant faisant référence à un profil | Toute définition de segment faisant référence à un seul événement entrant, sans restriction de temps, et à un ou plusieurs attributs de profil. | ![](../images/segment-builder/profile-hit.png) |
| Accès entrant faisant référence à un profil dans une fenêtre de temps relative | Toute définition de segment faisant référence à un seul événement entrant et à un ou plusieurs attributs de profil, **au cours des sept derniers jours**. | ![](../images/segment-builder/profile-relative-success.png) |
| Plusieurs événements faisant référence à un profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | ![](../images/segment-builder/event-history-success.png) |

La section suivante liste des exemples de définition de segment qui **ne seront pas** activés pour la segmentation en flux continu.

| Type de requête | Détails |
| ---------- | ------- | 
| Accès entrant dans une fenêtre de temps relative | Si la définition de segment fait référence à un événement entrant **qui ne se trouve pas** dans la **dernière période** de sept jours. Par exemple, au cours des deux **dernières semaines**. | ![](../images/segment-builder/relative-hit-failure.png) |
| Accès entrant faisant référence à un profil dans une fenêtre relative | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>événement entrant **non** compris dans la **dernière période** de sept jours.</li><li>Définition de segment qui inclut [!DNL Adobe Audience Manager (AAM)] des segments ou des caractéristiques.</li></ul> | ![](../images/segment-builder/profile-relative-failure.png) |
| Plusieurs événements faisant référence à un profil | Les options suivantes **ne prennent pas** en charge la segmentation en flux continu :<ul><li>événement qui **ne se produit pas** au cours **des dernières 24 heures**.</li><li>Définition de segment qui comprend des segments ou des caractéristiques d’Adobe Audience Manager (AAM).</li></ul> | ![](../images/segment-builder/event-history-failure.png) |
| requêtes multientité | Les requêtes multientités **ne sont pas** prises en charge dans leur ensemble par la segmentation en flux continu. |  |

En outre, certaines directives s’appliquent lors de la segmentation en flux continu :

| Type de requête | Ligne directrice |
| ---------- | -------- |
| requête événement unique | La fenêtre de rétrospective est limitée à **sept jours**. |
| Requête avec historique des événements | <ul><li>La fenêtre de rétrospective est limitée à **un jour**.</li><li>Une condition d’ordre temporel strict **doit** exister entre les événements.</li><li>Seules les commandes de temps simples (avant et après) entre les événements sont autorisées.</li><li>Les événements individuels **ne peuvent** être annulés. Cependant, toute la requête **peut** être annulée.</li></ul> |

### Surveillance de la segmentation en flux continu

Après avoir créé un segment compatible avec la diffusion en continu, vous pouvez contrôler les détails de ce segment.

![](../images/segment-builder/monitoring-streaming-segment.png)

Plus précisément, des détails sur la taille ** totale des audiences qualifiées sont affichés. Si une tâche a été exécutée au cours des 24 dernières heures, la taille **** totale de l’Audience de la tâche s’affiche, en plus d’un graphique linéaire pour l’audience ajoutée. Sinon, la taille **** estimée de l’Audience s’affiche, en plus d’une ligne de tendance de visualisation.

![](../images/segment-builder/monitoring-streaming-segment-graph.png)

Pour plus d’informations sur l’évaluation du dernier segment, cliquez sur la bulle d’informations.

![](../images/segment-builder/info-bubble.png)

### Démo vidéo de segmentation en flux continu

La vidéo suivante est destinée à vous aider à comprendre la segmentation en flux continu. Il présente un exemple d’expérience client suivie d’une visite rapide des principales fonctionnalités de l’ [!DNL Platform] interface.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Violations de stratégie DULE

>[!NOTE]
>
>Les violations de stratégie DULE ne s’appliquent que si vous créez un segment qui a été affecté à une destination.

Once you are done creating your segment, the segment will be analyzed by [!DNL Data Governance] to ensure there are no policy violations within the segment. Pour plus d’informations sur DULE et sur les violations de stratégie, reportez-vous à la [présentation des libellés d’utilisation des données](../../data-governance/labels/overview.md).

![](../images/segment-builder/segment-dule-policy-violations.png)

## Étapes suivantes and additional resources {#next-steps}

Segment Builder provides a rich workflow allowing you to isolate marketable audiences from [!DNL Real-time Customer Profile] data. Après avoir lu ce guide, vous devriez maintenant pouvoir :

- créer des définitions de segment en utilisant une combinaison d’attributs, d’événements et d’audiences existants comme blocs de création ;
- utiliser les conteneurs et les canevas du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation ;
- visualiser les estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins ;
- activer toutes les définitions de segment pour la segmentation planifiée ;
- activer des définitions de segment spécifiques pour la segmentation par flux.

Pour en savoir plus [!DNL Segmentation Service], veuillez continuer à lire la documentation et compléter votre apprentissage en regardant les vidéos ci-dessous. For step-by-step instructions on working with [!DNL Segmentation Service] using the [!DNL Segmentation Service] API, see the [creating audience segments using APIs](../tutorials/create-a-segment.md) tutorial.

>[!WARNING]
>
> L’ [!DNL Platform] interface utilisateur affichée dans les vidéos suivantes est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

**Création d’un segment:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Créez un segment dynamique :**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)
