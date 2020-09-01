---
keywords: Experience Platform;home;popular topics;segment;Segment;segment builder;Segment builder
solution: Experience Platform
title: Guide de l’utilisateur du créateur de segments de service de segmentation
topic: ui guide
description: 'Le créateur de segments offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. '
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 58%

---


# [!DNL Segment Builder] guide de l&#39;utilisateur

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] des éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

![](../images/ui/segment-builder/segment-builder.png)

## Blocs de création de définitions de segment

Les blocs de création de base des définitions de segment sont les **[!UICONTROL Attributs]** et les **[!UICONTROL Événements]**. En outre, les attributs et les événements contenus dans les **[!UICONTROL Audiences]** existantes peuvent également être utilisés comme éléments de nouvelles définitions.

You can see these building blocks in the **[!UICONTROL Fields]** section on the left side of the [!DNL Segment Builder] workspace. Les **[!UICONTROL champs]** contiennent un onglet pour chacun des blocs de création principaux : **[!UICONTROL Attributs]**, **[!UICONTROL Événements]** et **[!UICONTROL Audiences]**.

![](../images/ui/segment-builder/segment-fields.png)

### Attributs

The **[!UICONTROL Attributes]** tab allows you to browse [!DNL Profile] attributes belonging to the [!DNL XDM Individual Profile] class. Chaque dossier peut être développé pour afficher des attributs supplémentaires, où chaque attribut est une mosaïque qui peut être glissée sur le canevas du créateur de règles au centre de l’espace de travail. Le [canevas du créateur de règles](#rule-builder-canvas) est abordé plus en détail dans la suite de ce guide.

![](../images/ui/segment-builder/attributes.png)

### Événements

L’onglet **[!UICONTROL Événements]** vous permet de créer une audience basée sur des événements ou des actions qui ont eu lieu en utilisant des éléments de données [!DNL XDM ExperienceEvent] Vous pouvez également trouver les types d’événements dans l’onglet **[!UICONTROL Événements]**, qui sont une collection d’événements couramment utilisés pour vous permettre de créer vos segments plus rapidement.

In addition to being able to browse for [!DNL ExperienceEvent] elements, you can also search for Event Types. Event Types use the same coding logic as [!DNL ExperienceEvents], without requiring you to search through the [!DNL XDM ExperienceEvent] class looking for the correct event. For example, using the search bar to search &quot;cart&quot; returns the Event Types &quot;[!UICONTROL AddCart]&quot; and &quot;[!UICONTROL RemoveCart]&quot;, which are two very commonly used cart actions when building segment definitions.

Vous pouvez rechercher n’importe quel type de composant en tapant son nom dans la barre de recherche, qui utilise la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Les résultats de la recherche commencent à s’afficher au fur et à mesure que des mots entiers sont saisis. Par exemple, pour créer une règle basée sur le champ XDM `ExperienceEvent.commerce.productViews`, commencez à saisir « product views » dans le champ de recherche. Une fois le mot « product » saisi, les résultats de la recherche commencent à s’afficher. Chaque résultat inclut la hiérarchie d’objets à laquelle il appartient.

>[!NOTE]
>
>Les champs de schéma personnalisés définis par votre organisation peuvent mettre jusqu’à 24 heures pour s’afficher et être utilisables dans les règles de création.

You can then easily drag and drop [!DNL ExperienceEvents] and [!UICONTROL Event Types] into your segment definition.

![](../images/ui/segment-builder/events-eventTypes.png)

Par défaut, seuls les champs de schéma renseignés de votre banque de données s’affichent. This includes [!UICONTROL Event Types]. If the [!UICONTROL Event Types] list is not visible, or you are only able to select &quot;[!UICONTROL Any]&quot; as an [!UICONTROL Event Type], select the gear icon next to **[!UICONTROL Fields]**, then select **[!UICONTROL Show full XDM schema]** under **[!UICONTROL Available Fields]**. Select the gear icon again to return to the **[!UICONTROL Fields]** tab and you should now be able to view multiple [!UICONTROL Event Types] and schema fields, regardless of whether they contain data or not.

![](../images/ui/segment-builder/show-populated.png)

### Audiences

L’onglet **[!UICONTROL Audiences]** répertorie toutes les audiences importées de sources externes, telles qu’Adobe Audience Manager, ainsi que les audiences créées dans [!DNL Experience Platform].

On the **[!UICONTROL Audiences]** tab, you can see all of the available sources as a group of folders. Lorsque vous sélectionnez les dossiers, les sous-dossiers et audiences disponibles s’affichent. De plus, vous pouvez sélectionner l’icône de dossier (comme illustré dans l’image à l’extrême droite) afin de vue de la structure de dossiers (une coche indique le dossier dans lequel vous vous trouvez actuellement) et de parcourir facilement les dossiers en sélectionnant le nom d’un dossier dans l’arborescence.

Vous pouvez passer la souris sur l’option ⓘ située à côté d’une audience pour afficher des informations sur cette dernière, notamment son identifiant, sa description et la hiérarchie des dossiers permettant de la localiser.

![](../images/ui/segment-builder/audience-folder-structure.png)

You can also search for [!UICONTROL Audiences] using the search bar, which utilizes [Lucene&#39;s search syntax](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Dans l’onglet **[!UICONTROL Audiences]**, si vous sélectionnez un dossier de niveau supérieur, la barre de recherche s’affiche et vous permet de faire une recherche dans ce dossier. Les résultats de la recherche ne commencent à s’afficher que lorsque des mots entiers sont saisis. For example, to find an [!UICONTROL Audience] named `Online Shoppers`, start typing &quot;Online&quot; in the search bar. Une fois que le mot « Online » a été complètement saisi, les résultats de la recherche contenant ce mot apparaissent.

## Canevas du créateur de règles {#rule-builder-canvas}

Une définition de segment est un ensemble de règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible. These rules are created using the rule builder canvas, located in the center of [!DNL Segment Builder].

Pour ajouter une nouvelle règle à votre définition de segment, faites glisser une mosaïque depuis l’onglet **[!UICONTROL Champs]** et déposez-la sur le canevas du créateur de règles. Des options spécifiques au contexte vous seront ensuite présentées en fonction du type de données ajouté. Available data types include: strings, dates, [!DNL ExperienceEvents], [!UICONTROL Event Types], and [!UICONTROL Audiences].

![](../images/ui/segment-builder/rule-builder-canvas.png)

### Ajout d’audiences

Vous pouvez faire glisser une audience depuis l’onglet **[!UICONTROL Audience]** sur le canevas du créateur de règles pour référencer l’appartenance à l’audience dans la nouvelle définition de segment. Cela vous permet d’inclure ou d’exclure l’appartenance à une audience en tant qu’attribut dans la nouvelle règle de segmentation.

For [!DNL Platform] audiences created using [!DNL Segment Builder], you are given the option to convert the audience into the set of rules that were used in the segment definition for that audience. Cette conversion effectue une copie de la logique de règle, qui peut ensuite être modifiée sans affecter la définition de segment d’origine. Assurez-vous d’avoir enregistré les dernières modifications apportées à votre définition de segment avant de la convertir en logique de règle.

>[!NOTE]
>
>Lors de l’ajout d’une audience provenant d’une source externe, seule l’appartenance à l’audience est référencée. Vous ne pouvez pas convertir l’audience en règles. Par conséquent, les règles utilisées pour créer l’audience originale ne peuvent pas être modifiées dans la nouvelle définition de segment.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Si des conflits surviennent lors de la conversion d’audiences en règles, [!DNL Segment Builder] tentera de préserver les options existantes au mieux de ses capacités.

### Vue de code

Vous pouvez également vue une version basée sur un code d’une règle créée dans le [!DNL Segment Builder]. Une fois que vous avez créé votre règle dans le canevas du créateur de règles, vous pouvez sélectionner vue **[!UICONTROL de]** code pour voir votre segment comme étant PQL.

![](../images/ui/segment-builder/code-view.png)

La vue de code fournit un bouton qui vous permet de copier la valeur du segment à utiliser dans les appels d’API. Pour obtenir la dernière version du segment, veillez à enregistrer vos dernières modifications dans le segment.

![](../images/ui/segment-builder/copy-code.png)

## Conteneurs

Les règles de segmentation sont évaluées dans l’ordre dans lequel elles sont répertoriées. Les conteneurs permettent de contrôler l’ordre d’exécution grâce à l’utilisation de requêtes imbriquées.

Une fois que vous avez ajouté au moins une mosaïque au canevas du créateur de règles, vous pouvez commencer à ajouter des conteneurs. To create a new container, select the ellipses (...) in the top-right corner of the tile, then select **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

Un nouveau conteneur apparaît comme la descendance du premier conteneur, mais vous pouvez réorganiser la hiérarchie en faisant glisser et en déplaçant les conteneurs. The default behavior of a container is to &quot;[!UICONTROL Include]&quot; the attribute, event, or audience provided. You can set the rule to &quot;[!UICONTROL Exclude]&quot; profiles that match the container criteria by selecting **[!UICONTROL Include]** in the top-left corner of the tile and selecting &quot;[!UICONTROL Exclude]&quot;.

Un conteneur enfant peut également être extrait et ajouté en ligne au conteneur parent en sélectionnant &quot;Annuler le renvoi à la ligne&quot; sur le conteneur enfant. Sélectionnez les ellipses (...) dans le coin supérieur droit du conteneur enfant pour accéder à cette option.

![](../images/ui/segment-builder/include-exclude.png)

Once you select **[!UICONTROL Unwrap container]** the child container is removed and the criteria appear inline.

>[!NOTE]
>
>Lorsque vous extrayez des conteneurs, veillez à ce que la logique continue de correspondre à la définition de segment souhaitée.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Stratégies de fusion

[!DNL Experience Platform] permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create a profile.

Vous pouvez sélectionner une stratégie de fusion qui correspond à votre objectif marketing pour cette audience ou utiliser la stratégie de fusion par défaut fournie par [!DNL Platform]. Vous pouvez créer plusieurs stratégies de fusion propres à votre organisation, y compris créer votre propre stratégie de fusion par défaut. Pour obtenir des instructions détaillées sur la création de stratégies de fusion pour votre organisation, consultez le tutoriel sur l’[utilisation des stratégies de fusion à l’aide de l’interface utilisateur](../../profile/ui/merge-policies.md).

To select a merge policy for your segment definition, select the gear icon on the **[!UICONTROL Fields]** tab, then use the **[!UICONTROL Merge Policy]** dropdown menu to select the merge policy that you wish to use.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Propriétés du segment

Lors de la création d’une définition de segment, la section **[!UICONTROL Propriétés du segment]** située dans la partie droite de l’espace de travail affiche une estimation de la taille du segment obtenu, ce qui vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même.

La section **[!UICONTROL Propriétés du segment]** vous permet également de spécifier des informations importantes sur votre définition de segment, y compris son **[!UICONTROL nom]** et sa **[!UICONTROL description]**. Les noms des définitions de segment sont utilisés pour identifier votre segment parmi ceux définis par votre organisation et doivent donc être descriptifs, concis et uniques.

Au fur et à mesure que vous continuez à créer votre définition de segment, vous pouvez visualiser un aperçu paginé de l’audience en sélectionnant **[!UICONTROL Afficher les profils]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

## Étapes suivantes et ressources supplémentaires {#next-steps}

Segment Builder provides a rich workflow allowing you to isolate marketable audiences from [!DNL Real-time Customer Profile] data. Après avoir lu ce guide, vous devriez maintenant pouvoir :

- créer des définitions de segment en utilisant une combinaison d’attributs, d’événements et d’audiences existants comme blocs de création ;
- utiliser les conteneurs et les canevas du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation ;
- visualiser les estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins ;
- activer toutes les définitions de segment pour la segmentation planifiée ;
- activer des définitions de segment spécifiques pour la segmentation par flux.

Pour en savoir plus [!DNL Segmentation Service], veuillez continuer à lire la documentation et compléter votre apprentissage en regardant les vidéos ci-dessous. Pour en savoir plus sur les autres parties de l’ [!DNL Segmentation Service] interface utilisateur, consultez le guide [[!DNL Segmentation Service] d’utilisation](./overview.md)

>[!WARNING]
>
> L’ [!DNL Platform] interface utilisateur affichée dans les vidéos suivantes est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

**Création d’un segment:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Créez un segment dynamique :**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)