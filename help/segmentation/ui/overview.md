---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’interface utilisateur du créateur de segments
topic: ui guide
translation-type: tm+mt
source-git-commit: 91792f81a50d5752e46236d61b6ad645e3fda86c
workflow-type: tm+mt
source-wordcount: '2349'
ht-degree: 0%

---


# Guide d’utilisation du créateur de segments

Le service de segmentation de la plateforme Adobe Experience Platform fournit une API RESTful et une interface utilisateur pour la création de définitions de segment à partir des données du Profil client en temps réel.

## Prise en main

L’utilisation des définitions de segment nécessite une compréhension des différents services de la plate-forme d’expérience impliqués dans la segmentation. Avant de lire ce guide d&#39;utilisation, consultez la documentation relative aux services suivants :

- [Service](../home.md)de segmentation : Le service de segmentation vous permet de diviser les données stockées dans la plateforme d’expérience qui se rapportent à des individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits qui partagent des caractéristiques similaires et réagissent de la même manière aux stratégies marketing.
- [Profil](../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Service](../../identity-service/home.md)d&#39;identité : Permet le Profil client en temps réel en rapprochant les identités des sources de données disparates qui sont incorporées dans la plate-forme.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Il est également important de connaître deux termes clés qui sont utilisés dans ce document et de comprendre la différence entre eux :
- **Définition** de segment : Jeu de règles utilisé pour décrire les principales caractéristiques ou comportements d’une audience de cible.
- **Audience**: Ensemble de profils résultant qui répond aux critères d’une définition de segment.

## Accès aux définitions de segment

Pour commencer à utiliser les définitions de segment dans Adobe Experience Platform, cliquez sur **Segments** dans le volet de navigation de gauche. Pour afficher toutes les définitions de segment pour votre organisation, cliquez sur l’onglet *Parcourir* . Cette vue liste des informations sur la définition de segment, y compris la méthode d’évaluation, la date de création et la date de dernière modification.

La méthode d’évaluation peut être en flux continu ou par lot. Les segments de diffusion en continu sont constamment évalués à mesure que les données entrent dans le système. Les segments de lot sont évalués selon un calendrier défini.

Des informations supplémentaires s’affichent sur les segments de lot, indiquant à la fois la dernière date d’évaluation et la prochaine date d’évaluation du lot.

Cliquez sur **Créer un segment** dans le coin supérieur droit pour ouvrir l’espace de travail Créateur de segments, où vous pouvez commencer à créer une définition de segment.

![](../images/segment-builder/segment-browse.png)

## Espace de travail du créateur de segments

Le créateur de segments offre un espace de travail enrichi qui vous permet d’interagir avec des éléments de données de Profil. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que les mosaïques de glisser-déposer utilisées pour représenter les propriétés des données.

![](../images/segment-builder/segment-builder.png)

## Blocs de création de définitions de segment

Les éléments de base des définitions de segment sont **Attributs** et **Événements**. En outre, les attributs et les événements contenus dans les **Audiences** existantes peuvent également servir de composants pour de nouvelles définitions.

Vous pouvez voir ces blocs de construction dans la section *Champs* située sur le côté gauche de l’espace de travail Créateur de segments. *Les champs* contiennent un onglet pour chacun des blocs de construction principaux : **Attributs**, **Événements** et **Audiences**.

![](../images/segment-builder/segment-fields.png)

### Attributs

L&#39;onglet **Attributs** vous permet de parcourir les attributs de Profil appartenant à la classe de Profil XDM Individuel. Chaque dossier peut être développé pour afficher d’autres attributs, où chaque attribut est une mosaïque qui peut être glissée sur le canevas du créateur de règles au centre de l’espace de travail. Le canevas [du créateur de](#rule-builder-canvas) règles est décrit plus en détail plus loin dans ce guide.

![](../images/segment-builder/attributes.png)

### Événements

L&#39;onglet **Événements** vous permet de créer une audience basée sur des événements ou actions qui ont eu lieu à l&#39;aide des éléments de données XDM ExperienceEvent. Vous pouvez également trouver des Types d&#39;événement dans l’onglet **Événements** , qui sont un ensemble de événements couramment utilisés pour vous permettre de créer vos segments plus rapidement.

Outre la possibilité de rechercher des éléments ExperienceEvent, vous pouvez également rechercher des Types d&#39;événement. Les Types d&#39;événement utilisent la même logique de codage qu’ExperienceEvents, sans que vous ayez à rechercher le événement approprié dans la classe XDM ExperienceEvent. Par exemple, l’utilisation de la barre de recherche pour rechercher &quot;panier&quot; renvoie les Types d&#39;événement &quot;AddCart&quot; et &quot;RemoveCart&quot;, deux actions de panier très couramment utilisées lors de la création de définitions de segment.

