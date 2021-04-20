---
keywords: Experience Platform ; accueil ; rubriques populaires ; ui ; IU ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; éditeur de schémas ; éditeur de Schémas ; schéma ; Schéma ; schémas ; Schémas ; créer
solution: Experience Platform
title: Création d’un Schéma à l’aide de l’éditeur de Schéma
topic: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes de création d’un schéma à l’aide de l’éditeur de schémas d’Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
translation-type: tm+mt
source-git-commit: 53bf2ad757b24ad294af32101124e8047580807a
workflow-type: tm+mt
source-wordcount: '3683'
ht-degree: 17%

---

# Créez un schéma à l’aide de l’[!DNL Schema Editor]

L&#39;interface utilisateur de Adobe Experience Platform vous permet de créer et de gérer des schémas [!DNL Experience Data Model] (XDM) dans une trame visuelle interactive appelée [!DNL Schema Editor]. Ce didacticiel explique comment créer un schéma à l&#39;aide de [!DNL Schema Editor].

>[!NOTE]
>
>À des fins de démonstration, les étapes de ce didacticiel impliquent la création d’un exemple de schéma décrivant les membres d’un programme de fidélité de la clientèle. Bien que vous puissiez utiliser ces étapes pour créer un schéma différent pour vos propres besoins, il est recommandé de commencer par créer l&#39;exemple de schéma pour découvrir les fonctionnalités de [!DNL Schema Editor].

Si vous préférez composer un schéma à l&#39;aide de l&#39;API [!DNL Schema Registry], début en lisant le [[!DNL Schema Registry] guide du développeur](../api/getting-started.md) avant d&#39;essayer le didacticiel sur [la création d&#39;un schéma à l&#39;aide de l&#39;API](create-schema-api.md).

## Prise en main

Ce tutoriel exige une compréhension pratique des différents aspects de Adobe Experience Platform impliqués dans la création de schémas. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux concepts suivants :

* [[!DNL Experience Data Model (XDM)]](../home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../schema/composition.md) : présentation des schémas XDM et de leurs blocs de création, notamment les classes, les mixins, les types de données et les champs.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

## Ouvrez l&#39;espace de travail [!UICONTROL Schémas] {#browse}.

L&#39;espace de travail [!UICONTROL Schémas] de l&#39;interface utilisateur [!DNL Platform] fournit une visualisation du [!DNL Schema Library], ce qui vous permet de gérer les schémas disponibles pour votre organisation par vue. L’espace de travail comprend également le canevas [!DNL Schema Editor], sur lequel vous pouvez composer un schéma tout au long de ce didacticiel.

Après vous être connecté à [!DNL Experience Platform], sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l&#39;espace de travail **[!UICONTROL Schémas]**. L&#39;onglet **[!UICONTROL Parcourir]** affiche une liste de schémas (une représentation de [!DNL Schema Library]) que vous pouvez vue et personnaliser. La liste comprend le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels repose le schéma, ainsi que la date et l’heure de la dernière modification du schéma.

Pour plus d&#39;informations, consultez le guide [exploration des ressources XDM existantes dans l&#39;interface utilisateur](../ui/explore.md).

## Création et attribution d’un nom à un schéma {#create}

Pour commencer à composer un schéma, sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l&#39;espace de travail **[!UICONTROL Schémas]**. Un menu déroulant s&#39;affiche, vous permettant de choisir entre les classes de base [!UICONTROL XDM Individuel Profil] et [!UICONTROL XDM ExperienceEvent]. Si ces classes ne répondent pas à vos besoins, vous pouvez également sélectionner **[!UICONTROL Parcourir]** pour choisir parmi d&#39;autres classes disponibles ou [créer une nouvelle classe](#create-new-class).

Pour les besoins de ce didacticiel, sélectionnez **[!UICONTROL Profil individuel XDM]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Puisque vous avez choisi une classe XDM standard pour baser le schéma, la boîte de dialogue **[!UICONTROL Ajouter mixin]** s&#39;affiche, ce qui vous permet de immédiatement début en ajoutant des champs au schéma. Pour l’instant, sélectionnez **[!UICONTROL Annuler]** pour quitter la boîte de dialogue.

