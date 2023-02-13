---
keywords: Experience Platform;accueil;rubriques les plus consultées;Service de segmentation;segmentation;service de segmentation;guide de l’utilisateur;guide de l’interface utilisateur;guide de l’interface utilisateur de segmentation;créateur de segments;Créateur de segments;
solution: Experience Platform
title: Guide de l’interface utilisateur du créateur de segments
description: Le créateur de segments de l’interface utilisateur d’Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 28b9458d29ce69bcbfdff53c0cb6bd7f427e4a2e
workflow-type: tm+mt
source-wordcount: '3258'
ht-degree: 95%

---

# Guide de l’interface utilisateur de [!DNL Segment Builder]

Le [!DNL Segment Builder] offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

![L’interface utilisateur du créateur de segments s’affiche.](../images/ui/segment-builder/segment-builder.png)

## Blocs de création de définitions de segment {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Champs"
>abstract="Un segment est constitué des trois types de champ suivants : attributs, événements et audiences. Les attributs vous permettent d’utiliser des attributs de profil appartenant à la classe XDM Individual Profile, les événements vous permettent de créer une audience basée sur des actions ou des événements qui ont lieu à l’aide des éléments de données XDM ExperienceEvent et les audiences vous permettent d’utiliser des audiences importées à partir de sources externes."

Les blocs de création de base des définitions de segment sont les attributs et les événements. En outre, les attributs et les événements contenus dans les audiences existantes peuvent être utilisés comme éléments de nouvelles définitions.

Vous pouvez voir ces blocs de création dans la section **[!UICONTROL Champs]** sur le côté gauche de l’espace de travail [!DNL Segment Builder]. Les **[!UICONTROL champs]** contiennent un onglet pour chacun des blocs de création principaux : « [!UICONTROL attributs] », « [!UICONTROL événements] », et « [!UICONTROL audiences] ».

![La section des champs du créateur de segments est mise en surbrillance.](../images/ui/segment-builder/segment-fields.png)

### Attributs

