---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;éditeur de schémas;éditeur de schémas;schéma;schémas;schémas;créer;relation;relation;référence;référence;référence;référence;
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas
description: Ce document fournit un tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans l’interface utilisateur de l’Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 86a230d746d6642437c4e37958c07a1186ebadc3
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 22%

---

# Définissez une relation un-à-un entre deux schémas à l’aide de la variable [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="Relations de schéma"
>abstract="Les schémas appartenant à différentes classes peuvent être liés de manière contextuelle par le biais de champs de relation, ce qui vous permet de créer des règles de segmentation plus complexes. Pour plus d’informations sur les relations de schéma, consultez la documentation ."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="Schéma de référence"
>abstract="Sélectionnez le schéma avec lequel vous souhaitez établir une relation. Ce schéma peut être une classe différente du schéma actuel. Pour plus d’informations sur les relations de schéma, consultez la documentation ."

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="Espace de noms d’identité de référence"
>abstract="L’espace de noms (type) du champ d’identité Principal du schéma de référence. Le schéma de référence doit disposer d’un champ d’identité Principal établi pour pouvoir participer à une relation. Pour plus d’informations sur les relations de schéma, consultez la documentation ."

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Définir ces relations au sein de la structure de votre [!DNL Experience Data Model] Les schémas (XDM) vous permettent d’obtenir des informations complexes sur les données de vos clients.

Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et [!DNL Real-time Customer Profile], cela s’applique uniquement aux schémas qui partagent la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui référence l’identité d’un schéma de destination.

Ce document fournit un tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans la variable [!DNL Experience Platform] de l’interface utilisateur. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

>[!NOTE]
>
>Pour savoir comment créer une relation multiple-à-un dans Real-time Customer Data Platform B2B Edition, consultez le guide sur [création de relations B2B](./relationship-b2b.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique de [!DNL XDM System] et de l’éditeur de schémas dans le [!DNL Experience Platform] Interface utilisateur. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md): Présentation de XDM et de son implémentation dans [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide du [!DNL Schema Editor]](create-schema-ui.md): Un tutoriel sur les principes de base de l’utilisation de la fonction [!DNL Schema Editor].

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce tutoriel crée une relation entre les membres du programme de fidélité d’une organisation (définis dans un &quot;[!DNL Loyalty Members]&quot;&quot; et leur hôtel préféré (défini dans un &quot;)[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être activés pour [!DNL Real-time Customer Profile]. Voir la section sur [activation d’un schéma à utiliser dans Profile](./create-schema-ui.md#profile) dans le tutoriel sur la création de schémas si vous avez besoin de conseils sur la configuration de vos schémas en conséquence.

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui fait référence à un autre champ d’un **schéma de destination**. Dans les étapes suivantes, &quot;[!DNL Loyalty Members]&quot; sera le schéma source, tandis que &quot;[!DNL Hotels]&quot; agira comme schéma de destination.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation.

### [!DNL Loyalty Members] schema

Le schéma source &quot;[!DNL Loyalty Members]&quot; est basé sur la variable [!DNL XDM Individual Profile] et est le schéma qui a été créé dans le tutoriel pour [création d’un schéma dans l’interface utilisateur](create-schema-ui.md). Il comprend un `loyalty` sous `_tenantId` qui comprend plusieurs champs spécifiques à la fidélité. Un de ces champs, `loyaltyId`, sert d’identité Principale pour le schéma sous le [!UICONTROL Email] espace de noms. Comme vous pouvez le voir sous **[!UICONTROL Propriétés du schéma]**, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Le schéma de destination &quot;[!DNL Hotels]&quot; est basé sur un[!DNL Hotels]&quot; et contient des champs qui décrivent un hôtel.

![](../images/tutorials/relationship/hotels.png)

Pour participer à une relation, le schéma de destination doit avoir une identité Principale. Dans cet exemple, la variable `hotelId` est utilisé comme identité Principale, à l’aide d’un espace de noms d’identité personnalisé &quot;ID d’hôtel&quot;.

![Identité Principale de l&#39;hôtel](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>Pour savoir comment créer des espaces de noms d’identité personnalisés, reportez-vous à la section [Documentation d’Identity Service](../../identity-service/namespaces.md#manage-namespaces).

Une fois l’identité Principale définie, le schéma de destination doit être activé pour [!DNL Real-time Customer Profile].

![Activation pour Profile](../images/tutorials/relationship/hotel-profile.png)

## Création d’un groupe de champs de schéma de relation

>[!NOTE]
>
>Cette étape n’est nécessaire que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence au schéma de destination. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau groupe de champs de schéma.

Commencez par sélectionner **[!UICONTROL Ajouter]** dans le **[!UICONTROL Groupes de champs]** .

![](../images/tutorials/relationship/loyalty-add-field-group.png)

Le [!UICONTROL Ajouter un groupe de champs] s’affiche. À partir de là, sélectionnez **[!UICONTROL Créer un groupe de champs]**. Dans les champs de texte qui s&#39;affichent, saisissez le nom d&#39;affichage et la description du nouveau groupe de champs. Sélectionner **[!UICONTROL Ajouter des groupes de champs]** lorsque vous avez terminé.

![](../images/tutorials/relationship/create-field-group.png)

Le canevas réapparaît avec &quot;[!DNL Favorite Hotel]&quot; apparaissant dans la variable **[!UICONTROL Groupes de champs]** . Sélectionnez le nom du groupe de champs, puis sélectionnez **[!UICONTROL Ajouter un champ]** en regard du niveau racine `Loyalty Members` champ .

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouveau champ s’affiche dans la zone de travail sous `_tenantId` espace de noms. Sous **[!UICONTROL Propriétés du champ]**, indiquez un nom de champ et un nom d’affichage pour le champ, puis définissez son type sur &quot;[!UICONTROL Chaîne]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

La mise à jour `favoriteHotel` s’affiche dans la zone de travail. Sélectionner **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

>[!NOTE]
>
>Les étapes ci-dessous expliquent comment définir un champ de relation à l’aide des commandes de rail droit dans la zone de travail. Si vous avez accès à l’édition B2B de Real-Time CDP, vous pouvez également définir une relation un-à-un à l’aide de la variable [même boîte de dialogue](./relationship-b2b.md#relationship-field) comme lors de la création de relations multiples-à-un.

Sélectionnez la `favoriteHotel` dans la zone de travail, puis faites défiler l’écran vers le bas sous **[!UICONTROL Propriétés du champ]** jusqu’à ce que la variable **[!UICONTROL Relation]** s’affiche. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Sélectionnez la liste déroulante pour **[!UICONTROL Schéma de référence]** et sélectionnez le schéma de destination de la relation (&quot;[!DNL Hotels]&quot; dans cet exemple). Si le schéma de destination est activé pour [!DNL Profile], la variable **[!UICONTROL Espace de noms d’identité de référence]** est automatiquement défini sur l’espace de noms de l’identité Principale du schéma de destination. Si aucune identité principale n’est définie pour le schéma, vous devez sélectionner manuellement l’espace de noms que vous prévoyez d’utiliser dans le menu déroulant. Sélectionner **[!UICONTROL Appliquer]** lorsque vous avez terminé.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le `favoriteHotel` est maintenant mis en surbrillance en tant que relation dans la zone de travail, affichant le nom et l’espace de noms d’identité de référence du schéma de destination. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas à l’aide de la variable [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
