---
title: Définition d’une relation entre deux schémas dans Real-Time Customer Data Platform B2B edition
description: Découvrez comment définir une relation multiple-à-un entre deux schémas dans Adobe Real-Time Customer Data Platform B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: cb036262ff81d245fe436fc337b3911170c61425
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 14%

---

# Définir une relation plusieurs-à-un entre deux schémas dans l’édition B2B de Real-time Customer Data Platform {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Schéma de référence"
>abstract="Sélectionnez le schéma avec lequel vous souhaitez établir une relation. Selon la classe du schéma, il peut également avoir des relations existantes avec d&#39;autres entités dans le contexte B2B. Pour en savoir plus sur la manière dont les classes de schéma B2B se connectent entre elles, consultez la documentation."

Adobe Real-Time Customer Data Platform B2B edition fournit plusieurs classes de modèle de données d’expérience (XDM) qui capturent les entités de données B2B fondamentales, notamment les [comptes](../classes/b2b/business-account.md), [opportunités](../classes/b2b/business-opportunity.md), [campagnes](../classes/b2b/business-campaign.md), etc. En créant des schémas basés sur ces classes et en les activant pour les utiliser dans [Real-Time Customer Profile](../../profile/home.md), vous pouvez fusionner des données provenant de sources disparates en une représentation unifiée appelée schéma d’union.

Cependant, les schémas d’union ne peuvent contenir que des champs capturés par des schémas partageant la même classe. C’est là que les relations de schéma entrent en jeu. En implémentant des relations dans vos schémas B2B, vous pouvez décrire la manière dont ces entités commerciales sont liées les unes aux autres et inclure des attributs provenant de plusieurs classes dans les cas d’utilisation de segmentation en aval.

Le diagramme suivant fournit un exemple de la manière dont les différentes classes B2B peuvent être liées les unes aux autres dans une implémentation de base :

![Relations de classe B2B](../images/tutorials/relationship-b2b/classes.png)

Ce tutoriel décrit les étapes à suivre pour définir une relation multiple-à-un entre deux schémas dans Real-Time CDP B2B edition.

>[!NOTE]
>
>Si vous n’utilisez pas Real-Time Customer Data Platform B2B edition ou souhaitez créer une relation un-à-un, consultez le guide sur la [création d’une relation un-à-un](./relationship-ui.md) à la place.
>
>Ce tutoriel se concentre sur la manière d’établir manuellement des relations entre les schémas B2B dans l’interface utilisateur d’Experience Platform. Si vous importez des données à partir d’une connexion source B2B, vous pouvez utiliser un utilitaire de génération automatique pour créer les schémas, identités et relations requis à la place. Consultez la documentation sur les sources relative aux espaces de noms et aux schémas B2B pour plus d’informations sur [l’utilisation de l’utilitaire de génération automatique](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Commencer

Ce tutoriel nécessite une compréhension pratique de [!DNL XDM System] et de l’éditeur de schémas dans l’interface utilisateur de [!DNL Experience Platform]. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM dans Experience Platform](../home.md) : présentation de XDM et de sa mise en œuvre dans [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Création d’un schéma à l’aide du  [!DNL Schema Editor]](create-schema-ui.md) : tutoriel présentant les principes de base de la création et de la modification de schémas dans l’interface utilisateur.

## Définition d’un schéma source et de référence

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. À des fins de démonstration, ce tutoriel crée une relation entre les opportunités commerciales (définies dans un schéma « [!DNL Opportunities] ») et leur compte commercial associé (défini dans un schéma « [!DNL Accounts] »).

Les relations de schéma sont représentées par un champ dédié dans un **schéma source** qui fait référence au champ d’identité principale d’un **schéma de référence**. Dans les étapes qui suivent, « [!DNL Opportunities] » sert de schéma source, tandis que « [!DNL Accounts] » agit comme schéma de référence.

### Comprendre les identités dans les relations B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Espace de noms d&#39;identité de référence"
>abstract="L&#39;espace de noms (type) du champ d&#39;identité principal du schéma de référence. Le schéma de référence doit disposer d&#39;un champ d&#39;identité principal établi pour pouvoir participer à une relation. Pour en savoir plus sur les identités dans les relations B2B, consultez la documentation."

Pour établir une relation, le schéma de référence doit avoir une identité principale définie. Lors de la définition d’une identité principale pour une entité B2B, gardez à l’esprit que les ID d’entité basés sur des chaînes peuvent se chevaucher si vous les collectez sur différents systèmes ou emplacements, ce qui peut entraîner des conflits de données dans Experience Platform.