Vous pouvez rechercher n’importe quel type de composant en entrant son nom dans la barre de recherche, qui utilise la syntaxe [de recherche de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Les résultats de la recherche commencent à être renseignés à mesure que des mots entiers sont saisis. Par exemple, pour créer une règle basée sur le champ XDM `ExperienceEvent.commerce.productViews`, début de saisir &quot;vues de produit&quot; dans le champ de recherche. Une fois le mot &quot;produit&quot; saisi, les résultats de la recherche commencent à apparaître. Chaque résultat inclut la hiérarchie d’objets à laquelle il appartient.

>[!NOTE] Les champs de schéma personnalisés définis par votre organisation peuvent prendre jusqu’à 24 heures pour apparaître et devenir disponibles pour une utilisation dans les règles de création.

Vous pouvez ensuite facilement faire glisser des événements d’expérience et des Types d&#39;événement dans votre définition de segment.

![](../images/segment-builder/events-eventTypes.png)

Par défaut, seuls les champs de schéma renseignés de votre banque de données s’affichent. Cela inclut les Types d&#39;événement. Si la liste de Types d&#39;événement n&#39;est pas visible ou si vous ne pouvez sélectionner &quot;N&#39;importe quel&quot; que comme Type d&#39;événement, cliquez sur l&#39;icône d&#39;engrenage en regard de *Champs*, puis sélectionnez **Afficher le schéma** XDM complet sous Champs ** disponibles. Cliquez de nouveau sur l’icône d’engrenage pour revenir à l’onglet *Champs* et vous devez maintenant pouvoir vue plusieurs champs de Type d&#39;événement et de schéma, qu’ils contiennent ou non des données.

![](../images/segment-builder/show-populated.png)

### Audiences

L’onglet **Audiences** liste toutes les audiences importées à partir de sources externes, telles qu’Adobe Audience Manager, ainsi que les audiences créées dans Experience Platform.

Dans l’onglet Audiences, vous pouvez voir toutes les sources disponibles sous la forme d’un groupe de dossiers. Lorsque vous cliquez dans ces dossiers, les sous-dossiers et audiences disponibles s’affichent. De plus, vous pouvez cliquer sur l&#39;icône de dossier (comme illustré dans l&#39;image à l&#39;extrême droite) pour vue de la structure de dossiers (une coche indique le dossier dans lequel vous vous trouvez actuellement) et parcourir facilement les dossiers en cliquant sur le nom d&#39;un dossier dans l&#39;arborescence.

Vous pouvez placer le pointeur de la souris sur le ⓘ en regard d’une audience à des informations de vue sur l’audience, y compris son identifiant, sa description et la hiérarchie de dossiers pour localiser l’audience.

![](../images/segment-builder/audience-folder-structure.png)

Vous pouvez également rechercher des Audiences à l&#39;aide de la barre de recherche, qui utilise la syntaxe [de recherche de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Dans l’onglet *Audiences* , la sélection d’un dossier de niveau supérieur entraîne l’affichage de la barre de recherche, ce qui vous permet d’effectuer des recherches dans ce dossier. Les résultats de la recherche ne commencent à être renseignés qu&#39;une fois des mots entiers saisis. Par exemple, pour trouver une Audience nommée `Online Shoppers`, début de saisie &quot;En ligne&quot; dans la barre de recherche. Une fois le mot &quot;Online&quot; saisi dans son intégralité, les résultats de la recherche contenant le mot &quot;Online&quot; apparaissent.

## Canevas du créateur de règles

Une définition de segment est un ensemble de règles utilisées pour décrire les principales caractéristiques ou le comportement d’une audience de cible. Ces règles sont créées à l’aide du canevas *du créateur de* règles, situé au centre du créateur de segments.

Pour ajouter une nouvelle règle à votre définition de segment, faites glisser une mosaïque de l’onglet *Champs* et déposez-la sur le canevas du créateur de règles. Des options spécifiques au contexte vous seront ensuite présentées en fonction du type de données à ajouter. Les types de données disponibles sont les suivants : chaînes, dates, événements d’expérience, Types d&#39;événement et Audiences.

![](../images/segment-builder/rule-builder-canvas.png)

### Ajout d’audiences

Vous pouvez faire glisser une audience de l’onglet *Audience* sur le canevas du créateur de règles pour référencer l’appartenance à l’audience dans la nouvelle définition de segment. Cela vous permet d’inclure ou d’exclure l’appartenance à une audience en tant qu’attribut dans la nouvelle règle de segment.

Pour les audiences de plateformes créées à l’aide du créateur de segments, vous avez la possibilité de convertir l’audience en jeu de règles utilisées dans la définition de segment pour cette audience. Cette conversion effectue une copie de la logique de règle, qui peut ensuite être modifiée sans affecter la définition de segment d’origine.

>[!NOTE] Lors de l’ajout d’une audience provenant d’une source externe, seul l’appartenance à l’audience est référencée. Vous ne pouvez pas convertir l’audience en règles. Par conséquent, les règles utilisées pour créer l’audience d’origine ne peuvent pas être modifiées dans la nouvelle définition de segment.

![](../images/segment-builder/add-audience-to-segment.png)

## Conteneurs

Les règles de segment sont évaluées dans l’ordre dans lequel elles sont répertoriées. Les Conteneurs permettent de contrôler l’ordre d’exécution à l’aide de requêtes imbriquées.

Une fois que vous avez ajouté au moins une mosaïque au canevas du créateur de règles, vous pouvez commencer à ajouter des conteneurs. Pour créer un conteneur, cliquez sur les ellipses (...) dans le coin supérieur droit de la mosaïque, puis cliquez sur **Ajouter conteneur**.

![](../images/segment-builder/add-container.png)

Un nouveau conteneur s’affiche en tant qu’enfant du premier conteneur, mais vous pouvez ajuster la hiérarchie en faisant glisser et en déplaçant les conteneurs. Le comportement par défaut d’un conteneur consiste à &quot;Inclure&quot; l’attribut, le événement ou l’audience fourni. Vous pouvez définir la règle sur &quot;Exclure&quot; les profils qui correspondent aux critères du conteneur en cliquant sur **Inclure** dans le coin supérieur gauche du volet et en sélectionnant &quot;Exclure&quot;.

Un conteneur enfant peut également être extrait et ajouté en ligne au conteneur parent en cliquant sur &quot;Annuler le renvoi à la ligne&quot; sur le conteneur enfant. Cliquez sur les ellipses (...) dans le coin supérieur droit du conteneur enfant pour accéder à cette option.

![](../images/segment-builder/include-exclude.png)

Une fois que vous avez cliqué sur **Annuler le renvoi à la ligne du conteneur** , le conteneur enfant est supprimé et les critères apparaissent en ligne.

>[!NOTE] Lorsque vous décompressez des conteneurs, veillez à ce que la logique continue de respecter la définition de segment souhaitée.

![](../images/segment-builder/unwrapped-container-inline.png)

## Stratégies de fusion

Experience Platform vous permet de rassembler des données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer un profil.

Vous pouvez sélectionner une stratégie de fusion correspondant à votre objectif marketing pour cette audience ou utiliser la stratégie de fusion par défaut fournie par Platform. Vous pouvez créer plusieurs stratégies de fusion propres à votre organisation, y compris la création de votre propre stratégie de fusion par défaut. Pour obtenir des instructions détaillées sur la création de stratégies de fusion pour votre entreprise, consultez le didacticiel sur l’ [utilisation de stratégies de fusion à l’aide de l’interface utilisateur](../../profile/ui/merge-policies.md).

Pour sélectionner une stratégie de fusion pour votre définition de segment, cliquez sur l&#39;icône d&#39;engrenage dans l&#39;onglet *Champs* , puis utilisez le menu *déroulant Stratégie de* fusion pour sélectionner la stratégie de fusion que vous souhaitez utiliser.

![](../images/segment-builder/merge-policy-selector.png)

## Propriétés de segment

Lors de la création d’une définition de segment, la section Propriétés *du* segment sur le côté droit de l’espace de travail affiche une estimation de la taille du segment résultant, ce qui vous permet d’ajuster la définition de segment en fonction des besoins avant de créer l’audience elle-même.

La section Propriétés *du* segment permet également de spécifier des informations importantes sur la définition de segment, notamment son *nom* et sa *description*. Les noms de définition de segment sont utilisés pour identifier votre segment parmi ceux définis par votre organisation et doivent donc être descriptifs, concis et uniques.

Au fur et à mesure que vous créez votre définition de segment, vous pouvez vue une prévisualisation paginée de l’audience en sélectionnant des Profils **de** Vue.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] Les estimations des Audiences sont générées à l’aide d’une taille d’échantillon des données d’échantillon de cette journée. S&#39;il y a moins d&#39;un million d&#39;entités dans votre magasin de profils, l&#39;ensemble complet de données est utilisé ; entre 1 et 20 millions d&#39;entités, 1 million d&#39;entités sont utilisées ; et pour plus de 20 millions d&#39;entités, 5 % du total des entités sont utilisées. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la section [Génération d’](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) estimations du didacticiel sur la création de segments.