![](../images/tutorials/create-schema/cancel-mixin.png)

Le [!DNL Schema Editor] apparaît. C’est le canevas sur lequel vous allez composer votre schéma. Un schéma sans titre est automatiquement créé dans la section **[!UICONTROL Structure]** du canevas lorsque vous arrivez dans l’éditeur, avec les champs standard inclus dans tous les schémas en fonction de cette classe. La classe affectée au schéma est également répertoriée sous **[!UICONTROL Classe]** dans la section **[!UICONTROL Composition]**.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Vous pouvez [modifier la classe d’un schéma](#change-class) à tout moment au cours du processus de composition initial avant que le schéma ne soit enregistré, mais cela doit être fait avec la plus grande prudence. Les mixins ne sont compatibles qu&#39;avec certaines classes. Par conséquent, modifier la classe réinitialise le canevas et les champs que vous avez ajoutés.

Utilisez les champs situés à droite de l’éditeur pour fournir un nom d’affichage et une description facultative du schéma. Une fois qu’un nom est saisi, le canevas se met à jour pour tenir compte du nouveau nom du schéma.

![](../images/tutorials/create-schema/name_schema.png)

Plusieurs éléments importants doivent être pris en compte lors du choix d’un nom pour votre schéma :

* Les noms des schémas doivent être courts et descriptifs afin que le schéma puisse être facilement trouvé plus tard.
* Le nom d’un schéma doit être unique, ce qui signifie qu’il doit également être suffisamment précis pour ne pas être réutilisé à l’avenir. Par exemple, si votre organisation dispose de programmes de fidélité distincts pour différentes marques, nous vous conseillons de nommer votre schéma « Brand A Loyalty Members » pour faciliter la distinction avec d’autres schémas relatifs à la fidélité que vous pourriez définir ultérieurement.
* Vous pouvez également utiliser la description du schéma pour fournir toute information contextuelle supplémentaire concernant le schéma.

Ce didacticiel compose un schéma d’assimilation de données relatives aux membres d’un programme de fidélité. Par conséquent, le schéma est nommé &quot;Membres de fidélité&quot;.

## Ajout d’un mixin {#mixin}

Vous pouvez maintenant commencer à ajouter des champs à votre schéma grâce à l’ajout de mixins. Un mixin est un groupe d’un ou de plusieurs champs qui sont souvent utilisés ensemble pour décrire un concept particulier. Ce tutoriel utilise des mixins pour décrire les membres du programme de fidélité et recueillir des informations clés telles que le nom, la date d’anniversaire, le numéro de téléphone, l’adresse, etc.

Pour ajouter un mixin, sélectionnez **[!UICONTROL Ajouter]** dans la sous-section **[!UICONTROL Mixins]**.

![](../images/tutorials/create-schema/add_mixin_button.png)

Une nouvelle boîte de dialogue s’affiche, affichant une liste de mixins disponibles. Chaque mixin n&#39;est destiné qu&#39;à une classe spécifique. Par conséquent, la boîte de dialogue ne liste que les mixins compatibles avec la classe que vous avez sélectionnée (dans ce cas, la classe [!DNL XDM Individual Profile]). Si vous utilisez une classe XDM standard, la liste des mixins sera triée intelligemment en fonction de la popularité de l’utilisation.

![](../images/tutorials/create-schema/mixin-popularity.png)

Si vous sélectionnez un mixin dans la liste, il apparaît dans le rail de droite. Vous pouvez sélectionner plusieurs mixins si vous le souhaitez, en ajoutant chacun à la liste dans le rail de droite avant de confirmer. En outre, une icône s’affiche sur le côté droit du mixin actuellement sélectionné, ce qui vous permet de prévisualisation de la structure des champs fournis.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Lors de la prévisualisation d&#39;un mixin, une description détaillée du schéma du mixin est fournie dans le rail droit. Vous pouvez également parcourir les champs du mixin dans la trame fournie. Lorsque vous sélectionnez différents champs, le rail de droite se met à jour pour afficher des détails sur le champ en question. Sélectionnez **[!UICONTROL Précédent]** lorsque vous avez terminé de prévisualiser pour revenir à la boîte de dialogue de sélection du mixin.

![](../images/tutorials/create-schema/preview-mixin.png)

Pour ce didacticiel, sélectionnez le mixin **[!UICONTROL Détails démographiques]**, puis **[!UICONTROL Ajouter le mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Le canevas du schéma réapparaît. La section **[!UICONTROL Mixins]** liste désormais &quot;[!UICONTROL Détails démographiques]&quot; et la section **[!UICONTROL Structure]** comprend les champs fournis par le mixin. Vous pouvez sélectionner le nom du mixin sous la section **[!UICONTROL Mixins]** pour mettre en surbrillance les champs spécifiques qu’il fournit dans la trame.

![](../images/tutorials/create-schema/person_details_structure.png)

Ce mixin fournit plusieurs champs sous le nom de niveau supérieur `person` avec le type de données &quot;[!UICONTROL Personne]&quot;. Ce groupe de champs décrit les informations sur un individu, notamment son nom, sa date de naissance et son genre.

>[!NOTE]
>
>Rappelez-vous que les champs peuvent utiliser des types scalaires (tels que chaîne, entier, tableau ou date), ainsi que tout type de données (un groupe de champs représentant un concept commun) défini dans [!DNL Schema Registry].

Notez que le champ `name` possède un type de données &quot;[!UICONTROL Nom de personne]&quot;, ce qui signifie qu’il décrit également un concept commun et qu’il contient des sous-champs liés aux noms tels que prénom, nom, titre de politesse et suffixe.

Sélectionnez les différents champs de la zone de travail pour afficher les champs supplémentaires qui contribuent à la structure du schéma.

## Ajout d’un autre mixin {#mixin-2}

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre mixin. Lorsque vous vue cette fois la boîte de dialogue **[!UICONTROL Ajouter le mixin]**, notez que le mixin &quot;[!UICONTROL Détails démographiques]&quot; a été grisé et que la case à cocher située en regard de celui-ci ne peut pas être sélectionnée. Cela vous évite de dupliquer accidentellement des mixins que vous avez déjà inclus dans le schéma actuel.

Pour ce didacticiel, sélectionnez le mixin &quot;[!DNL Personal Contact Details]&quot; dans la boîte de dialogue, puis sélectionnez **[!UICONTROL Ajouter le mixin]** pour l’ajouter au schéma.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Une fois ajouté, le canevas réapparaît. &quot;[!UICONTROL Détails du contact personnel]&quot; est maintenant répertorié sous **[!UICONTROL Mixins]** dans la section **[!UICONTROL Composition]**, et les champs pour l&#39;adresse de domicile, le téléphone portable, et plus ont été ajoutés sous **[!UICONTROL Structure]**.

Tout comme le champ `name`, les champs que vous venez d’ajouter représentent des concepts à plusieurs champs. Par exemple, `homeAddress` possède un type de données &quot;[!UICONTROL Adresse postale]&quot; et `mobilePhone` un type de données &quot;[!UICONTROL Numéro de téléphone]&quot;. Vous pouvez sélectionner chacun de ces champs pour les développer et afficher les champs supplémentaires inclus dans le type de données.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Définir un mixin personnalisé {#define-mixin}

Le schéma &quot;[!UICONTROL Membres de fidélité]&quot; est destiné à capturer les données relatives aux membres d&#39;un programme de fidélité. Il nécessite donc certains champs spécifiques liés à la fidélité.

Il existe un mixin [!UICONTROL Détails de fidélité] standard que vous pouvez ajouter au schéma pour capturer des champs communs liés à un programme de fidélité. Bien que vous soyez fortement encouragé à utiliser des mixins standard pour représenter des concepts capturés par vos schémas, la structure du mixin de fidélité standard peut ne pas être en mesure de capturer toutes les données pertinentes pour votre programme de fidélité particulier. Dans ce scénario, vous pouvez choisir de définir un nouveau mixin personnalisé pour capturer ces champs à la place.

Ouvrez à nouveau la boîte de dialogue **[!UICONTROL Ajouter le mixin]**, mais cette fois, sélectionnez **[!UICONTROL Créer un nouveau mixin]** près du haut. Vous êtes alors invité à fournir un nom d’affichage et une description pour votre mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Comme pour les noms de classe, le nom du mixin doit être court et simple, décrivant ce que le mixin va apporter au schéma. Ces noms sont également uniques. Vous ne pourrez donc pas réutiliser le nom et devrez donc veiller à ce qu’il soit suffisamment spécifique.

Pour ce tutoriel, nommez le nouveau mixin « Loyalty Details ».

Sélectionnez **[!UICONTROL Ajouter le mixin]** pour revenir au [!DNL Schema Editor]. &quot;[!UICONTROL Les détails de fidélité]&quot; doivent maintenant apparaître sous **[!UICONTROL Mixins]** à gauche du canevas, mais aucun champ n&#39;y est associé pour le moment et, par conséquent, aucun nouveau champ n&#39;apparaît sous **[!UICONTROL Structure]**.

## Ajout de champs au mixin {#mixin-fields}

Maintenant que vous avez créé le mixin « Loyalty Details », il est temps de définir les champs que le mixin va ajouter au schéma.

Pour commencer, sélectionnez le nom du mixin dans la section **[!UICONTROL Mixins]**. Une fois que vous avez effectué cette opération, les propriétés du mixin s’affichent sur le côté droit de l’éditeur et une icône **plus (+)** apparaît en regard du nom du schéma sous **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Sélectionnez l&#39;icône **plus (+)** en regard de &quot;[!DNL Loyalty Members]&quot; pour créer un nouveau noeud dans la structure. Ce noeud (appelé `_tenantId` dans cet exemple) représente l’ID de client de votre organisation IMS, précédé d’un trait de soulignement. La présence de l’identifiant du client indique que les champs que vous ajoutez sont contenus dans l’espace de noms de votre organisation.

En d’autres termes, les champs que vous ajoutez sont propres à votre organisation et seront enregistrés dans [!DNL Schema Registry] dans une zone spécifique accessible uniquement à votre organisation. Les champs que vous définissez doivent toujours être ajoutés à votre espace de nommage locataire afin d’éviter les collisions avec des noms provenant d’autres classes standard, mixins, types de données et champs.

À l’intérieur de ce noeud, l’espace de noms est un &quot;[!UICONTROL Nouveau champ]&quot;. Il s’agit du début du mixin &quot;[!UICONTROL Détails de fidélité]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

En utilisant les contrôles sur le côté droit de l’éditeur, début en créant un champ `loyalty` de type &quot;[!UICONTROL Objet]&quot; qui sera utilisé pour contenir vos champs liés à la fidélité. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Les modifications sont appliquées et l&#39;objet `loyalty` nouvellement créé s&#39;affiche. Sélectionnez l’icône **plus (+)** en regard de l’objet pour ajouter d’autres champs liés à la fidélité. Un &quot;[!UICONTROL Nouveau champ]&quot; apparaît et la section **[!UICONTROL Propriétés du champ]** est visible sur le côté droit de la trame.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Chaque champ nécessite les informations suivantes :

* **[!UICONTROL Nom] du champ :** nom du champ, écrit dans la casse du chameau. Exemple : loyaltyLevel
* **[!UICONTROL Nom] d’affichage :** nom du champ, écrit en casse de titre. Exemple : Loyalty Level
* **[!UICONTROL Type] :** type de données du champ. Cela inclut les types scalaires de base et tous les types de données définis dans [!DNL Schema Registry]. Exemples : [!UICONTROL Chaîne], [!UICONTROL Entier], [!UICONTROL Boolean], [!UICONTROL Personne], [!UICONTROL Adresse], [!UICONTROL Numéro de téléphone], etc.
* **[!UICONTROL Description] :** Une description facultative du champ doit être incluse, écrite en cas de phrase, avec un maximum de 200 caractères.

Le premier champ de l&#39;objet `Loyalty` sera une chaîne appelée `loyaltyId`. Lorsque vous définissez le type du nouveau champ sur &quot;[!UICONTROL String]&quot;, la section **[!UICONTROL Propriétés du champ]** devient renseignée avec plusieurs options pour appliquer des contraintes, notamment la valeur par défaut, le format et la longueur maximale.

![](../images/tutorials/create-schema/string_constraints.png)

Différentes options de contraintes sont disponibles selon le type de données sélectionné. Puisque `loyaltyId` sera une adresse électronique, sélectionnez &quot;[!UICONTROL email]&quot; dans le menu déroulant **[!UICONTROL Format]**. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer vos modifications.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Ajouter plus de champs au mixin {#mixin-fields-2}

Maintenant que vous avez ajouté le champ `loyaltyId`, vous pouvez ajouter d’autres champs pour capturer des informations relatives à la fidélité, telles que :

* Points (entier)
* Membre depuis (date)

Pour ajouter chaque champ au schéma, sélectionnez l&#39;icône **plus (+)** en regard de l&#39;objet `loyalty` et renseignez les informations requises.

Une fois terminé, l’objet Fidélité contient des champs pour l’identifiant de fidélité, les points et le membre depuis.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Ajouter un champ enum au mixin {#enum}

Lors de la définition de champs dans [!DNL Schema Editor], vous pouvez appliquer d&#39;autres options aux types de champs de base afin de limiter davantage les données que le champ peut contenir. Les cas d’utilisation de ces contraintes sont expliqués dans le tableau suivant :

| Contrainte | Description |
| --- | --- |
| [!UICONTROL Obligatoire] | Indique que le champ est requis pour l’assimilation de données. Toute donnée chargée dans un ensemble de données basé sur ce schéma qui ne contient pas ce champ sera défaillante lors de l’ingestion. |
| [!UICONTROL Tableau] | Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, l’utilisation de cette contrainte sur un champ dont le type de données est &quot;[!UICONTROL String]&quot; indique que le champ contiendra un tableau de chaînes. |
| [!UICONTROL Enum] | Indique que ce champ doit contenir l’une des valeurs d’une liste énumérée de valeurs possibles. |
| [!UICONTROL Identité] | Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [dans la suite de ce tutoriel](#identity-field). |
| [!UICONTROL Relation] | Bien que les relations de schéma puissent être déduites par l&#39;utilisation du schéma d&#39;union et [!DNL Real-time Customer Profile], cela ne s&#39;applique qu&#39;aux schémas qui partagent la même classe. La contrainte [!UICONTROL Relation] indique que ce champ fait référence à l&#39;identité Principale d&#39;un schéma en fonction d&#39;une classe différente, ce qui implique une relation entre les deux schémas. Pour plus d&#39;informations, consultez le didacticiel sur la [définition d&#39;une relation](./relationship-ui.md). |

>[!NOTE]
>
>Les champs obligatoires, d’identité ou de relation s’affichent dans le rail de gauche, ce qui vous permet de les localiser facilement, quelle que soit la complexité du schéma.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Pour ce didacticiel, l’objet [!DNL "loyalty"] du schéma nécessite un nouveau champ d’énumération qui décrit le &quot;niveau de fidélité&quot; d’un client, où la valeur ne peut être que l’une des quatre options possibles. Pour ajouter ce champ au schéma, sélectionnez l’icône **plus (+)** en regard de l’objet `loyalty` et renseignez les champs obligatoires pour **[!UICONTROL Nom du champ]** et **[!UICONTROL Nom d’affichage]**. Pour **[!UICONTROL Type]**, sélectionnez &quot;[!UICONTROL Chaîne]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

D’autres cases à cocher s’affichent pour le champ une fois son type sélectionné, notamment les cases **[!UICONTROL Tableau]**, **[!UICONTROL Enum]** et **[!UICONTROL Identité]**.

Cochez la case **[!UICONTROL Enum]** pour ouvrir la section **[!UICONTROL Valeurs Enum]** ci-dessous. Ici, vous pouvez saisir la **[!UICONTROL valeur]** (en Camel Case) et le **[!UICONTROL libellé]** (nom facultatif et facile à lire écrit en Title Case) pour chaque niveau de fidélité acceptable.

Une fois toutes les propriétés de champ remplies, sélectionnez **[!UICONTROL Appliquer]** pour ajouter le champ &quot;[!DNL loyaltyLevel]&quot; à l&#39;objet `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversion d’un objet à plusieurs champs en un type de données {#datatype}

L&#39;objet `loyalty` contient désormais plusieurs champs spécifiques à la fidélité et représente une structure de données commune qui peut s&#39;avérer utile dans d&#39;autres schémas. Le [!DNL Schema Editor] permet d&#39;appliquer facilement des objets multichamps réutilisables en convertissant la structure de ces objets en types de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les mixins, car ils peuvent être utilisés n’importe où dans un schéma. Pour ce faire, définissez la valeur **[!UICONTROL Type]** du champ sur celle de tout type de données défini dans [!DNL Schema Registry].

Pour convertir l&#39;objet `loyalty` en type de données, sélectionnez le champ `loyalty` sous **[!UICONTROL Structure]**, puis sélectionnez **[!UICONTROL Convertir en nouveau type de données]** sur le côté droit de l&#39;éditeur sous **[!UICONTROL Propriétés du champ]**. Une fenêtre contextuelle verte s’affiche, confirmant que l’objet a bien été converti.

![](../images/tutorials/create-schema/convert-data-type.png)

Maintenant, lorsque vous observez sous **[!UICONTROL Structure]**, vous pouvez voir que le champ `loyalty` a un type de données &quot;[!DNL Loyalty]&quot; et que les champs ont de petites icônes de verrouillage à côté d&#39;eux, indiquant qu&#39;ils ne sont plus des champs individuels mais qu&#39;ils font plutôt partie d&#39;un type de données à champs multiples.

![](../images/tutorials/create-schema/loyalty_data_type.png)

Dans un schéma ultérieur, vous pouvez désormais attribuer un champ sous la forme &quot;[!DNL Loyalty]&quot; et inclure automatiquement des champs pour l’ID, le niveau de fidélité, le membre depuis et les points.

>[!NOTE]
>
>Vous pouvez également créer et modifier des types de données personnalisés indépendamment de la modification de schémas. Pour plus d&#39;informations, consultez le guide [Création et modification des types de données](../ui/resources/data-types.md).

## Rechercher et filtrer les champs de schéma

Votre schéma contient désormais plusieurs mixins en plus des champs fournis par sa classe de base. Lorsque vous travaillez avec des schémas plus volumineux, vous pouvez cocher les cases en regard des noms de mixin dans le rail de gauche pour filtrer les champs affichés uniquement ceux fournis par les mixins qui vous intéressent.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Si vous recherchez un champ spécifique dans votre schéma, vous pouvez également utiliser la barre de recherche pour filtrer les champs affichés par nom, quel que soit le mixin sous lequel ils sont fournis.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La fonction de recherche tient compte des filtres de mixin sélectionnés lors de l’affichage des champs correspondants. Si une requête de recherche n’affiche pas les résultats attendus, vous devrez peut-être vérifier par doublon que vous ne filtrez aucun mixin pertinent.

## Définition d’un champ de schéma comme champ d’identité {#identity-field}

La structure de données standard fournie par les schémas peut être exploitée pour identifier les données appartenant à la même personne sur plusieurs sources, ce qui permet d&#39;utiliser divers cas d&#39;utilisation en aval tels que la segmentation, le rapports, l&#39;analyse des données scientifiques, etc. Pour regrouper les données en fonction des identités individuelles, les champs clés doivent être marqués comme des champs [!UICONTROL Identité] dans les schémas applicables.

[!DNL Experience Platform] facilite la désignation d&#39;un champ d&#39;identité par le biais d&#39;une case à cocher  **** Identité dans la  [!DNL Schema Editor]section. Cependant, vous devez déterminer quel champ est le meilleur candidat à utiliser comme identité, en fonction de la nature de vos données.

Par exemple, il peut y avoir des milliers de membres du programme de fidélité appartenant au même &quot;niveau de fidélité&quot;, mais chaque membre du programme de fidélité a un `loyaltyId` unique (qui dans ce cas est l&#39;adresse électronique du membre individuel). Le fait que `loyaltyId` soit un identifiant unique pour chaque membre en fait un bon candidat pour un champ d&#39;identité, contrairement à `loyaltyLevel`.

>[!IMPORTANT]
>
>Les étapes décrites ci-dessous expliquent comment ajouter un descripteur d&#39;identité à un champ de schéma existant. Au lieu de définir des champs d&#39;identité dans la structure du schéma lui-même, vous pouvez également utiliser un champ `identityMap` pour contenir des informations d&#39;identité.
>
>Si vous prévoyez d&#39;utiliser `identityMap`, gardez à l&#39;esprit qu&#39;il remplacera toute identité Principale que vous ajouterez directement au schéma. Pour plus d&#39;informations, consultez la section `identityMap` du [guide de base sur la composition des schémas](../schema/composition.md#identityMap).

Dans la section **[!UICONTROL Structure]** de l’éditeur, sélectionnez le champ `loyaltyId` et la case **[!UICONTROL Identité]** apparaît sous **[!UICONTROL Propriétés du champ]**. Cochez la case et l&#39;option permettant de définir cette valeur comme **[!UICONTROL identité Principal]** apparaît. Sélectionnez également cette zone.

>[!NOTE]
>
>Chaque schéma ne peut contenir qu’un seul champ d’identité principal. Une fois qu&#39;un champ de schéma a été défini comme identité Principale, vous recevrez un message d&#39;erreur si vous tentez par la suite de définir un autre champ d&#39;identité dans le schéma comme Principal.

Ensuite, vous devez fournir un **[!UICONTROL espace de nommage d&#39;identité]** à partir de la liste d&#39;espaces de nommage prédéfinis dans la liste déroulante. `loyaltyId` étant l’adresse électronique du client, sélectionnez &quot;[!UICONTROL Courriel]&quot; dans la liste déroulante. Sélectionnez **[!UICONTROL Appliquer]** pour confirmer les mises à jour du champ `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Pour une liste des espaces de nommage standard et de leurs définitions, voir la [[!DNL Identity Service] documentation](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Après avoir appliqué la modification, l&#39;icône `loyaltyId` affiche un symbole d&#39;empreinte digitale, indiquant qu&#39;il s&#39;agit désormais d&#39;un champ d&#39;identité.

![](../images/tutorials/create-schema/identity-applied.png)

Désormais, toutes les données saisies dans le champ `loyaltyId` seront utilisées pour identifier cette personne et assembler une seule vue de ce client. Pour en savoir plus sur l&#39;utilisation des identités dans [!DNL Experience Platform], consultez la documentation [[!DNL Identity Service]](../../identity-service/home.md).

## Activez le schéma à utiliser dans [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) exploite les données d&#39;identité  [!DNL Experience Platform] pour fournir une vue holistique à chaque client. Le service crée des profils robustes de 360° d&#39;attributs du client ainsi que des comptes horodatés de chaque interaction que les clients ont eue dans tout système intégré à [!DNL Experience Platform].

Pour qu&#39;un schéma puisse être activé pour une utilisation avec [!DNL Real-time Customer Profile], une identité Principale doit être définie. Vous recevrez un message d&#39;erreur si vous tentez d&#39;activer un schéma sans définir au préalable une identité Principale.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Pour activer le schéma &quot;Membres de la fidélité&quot; à utiliser dans [!DNL Profile], commencez par sélectionner &quot;[!DNL Loyalty Members]&quot; dans la section **[!UICONTROL Structure]** de l&#39;éditeur.

Sur le côté droit de l’éditeur, des informations sur le schéma, y compris son nom d’affichage, sa description et son type, s’affichent. Outre ces informations, il existe un bouton de bascule **[!UICONTROL Profil]**.

![](../images/tutorials/create-schema/profile-toggle.png)

Sélectionnez **[!UICONTROL Profil]** et une fenêtre contextuelle s’affiche, vous demandant de confirmer que vous souhaitez activer le schéma pour [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Une fois qu&#39;un schéma a été activé pour [!DNL Real-time Customer Profile] et enregistré, il ne peut plus être désactivé.

Sélectionnez **[!UICONTROL Activer]** pour confirmer votre choix. Vous pouvez sélectionner à nouveau la bascule **[!UICONTROL Profil]** pour désactiver le schéma si vous le souhaitez, mais une fois que le schéma a été enregistré alors que [!DNL Profile] est activé, il ne peut plus être désactivé.

## Étapes suivantes et ressources supplémentaires

Maintenant que vous avez fini de composer le schéma, vous pouvez voir le schéma complet dans la trame. Sélectionnez **[!UICONTROL Enregistrer]** et le schéma sera enregistré dans [!DNL Schema Library], ce qui le rendra accessible par [!DNL Schema Registry].

Votre nouveau schéma peut désormais être utilisé pour importer des données dans [!DNL Platform]. Pour rappel, une fois que le schéma a été utilisé pour ingérer des données, seules des modifications additives peuvent être apportées. Reportez-vous aux [principes de base de la composition des schémas](../schema/composition.md) pour plus d’informations sur le contrôle de version des schémas.

Vous pouvez maintenant suivre le didacticiel sur la [définition d&#39;une relation de schéma dans l&#39;interface utilisateur](./relationship-ui.md) pour ajouter un nouveau champ de relation au schéma &quot;Membres fidèles&quot;.

Le schéma &quot;Membres fidèles&quot; est également disponible pour être affiché et géré à l’aide de l’API [!DNL Schema Registry]. Pour commencer à travailler avec l&#39;API, début en lisant le [[!DNL Schema Registry API] guide du développeur](../api/getting-started.md).

### Ressources vidéo

>[!WARNING]
>
>L&#39;interface utilisateur [!DNL Platform] affichée dans les vidéos suivantes est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

La vidéo suivante montre comment créer un schéma simple dans l&#39;[!DNL Platform] interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

La vidéo ci-dessous est destinée à vous aider à mieux comprendre comment travailler avec des mixins et des classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Annexe

Les sections suivantes fournissent des informations complémentaires sur l&#39;utilisation de [!DNL Schema Editor].

### Création d’une nouvelle classe {#create-new-class}

[!DNL Experience Platform] offre la possibilité de définir un schéma basé sur une classe propre à votre organisation. Pour savoir comment créer une nouvelle classe, consultez le guide [Création et modification de classes dans l&#39;interface utilisateur](../ui/resources/classes.md#create).

### Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d&#39;un schéma à tout moment pendant le processus de composition initial avant que le schéma n&#39;ait été enregistré.

>[!WARNING]
>
>Réassigner la classe à un schéma doit être fait avec une extrême prudence. Les mixins ne sont compatibles qu&#39;avec certaines classes. Par conséquent, modifier la classe réinitialise le canevas et les champs que vous avez ajoutés.

Pour savoir comment modifier la classe d&#39;un schéma, consultez le guide intitulé [gestion des schémas dans l&#39;interface utilisateur](../ui/resources/schemas.md).