Pour en tenir compte, toutes les classes B2B standard contiennent des champs « clé » conformes au type de données [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Ce type de données fournit des champs pour un identifiant de chaîne pour l’entité B2B ainsi que d’autres informations contextuelles sur la source de l’identifiant. L’un de ces champs, `sourceKey`, concatène les valeurs des autres champs du type de données afin de produire un identifiant totalement unique pour l’entité. Ce champ doit toujours être utilisé comme identité principale pour les schémas d’entité B2B.

![&#x200B; champ sourceKey &#x200B;](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Lors de la [définition d’un champ XDM en tant qu’identité](../ui/fields/identity.md), vous devez fournir un espace de noms d’identité pour définir l’identité sous. Il peut s’agir d’un espace de noms standard fourni par Adobe ou d’un espace de noms personnalisé défini par votre organisation. En pratique, l’espace de noms est simplement une chaîne contextuelle et peut être défini sur n’importe quelle valeur, à condition qu’il soit significatif pour votre organisation lors de la classification du type d’identité. Pour plus d’informations, consultez la présentation des [espaces de noms d’identité](../../identity-service/features/namespaces.md).

À des fins de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant la définition d’une relation. Notez l’emplacement où les identités principales ont été définies dans la structure du schéma et les espaces de noms personnalisés qu’elles utilisent.

### Schéma des opportunités

Le schéma source « [!DNL Opportunities] » est basé sur la classe [!UICONTROL XDM Business Opportunity]. L’un des champs fournis par la classe, `opportunityKey`, sert d’identifiant pour le schéma. Plus précisément, le champ `sourceKey` sous l’objet `opportunityKey` est défini comme identité principale du schéma sous un espace de noms personnalisé appelé [!DNL B2B Opportunity].

Comme indiqué sous **[!UICONTROL Field Properties]**, ce schéma a été activé pour une utilisation dans [!DNL Real-Time Customer Profile].

![Schéma d’opportunités dans l’éditeur de schémas avec l’objet opportunitéKey et le bouton (bascule) Activer pour le profil mis en surbrillance.](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] le schéma

Le schéma de référence « [!DNL Accounts] » est basé sur la classe [!UICONTROL XDM Account]. Le champ de `accountKey` de niveau racine contient le `sourceKey` qui agit comme identité principale sous un espace de noms personnalisé appelé [!DNL B2B Account]. Ce schéma peut également être utilisé dans Profile.

![Schéma Comptes dans l’éditeur de schémas avec l’objet accountKey et le bouton Activer pour le profil mis en surbrillance.](../images/tutorials/relationship-b2b/accounts.png)

## Définir un champ de relation pour le schéma source {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nom de la relation à partir du schéma actuel"
>abstract="Libellé décrivant la relation entre le schéma actuel et le schéma de référence (par exemple, « Compte associé »). Ce libellé est utilisé dans Profil et Segmentation pour donner un contexte aux données des entités B2B associées. Pour en savoir plus sur la création de relations de schémas B2B, consultez la documentation."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nom de la relation à partir du schéma de référence"
>abstract="Libellé qui décrit la relation entre le schéma de référence et le schéma actuel (par exemple, « Opportunités liées »). Ce libellé est utilisé dans Profil et Segmentation pour donner un contexte aux données des entités B2B associées. Pour en savoir plus sur la création de relations de schémas B2B, consultez la documentation."

Pour définir une relation entre deux schémas, le schéma source doit comporter un champ dédié qui indique l’identité principale du schéma de référence. Les classes B2B standard incluent des champs de clé source dédiés pour les entités commerciales fréquemment liées. Par exemple, la classe [!UICONTROL XDM Business Opportunity] contient les champs de clé source pour un compte associé (`accountKey`) et une campagne associée (`campaignKey`). Cependant, vous pouvez également ajouter d’autres champs [!UICONTROL B2B Source] au schéma à l’aide de groupes de champs personnalisés si vous avez besoin de plus que les composants par défaut.

>[!NOTE]
>
>Actuellement, seules les relations multiples-à-un et un-à-un peuvent être définies d’un schéma source vers un schéma de référence. Pour les relations de type « un à plusieurs », vous devez définir le champ de relation dans le schéma qui représente le « plusieurs ».

Pour définir un champ de relation, sélectionnez le champ en question dans la zone de travail, puis **[!UICONTROL Add relationship]** dans la barre latérale [!UICONTROL Schema properties]. Dans le cas du schéma [!DNL Opportunities], il s’agit du champ `accountKey.sourceKey`, car l’objectif est d’établir une relation multiple-à-un avec un compte.

![L’éditeur de schémas avec le champ sourceKey et l’option Ajouter une relation mise en surbrillance.](../images/tutorials/relationship-b2b/add-relationship.png)

La boîte de dialogue [!UICONTROL Add relationship] s’affiche. Utilisez cette boîte de dialogue pour spécifier les détails de la relation. Par défaut, le type de relation est défini sur **[!UICONTROL Many-to-one]**.

![La boîte de dialogue Ajouter une relation avec la relation de schéma plusieurs-à-un mise en surbrillance.](../images/tutorials/relationship-b2b/relationship-dialog.png)

Sous **[!UICONTROL Reference Schema]**, utilisez la barre de recherche ou le menu déroulant pour trouver le nom du schéma de référence. Lorsque vous mettez en surbrillance le nom du schéma de référence, le champ **[!UICONTROL Reference Identity Namespace]** est automatiquement mis à jour vers l’espace de noms de l’identité principale du schéma de référence.

>[!NOTE]
>
>La liste des schémas de référence disponibles est filtrée afin de ne contenir que les schémas appropriés. Les schémas **doivent** disposent d’une identité principale attribuée et doivent être soit une classe B2B, soit la classe Individual Profile. Les schémas de classe de prospects ne peuvent pas avoir de relations.

![La boîte de dialogue Ajouter une relation avec les champs Schéma de référence et Espace de noms d’identité de référence en surbrillance.](../images/tutorials/relationship-b2b/reference-schema.png)

Sous **[!UICONTROL Relationship Name From Current Schema]** et **[!UICONTROL Relationship Name From Reference Schema]**, fournissez des noms conviviaux pour la relation dans le contexte des schémas source et de référence, respectivement. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Apply]** pour confirmer les modifications et enregistrer la relation.

>[!NOTE]
>
>Les noms des relations doivent comporter 35 caractères maximum.

![La boîte de dialogue Ajouter une relation avec les champs Nom de la relation mis en surbrillance.](../images/tutorials/relationship-b2b/relationship-name.png)

La zone de travail réapparaît, et le champ de relation est maintenant marqué du nom convivial que vous avez fourni précédemment. Le nom de la relation est également répertorié dans le rail de gauche pour en faciliter la référence.

![Application du nouveau nom de relation à l’éditeur de schémas.](../images/tutorials/relationship-b2b/relationship-applied.png)

Si vous affichez la structure du schéma de référence, le marqueur de relation s’affiche en regard du champ d’identité principale du schéma et dans le rail de gauche.

![Schéma de destination dans l’éditeur de schémas avec le nouveau marqueur de relation mis en surbrillance.](../images/tutorials/relationship-b2b/destination-relationship.png)

## Modification d’une relation de schéma B2B {#edit-schema-relationship}

Une fois qu’une relation de schéma est établie, sélectionnez le champ de relation dans le schéma source, puis **[!UICONTROL Edit relationship]**.

>[!NOTE]
>
>Pour afficher toutes les relations associées, sélectionnez le champ Identité principale dans le schéma de référence, suivi de [!UICONTROL View relationships].
>![L’éditeur de schémas avec un champ de relation sélectionné et Afficher la relation en surbrillance.](../images/tutorials/relationship-b2b/view-relationships.png "Éditeur de schémas avec un champ de relation sélectionné et Afficher la relation en surbrillance."){width="100" zoomable="yes"}

![Éditeur de schémas avec un champ de relation et Modifier la relation en surbrillance.](../images/tutorials/relationship-b2b/edit-b2b-relationship.png)

La boîte de dialogue [!UICONTROL Edit relationship] s’affiche. À partir de cette boîte de dialogue, vous pouvez modifier le schéma de référence et les noms des relations, ou supprimer la relation. Le type de relation multiple-à-un ne peut pas être modifié.

![Boîte de dialogue Modifier la relation.](../images/tutorials/relationship-b2b/edit-b2b-relationship-dialog.png)

Pour maintenir l’intégrité des données et éviter toute perturbation de la segmentation et d’autres processus, tenez compte des instructions suivantes lors de la gestion des relations de schémas avec des jeux de données liés :

* Évitez de supprimer directement des relations si un schéma est associé à un jeu de données, car cela peut avoir un impact négatif sur la segmentation. Supprimez plutôt le jeu de données associé avant de supprimer la relation.
* Vous ne pouvez pas modifier le schéma de référence sans supprimer au préalable la relation existante. Toutefois, cette opération doit être effectuée avec précaution, car la suppression d’une relation avec un jeu de données associé peut avoir des conséquences inattendues.
* L’ajout de nouvelles relations à un schéma avec des jeux de données liés existants peut ne pas fonctionner comme prévu et pourrait entraîner des conflits potentiels.

## Filtrer et rechercher des relations {#filter-and-search}

Vous pouvez filtrer et rechercher des relations spécifiques dans vos schémas à partir de l’onglet [!UICONTROL Relationships] de l’espace de travail [!UICONTROL Schemas]. Vous pouvez utiliser cette vue pour localiser et gérer rapidement vos relations. Lisez le document [exploration des ressources de schéma](../ui/explore.md#lookup) pour obtenir des instructions détaillées sur les options de filtrage.

![Onglet Relations de l’espace de travail Schémas.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à créer une relation multiple-à-un entre deux schémas à l’aide de l’[!DNL Schema Editor] . Une fois que les données ont été ingérées à l’aide de jeux de données basés sur ces schémas et que ces données ont été activées dans la banque de données de profils, vous pouvez utiliser les attributs des deux schémas pour les [cas d’utilisation de la segmentation multiclasse](../../rtcdp/segmentation/b2b.md).