## Activer la segmentation planifiée

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation à la demande ou programmée (continue). L’évaluation consiste à déplacer les données du Profil client en temps réel au moyen de définitions de segment afin de produire des audiences correspondantes. Une fois créées, les audiences sont enregistrées et stockées afin de pouvoir être exportées à l’aide des API de plateforme d’expérience.

L’évaluation à la demande implique l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, tandis que l’évaluation planifiée (également appelée &quot;segmentation planifiée&quot;) vous permet de créer un calendrier récurrent pour évaluer les définitions de segment à un moment spécifique (au maximum une fois par jour).

Vous pouvez activer les définitions de segment pour l’évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. Dans l’interface utilisateur, revenez à l’onglet *Parcourir* dans **Segments** et basculez sur **Évaluer tous les segments**. De ce fait, tous les segments seront évalués en fonction du planning défini par votre organisation.

>[!NOTE] L’évaluation planifiée peut être activée pour les sandbox avec un maximum de cinq (5) stratégies de fusion pour un Profil XDM individuel. Si votre entreprise dispose de plus de cinq stratégies de fusion pour un Profil XDM individuel dans un seul environnement de sandbox, vous ne pourrez pas utiliser l’évaluation planifiée.

Actuellement, les calendriers ne peuvent être créés qu&#39;à l&#39;aide de l&#39;API. Pour obtenir des instructions détaillées sur la création, la modification et l&#39;utilisation des planifications à l&#39;aide de l&#39;API, suivez le didacticiel d&#39;évaluation et d&#39;accès aux résultats des segments, en particulier la section sur l&#39;évaluation [planifiée à l&#39;aide de l&#39;API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Activer la segmentation en flux continu

