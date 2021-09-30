---
title: Définition d’une relation entre deux schémas dans l’édition B2B de la plateforme de données clients en temps réel
description: Découvrez comment définir une relation multiple-à-un entre deux schémas dans l’édition B2B de la plateforme de données clients en temps réel.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 2ad20a4c7a9d1cc71fc4e589de90d7eabf8c87b7
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 8%

---

# Définition d’une relation entre deux schémas dans la plateforme de données clients en temps réel B2B (version bêta)

>[!IMPORTANT]
>
>La plateforme de données clients en temps réel de l’édition B2B est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

>[!NOTE]
>
>Si vous n’utilisez pas l’édition B2B de la plateforme de données clients en temps réel, reportez-vous au guide sur la [création d’une relation non-B2B](./relationship-ui.md) à la place.

La plateforme de données clients en temps réel de l’édition B2B fournit plusieurs classes de modèle de données d’expérience (XDM) qui capturent les entités de données B2B fondamentales, y compris les [comptes](../classes/b2b/business-account.md), les [opportunités](../classes/b2b/business-opportunity.md), les [campagnes](../classes/b2b/business-campaign.md), etc. En créant des schémas basés sur ces classes et en les activant pour une utilisation dans [Real-time Customer Profile](../../profile/home.md), vous pouvez fusionner les données de sources disparates dans une représentation unifiée appelée schéma d’union.

Cependant, les schémas d’union ne peuvent contenir que des champs capturés par des schémas qui partagent la même classe. C’est là que les relations de schéma entrent en jeu. En implémentant des relations dans vos schémas B2B, vous pouvez décrire la manière dont ces entités commerciales se relient les unes aux autres et peut inclure des attributs provenant de plusieurs classes dans les cas d’utilisation de la segmentation en aval.

Le diagramme suivant illustre la manière dont les différentes classes B2B peuvent se relier les unes aux autres dans une mise en oeuvre de base :

![Relations de classe B2B](../images/tutorials/relationship-b2b/classes.png)

Ce tutoriel décrit les étapes de définition d’une relation multiple-à-un entre deux schémas dans l’édition CDP B2B en temps réel.

>[!NOTE]
>
>Ce tutoriel se concentre sur la manière d’établir manuellement des relations entre les schémas B2B dans l’interface utilisateur de Platform. Si vous importez des données à partir d’une connexion source B2B, vous pouvez utiliser un utilitaire de génération automatique pour créer les schémas, les identités et les relations requis à la place. Pour plus d’informations sur [l’utilisation de l’utilitaire de génération automatique](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md), consultez la documentation des sources sur les espaces de noms et schémas B2B .

## Prise en main

Ce tutoriel nécessite une compréhension pratique de [!DNL XDM System] et de l’éditeur de schémas dans l’interface utilisateur [!DNL Experience Platform]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md) : Présentation de XDM et de sa mise en oeuvre dans  [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide de [!DNL Schema Editor]](create-schema-ui.md) : Tutoriel abordant les principes de base de la création et de la modification de schémas dans l’interface utilisateur.

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce tutoriel crée une relation entre les opportunités commerciales (définies dans un schéma &quot;[!DNL Opportunities]&quot;) et leur compte professionnel associé (défini dans un schéma &quot;[!DNL Accounts]&quot;).

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui référence le champ d’identité Principal d’un **schéma de destination**. Dans les étapes suivantes, &quot;[!DNL Opportunities]&quot; sert de schéma source, tandis que &quot;[!DNL Accounts]&quot; agit comme schéma de destination.

### Comprendre les identités dans les relations B2B

Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être activés pour [!DNL Real-time Customer Profile]. Lors de la définition d’une identité Principale pour une entité B2B, gardez à l’esprit que les identifiants d’entité basés sur des chaînes peuvent se chevaucher si vous les collectez sur différents systèmes ou emplacements, ce qui peut entraîner des conflits de données dans Platform.

Pour ce faire, toutes les classes B2B standard contiennent des champs &quot;key&quot; conformes au [[!UICONTROL type de données ](../data-types/b2b-source.md) de la source B2B]. Ce type de données fournit des champs pour un identifiant de chaîne pour l’entité B2B, ainsi que d’autres informations contextuelles sur la source de l’identifiant. L’un de ces champs, `sourceKey`, concatène les valeurs des autres champs du type de données afin de produire un identifiant totalement unique pour l’entité. Ce champ doit toujours être utilisé comme identité Principale pour les schémas d’entité B2B.