L’onglet **[!UICONTROL Attributs]** vous permet de parcourir les attributs [!DNL Profile] appartenant à la classe [!DNL XDM Individual Profile]. Chaque dossier peut être développé pour afficher des attributs supplémentaires, où chaque attribut est une mosaïque qui peut être glissée sur le canevas du créateur de règles au centre de l’espace de travail. Le [canevas du créateur de règles](#rule-builder-canvas) est abordé plus en détail dans la suite de ce guide.

![La section Attributs des champs du créateur de segments est mise en surbrillance.](../images/ui/segment-builder/attributes.png)

### Événements

L’onglet **[!UICONTROL Événements]** vous permet de créer une audience basée sur des événements ou des actions qui ont eu lieu en utilisant des éléments de données [!DNL XDM ExperienceEvent] Vous pouvez également trouver les types d’événements dans l’onglet **[!UICONTROL Événements]**, qui sont une collection d’événements couramment utilisés pour vous permettre de créer vos segments plus rapidement.

Outre la possibilité de rechercher des éléments [!DNL ExperienceEvent], vous pouvez également rechercher des types d’événements. Les types d’événements utilisent la même logique de codage que [!DNL ExperienceEvents] sans qu’il soit nécessaire de faire une recherche dans la classe [!DNL XDM ExperienceEvent] pour trouver l’événement correct. Par exemple, l’utilisation de la barre de recherche pour rechercher « cart » (panier) renvoie les types d’événements « [!UICONTROL AddCart] » et « [!UICONTROL RemoveCart] », qui sont deux actions liées au panier très couramment utilisées lors de la création de définitions de segment.

Vous pouvez rechercher n’importe quel type de composant en tapant son nom dans la barre de recherche, qui utilise la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Les résultats de la recherche commencent à s’afficher au fur et à mesure que des mots entiers sont saisis. Par exemple, pour créer une règle basée sur le champ XDM `ExperienceEvent.commerce.productViews`, commencez à saisir « product views » dans le champ de recherche. Une fois le mot « product » saisi, les résultats de la recherche commencent à s’afficher. Chaque résultat inclut la hiérarchie d’objets à laquelle il appartient.

>[!NOTE]
>
>Les champs de schéma personnalisés définis par votre organisation peuvent mettre jusqu’à 24 heures pour s’afficher et être utilisables dans les règles de création.

Vous pouvez ensuite facilement glisser-déposer [!DNL ExperienceEvents] et « [!UICONTROL Types d’évènement] » vers votre définition de segment.

![La section événements de l’interface utilisateur du créateur de segments est mise en surbrillance.](../images/ui/segment-builder/events.png)

Par défaut, seuls les champs de schéma renseignés de votre banque de données s’affichent. Cela inclut les « [!UICONTROL types d’événements] ». Si la liste des « [!UICONTROL types d’événements] » n’est pas visible, ou si vous ne pouvez sélectionner que « [!UICONTROL Any] » comme « [!UICONTROL type d’événement] », sélectionnez l’ **icône en forme d’engrenage** à côté de **[!UICONTROL Champs]**, puis sélectionnez **[!UICONTROL Afficher l’ensemble du schéma XDM]** sous **[!UICONTROL Champs disponibles]**. Sélectionnez à nouveau l’**icône en forme d’engrenage** pour revenir à l’onglet **[!UICONTROL Champs]**. Vous devriez maintenant pouvoir afficher plusieurs « [!UICONTROL types d’événements] » et champs de schéma, qu’ils contiennent des données ou non.

![Les boutons radio qui vous permettent de choisir entre afficher uniquement les champs contenant des données ou tous les champs XDM sont mis en surbrillance.](../images/ui/segment-builder/show-populated.png)

#### Jeux de données de suite de rapports Adobe Analytics

Vous pouvez utiliser les données d’une ou de plusieurs suites de rapports Adobe Analytics comme événements dans la segmentation.

Lors de l’utilisation de données provenant d’une seule suite de rapports Analytics, Platform ajoutera automatiquement des descripteurs et des noms conviviaux aux eVars, ce qui facilite la recherche de ces champs dans [!DNL Segment Builder].

![Image montrant comment les variables génériques (eVars) sont mappées avec un nom convivial d’utilisateur.](../images/ui/segment-builder/single-report-suite.png)

Lors de l’utilisation de données provenant de plusieurs suites de rapports Analytics, Platform **ne pourra pas** ajouter automatiquement de descripteurs ou de noms conviviaux aux eVars. Par conséquent, avant d’utiliser les données de suites de rapports Analytics, vous devez les mapper aux champs XDM. Vous trouverez plus d’informations sur le mappage des variables Analytics à XDM dans le [guide de connexion source Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

Supposons, par exemple, que vous ayez deux suites de rapports avec les variables suivantes :

| Champ | Suite de rapports schéma A | Suite de rapports schéma B |
| ----- | --------------------- | --------------------- |
| eVar1 | Domaine référent | Connecté O/N |
| eVar2 | Nom de la page | Identifiant de fidélité du membre |
| eVar3 | URL | Nom de la page |
| eVar4 | Termes de recherche | Nom du produit |
| event1 | Clics | Pages vues |
| event2 | Pages vues | Ajouts au panier |
| event3 | Ajouts au panier | Passages en caisse |
| event4 | Achats | Achats |

Dans ce cas, vous pouvez mapper les deux suites de rapports avec le schéma suivant :

![Image montrant comment deux suites de rapports peuvent être mappées dans un schéma d’union.](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>Bien que les valeurs eVar génériques soient toujours renseignées, vous ne devez **pas** les utiliser dans vos définitions de segment (si possible), car les valeurs peuvent avoir des significations différentes de leurs significations d’origine dans leurs rapports.

Une fois les suites de rapports mappées, vous pouvez utiliser ces nouveaux champs mappés dans vos workflows et segmentation liés à Profile.

| Scénario | Expérience du schéma d’union | Variable générique de segmentation | Variable mappée de segmentation |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| Suite de rapports unique | Le descripteur de nom convivial est inclus avec les variables génériques. <br><br>**Exemple :** Nom de page (eVar2) | <ul><li>Descripteur de nom convivial inclus avec les variables génériques</li><li>Les requêtes utilisent des données du jeu de données spécifique, puisqu’il est le seul.</li></ul> | Les requêtes peuvent utiliser des données Adobe Analytics et potentiellement d’autres sources. |
| Suites de rapports multiples | Aucun descripteur de nom convivial n’est inclus avec les variables génériques. <br><br>**Exemple :** eVar2 | <ul><li>Tout champ comportant plusieurs descripteurs apparaît comme générique. Cela signifie qu’aucun nom convivial n’apparaît dans l’interface utilisateur.</li><li>Les requêtes peuvent utiliser les données de n’importe quel jeu de données contenant l’eVar, ce qui peut entraîner des résultats variés ou incorrects.</li></ul> | Les requêtes utilisent correctement les résultats combinés de plusieurs jeux de données. |

### Audiences

L’onglet **[!UICONTROL Audiences]** répertorie toutes les audiences importées de sources externes, telles qu’Adobe Audience Manager, ainsi que les audiences créées dans [!DNL Experience Platform].

Dans l’onglet **[!UICONTROL Audiences]**, vous pouvez voir toutes les sources disponibles sous la forme d’un groupe de dossiers. En sélectionnant ces dossiers, vous pouvez voir les sous-dossiers et les audiences disponibles. De plus, vous pouvez sélectionner l’icône du dossier (comme indiqué dans l’image située à l’extrême droite) afin de visualiser la structure des dossiers (une coche indique le dossier dans lequel vous vous trouvez actuellement) et de parcourir facilement les dossiers en sélectionnant le nom d’un dossier dans l’arborescence.

Vous pouvez passer la souris sur l’option ⓘ située à côté d’une audience pour afficher des informations sur cette dernière, notamment son identifiant, sa description et la hiérarchie des dossiers permettant de la localiser.

![Image montrant le fonctionnement de la hiérarchie de dossiers pour les audiences.](../images/ui/segment-builder/audience-folder-structure.png)

Vous pouvez également rechercher des audiences à l’aide de la barre de recherche, laquelle utilise la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Dans l’onglet **[!UICONTROL Audiences]**, si vous sélectionnez un dossier de niveau supérieur, la barre de recherche s’affiche et vous permet de faire une recherche dans ce dossier. Les résultats de la recherche ne commencent à s’afficher que lorsque des mots entiers sont saisis. Par exemple, pour trouver une audience nommée `Online Shoppers`, commencez à taper « Online » dans la barre de recherche. Une fois que le mot « Online » a été complètement saisi, les résultats de la recherche contenant ce mot apparaissent.

## Canevas du créateur de règles {#rule-builder-canvas}

Une définition de segment est un ensemble de règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible. Ces règles sont créées à l’aide du canevas du créateur de règles, situé au centre du [!DNL Segment Builder].

Pour ajouter une nouvelle règle à votre définition de segment, faites glisser une mosaïque depuis l’onglet **[!UICONTROL Champs]** et déposez-la sur le canevas du créateur de règles. Des options spécifiques au contexte vous seront ensuite présentées en fonction du type de données ajouté. Les types de données disponibles sont les suivants : chaînes, dates, [!DNL ExperienceEvents], [!UICONTROL types d’événement], et audiences.

![Canevas du créateur de règles vierge.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Les dernières modifications apportées à Adobe Experience Platform ont mis à jour l’utilisation des opérateurs logiques `OR` et `AND` entre les événements. Ces mises à jour n’auront aucune incidence sur les segments existants. Cependant, toutes les mises à jour ultérieures des segments existants et des nouvelles créations de segments seront affectées par ces modifications. Consultez la [mise à jour des constantes de temps](./segment-refactoring.md) pour plus d’informations.

Lors de la sélection d’une valeur pour l’attribut, vous verrez une liste de valeurs d’énumération pour l’attribut.

![Image montrant la liste des valeurs d’énumération pour un attribut.](../images/ui/segment-builder/enum-list.png)

Si vous sélectionnez une valeur dans cette liste d’énumérations, elle sera entourée d’une bordure pleine. Toutefois, pour les champs qui utilisent les énumérations `meta:enum` (soft), vous pouvez également sélectionner une valeur qui n’est **pas** dans la liste d’énumérations. Si vous créez votre propre valeur, elle est entourée d’une bordure en pointillés, avec un avertissement indiquant que cette valeur ne figure pas dans la liste d’énumérations.

![Avertissement qui s’affiche si vous insérez une valeur qui ne fait pas partie de la liste d’énumérations.](../images/ui/segment-builder/enum-warning.png)

Si vous créez plusieurs valeurs, vous pouvez toutes les ajouter en même temps à l’aide du téléchargement en masse. Sélectionnez la ![icône plus](../images/ui/segment-builder/plus-icon.png) pour afficher le **[!UICONTROL Ajouter des valeurs en bloc]** de la fenêtre contextuelle.

![L’icône plus est mise en surbrillance, affichant le bouton que vous pouvez sélectionner pour accéder à la fenêtre contextuelle de téléchargement en bloc.](../images/ui/segment-builder/add-bulk-values.png)

Sur le **[!UICONTROL Ajouter des valeurs en bloc]** vous pouvez transférer un fichier CSV ou TSV.

![La fenêtre contextuelle Ajouter des valeurs s’affiche en bloc. La boîte de dialogue que vous pouvez sélectionner pour charger un fichier CSV ou TSV est mise en surbrillance.](../images/ui/segment-builder/bulk-values-popover.png)

Vous pouvez également ajouter manuellement des valeurs séparées par des virgules.

![La fenêtre contextuelle Ajouter des valeurs s’affiche en bloc. La boîte de dialogue que vous pouvez utiliser pour insérer des valeurs et les valeurs ajoutées sont mises en surbrillance.](../images/ui/segment-builder/bulk-values-comma-separated.png)

250 valeurs au maximum sont autorisées. Si vous dépassez ce montant, vous devrez supprimer certaines valeurs avant d’en ajouter d’autres.

![Un avertissement indiquant que vous avez atteint le nombre maximum de valeurs s’affiche.](../images/ui/segment-builder/maximum-values.png)

### Ajout d’audiences

Vous pouvez faire glisser une audience depuis l’onglet **[!UICONTROL Audience]** sur le canevas du créateur de règles pour référencer l’appartenance à l’audience dans la nouvelle définition de segment. Cela vous permet d’inclure ou d’exclure l’appartenance à une audience en tant qu’attribut dans la nouvelle règle de segmentation.

Pour les [!DNL Platform]audiences créées à l’aide du [!DNL Segment Builder], vous avez la possibilité de convertir l’audience en un ensemble de règles utilisées dans la définition de segment pour cette audience. Cette conversion effectue une copie de la logique de règle, qui peut ensuite être modifiée sans affecter la définition de segment d’origine. Assurez-vous d’avoir enregistré les modifications récentes apportées à votre définition de segment avant de la convertir en logique de règle.

>[!NOTE]
>
>Lors de l’ajout d’une audience provenant d’une source externe, seule l’appartenance à l’audience est référencée. Vous ne pouvez pas convertir l’audience en règles. Par conséquent, les règles utilisées pour créer l’audience originale ne peuvent pas être modifiées dans la nouvelle définition de segment.

![Cette image montre comment convertir un attribut d’audience en règles.](../images/ui/segment-builder/add-audience-to-segment.png)

Si des conflits surviennent lors de la conversion d’audiences en règles, le [!DNL Segment Builder] tentera de conserver au mieux les options existantes.

### Affichage du code

Vous pouvez également afficher une version codée d’une règle créée dans le [!DNL Segment Builder]. Une fois que vous avez créé votre règle dans la zone de travail du créateur de règles, vous pouvez sélectionner **[!UICONTROL Affichage du code]** pour afficher votre segment en PQL.

![Le bouton d’affichage du code est mis en surbrillance, ce qui vous permet d’afficher le segment en PQL.](../images/ui/segment-builder/code-view.png)

L’affichage du code fournit un bouton qui vous permet de copier la valeur du segment à utiliser dans les appels API. Pour obtenir la dernière version du segment, assurez-vous d’avoir sauvegardé vos dernières modifications du segment.

![Le bouton « Copier le code » est mis en surbrillance, ce qui vous permet de ](../images/ui/segment-builder/copy-code.png)

### Fonctions d’agrégation

Dans le [!DNL Segment Builder], une agrégation est un calcul effectué sur un groupe d’attributs XDM dont le type de données est un nombre (double ou entier). Les quatre fonctions d’agrégation prises en charge dans le créateur de segments sont SOMME, MOYENNE, MIN et MAX.

Pour créer une fonction d’agrégation, sélectionnez un événement dans le rail de gauche, puis insérez-le dans le conteneur [!UICONTROL Événements].

![La section Événements est mise en surbrillance.](../images/ui/segment-builder/events.png)

Après avoir placé l’événement dans le conteneur Événements, sélectionnez l’icône représentant des points de suspension (...), puis sélectionnez **[!UICONTROL Agréger]**.

![Le texte agrégé est mis en surbrillance. En le sélectionnant, vous pouvez sélectionner des fonctions d’agrégation.](../images/ui/segment-builder/add-aggregation.png)

L’agrégation est maintenant ajoutée. Vous pouvez maintenant sélectionner la fonction d’agrégation, choisir l’attribut à agréger, la fonction d’égalité, ainsi que la valeur. Pour l’exemple ci-dessous, ce segment peut être considéré comme un profil dont la somme des valeurs achetées est supérieure à 100$, même si chaque achat individuel est inférieur à 100$.

![Les règles d’événement, qui affichent une fonction d’agrégation.](../images/ui/segment-builder/filled-aggregation.png)

### Fonctions de comptage {#count-functions}

Dans le créateur de segments, les fonctions de comptage permettent de rechercher des événements spécifiques et de compter le nombre de fois qu’ils se produisent. Les fonctions de comptage prises en charge dans le créateur de segments sont « Au moins », « Au plus », « Exactement », « Entre » et « Tout ».

Pour créer une fonction de comptage, sélectionnez un événement dans le rail de gauche et insérez-le dans un conteneur [!UICONTROL Événements].

![Les champs d’événement sont mis en surbrillance.](../images/ui/segment-builder/events.png)

Après avoir placé l’événement dans le conteneur Événements, sélectionnez le bouton [!UICONTROL Au moins 1].

![L’option « Au moins » est mise en surbrillance, montrant la zone à sélectionner pour afficher la liste complète des fonctions de comptage.](../images/ui/segment-builder/add-count.png)

La fonction de comptage est maintenant ajoutée. Vous pouvez maintenant sélectionner la fonction de comptage et la valeur de la fonction. L’exemple ci-dessous consisterait à inclure tout événement qui a au moins un clic.

![Une liste des fonctions de comptage s’affiche et est mise en surbrillance.](../images/ui/segment-builder/select-count.png)

## Conteneurs

Les règles de segmentation sont évaluées dans l’ordre dans lequel elles sont répertoriées. Les conteneurs permettent de contrôler l’ordre d’exécution grâce à l’utilisation de requêtes imbriquées.

Une fois que vous avez ajouté au moins une mosaïque au canevas du créateur de règles, vous pouvez commencer à ajouter des conteneurs. Pour créer un nouveau conteneur, sélectionnez les points de suspension (...) dans le coin supérieur droit du volet, puis sélectionnez **[!UICONTROL Ajouter un conteneur]**.

![Le bouton « Ajouter un conteneur » est mis en surbrillance, ce qui vous permet d’ajouter un conteneur en tant qu’enfant du premier conteneur.](../images/ui/segment-builder/add-container.png)

Un nouveau conteneur apparaît comme la descendance du premier conteneur, mais vous pouvez réorganiser la hiérarchie en faisant glisser et en déplaçant les conteneurs. Le comportement par défaut d’un conteneur est d’« [!UICONTROL inclure] » l’attribut, l’audience ou l’événement fourni. Vous pouvez définir la règle pour « [!UICONTROL Exclure] » les profils qui correspondent aux critères du conteneur en sélectionnant **[!UICONTROL Inclure]** dans le coin supérieur gauche du volet et en sélectionnant « [!UICONTROL Exclure] ».

Un conteneur enfant peut également être extrait et intégré au conteneur parent en sélectionnant « Déplier le conteneur » dans le conteneur enfant. Sélectionnez les points de suspension (...) dans le coin supérieur droit du conteneur enfant pour accéder à cette option.

![Les options permettant de déplier ou de supprimer le conteneur sont mises en surbrillance.](../images/ui/segment-builder/include-exclude.png)

Après avoir selectionné **[!UICONTROL Déplier le conteneur]**, le conteneur enfant est supprimé et les critères intégrés apparaissent.

>[!NOTE]
>
>Lorsque vous extrayez des conteneurs, veillez à ce que la logique continue de correspondre à la définition de segment souhaitée.

![Le conteneur s’affiche après avoir été déplié.](../images/ui/segment-builder/unwrapped-container.png)

## Stratégies de fusion

[!DNL Experience Platform] vous permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lors du regroupement de ces données, les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer un profil.

Vous pouvez sélectionner une stratégie de fusion qui correspond à votre objectif marketing pour cette audience ou utiliser la stratégie de fusion par défaut fournie par [!DNL Platform]. Vous pouvez créer plusieurs stratégies de fusion propres à votre organisation, y compris créer votre propre stratégie de fusion par défaut. Pour obtenir des instructions détaillées sur la création de stratégies de fusion pour votre organisation, commencez par lire la [présentation des stratégies de fusion](../../profile/merge-policies/overview.md).

Pour sélectionner une stratégie de fusion pour votre définition de segment, sélectionnez l’icône en forme d’engrenage dans l’onglet **[!UICONTROL Champs]**, puis utilisez le menu déroulant **[!UICONTROL Stratégie de fusion]** pour sélectionner la stratégie de fusion à utiliser.

![Le sélecteur de stratégie de fusion est mis en surbrillance. Vous pouvez ainsi choisir la stratégie de fusion à sélectionner pour votre définition de segment.](../images/ui/segment-builder/merge-policy-selector.png)

## Propriétés du segment {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Propriétés du segment"
>abstract="La section des propriétés du segment affiche une estimation de la taille du segment résultant, en affichant le nombre de profils qualifiés par rapport au nombre total de profils. Cela vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Actualiser les estimations"
>abstract="Vous pouvez actualiser les estimations de votre segment pour afficher immédiatement un aperçu du nombre de profils admissibles pour le segment proposé. Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=fr#estimate-and-preview-an-audience" text="Estimation et prévisualisation d’une audience"

Lors de la création d’une définition de segment, la section **[!UICONTROL Propriétés du segment]** située dans la partie droite de l’espace de travail affiche une estimation de la taille du segment obtenu, ce qui vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même.

La section **[!UICONTROL Propriétés du segment]** vous permet également de spécifier des informations importantes sur votre définition de segment, y compris son nom, sa description et son type d’évaluation. Les noms des définitions de segment sont utilisés pour identifier votre segment parmi ceux définis par votre organisation et doivent donc être descriptifs, concis et uniques.

Au fur et à mesure que vous continuez à créer votre définition de segment, vous pouvez visualiser un aperçu paginé de l’audience en sélectionnant **[!UICONTROL Afficher les profils]**.

![La section des propriétés de définition de segment est mise en surbrillance. Les propriétés du segment comportent, sans s’y limiter, le nom, la description et la méthode d’évaluation du segment.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

Vous pouvez également sélectionner votre méthode d’évaluation. Si vous savez quelle méthode d’évaluation vous voulez utiliser, vous pouvez sélectionner la méthode d’évaluation souhaitée à l’aide de la liste déroulante. Si vous souhaitez savoir pour quels types d’évaluation ce segment est admissible, vous pouvez sélectionner l’![icône de dossier Parcourir avec une loupe](../images/ui/segment-builder/segment-evaluation-select-icon.png) pour voir la liste des méthodes d’évaluation de segment disponibles.

L’[!UICONTROL Éligibilité de la méthode d’évaluation] s’affiche. Cette fenêtre contextuelle affiche les méthodes d’évaluation disponibles, à savoir par lots, en flux continu et Edge. La fenêtre contextuelle affiche les méthodes d’évaluation éligibles et non éligibles. Selon les paramètres que vous avez utilisés dans votre définition de segment, il se peut qu’elle ne soit pas admissible pour certaines méthodes d’évaluation. Pour plus d’informations sur les exigences de chaque méthode d’évaluation, veuillez lire les présentations sur la [segmentation en flux continu](./streaming-segmentation.md#query-types) ou la [segmentation Edge](./edge-segmentation.md#query-types).

![La fenêtre contextuelle d’éligibilité de la méthode d’évaluation s’affiche. Elle affiche les méthodes d’évaluation de segment éligibles et non éligibles pour le segment.](../images/ui/segment-builder/select-evaluation-method.png)

Si vous sélectionnez une méthode d’évaluation non valide, vous serez invité à modifier vos règles de définition de segment ou la méthode d’évaluation.

![La fenêtre contextuelle de méthode d’évaluation s’affiche. Si une méthode d’évaluation de segment non éligible est sélectionnée, la fenêtre contextuelle explique pourquoi celle-ci n’est pas éligible.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Vous trouverez plus d’informations sur les différentes méthodes d’évaluation de définition de segment dans la [présentation de la segmentation](../home.md#evaluate-segments).

## Étapes suivantes {#next-steps}

Le créateur de segments fournit un workflow complet qui vous permet d’isoler les audiences commercialisables des données [!DNL Real-Time Customer Profile]. Après avoir lu ce guide, vous devriez maintenant pouvoir :

- créer des définitions de segment en utilisant une combinaison d’attributs, d’événements et d’audiences existants comme blocs de création ;
- utiliser les conteneurs et les canevas du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation ;
- visualiser les estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins ;
- activer toutes les définitions de segment pour la segmentation planifiée ;
- activer des définitions de segment spécifiques pour la segmentation par flux.

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation et compléter votre apprentissage en regardant les vidéos associées. Pour en savoir plus sur les autres parties de l’interface utilisateur de [!DNL Segmentation Service], veuillez lire le [[!DNL Segmentation Service] guide de l’utilisateur](./overview.md).
