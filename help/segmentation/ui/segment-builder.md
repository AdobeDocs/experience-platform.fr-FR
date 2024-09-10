---
solution: Experience Platform
title: Guide de l’interface utilisateur du créateur de segments
description: Le créateur de segments de l’interface utilisateur d’Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 7d2fe8d5e5abea768b3514d97ea7edfbb9334511
workflow-type: tm+mt
source-wordcount: '4767'
ht-degree: 67%

---

# Guide de l’interface utilisateur de [!DNL Segment Builder]

>[!NOTE]
>
>Ce guide décrit la création d’audiences par le biais de **définitions de segment** dans le créateur de segments. Pour savoir comment créer des audiences à l’aide de la composition d’audience, consultez le [Guide de l’interface utilisateur de la composition d’audience](./audience-composition.md).

Le [!DNL Segment Builder] offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données de [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

![L’interface utilisateur du créateur de segments s’affiche.](../images/ui/segment-builder/segment-builder.png)

## Blocs de création de définitions de segment {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Champs"
>abstract="Une définition de segment est constituée des trois types de champ suivants : les attributs, les événements et les audiences. Les attributs vous permettent d’utiliser des attributs de profil appartenant à la classe XDM Individual Profile, les événements vous permettent de créer une audience basée sur des actions ou des événements qui ont lieu à l’aide des éléments de données XDM ExperienceEvent et les audiences vous permettent d’utiliser des audiences importées à partir de sources externes."

Les blocs de création de base des définitions de segment sont les attributs et les événements. En outre, les attributs et les événements contenus dans les audiences existantes peuvent être utilisés comme éléments de nouvelles définitions.

Vous pouvez voir ces blocs de création dans la section **[!UICONTROL Champs]** sur le côté gauche de l’espace de travail [!DNL Segment Builder]. Les **[!UICONTROL champs]** contiennent un onglet pour chacun des blocs de création principaux : « [!UICONTROL attributs] », « [!UICONTROL événements] », et « [!UICONTROL audiences] ».

![La section des champs du créateur de segments est mise en surbrillance.](../images/ui/segment-builder/segment-fields.png)

### Attributs

L’onglet **[!UICONTROL Attributs]** vous permet de parcourir les attributs [!DNL Profile] appartenant à la classe [!DNL XDM Individual Profile]. Chaque dossier peut être développé pour afficher des attributs supplémentaires, où chaque attribut est une mosaïque qui peut être glissée sur la zone de travail du créateur de règles au centre de l’espace de travail. La [zone de travail du créateur de règles](#rule-builder-canvas) est abordée plus en détail dans la suite de ce guide.

![La section Attributs des champs du créateur de segments est mise en surbrillance.](../images/ui/segment-builder/attributes.png)

### Événements

L’onglet **[!UICONTROL Événements]** vous permet de créer une audience basée sur des événements ou des actions qui ont eu lieu en utilisant des éléments de données [!DNL XDM ExperienceEvent] Vous pouvez également trouver les types d’événements dans l’onglet **[!UICONTROL Événements]**, qui sont une collection d’événements couramment utilisés pour vous permettre de créer vos définitions de segments plus rapidement.

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

>[!NOTE]
>
>Pour les audiences créées dans Platform, seules les audiences ayant la stratégie de fusion **same** s’affichent.

L’onglet **[!UICONTROL Audiences]** répertorie toutes les audiences importées de sources externes, telles que Adobe Audience Manager ou Customer Journey Analytics, ainsi que les audiences créées dans [!DNL Experience Platform].

Dans l’onglet **[!UICONTROL Audiences]**, vous pouvez voir toutes les sources disponibles sous la forme d’un groupe de dossiers. En sélectionnant ces dossiers, vous pouvez voir les sous-dossiers et les audiences disponibles. De plus, vous pouvez sélectionner l’icône du dossier (comme indiqué dans l’image située à l’extrême droite) afin de visualiser la structure des dossiers (une coche indique le dossier dans lequel vous vous trouvez actuellement) et de parcourir facilement les dossiers en sélectionnant le nom d’un dossier dans l’arborescence.

Vous pouvez passer la souris sur l’option ⓘ située à côté d’une audience pour afficher des informations sur cette dernière, notamment son identifiant, sa description et la hiérarchie des dossiers permettant de la localiser.

![Image montrant le fonctionnement de la hiérarchie de dossiers pour les audiences.](../images/ui/segment-builder/audience-folder-structure.png)

Vous pouvez également rechercher des audiences à l’aide de la barre de recherche, laquelle utilise la [syntaxe de recherche Lucene](https://docs.microsoft.com/fr-fr/azure/search/query-lucene-syntax). Dans l’onglet **[!UICONTROL Audiences]**, si vous sélectionnez un dossier de niveau supérieur, la barre de recherche s’affiche et vous permet de faire une recherche dans ce dossier. Les résultats de la recherche ne commencent à s’afficher que lorsque des mots entiers sont saisis. Par exemple, pour trouver une audience nommée `Online Shoppers`, commencez à taper « Online » dans la barre de recherche. Une fois que le mot « Online » a été complètement saisi, les résultats de la recherche contenant ce mot apparaissent.

## Zone de travail du créateur de règles {#rule-builder-canvas}

>[!IMPORTANT]
>
>Depuis la version de juin 2024, les contraintes de temps &quot;Ce mois-ci&quot; et &quot;Cette année&quot; représentent respectivement &quot;le mois à jour&quot; et &quot;l’année à jour&quot;. Par exemple, si vous avez créé une audience le 18 juillet à la recherche de &quot;tous les clients dont l’anniversaire a lieu ce mois-ci&quot;, l’audience obtiendra tous les clients dont l’anniversaire a eu lieu du 1er au 31 juillet. Le 1er août, ce public recevra tous les clients dont l&#39;anniversaire a lieu du 1er au 31 août.
>
>Auparavant, &quot;Ce mois-ci&quot; et &quot;cette année&quot; représentaient respectivement 30 et 365 jours, ce qui ne rendait pas compte des mois de 31 jours et des années bissextiles.
>
>Pour mettre à jour la logique de vos audiences, réenregistrez les audiences créées précédemment.

Une définition de segment est un ensemble de règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible. Ces règles sont créées à l’aide de la zone de travail du créateur de règles, au centre du [!DNL Segment Builder].

Pour ajouter une nouvelle règle à votre définition de segment, faites glisser une mosaïque depuis l’onglet **[!UICONTROL Champs]** et déposez-la sur la zone de travail du créateur de règles. Des options spécifiques au contexte vous seront ensuite présentées en fonction du type de données ajouté. Les types de données disponibles sont les suivants : chaînes, dates, [!DNL ExperienceEvents], [!UICONTROL types d’événement], et audiences.

![Zone de travail du créateur de règles vide.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Les dernières modifications apportées à Adobe Experience Platform ont mis à jour l’utilisation des opérateurs logiques `OR` et `AND` entre les événements. Ces mises à jour n’auront aucune incidence sur les définitions de segment existantes. Cependant, toutes les mises à jour ultérieures des définitions de segment existantes et des définitions de segment nouvellement créées seront affectées par ces modifications. Consultez la [mise à jour des constantes de temps](./segment-refactoring.md) pour plus d’informations.

Lors de la sélection d’une valeur pour l’attribut, vous verrez une liste de valeurs d’énumération pour l’attribut.

![Image montrant la liste des valeurs d’énumération pour un attribut.](../images/ui/segment-builder/enum-list.png)

Si vous sélectionnez une valeur dans cette liste d’énumérations, elle sera entourée d’une bordure pleine. Toutefois, pour les champs qui utilisent les énumérations `meta:enum` (soft), vous pouvez également sélectionner une valeur qui n’est **pas** dans la liste d’énumérations. Si vous créez votre propre valeur, elle est entourée d’une bordure en pointillés, avec un avertissement indiquant que cette valeur ne figure pas dans la liste d’énumérations.

![Avertissement qui s’affiche si vous insérez une valeur qui ne fait pas partie de la liste d’énumérations.](../images/ui/segment-builder/enum-warning.png)

Si vous créez plusieurs valeurs, vous pouvez toutes les ajouter en même temps à l’aide du téléchargement massif. Sélectionnez l’![icône plus](/help/images/icons/add-circle.png) pour afficher la fenêtre contextuelle **[!UICONTROL Ajouter des valeurs en bloc]**.

![L’icône plus est mise en surbrillance, affichant le bouton que vous pouvez sélectionner pour accéder à la fenêtre contextuelle de téléchargement massif.](../images/ui/segment-builder/add-bulk-values.png)

Sur la fenêtre contextuelle **[!UICONTROL Ajouter des valeurs en bloc]**, vous pouvez télécharger un fichier CSV ou TSV.

![La fenêtre contextuelle Ajouter des valeurs en bloc s’affiche. La boîte de dialogue que vous pouvez sélectionner pour télécharger un fichier CSV ou TSV est mise en surbrillance.](../images/ui/segment-builder/bulk-values-popover.png)

Vous pouvez également ajouter manuellement des valeurs séparées par des virgules.

![La fenêtre contextuelle Ajouter des valeurs en bloc s’affiche. La boîte de dialogue que vous pouvez utiliser pour insérer des valeurs et les valeurs ajoutées sont mises en surbrillance.](../images/ui/segment-builder/bulk-values-comma-separated.png)

Veuillez noter qu’un maximum de 250 valeurs est autorisé. Si vous dépassez ce nombre, vous devrez supprimer certaines valeurs avant d’en ajouter d’autres.

![Un avertissement indiquant que vous avez atteint le nombre maximum de valeurs s’affiche.](../images/ui/segment-builder/maximum-values.png)

### Ajout d’audiences

Vous pouvez faire glisser une audience depuis l’onglet **[!UICONTROL Audience]** sur la zone de travail du créateur de règles pour référencer l’appartenance à l’audience dans la nouvelle définition de segment. Cela vous permet d’inclure ou d’exclure l’appartenance à une audience en tant qu’attribut dans les nouvelles règles de définition de segment.

Pour les [!DNL Platform]audiences créées à l’aide du [!DNL Segment Builder], vous avez la possibilité de convertir l’audience en un ensemble de règles utilisées dans la définition de segment pour cette audience. Cette conversion effectue une copie de la logique de règle, qui peut ensuite être modifiée sans affecter la définition de segment d’origine. Assurez-vous d’avoir enregistré les modifications récentes apportées à votre définition de segment avant de la convertir en logique de règle.

>[!NOTE]
>
>Lors de l’ajout d’une audience provenant d’une source externe, seule l’appartenance à l’audience est référencée. Vous ne pouvez pas convertir l’audience en règles. Par conséquent, les règles utilisées pour créer l’audience originale ne peuvent pas être modifiées dans la nouvelle définition de segment.

![Cette image montre comment convertir un attribut d’audience en règles.](../images/ui/segment-builder/add-audience-to-segment.png)

Si des conflits surviennent lors de la conversion d’audiences en règles, le [!DNL Segment Builder] tentera de conserver au mieux les options existantes.

### Affichage du code

Vous pouvez également afficher une version codée d’une règle créée dans le [!DNL Segment Builder]. Une fois que vous avez créé votre règle dans la zone de travail du créateur de règles, vous pouvez sélectionner **[!UICONTROL Affichage du code]** pour afficher votre définition de segment en PQL.

![Le bouton d’affichage du code est mis en surbrillance, ce qui vous permet d’afficher la définition de segment en PQL.](../images/ui/segment-builder/code-view.png)

L’affichage du code fournit un bouton qui vous permet de copier la valeur de la définition de segment à utiliser dans les appels d’API. Pour obtenir la dernière version de la définition de segment, assurez-vous d’avoir enregistré vos dernières modifications apportées à la définition de segment.

![Le bouton « Copier le code » est mis en surbrillance, ce qui vous permet de ](../images/ui/segment-builder/copy-code.png)

### Fonctions d’agrégation

Dans le [!DNL Segment Builder], une agrégation est un calcul effectué sur un groupe d’attributs XDM dont le type de données est un nombre (double ou entier). Les quatre fonctions d’agrégation prises en charge dans le créateur de segments sont SOMME, MOYENNE, MIN et MAX.

Pour créer une fonction d’agrégation, sélectionnez un événement dans le rail de gauche, puis insérez-le dans le conteneur [!UICONTROL Événements].

![La section Événements est mise en surbrillance.](../images/ui/segment-builder/events.png)

Après avoir placé l’événement dans le conteneur Événements, sélectionnez l’icône représentant des points de suspension (...), puis sélectionnez **[!UICONTROL Agréger]**.

![Le texte agrégé est mis en surbrillance. En le sélectionnant, vous pouvez sélectionner des fonctions d’agrégation.](../images/ui/segment-builder/add-aggregation.png)

L’agrégation est maintenant ajoutée. Vous pouvez maintenant sélectionner la fonction d’agrégation, choisir l’attribut à agréger, la fonction d’égalité, ainsi que la valeur. Pour l’exemple ci-dessous, cette définition de segment peut être considérée comme un profil dont la somme des valeurs achetées est supérieure à 100 $, même si chaque achat individuel est inférieur à 100 $.

![Les règles d’événement, qui affichent une fonction d’agrégation.](../images/ui/segment-builder/filled-aggregation.png)

### Fonctions de comptage {#count-functions}

Dans le créateur de segments, les fonctions de comptage permettent de rechercher des événements spécifiques et de compter le nombre de fois qu’ils se produisent. Les fonctions de comptage prises en charge dans le créateur de segments sont « Au moins », « Au plus », « Exactement », « Entre » et « Tout ».

Pour créer une fonction de comptage, sélectionnez un événement dans le rail de gauche et insérez-le dans un conteneur [!UICONTROL Événements].

![Les champs d’événement sont mis en surbrillance.](../images/ui/segment-builder/events.png)

Après avoir placé l’événement dans le conteneur Événements, sélectionnez le bouton [!UICONTROL Au moins 1].

![L’option « Au moins » est mise en surbrillance, montrant la zone à sélectionner pour afficher la liste complète des fonctions de comptage.](../images/ui/segment-builder/add-count.png)

La fonction de comptage est maintenant ajoutée. Vous pouvez maintenant sélectionner la fonction de comptage et la valeur de la fonction. L’exemple ci-dessous consisterait à inclure tout événement qui a au moins un clic.

![Une liste des fonctions de comptage s’affiche et est mise en surbrillance.](../images/ui/segment-builder/select-count.png)

### Contraintes temporelles {#time-constraints}

Les contraintes de temps vous permettent d’appliquer des restrictions de temps aux attributs temporels, aux événements et à la séquence entre les événements.

>[!IMPORTANT]
>
>Si vous avez créé une définition de segment avec les contraintes de temps &quot;Ce mois-ci&quot; ou &quot;Cette année&quot; avant juin 2024, vous devez enregistrer à nouveau vos définitions de segment. Avant juin 2024, &quot;Ce mois-ci&quot; était basé sur 30 jours et &quot;Cette année&quot; était basé sur 365 jours.

La liste des contraintes de temps disponibles est la suivante :

+++ Contraintes de temps disponibles

>[!NOTE]
>
>Toutes les contraintes de temps sont basées sur l’UTC.
>
>De plus, si la case à cocher [!UICONTROL Ignorer l’année] est activée, l’année sera **pas** comparée dans le cadre de l’évaluation de la définition de segment.

| Contrainte horaire | Description | Peut activer l’année ignorée | Exemple |
| --------------- | ----------- | ------------------- | ------- |
| Today | L’attribut ou l’événement comparé **must** se produit aujourd’hui. | Oui | ![Exemple de contrainte horaire &quot;Aujourd’hui&quot; utilisée.](../images/ui/segment-builder/time-constraints/today.png){width="100" zoomable="yes"} |
| Hier | L’attribut ou l’événement en cours de comparaison **must** a lieu hier. | Oui | ![Exemple de contrainte d’heure &quot;Hier&quot; utilisée.](../images/ui/segment-builder/time-constraints/yesterday.png){width="100" zoomable="yes"} |
| Ce mois-ci | L’attribut ou l’événement en cours de comparaison **must** se produit ce mois-ci du calendrier. | Oui | ![Exemple de contrainte horaire &quot;Ce mois-ci&quot; utilisée.](../images/ui/segment-builder/time-constraints/this-month.png){width="100" zoomable="yes"} |
| Cette année | L’attribut ou l’événement comparé **must** a lieu cette année calendaire. | Non | ![Exemple de contrainte horaire &quot;Cette année&quot; utilisée.](../images/ui/segment-builder/time-constraints/this-year.png){width="100" zoomable="yes"} |
| Date personnalisée | L’attribut ou l’événement en cours de comparaison **must** se produit à la date indiquée. | Oui | ![Exemple de contrainte d&#39;heure &quot;Date personnalisée&quot; utilisée.](../images/ui/segment-builder/time-constraints/custom-date.png){width="100" zoomable="yes"} |
| En dernier | L’attribut ou l’événement en cours de comparaison **must** se produit au cours de la dernière période choisie. Cette période est **incluse** jusqu’à l’heure d’évaluation. | Non | ![Exemple de contrainte d’heure &quot;In last&quot; utilisée.](../images/ui/segment-builder/time-constraints/in-last.png){width="100" zoomable="yes"} |
| De (à) | L’attribut ou l’événement en cours de comparaison **must** se produit dans les deux dates calendaires sélectionnées. Cette période est **incluse** des deux dates. | Oui, si date personnalisée | ![Exemple de &quot;De à&quot; utilisé.](../images/ui/segment-builder/time-constraints/from-to.png){width="100" zoomable="yes"} |
| Durant | L’attribut ou l’événement en cours de comparaison **must** se produit au cours du mois ou de l’année sélectionné. Si un mois est sélectionné, vous devez choisir le mois et l’année au cours desquels l’attribut ou l’événement a eu lieu.  Si une année est sélectionnée, vous devez simplement choisir l’année dans laquelle l’attribut ou l’événement a eu lieu. Si vous sélectionnez un mois, vous pouvez également activer la case à cocher [!UICONTROL Ignorer l&#39;année] . | Oui | ![Exemple de contrainte de temps &quot;Durant&quot; utilisée.](../images/ui/segment-builder/time-constraints/during.png){width="100" zoomable="yes"} |
| Dans (+/-) | L’attribut ou l’événement comparé **must** se produit dans les jours, semaines, mois ou années suivant la date sélectionnée. Cette période est **incluse** des deux dates. La date sélectionnée peut être aujourd’hui, hier ou une autre date personnalisée de votre choix. | Oui | ![Exemple de contrainte temporelle &quot;Within&quot; utilisée.](../images/ui/segment-builder/time-constraints/within.png){width="100" zoomable="yes"} |
| Avant | L’attribut ou l’événement en cours de comparaison **doit** a lieu avant la date sélectionnée. La date sélectionnée peut être une date personnalisée de votre choix ou une sélection entre jours, semaines, mois ou années auparavant. | Oui | ![Exemple de contrainte horaire &quot;Avant&quot; utilisée.](../images/ui/segment-builder/time-constraints/before.png){width="100" zoomable="yes"} |
| Après | L’attribut ou l’événement en cours de comparaison **must** se produit après la date sélectionnée. La date sélectionnée peut être une date personnalisée de votre choix ou une sélection entre jours, semaines, mois ou années auparavant. | Oui | ![Exemple de contrainte de temps &quot;Après&quot; utilisée.](../images/ui/segment-builder/time-constraints/after.png){width="100" zoomable="yes"} |
| Plage variable | L’attribut ou l’événement en cours de comparaison doit se produire entre les deux dates relatives. Les dates peuvent être représentées en secondes, minutes, heures, jours, semaines, mois ou années. | Non | ![Exemple de contrainte temporelle &quot;Plage variable&quot; utilisée.](../images/ui/segment-builder/time-constraints/rolling-range.png){width="100" zoomable="yes"} |
| Dans le suivant | L’attribut ou l’événement en cours de comparaison doit se produire au cours de la période sélectionnée suivante. Les périodes sélectionnées comprennent les minutes, les heures, les jours, les semaines, les mois et les années. | Non | ![Exemple de contrainte d&#39;heure &quot;Dans la prochaine&quot; utilisée.](../images/ui/segment-builder/time-constraints/in-next.png){width="100" zoomable="yes"} |
| Existe | L’attribut existe. | Non | ![Exemple de contrainte temporelle &quot;Existe&quot; utilisée.](../images/ui/segment-builder/time-constraints/exists.png){width="100" zoomable="yes"} |
| N’existe pas | L’attribut n’existe pas. | Non | ![Exemple de contrainte temporelle &quot;N’existe pas&quot; utilisée.](../images/ui/segment-builder/time-constraints/does-not-exist.png){width="100" zoomable="yes"} |

+++

Lorsque vous appliquez une contrainte temporelle à un événement, vous pouvez l’appliquer au niveau de la zone de travail, au niveau de la carte ou entre les événements.

#### Contrainte au niveau de la zone de travail

Pour appliquer une contrainte temporelle au niveau de la zone de travail, sélectionnez l’icône d’horloge qui s’affiche au-dessus de la chronologie des événements.

![Le sélecteur de contraintes temporelles au niveau de la zone de travail est mis en surbrillance.](../images/ui/segment-builder/time-constraints/canvas-level.png)

Lorsque vous appliquez une contrainte temporelle au niveau de la zone de travail, celle-ci s’applique à tous les événements **1} de l’audience.**

#### Contrainte de niveau carte

Pour appliquer une contrainte de niveau carte, sélectionnez la carte sur laquelle vous souhaitez appliquer la contrainte de temps, suivie de l’icône représentant des ellipses, et de la **[!UICONTROL règle d’application de la durée]**. Vous pouvez ainsi sélectionner une contrainte temporelle dans le conteneur **[!UICONTROL Règles d’événement]**.

![Le sélecteur de contraintes temporelles de niveau carte est mis en surbrillance.](../images/ui/segment-builder/time-constraints/card-level.png)

Lorsque vous appliquez une contrainte temporelle au niveau de la carte, elle s’applique à l’événement **specified** dans l’audience.

#### Contrainte entre événements

Pour appliquer une contrainte temporelle entre les événements, sélectionnez l’icône d’horloge entre les deux événements sur lesquels vous souhaitez appliquer la contrainte temporelle.

![ Le sélecteur de contraintes de temps entre les événements est mis en surbrillance.](../images/ui/segment-builder/time-constraints/between-event.png)

Lorsque vous appliquez une contrainte temporelle entre l’événement, elle s’applique à la contrainte temporelle entre **et les événements.**

La liste des contraintes de temps disponibles pour cette opération diffère de la liste principale des contraintes de temps et se présente comme suit :

+++ Contraintes de temps disponibles

| Contrainte horaire | Description |
| --------------- | ----------- |
| Après | Le dernier événement **doit avoir lieu au moins** après l’événement précédent. |
| Within | Les deux événements **must** ont lieu pendant la période répertoriée dans la contrainte temporelle. |

>[!NOTE]
>
>Lors de l’utilisation de la contrainte de temps &quot;Après&quot;, ce dernier événement peut avoir lieu pendant plus de la durée indiquée dans la contrainte de temps. >
>Par exemple, si vous avez un événement Page vue et un événement Checkout (Passage en caisse) et que vous placez la contrainte temporelle &quot;Après 1 heure&quot; entre ces deux événements, une définition de segment avec un événement Checkout (Passage en caisse) 2 heures après l’événement Page vue est admissible.
>
>En outre, ces deux contraintes de temps peuvent être utilisées en coordination les unes avec les autres.
>
>Par exemple, si vous avez un événement Page vue et un événement Checkout (Passage en caisse) et que vous placez les contraintes de temps &quot;Après 1 heure&quot; et &quot;Dans les 24 heures&quot;, une définition de segment avec un événement Checkout (Passage en caisse) 12 heures après l’événement Page vue est admissible, mais une définition de segment avec un événement Checkout (Passage en caisse) 36 heures après l’événement Page vue ne peut pas être.

+++

## Conteneurs

Les règles de segmentation sont évaluées dans l’ordre dans lequel elles sont répertoriées. Les conteneurs permettent de contrôler l’ordre d’exécution grâce à l’utilisation de requêtes imbriquées.

Une fois que vous avez ajouté au moins une mosaïque à la zone de travail du créateur de règles, vous pouvez commencer à ajouter des conteneurs. Pour créer un nouveau conteneur, sélectionnez les points de suspension (...) dans le coin supérieur droit du volet, puis sélectionnez **[!UICONTROL Ajouter un conteneur]**.

![Le bouton « Ajouter un conteneur » est mis en surbrillance, ce qui vous permet d’ajouter un conteneur en tant qu’enfant du premier conteneur.](../images/ui/segment-builder/add-container.png)

Un nouveau conteneur apparaît comme la descendance du premier conteneur, mais vous pouvez réorganiser la hiérarchie en faisant glisser et en déplaçant les conteneurs. Le comportement par défaut d’un conteneur est d’« [!UICONTROL inclure] » l’attribut, l’audience ou l’événement fourni. Vous pouvez définir la règle pour « [!UICONTROL Exclure] » les profils qui correspondent aux critères du conteneur en sélectionnant **[!UICONTROL Inclure]** dans le coin supérieur gauche du volet et en sélectionnant « [!UICONTROL Exclure] ».

Un conteneur enfant peut également être extrait et intégré au conteneur parent en sélectionnant « Déplier le conteneur » dans le conteneur enfant. Sélectionnez les points de suspension (...) dans le coin supérieur droit du conteneur enfant pour accéder à cette option.

![Les options permettant de déplier ou de supprimer le conteneur sont mises en surbrillance.](../images/ui/segment-builder/include-exclude.png)

Après avoir selectionné **[!UICONTROL Déplier le conteneur]**, le conteneur enfant est supprimé et les critères intégrés apparaissent.

>[!NOTE]
>
>Lorsque vous extrayez des conteneurs, veillez à ce que la logique continue de correspondre à la définition de segment souhaitée.

![Le conteneur s’affiche après avoir été déplié.](../images/ui/segment-builder/unwrapped-container.png)

## Politiques de fusion

>[!CONTEXTUALHELP]
>id="platform_segmentation_createSegment_segmentBuilder_mergePolicies"
>title="Politiques de fusion"
>abstract="Une politique de fusion permet de fusionner les différents jeux de données pour former votre profil. Platform a fourni une politique de fusion par défaut ; vous pouvez également créer une politique de fusion par défaut dans les profils. Choisissez une politique de fusion correspondant à votre objectif marketing pour cette audience."

[!DNL Experience Platform] vous permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lors du regroupement de ces données, les politiques de fusion sont les règles utilisées par [!DNL Platform] pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer un profil.

Vous pouvez sélectionner une politique de fusion qui correspond à votre objectif marketing pour cette audience ou utiliser la politique de fusion par défaut fournie par [!DNL Platform]. Vous pouvez créer plusieurs politiques de fusion propres à votre organisation, y compris créer votre propre politique de fusion par défaut. Pour obtenir des instructions détaillées sur la création de politiques de fusion pour votre organisation, commencez par lire la [présentation des politiques de fusion](../../profile/merge-policies/overview.md).

Pour sélectionner une politique de fusion pour votre définition de segment, sélectionnez l’icône en forme d’engrenage dans l’onglet **[!UICONTROL Champs]**, puis utilisez le menu déroulant **[!UICONTROL Politique de fusion]** pour sélectionner la politique de fusion à utiliser.

![Le sélecteur de politique de fusion est mis en surbrillance. Vous pouvez ainsi choisir la stratégie de fusion à sélectionner pour votre définition de segment.](../images/ui/segment-builder/merge-policy-selector.png)

## Propriétés de définition de segment {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Propriétés de définition de segment"
>abstract="La section des propriétés de définition de segment affiche une estimation de la taille de la définition de segment résultante, en affichant le nombre de profils qualifiés par rapport au nombre total de profils. Cela vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Actualiser les estimations"
>abstract="Vous pouvez actualiser les estimations de votre définition de segment pour afficher immédiatement un aperçu du nombre de profils admissibles pour la définition de segment proposé. Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=fr#estimate-and-preview-an-audience" text="Estimation et prévisualisation d’une audience"

Lors de la création d’une définition de segment, la section **[!UICONTROL Propriétés de l’audience]** sur le côté droit de l’espace de travail affiche une estimation de la taille de la définition de segment résultante, ce qui vous permet d’ajuster votre définition de segment selon vos besoins avant de créer l’audience elle-même.

**[!UICONTROL Profils qualifiés]** indique le nombre **actuel** de profils qui correspondent aux règles de la définition de segment. Ce nombre est mis à jour toutes les 24 heures, après l’exécution de la tâche d’évaluation de segment.

L’horodatage des profils qualifiés indique la tâche d’évaluation de segment **batch** la plus récente et est **not** affiché pour les définitions de segment évaluées à l’aide de la segmentation par flux ou en périphérie. Si vous modifiez la définition de segment, le nombre de profils qualifiés reste le même jusqu’à l’exécution de la tâche d’évaluation de segment suivante.

**[!UICONTROL Profils estimés]** indique un nombre **approximatif** de profils en fonction de l’ **exemple de tâche**. Vous pouvez voir une version mise à jour de cette valeur après avoir ajouté de nouvelles règles ou conditions et sélectionné **[!UICONTROL Actualiser l’estimation]**. La sélection de la bulle d’informations donne le seuil d’erreur et l’exemple de temps de tâche le plus récent.

![ Les profils qualifiés et les profils estimés sont mis en surbrillance dans la section Propriétés de l’audience.](../images/ui/segment-builder/audience-estimates.png)

La section **[!UICONTROL Propriétés d’audience]** vous permet également de spécifier des informations importantes sur votre définition de segment, y compris son nom, sa description et son type d’évaluation. Les noms des définitions de segment sont utilisés pour identifier votre définition de segment parmi celles définies par votre organisation et doivent donc être descriptifs, concis et uniques.

Au fur et à mesure que vous continuez à créer votre définition de segment, vous pouvez visualiser un aperçu paginé de l’audience en sélectionnant **[!UICONTROL Afficher les profils]**.

![La section des propriétés de définition de segment est mise en surbrillance. Les propriétés de la définition de segment comportent, sans s’y limiter, le nom, la description et la méthode d’évaluation de la définition de segment.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Les estimations d’audience sont générées en utilisant une taille d’échantillon des données d’exemple du jour. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé ; entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées ; et pour plus de 20 millions d’entités, 5 % du total des entités est utilisé.
>
>En outre, cette estimation est basée sur la date de la dernière exécution de l’exemple de tâche de profil. Cela signifie que si vous utilisez une fonction de date relative telle que &quot;Aujourd’hui&quot; ou &quot;Cette semaine&quot;, l’estimation basera ses calculs sur le dernier exemple de temps d’exécution de tâche de profil. Par exemple, si nous sommes aujourd’hui le 24 janvier et que le dernier exemple de tâche de profil s’est exécuté le 22 janvier, la fonction de date relative &quot;Hier&quot; sera basée sur le 21 janvier et non le 23 janvier.
>
>Vous trouverez plus d’informations sur la génération d’estimations de définitions de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de définitions de segments.

Vous pouvez également sélectionner votre méthode d’évaluation. Si vous savez quelle méthode d’évaluation vous voulez utiliser, vous pouvez sélectionner la méthode d’évaluation souhaitée à l’aide de la liste déroulante. Si vous souhaitez savoir pour quels types d’évaluation cette définition de segment est admissible, vous pouvez sélectionner l’icône Parcourir ![icône de dossier avec une loupe](/help/images/icons/folder-search.png) pour voir la liste des méthodes d’évaluation de définition de segment disponibles.

L’[!UICONTROL Éligibilité de la méthode d’évaluation] s’affiche. Cette fenêtre contextuelle affiche les méthodes d’évaluation disponibles, à savoir par lots, en flux continu et Edge. La fenêtre contextuelle affiche les méthodes d’évaluation éligibles et non éligibles. Selon les paramètres que vous avez utilisés dans votre définition de segment, il se peut qu’elle ne soit pas admissible pour certaines méthodes d’évaluation. Pour plus d’informations sur les exigences de chaque méthode d’évaluation, veuillez lire les présentations sur la [segmentation en flux continu](./streaming-segmentation.md#query-types) ou la [segmentation Edge](./edge-segmentation.md#query-types).

Vous pouvez également modifier la méthode d’évaluation de la définition de segment une fois que vous avez fini de la créer. Si vous changez la méthode d’évaluation d’Edge ou de Streaming en Batch, vous ne pourrez **pas** la redéfinir sur Edge ou Streaming. La modification de la méthode d’évaluation prend effet **uniquement** une fois que vous avez sélectionné **[!UICONTROL Enregistrer]** dans la fenêtre contextuelle. L’annulation de la boîte de dialogue **conserve** la méthode d’évaluation d’origine.

![La fenêtre contextuelle d’éligibilité de la méthode d’évaluation s’affiche. Elle affiche les méthodes d’évaluation éligibles et non éligibles pour la définition de segment.](../images/ui/segment-builder/select-evaluation-method.png)

Si vous sélectionnez une méthode d’évaluation non valide, vous serez invité à modifier vos règles de définition de segment ou la méthode d’évaluation.

![La fenêtre contextuelle de méthode d’évaluation s’affiche. Si une méthode d’évaluation non éligible est sélectionnée, la fenêtre contextuelle explique pourquoi celle-ci n’est pas éligible.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Vous trouverez plus d’informations sur les différentes méthodes d’évaluation de définition de segment dans la [présentation de la segmentation](../home.md#evaluate-segments).

## Étapes suivantes {#next-steps}

Le créateur de segments fournit un workflow complet qui vous permet d’isoler les audiences commercialisables des données [!DNL Real-Time Customer Profile]. Après avoir lu ce guide, vous devriez maintenant pouvoir :

- créer des définitions de segment en utilisant une combinaison d’attributs, d’événements et d’audiences existants comme blocs de création ;
- utiliser les conteneurs et les zones de travail du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation ;
- visualiser les estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins ;
- activer toutes les définitions de segment pour la segmentation planifiée ;
- activer des définitions de segment spécifiques pour la segmentation par flux.

Pour en savoir plus sur [!DNL Segmentation Service], veuillez continuer à lire la documentation et compléter votre apprentissage en regardant les vidéos associées. Pour en savoir plus sur les autres parties de l’interface utilisateur de [!DNL Segmentation Service], veuillez lire le [[!DNL Segmentation Service] guide de l’utilisateur](./overview.md).
