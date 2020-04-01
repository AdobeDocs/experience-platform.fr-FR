---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Définissez une relation entre deux  d'à l'aide de l'éditeur de  de
topic: tutorials
translation-type: tm+mt
source-git-commit: f8c34d84e30ae14c3936c2e32ee84a2fcd3abdc3

---


# Définir une relation entre deux  à l’aide de l’éditeur de  de

La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque dans divers  de est un élément important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de votre de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Ce fournit un didacticiel pour la définition d’une relation de type &quot;un à un&quot; entre deux  définis par votre organisation à l’aide de l’éditeur de  d’expérience dans l’interface utilisateur de la plateforme d’expérience. Pour connaître les étapes de définition des relations  à l’aide de l’API, consultez le didacticiel sur la [définition d’une relation à l’aide de l’API](relationship-api.md)de registre de.

## Prise en main

Ce didacticiel nécessite une compréhension pratique de XDM System et de l’éditeur de  dans l’interface utilisateur de la plateforme d’expérience. Avant de commencer ce didacticiel, consultez la documentation suivante :

* [Système XDM dans la plate-forme](../home.md)d’expérience : Présentation de XDM et de son implémentation dans la plateforme d’expérience.
* [Principes de base de la composition](../schema/composition.md)de  : Présentation des blocs de création de  XDM.
* [Créez un  à l’aide de l’éditeur](create-schema-ui.md)de  de : Didacticiel sur les principes de base de l’utilisation de l’éditeur de .

## Définition d’un source et de destination 

Vous devez avoir déjà créé les deux  de qui seront définies dans la relation. À des fins de démonstration, ce didacticiel crée une relation entre les membres d’un  de fidélité d’une organisation (défini dans un &quot;Membres de la fidélité&quot;) et leurs hôtels préférés (défini dans un &quot;Hôtels&quot;).

Les relations de  sont représentées par un **source** ayant un champ qui fait référence à un autre champ dans une **destination**. Dans les étapes qui suivent, &quot;Membres de la Fidélité&quot; sera la source du , tandis que &quot;Hôtels&quot; agira comme de destination .

À titre de référence, les sections suivantes décrivent la structure de chaque  de utilisée dans ce didacticiel avant la définition d’une relation.

### Membres de la fidélité 

Le source  &quot;Membres de la fidélité&quot; est le qui a été créé dans le didacticiel pour [créer un](create-schema-ui.md)dans l’interface utilisateur. Il inclut un objet &quot;loyalty&quot; sous son &quot;\_locataireId&quot; , qui comprend plusieurs champs spécifiques à la fidélité. L’un de ces champs, &quot;loyaltyId&quot;, sert d’identité principale au sous le  de la  de  &quot;Email&quot;. Comme le montre la section Propriétés _de_, ce  de a été activé pour une utilisation dans le [client en temps](../../profile/home.md)réel.

![](../images/tutorials/relationship/loyalty-members.png)

### Hôtels 

Le de destination  &quot;Hôtels&quot; contient les champs qui décrivent un hôtel, y compris son adresse, sa marque, le nombre de chambres et le classement par étoiles. Le champ &quot;hotelId&quot; sert d’identité principale pour le  sous le &quot;ECID&quot;  la . Contrairement aux &quot;membres de fidélité&quot;, cette  de n’a pas été activée pour l’ du client en temps réel.

![](../images/tutorials/relationship/hotels.png)

## Création d’un mélange de relations

>[!NOTE] Cette étape n’est requise que si votre  source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence à un autre  de. Si ce champ est déjà défini dans votre  source, passez à l’étape suivante de [définition d’un champ](#relationship-field)de relation.

Pour définir une relation entre deux , le source  doit disposer d’un champ dédié à utiliser comme référence à la  de destination. Vous pouvez ajouter ce champ au  source en créant un nouveau mixin.

 en cliquant sur **Ajouter** dans la section _Mixins_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

La boîte de dialogue _Ajouter Mixin_ s’affiche. A partir de là, cliquez sur **Créer un nouveau mixin**. Dans les champs de texte qui s’affichent, saisissez le nom d’affichage et la description du nouveau mixin. Cliquez sur **Ajouter Mixin** lorsque vous avez terminé.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Le canevas réapparaît avec &quot;Relation de fidélité&quot; apparaissant dans la section _Mixins_ . Cliquez sur le nom du mixin, puis sur Champ **** Ajouter en regard du champ racine &quot;Membres de la fidélité&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouveau champ apparaît dans le canevas sous le  \_locataireId. Sous Propriétés _du_ champ, indiquez un nom de champ et un nom d’affichage pour le champ, puis définissez son type sur &quot;Chaîne&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, cliquez sur **Appliquer**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Le champ &quot;loyaltyRelationship&quot; mis à jour s’affiche dans le canevas. Cliquez sur **Enregistrer** pour finaliser les modifications apportées au  de.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définir un champ de relation pour le source {#relationship-field}

Une fois que le champ de référence dédié de votre source est défini, vous pouvez le désigner comme champ de relation.

Cliquez sur le champ de référence dans le canevas, puis faites défiler la liste sous Propriétés _du_ champ jusqu’à ce que la case **Relation** s’affiche. Cochez la case pour afficher les paramètres requis pour configurer un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Cliquez sur la liste déroulante pour de **de** référence et sélectionnez le de destination pour la relation (&quot;Hôtels&quot; dans cet exemple). Si le de destination est activé  l&#39;option, le champ **Référence -** d&#39;identité est automatiquement défini sur le de l&#39;identité principale de la de destination. Si aucune identité principale n&#39;est définie pour le , vous devez sélectionner manuellement le  que vous prévoyez d&#39;utiliser dans le menu déroulant. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le champ s’affiche sous la forme d’une relation dans le canevas, affichant le nom et l’identité de référence   du de destination. Cliquez sur **Enregistrer** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer une relation de type &quot;un à un&quot; entre deux  à l’aide de l’éditeur de  de. Pour savoir comment définir des relations à l’aide de l’API, consultez le didacticiel sur la [définition d’une relation à l’aide de l’API](relationship-api.md)de Registre .