![champ sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Lorsque [définissez un champ XDM en tant qu’identité](../ui/fields/identity.md), vous devez fournir un espace de noms d’identité pour définir l’identité sous . Il peut s’agir d’un espace de noms standard fourni par Adobe ou d’un espace de noms personnalisé défini par votre organisation. En pratique, l’espace de noms est simplement une chaîne contextuelle et peut être définie sur n’importe quelle valeur, à condition qu’il soit significatif pour votre organisation pour la classification du type d’identité. Pour plus d’informations, consultez la présentation sur [espaces de noms d’identité](../../identity-service/namespaces.md) .

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation. Prenez note de l’emplacement où les identités Principales ont été définies dans la structure du schéma et les espaces de noms personnalisés qu’elles utilisent.

### [!DNL Opportunities] schema

Le schéma source &quot;[!DNL Opportunities]&quot; est basé sur la classe [!UICONTROL XDM Business Opportunity]. L’un des champs fournis par la classe, `opportunityKey`, sert d’identifiant au schéma. Plus précisément, le champ `sourceKey` sous l’objet `opportunityKey` est défini comme identité Principale du schéma sous un espace de noms personnalisé appelé [!DNL B2B Opportunity].
Comme vous pouvez le voir sous **[!UICONTROL Propriétés du schéma]**, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile].

![Schéma d’opportunités](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Le schéma de destination &quot;[!DNL Accounts]&quot; est basé sur la classe [!UICONTROL XDM Account] . Le champ `accountKey` de niveau racine contient la balise `sourceKey` qui agit comme son identité Principale sous un espace de noms personnalisé appelé [!DNL B2B Account]. Ce schéma a également été activé pour une utilisation dans Profile.

![Schéma des comptes](../images/tutorials/relationship-b2b/accounts.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié qui référence l’identité Principale du schéma de destination. Les classes B2B standard incluent des champs source clés dédiés pour les entités commerciales les plus courantes. Par exemple, la classe [!UICONTROL XDM Business Opportunity] contient les champs de clé source pour un compte associé (`accountKey`) et une campagne associée (`campaignKey`). Cependant, vous pouvez également ajouter d’autres champs [!UICONTROL Source B2B] au schéma à l’aide de groupes de champs personnalisés si vous avez besoin de plus que les composants par défaut.

>[!NOTE]
>
>Actuellement, seules les relations multiples-à-un peuvent être définies d’un schéma source à un schéma de destination. Pour les relations de type &quot;un à plusieurs&quot;, vous devez définir le champ de relation dans le schéma qui représente le &quot;plusieurs&quot;.

Pour définir un champ de relation, sélectionnez l’icône de flèche (![Icône de flèche](../images/tutorials/relationship-b2b/arrow.png)) en regard du champ en question dans la zone de travail. Dans le cas du schéma [!DNL Opportunities], il s’agit du champ `accountKey.sourceKey` , car l’objectif est d’établir une relation multiple-à-un avec un compte.

![Bouton Relation](../images/tutorials/relationship-b2b/relationship-button.png)

Une boîte de dialogue s’affiche, vous permettant de spécifier les détails de la relation. Le type de relation est automatiquement défini sur **[!UICONTROL Multiple-to-one]**.

![Boîte de dialogue de relation](../images/tutorials/relationship-b2b/relationship-dialog.png)

Sous **[!UICONTROL Schéma de référence]**, utilisez la barre de recherche pour trouver le nom du schéma de destination. Lorsque vous mettez en surbrillance le nom du schéma de destination, le champ **[!UICONTROL Espace de noms d’identité de référence]** est automatiquement mis à jour vers l’espace de noms de l’identité Principale du schéma.

![Schéma de référence](../images/tutorials/relationship-b2b/reference-schema.png)

Sous **[!UICONTROL Nom de la relation à partir du schéma actuel]** et **[!UICONTROL Nom de la relation à partir du schéma de référence]**, fournissez des noms conviviaux pour la relation dans le contexte des schémas source et de destination, respectivement. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour appliquer les modifications et enregistrer le schéma.

![Nom de la relation](../images/tutorials/relationship-b2b/relationship-name.png)

Le canevas réapparaît, le champ de relation étant désormais marqué du nom convivial que vous avez fourni précédemment. Le nom de la relation est également répertorié sous le rail de gauche pour référence facile.

![Relation appliquée](../images/tutorials/relationship-b2b/relationship-applied.png)

Si vous affichez la structure du schéma de destination, le marqueur de relation s’affiche en regard du champ d’identité Principal du schéma et dans le rail de gauche.

![Marqueur de relation du schéma de destination](../images/tutorials/relationship-b2b/destination-relationship.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez créé avec succès une relation multiple-à-un entre deux schémas à l’aide de [!DNL Schema Editor]. Une fois que les données ont été ingérées à l’aide de jeux de données basés sur ces schémas et que ces données ont été activées dans l’entrepôt de données Profile, vous pouvez utiliser les attributs des deux schémas pour les cas d’utilisation de la segmentation multi-classe. Pour plus d’informations, consultez la documentation sur l’édition CDP B2B en temps réel .
