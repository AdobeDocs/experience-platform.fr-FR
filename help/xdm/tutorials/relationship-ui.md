---
keywords: Experience Platform ; accueil ; rubriques populaires ; ui ; IU ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; éditeur de schémas ; éditeur de Schémas ; schéma ; Schéma ; schémas ; Schémas ; créer ; relation ; référence ; référence ;
solution: Experience Platform
title: Définir une relation entre deux Schémas à l’aide de l’éditeur de Schéma
description: Ce document fournit un didacticiel pour la définition d'une relation entre deux schémas à l'aide de l'éditeur de Schémas dans l'interface utilisateur de l'Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 27%

---

# Définissez une relation entre deux schémas à l&#39;aide de [!DNL Schema Editor]

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas [!DNL Experience Data Model] (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Bien que les relations de schéma puissent être déduites par l&#39;utilisation du schéma d&#39;union et [!DNL Real-time Customer Profile], cela ne s&#39;applique qu&#39;aux schémas qui partagent la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui fait référence à l&#39;identité d&#39;un schéma de destination.

Ce document fournit un didacticiel pour la définition d&#39;une relation entre deux schémas à l&#39;aide de l&#39;éditeur de Schéma dans l&#39;interface utilisateur [!DNL Experience Platform]. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

## Prise en main

Ce didacticiel nécessite une bonne compréhension de [!DNL XDM System] et de l’éditeur de Schéma dans l’interface utilisateur [!DNL Experience Platform]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md) : Présentation de XDM et de sa mise en oeuvre dans  [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide des [!DNL Schema Editor]](create-schema-ui.md) éléments suivants : Didacticiel sur les bases de l&#39;utilisation de la  [!DNL Schema Editor]méthode.

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce didacticiel crée une relation entre les membres du programme de fidélité d&#39;une organisation (défini dans un schéma &quot;[!DNL Loyalty Members]&quot;) et leur hôtel favori (défini dans un schéma &quot;[!DNL Hotels]&quot;).

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être autorisés pour [!DNL Real-time Customer Profile]. Consultez la section [activation d&#39;un schéma à utiliser dans Profil](./create-schema-ui.md#profile) du didacticiel de création de schéma si vous avez besoin de conseils sur la manière de configurer vos schémas en conséquence.

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui fait référence à un autre champ dans un **schéma de destination**. Dans les étapes suivantes, &quot;[!DNL Loyalty Members]&quot; sera le schéma source, tandis que &quot;[!DNL Hotels]&quot; agira comme schéma de destination.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation.

### [!DNL Loyalty Members] schema

Le schéma source &quot;[!DNL Loyalty Members]&quot; est basé sur la classe [!DNL XDM Individual Profile] et est le schéma qui a été construit dans le didacticiel pour [créer un schéma dans l&#39;interface utilisateur](create-schema-ui.md). Il comprend un objet `loyalty` sous son espace de nommage `_tenantId`, qui comprend plusieurs champs spécifiques à la fidélité. L&#39;un de ces champs, `loyaltyId`, sert d&#39;identité Principale au schéma sous l&#39;espace de nommage [!UICONTROL E-mail]. Comme vous pouvez le voir sous **[!UICONTROL Propriétés du schéma]**, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schéma

Le schéma de destination &quot;[!DNL Hotels]&quot; est basé sur une classe personnalisée &quot;[!DNL Hotels]&quot; et contient des champs qui décrivent un hôtel. Le champ `hotelId` sert d&#39;identité Principale pour le schéma sous un espace de nommage personnalisé `hotelId`. Comme le schéma [!DNL Loyalty Members], ce schéma a également été activé pour [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Créer un groupe de champs de schéma de relation

>[!NOTE]
>
>Cette étape n’est requise que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence au schéma de destination. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau groupe de champs de schéma.

Début en sélectionnant **[!UICONTROL Ajouter]** dans la section **[!UICONTROL Groupes de champs]**.

![](../images/tutorials/relationship/loyalty-add-field-group.png)

La boîte de dialogue [!UICONTROL Ajouter le groupe de champs] s&#39;affiche. À partir de là, sélectionnez **[!UICONTROL Créer un nouveau groupe de champs]**. Dans les champs de texte qui s’affichent, entrez le nom d’affichage et la description du nouveau groupe de champs. Sélectionnez **[!UICONTROL Ajouter des groupes de champs]** une fois terminé.

![](../images/tutorials/relationship/create-field-group.png)

Le canevas réapparaît avec &quot;[!DNL Favorite Hotel]&quot; apparaissant dans la section **[!UICONTROL Groupes de champs]**. Sélectionnez le nom du groupe de champs, puis **[!UICONTROL Ajouter le champ]** en regard du champ racine `Loyalty Members`.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouveau champ apparaît dans la trame sous l&#39;espace de nommage `_tenantId`. Sous **[!UICONTROL Propriétés de champ]**, indiquez un nom de champ et un nom d’affichage pour le champ, puis définissez son type sur &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Le champ `favoriteHotel` mis à jour apparaît dans la trame. Sélectionnez **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

Sélectionnez le champ `favoriteHotel` dans la trame, puis faites défiler la liste sous **[!UICONTROL Propriétés du champ]** jusqu&#39;à ce que la case **[!UICONTROL Relation]** s&#39;affiche. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Sélectionnez la liste déroulante **[!UICONTROL schéma de référence]** et sélectionnez le schéma de destination de la relation (&quot;[!DNL Hotels]&quot; dans cet exemple). Si le schéma de destination est activé pour [!DNL Profile], le champ **[!UICONTROL espace de nommage d&#39;identité de référence]** est automatiquement défini sur l&#39;espace de nommage de l&#39;identité Principale du schéma de destination. Si aucune identité principale n’est définie pour le schéma, vous devez sélectionner manuellement l’espace de noms que vous prévoyez d’utiliser dans le menu déroulant. Sélectionnez **[!UICONTROL Appliquer]** une fois terminé.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le champ `favoriteHotel` est désormais mis en évidence en tant que relation dans la trame, affichant le nom et l&#39;espace de nommage d&#39;identité de référence du schéma de destination. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer une relation de type &quot;un à un&quot; entre deux schémas à l’aide de [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