>[!NOTE] La segmentation en flux continu est une fonctionnalité bêta, disponible sur demande.

En outre, une définition de segment peut être activée pour la segmentation en flux continu avant ou après sa création. La segmentation en flux continu évalue instantanément un client dès qu’un événement arrive dans un groupe de segments particulier. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées lorsque les données sont transmises à la plate-forme, ce qui signifie que l’appartenance à un segment est tenue à jour sans exécuter les tâches de segmentation planifiées. Pour plus d’informations sur la segmentation en flux continu, consultez la documentation [sur la segmentation en](../api/streaming-segmentation.md)flux continu.

Vous pouvez activer les définitions de segment pour la diffusion en continu à l’aide de l’interface utilisateur ou de l’API. Pour activer une nouvelle définition de segment ou une définition de segment existante pour la diffusion en continu dans l’interface utilisateur, vous devez activer l’option *Diffusion en continu* sur **ON**.

![](../images/segment-builder/enable-streaming-segmentation.png)

Une fois la segmentation en flux continu activée, une ligne de base doit être définie (il s’agit de l’exécution initiale après laquelle le segment sera toujours à jour). Le système gère automatiquement la segmentation, mais cela n&#39;est possible que si la segmentation planifiée a été activée. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à [la section précédente de ce guide](#enable-scheduled-segmentation)d’utilisateur.

## Violations de stratégie de DUM

>[!NOTE] Les violations de stratégie DULE ne s&#39;appliquent que si vous créez un segment qui a été affecté à une destination.

Une fois le segment créé, il est analysé par la gouvernance des données afin de s’assurer qu’il n’y a aucune violation de stratégie dans le segment. Pour plus d&#39;informations sur les violations de DULE et de stratégie, reportez-vous à la présentation [des étiquettes d&#39;utilisation des](../../data-governance/labels/overview.md)données.

![](../images/segment-builder/segment-dule-policy-violations.png)

## Étapes suivantes

Le créateur de segments offre un flux de travail riche qui vous permet d’isoler les audiences commercialisables des données de Profil client en temps réel. Après avoir lu ce guide, vous devez maintenant pouvoir :

- Créez des définitions de segment à l’aide d’une combinaison d’attributs, de événements et d’audiences existantes en tant que blocs de création.
- Utilisez le canevas et les conteneurs du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation.
- Estimation des Vues de votre audience potentielle, ce qui vous permet d&#39;ajuster les définitions de segment selon vos besoins.
- Activez toutes les définitions de segment pour la segmentation planifiée.
- Activez les définitions de segment spécifiées pour la segmentation en flux continu.

Pour obtenir des instructions détaillées sur l’utilisation du service de segmentation à l’aide de l’API Profil client en temps réel, consultez le didacticiel [Création de segments d’audience à l’aide d’API](../tutorials/create-a-segment.md) .