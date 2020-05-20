---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Définir une relation entre deux schémas à l’aide de l’éditeur de Schéma de Schéma
topic: tutorials
translation-type: tm+mt
source-git-commit: f8c34d84e30ae14c3936c2e32ee84a2fcd3abdc3
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# Définir une relation entre deux schémas à l’aide de l’éditeur de Schéma

La capacité de comprendre les relations entre vos clients et leurs interactions avec votre marque sur différents canaux est un élément important d’Adobe Experience Platform. La définition de ces relations au sein de la structure de vos schémas de modèle de données d’expérience (XDM) vous permet d’obtenir des informations complexes sur vos données client.

Ce document fournit un didacticiel pour la définition d’une relation de type &quot;un à un&quot; entre deux schémas définis par votre organisation à l’aide de l’éditeur de Schémas dans l’interface utilisateur de la plateforme d’expérience. Pour connaître les étapes de définition des relations de schéma à l&#39;aide de l&#39;API, consultez le didacticiel sur la [définition d&#39;une relation à l&#39;aide de l&#39;API](relationship-api.md)de registre des Schémas.

## Prise en main

Ce didacticiel nécessite une bonne compréhension de XDM System et de l’éditeur de Schéma dans l’interface utilisateur de la plate-forme d’expérience. Avant de commencer ce didacticiel, consultez la documentation suivante :

* [Système XDM dans la plate-forme](../home.md)d’expérience : Présentation de XDM et de son implémentation dans la plateforme d’expérience.
* [Principes de base de la composition](../schema/composition.md)des schémas : Présentation des blocs de construction des schémas XDM.
* [Créez un schéma à l’aide de l’éditeur](create-schema-ui.md)de Schéma : Didacticiel sur les bases de l’utilisation de l’éditeur de Schéma.

## Définir un schéma source et de destination

Il est prévu que vous ayez déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce didacticiel crée une relation entre les membres du programme de fidélité d&#39;une organisation (défini dans un schéma &quot;Membres fidèles&quot;) et leurs hôtels favoris (défini dans un schéma &quot;Hôtels&quot;).

Les relations de Schéma sont représentées par un schéma **** source dont le champ fait référence à un autre champ dans un schéma **de** destination. Dans les étapes qui suivent, &quot;Membres de la Fidélité&quot; sera le schéma source, tandis que &quot;Hôtels&quot; agira comme schéma de destination.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce didacticiel avant la définition d&#39;une relation.

### schéma Membres de fidélité

Le schéma source &quot;Membres de la fidélité&quot; est le schéma qui a été construit dans le didacticiel pour [créer un schéma dans l’interface utilisateur](create-schema-ui.md). Il inclut un objet &quot;loyalty&quot; sous son espace de nommage &quot;\_locataireId&quot;, qui comprend plusieurs champs spécifiques à la fidélité. L’un de ces champs, &quot;loyaltyId&quot;, sert d’identité principale au schéma sous l’espace de nommage &quot;Email&quot;. Comme indiqué sous Propriétés _du_ Schéma, ce schéma a été activé pour une utilisation dans le Profil [client en temps](../../profile/home.md)réel.

![](../images/tutorials/relationship/loyalty-members.png)

### Hôtel schéma

Le schéma de destination &quot;Hôtels&quot; contient les champs qui décrivent un hôtel, y compris son adresse, sa marque, le nombre de chambres et le classement par étoiles. Le champ &quot;hotelId&quot; sert d’identité principale pour le schéma sous l’espace de nommage &quot;ECID&quot;. Contrairement aux &quot;membres de fidélité&quot;, ce schéma n’a pas été activé pour le Profil client en temps réel.

![](../images/tutorials/relationship/hotels.png)

## Créer un mixin de relation

>[!NOTE] Cette étape n’est requise que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence à un autre schéma. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de [définition d’un champ](#relationship-field)de relation.

Pour définir une relation entre deux schémas, le schéma source doit disposer d&#39;un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau mixin.

Début en cliquant sur **Ajouter** dans la section _Mélanges_ .

![](../images/tutorials/relationship/loyalty-add-mixin.png)

La boîte de dialogue _Ajouter Mixin_ s’affiche. A partir de là, cliquez sur **Créer un nouveau mixin**. Dans les champs de texte qui s’affichent, saisissez le nom d’affichage et la description du nouveau mixin. Cliquez sur **Ajouter Mixin** une fois terminé.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

Le canevas réapparaît avec &quot;Relation de fidélité&quot; apparaissant dans la section _Mélanges_ . Cliquez sur le nom du mixin, puis sur Champ **** Ajouter en regard du champ racine &quot;Membres de la fidélité&quot;.

![](../images/tutorials/relationship/loyalty-add-field.png)

Un nouveau champ apparaît dans le canevas sous l&#39;espace de nommage &quot;\_locataireId&quot;. Sous Propriétés _du_ champ, indiquez un nom de champ et un nom d’affichage pour le champ, puis définissez son type sur &quot;Chaîne&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, cliquez sur **Appliquer**.

![](../images/tutorials/relationship/relationship-field-apply.png)

Le champ &quot;loyaltyRelationship&quot; mis à jour s’affiche dans le canevas. Cliquez sur **Enregistrer** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définir un champ de relation pour le schéma source {#relationship-field}

Une fois que votre schéma source a défini un champ de référence dédié, vous pouvez le désigner comme champ de relation.

Cliquez sur le champ de référence dans la trame, puis faites défiler la liste sous Propriétés _du_ champ jusqu’à ce que la case **Relation** s’affiche. Cochez la case pour afficher les paramètres requis pour configurer un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Cliquez sur la liste déroulante du Schéma **de** référence et sélectionnez le schéma de destination de la relation (&quot;Hôtels&quot; dans cet exemple). Si l&#39;schéma de destination est compatible avec l&#39;union, le champ Espace de nommage **d&#39;identité de** référence est automatiquement défini sur l&#39;espace de nommage de l&#39;identité principale du schéma de destination. Si aucune identité principale n&#39;est définie pour le schéma, vous devez sélectionner manuellement l&#39;espace de nommage que vous prévoyez d&#39;utiliser dans le menu déroulant. Click **Apply** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le champ s’affiche sous la forme d’une relation dans la trame, affichant le nom et l’espace de nommage d’identité de référence du schéma de destination. Cliquez sur **Enregistrer** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer une relation de type &quot;un à un&quot; entre deux schémas à l’aide de l’éditeur de Schéma. Pour savoir comment définir des relations à l&#39;aide de l&#39;API, consultez le didacticiel sur la [définition d&#39;une relation à l&#39;aide de l&#39;API](relationship-api.md)de registre de Schéma.