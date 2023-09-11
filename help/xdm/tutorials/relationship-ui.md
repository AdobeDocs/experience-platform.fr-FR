---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;éditeur de schémas;éditeur de schémas;schéma;schémas;schémas;créer;relation;relation;référence;référence;référence;référence;
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas
description: Ce document fournit un tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans l’interface utilisateur de l’Experience Platform.
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 8b5c1776804bbacad5c3d72dd48c1716380cca79
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 26%

---

# Définissez une relation un-à-un entre deux schémas à l’aide de la variable [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relations de schéma"
>abstract="Les schémas appartenant à différentes classes peuvent être liés de manière contextuelle par le biais de champs de relation, ce qui vous permet de créer des règles de segmentation plus complexes. Pour plus d&#39;informations sur les relations de schéma, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Schéma de référence"
>abstract="Sélectionnez le schéma avec lequel vous souhaitez établir une relation. Ce schéma peut être une classe différente du schéma actuel. Pour plus d&#39;informations sur les relations de schéma, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Espace de noms d&#39;identité de référence"
>abstract="L&#39;espace de noms (type) du champ d&#39;identité principal du schéma de référence. Le schéma de référence doit disposer d&#39;un champ d&#39;identité principal établi pour pouvoir participer à une relation. Pour plus d&#39;informations sur les relations de schéma, consultez la documentation."

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Définir ces relations au sein de la structure de votre [!DNL Experience Data Model] Les schémas (XDM) vous permettent d’obtenir des informations complexes sur les données de vos clients.

Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et [!DNL Real-Time Customer Profile], cela s’applique uniquement aux schémas partageant la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui référence l’identité de l’autre schéma associé.

>[!NOTE]
>
>Si les schémas source et de destination appartiennent à la même classe, un champ de relation dédié doit **not** à utiliser. Dans ce cas, utilisez l’interface utilisateur du schéma d’union pour afficher la relation. Vous trouverez des instructions pour ce faire dans la section [Afficher les relations](../../profile/ui/union-schema.md#view-relationships) dans le guide de l’interface utilisateur du schéma d’union.

Ce document fournit un tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans la variable [!DNL Experience Platform] de l’interface utilisateur. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

>[!NOTE]
>
>Pour savoir comment créer une relation multiple-à-un dans Adobe Real-time Customer Data Platform B2B Edition, consultez le guide sur [création de relations B2B](./relationship-b2b.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique de [!DNL XDM System] et de l’éditeur de schémas dans le [!DNL Experience Platform] Interface utilisateur. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md): présentation de XDM et de son implémentation dans [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide du [!DNL Schema Editor]](create-schema-ui.md): tutoriel sur les principes de base de l’utilisation de la fonction [!DNL Schema Editor].

## Définition d’un schéma source et de référence

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce tutoriel crée une relation entre les membres du programme de fidélité d’une organisation (définis dans un &quot;[!DNL Loyalty Members]&quot;&quot; et leur hôtel préféré (défini dans un &quot;)[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités primaires et être activés pour [!DNL Real-Time Customer Profile]. Voir la section sur [activation d’un schéma à utiliser dans Profile](./create-schema-ui.md#profile) dans le tutoriel sur la création de schémas si vous avez besoin de conseils sur la configuration de vos schémas en conséquence.

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui pointe vers un autre champ dans un **schéma de référence**. Dans les étapes suivantes, &quot;[!DNL Loyalty Members]&quot; sera le schéma source, tandis que &quot;[!DNL Hotels]&quot; agira comme schéma de référence.

Les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant la définition d’une relation.

### [!DNL Loyalty Members] schema

Le schéma source &quot;[!DNL Loyalty Members]&quot; est basé sur la variable [!DNL XDM Individual Profile] contenant un champ décrivant les membres d’un programme de fidélité. Un de ces champs, `personalEmail.addess`, sert d’identité principale au schéma sous la propriété [!UICONTROL Email] espace de noms. Comme vu sous **[!UICONTROL Propriétés du schéma]**, ce schéma peut être utilisé dans [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Le schéma de référence &quot;[!DNL Hotels]&quot; est basé sur un[!DNL Hotels]&quot; et contient des champs qui décrivent un hôtel. Pour participer à une relation, une identité principale doit également être définie pour le schéma de référence et activée pour [!UICONTROL Profil]. Dans ce cas, `_tenantId.hotelId`agit comme l’identité principale du schéma, à l’aide d’un &quot; personnalisé&quot;[!DNL Hotel ID]&quot; identity namespace.

![Activez pour le Profil](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>Pour savoir comment créer des espaces de noms d’identité personnalisés, reportez-vous à la section [Documentation d’Identity Service](../../identity-service/namespaces.md#manage-namespaces).

## Création d’un groupe de champs de relation

>[!NOTE]
>
>Cette étape n’est nécessaire que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme pointeur vers l’identité principale du schéma de référence. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié qui indiquera l’identité principale du schéma de référence. Vous pouvez ajouter ce champ au schéma source en créant un nouveau groupe de champs de schéma ou en étendant un autre existant.

Dans le cas de la fonction [!DNL Loyalty Members] schéma, un nouveau `preferredHotel` sera ajouté pour indiquer l’hôtel préféré du membre du programme de fidélité pour les visites de la société. Sélectionnez d’abord l’icône Plus (**+**) en regard du nom du schéma source.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouvel espace réservé de champ apparaît dans la zone de travail. Sous **[!UICONTROL Propriétés du champ]**, indiquez le nom du champ et son nom d’affichage, puis définissez son type sur &quot;[!UICONTROL Chaîne]&quot;. Sous **[!UICONTROL Attribuer à]**, sélectionnez un groupe de champs existant à étendre ou saisissez un nom unique pour créer un groupe de champs. Dans ce cas, un nouveau &quot;[!DNL Preferred Hotel]&quot; est créé.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

La mise à jour `preferredHotel` apparaît dans la zone de travail, située sous un `_tenantId` car il s’agit d’un champ personnalisé. Sélectionner **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

>[!NOTE]
>
>Les étapes ci-dessous expliquent comment définir un champ de relation à l’aide des commandes de rail droit dans la zone de travail. Si vous avez accès à l’édition B2B de Real-Time CDP, vous pouvez également définir une relation un-à-un à l’aide de la variable [même boîte de dialogue](./relationship-b2b.md#relationship-field) comme lors de la création de relations multiples-à-un.

Sélectionnez la variable `preferredHotel` dans la zone de travail, puis faites défiler l’écran vers le bas sous **[!UICONTROL Propriétés du champ]** jusqu’à ce que la variable **[!UICONTROL Relation]** s’affiche. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Sélectionnez la liste déroulante pour **[!UICONTROL Schéma de référence]** et sélectionnez le schéma de référence de la relation (&quot;[!DNL Hotels]&quot; dans cet exemple). Sous **[!UICONTROL Espace d’identité de référence]**, sélectionnez l’espace de noms du champ d’identité du schéma de référence (ici : &quot;[!DNL Hotel ID]&quot;). Sélectionner **[!UICONTROL Appliquer]** lorsque vous avez terminé.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

La variable `preferredHotel` est maintenant mis en surbrillance en tant que relation dans la zone de travail, affichant le nom du schéma de référence. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas à l’aide de la variable [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
