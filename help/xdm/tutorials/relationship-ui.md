---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;éditeur de schémas;éditeur de schémas;schéma;schémas;schémas;créer;relation;relation;référence;référence;référence;référence;
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas
description: Ce document fournit un tutoriel sur la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans l’interface utilisateur de l’Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 2118dc175b421e856c6b0a33a83a7238f01b7ee3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 26%

---

# Définissez une relation entre deux schémas à l’aide de [!DNL Schema Editor]

>[!NOTE]
>
>Si vous utilisez l’édition B2B de la plateforme de données clients en temps réel, reportez-vous au guide sur la [création de relations B2B](./relationship-b2b.md) à la place.

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas [!DNL Experience Data Model] (XDM) vous permet d’obtenir des informations complexes sur les données de vos clients.

Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et de [!DNL Real-time Customer Profile], cela ne s’applique qu’aux schémas qui partagent la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui référence l’identité d’un schéma de destination.

Ce document fournit un tutoriel pour la définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas dans l’interface utilisateur [!DNL Experience Platform]. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique de [!DNL XDM System] et de l’éditeur de schémas dans l’interface utilisateur [!DNL Experience Platform]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md) : Présentation de XDM et de sa mise en oeuvre dans  [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide de [!DNL Schema Editor]](create-schema-ui.md) : Tutoriel traitant des principes de base de l’utilisation de  [!DNL Schema Editor].

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce tutoriel crée une relation entre les membres du programme de fidélité d’une organisation (définis dans un schéma &quot;[!DNL Loyalty Members]&quot;) et leur hôtel préféré (défini dans un schéma &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être activés pour [!DNL Real-time Customer Profile]. Consultez la section [Activation d’un schéma à utiliser dans Profile](./create-schema-ui.md#profile) dans le tutoriel de création de schéma si vous avez besoin de conseils sur la manière de configurer vos schémas en conséquence.

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui fait référence à un autre champ dans un **schéma de destination**. Dans les étapes suivantes, &quot;[!DNL Loyalty Members]&quot; sera le schéma source, tandis que &quot;[!DNL Hotels]&quot; agira comme schéma de destination.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation.

### [!DNL Loyalty Members] schema

Le schéma source &quot;[!DNL Loyalty Members]&quot; est basé sur la classe [!DNL XDM Individual Profile] et est le schéma qui a été créé dans le tutoriel pour [créer un schéma dans l’interface utilisateur](create-schema-ui.md). Il comprend un objet `loyalty` sous son espace de noms `_tenantId`, qui comprend plusieurs champs spécifiques à la fidélité. L’un de ces champs, `loyaltyId`, sert d’identité Principale pour le schéma sous l’espace de noms [!UICONTROL Email]. Comme vous pouvez le voir sous **[!UICONTROL Propriétés du schéma]**, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Le schéma de destination &quot;[!DNL Hotels]&quot; est basé sur une classe personnalisée &quot;[!DNL Hotels]&quot; et contient des champs qui décrivent un hôtel.

![](../images/tutorials/relationship/hotels.png)

Pour participer à une relation, le schéma de destination doit avoir une identité Principale. Dans cet exemple, le champ `hotelId` est utilisé comme identité Principale, à l’aide d’un espace de noms d’identité personnalisé &quot;ID d’hôtel&quot;.

![Identité Principale de l&#39;hôtel](../images/tutorials/relationship/hotel-identity.png)

>[!NOTE]
>
>Pour savoir comment créer des espaces de noms d’identité personnalisés, reportez-vous à la [documentation Identity Service](../../identity-service/namespaces.md#manage-namespaces).

Une fois l’identité Principale définie, le schéma de destination doit être activé pour [!DNL Real-time Customer Profile].

![Activation pour Profile](../images/tutorials/relationship/hotel-profile.png)

## Création d’un groupe de champs de schéma de relation

>[!NOTE]
>
>Cette étape n’est nécessaire que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence au schéma de destination. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau groupe de champs de schéma.

Sélectionnez d’abord **[!UICONTROL Ajouter]** dans la section **[!UICONTROL Groupes de champs]** .

![](../images/tutorials/relationship/loyalty-add-field-group.png)

La boîte de dialogue [!UICONTROL Ajouter un groupe de champs] s’affiche. À partir de là, sélectionnez **[!UICONTROL Créer un groupe de champs]**. Dans les champs de texte qui s&#39;affichent, saisissez le nom d&#39;affichage et la description du nouveau groupe de champs. Sélectionnez **[!UICONTROL Ajouter des groupes de champs]** lorsque vous avez terminé.

![](../images/tutorials/relationship/create-field-group.png)

Le canevas réapparaît avec &quot;[!DNL Favorite Hotel]&quot; apparaissant dans la section **[!UICONTROL Groupes de champs]**. Sélectionnez le nom du groupe de champs, puis **[!UICONTROL Ajouter un champ]** en regard du champ `Loyalty Members` de niveau racine.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouveau champ s’affiche dans la zone de travail sous l’espace de noms `_tenantId`. Sous **[!UICONTROL Propriétés du champ]**, indiquez un nom de champ et un nom d’affichage pour le champ, puis définissez son type sur &quot;[!UICONTROL Chaîne]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Le champ `favoriteHotel` mis à jour apparaît dans la zone de travail. Sélectionnez **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

Sélectionnez le champ `favoriteHotel` dans la zone de travail, puis faites défiler la liste sous **[!UICONTROL Propriétés du champ]** jusqu’à ce que la case **[!UICONTROL Relation]** s’affiche. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Sélectionnez la liste déroulante **[!UICONTROL Schéma de référence]** et sélectionnez le schéma de destination de la relation (&quot;[!DNL Hotels]&quot; dans cet exemple). Si le schéma de destination est activé pour [!DNL Profile], le champ **[!UICONTROL Espace de noms de l’identité de référence]** est automatiquement défini sur l’espace de noms de l’identité Principale du schéma de destination. Si aucune identité principale n’est définie pour le schéma, vous devez sélectionner manuellement l’espace de noms que vous prévoyez d’utiliser dans le menu déroulant. Sélectionnez **[!UICONTROL Appliquer]** lorsque vous avez terminé.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le champ `favoriteHotel` est désormais mis en surbrillance en tant que relation dans la zone de travail, affichant le nom et l’espace de noms d’identité de référence du schéma de destination. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une relation un-à-un entre deux schémas à l’aide de [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
