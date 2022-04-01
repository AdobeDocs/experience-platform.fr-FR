---
keywords: Experience Platform;accueil;rubriques populaires;Application des stratégies;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Application automatique des stratégies
topic-legacy: guide
description: Ce document présente l’application automatique des stratégies d’utilisation de données lors de l’activation de segments vers des destinations dans Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 63705bdcf102ff01b4d67ce5955d8e23b32dbfe6
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 91%

---

# Application automatique des stratégies

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation des segments d’audience vers les destinations, Adobe Experience Platform applique automatiquement les stratégies d’utilisation en cas de violation.

## Conditions préalables

Ce guide nécessite une compréhension pratique des divers services Platform impliqués dans l’application automatique. Consultez la documentation suivante pour en savoir plus avant de poursuivre avec ce guide :

* [Gouvernance des données d’Adobe Experience Platform](../home.md) : cadre en fonction duquel Platform applique la conformité de l’utilisation des données à l’aide des libellés et des stratégies.
* [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service de segmentation Adobe Experience Platform](../../segmentation/home.md) : moteur de segmentation de [!DNL Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.
* [Destinations](../../destinations/home.md) : les destinations sont des intégrations préconfigurées aux applications couramment utilisées. Elles permettent l’activation transparente des données de Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée, etc.

## Flux d’application {#flow}

Le diagramme suivant illustre la procédure d’intégration des politiques dans le flux de données de l’activation des segments :

![](../images/enforcement/enforcement-flow.png)

Lorsqu’un segment est activé pour la première fois, [!DNL Policy Service] recherche les stratégies applicables en fonction des facteurs suivants :

* Les libellés d’utilisation des données ont été appliquées aux champs et aux jeux de données du segment à activer.
* Objectif marketing de la destination.
<!-- * (Beta) The profiles that have consented to be included in the segment activation, based on your configured consent policies. -->

>[!NOTE]
>
>Si des libellés d’utilisation des données n’ont été appliqués qu’à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu), l’application de ces libellés au niveau du champ sur l’activation se fait uniquement dans les conditions suivantes :
>
>* Les champs sont utilisés dans la définition de segment.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination cible.


## Parenté des données {#lineage}

La parenté des données joue un rôle essentiel dans la façon dont les stratégies sont appliquées dans Platform. D’une façon générale, la parenté des données fait référence à l’origine d’un jeu de données ainsi qu’à son évolution (ou à son déplacement) au fil du temps.

Dans le cadre de la gouvernance des données, la parenté permet aux libellés d’utilisation des données de se propager des jeux de données aux services en aval qui utilisent leurs données, comme le profil client en temps réel et les destinations. Cela permet d’évaluer et d’appliquer les stratégies à plusieurs points clés du parcours des données par l’intermédiaire de Platform et fournit un contexte aux consommateurs de données quant aux raisons pour lesquelles une violation de stratégie a eu lieu.

Dans Experience Platform, l’application des stratégies est concernée par la parenté suivante :

1. Les données sont ingérées dans Platform et stockées dans des **jeux de données**.
1. Les profils clients sont identifiés et construits à partir de ces jeux de données grâce à la fusion des fragments de données, conformément à la **stratégie de fusion**.
1. Les groupes de profils sont divisés en **segments** en fonction d’attributs communs.
1. Les segments sont activés pour les **destinations** en aval.

Chaque étape de la chronologie ci-dessus représente une entité qui peut contribuer à une exception à la stratégie, comme indiqué dans le tableau ci-dessous :

| Étape relative à la parenté des données | Rôle dans l’application des stratégies |
| --- | --- |
| Jeu de données | Les jeux de données contiennent des libellés d’utilisation des données (appliquées au niveau du jeu de données ou du champ) qui définissent les cas d’utilisation pour lesquels l’intégralité du jeu de données ou des champs spécifiques peuvent être utilisés. Des violations de stratégie se produisent si un jeu de données ou un champ contenant certains libellés est utilisé à des fins limitées par une stratégie. |
<!-- | Dataset | Datasets contain data usage labels (applied at the dataset or field level) that define which use cases the entire dataset or specific fields can be used for. Policy violations will occur if a dataset or field containing certain labels is used for a purpose that a policy restricts.<br><br>Any consent attributes collected from your customers are also stored in datasets. If you have access to [consent policies](../policies/user-guide.md#consent-policy) (currently in beta), any profiles that do not meet the consent attribute requirements of your policies will be excluded from segments that are activated to a destination. | -->
| Stratégie de fusion | Les stratégies de fusion sont les règles utilisées par Platform pour déterminer la priorité des données lors de la fusion de fragments de plusieurs jeux de données. Des violations de stratégie se produisent si vos stratégies de fusion sont configurées de telle sorte que les jeux de données dotés de libellés limités sont activés pour une destination. Pour plus d’informations, consultez la [présentation des stratégies de fusion. ](../../profile/merge-policies/overview.md) | | Segment | Les règles de segment définissent les attributs qui doivent être inclus à partir des profils client. En fonction des champs inclus dans une définition de segment, le segment hérite des libellés d’utilisation appliqués pour ces champs. Des violations de stratégie se produisent si vous activez un segment dont les libellés hérités sont limités par les stratégies applicables de la destination cible, en fonction de son cas d’utilisation marketing. |
<!-- | Segment | Segment rules define which attributes should be included from customer profiles. Depending on which fields a segment definition includes, the segment will inherit any applied usage labels for those fields. Policy violations will occur if you activate a segment whose inherited labels are restricted by the target destination's applicable policies, based on its marketing use case. | -->
| Destination | Lors de la configuration d’une destination, une action marketing (parfois appelée cas d’utilisation marketing) peut être définie. Ce cas pratique correspond à une action marketing définie dans une stratégie. En d’autres termes, le cas d’utilisation marketing que vous définissez pour une destination détermine les stratégies d’utilisation des données et les stratégies de consentement applicables à cette destination. Des violations de stratégie se produisent si vous activez un segment dont les libellés d’utilisation sont limités par les stratégies applicables de la destination cible. |

>[!IMPORTANT]
>
>Certaines stratégies d’utilisation des données peuvent spécifier plusieurs libellés avec une relation ET. Par exemple, une stratégie peut limiter une action marketing si les libellés `C1` ET `C2` sont tous deux présents. Toutefois, elle ne limite pas l’action en question si un seul de ces libellés est présent.
>
>En ce qui concerne l’application automatique, le cadre de gouvernance des données ne considère pas l’activation de segments distincts vers une destination comme une combinaison de données. Par conséquent, la stratégie `C1 AND C2` d’exemple n’est **PAS** appliquée si ces libellés sont inclus dans des segments distincts. Au lieu de cela, cette stratégie n’est appliquée que lorsque les deux libellés sont présents dans le même segment lors de l’activation.

Lorsque des violations de stratégie se produisent, les messages qui s’affichent dans l’interface utilisateur fournissent des outils utiles à l’exploration de la parenté des données contribuant à la violation afin de résoudre le problème. Vous trouverez plus de détails dans la section suivante.

## Messages de violation de politique {#enforcement}

<!-- (TO INCLUDE FOR PHASE 2)
The sections below outline the different policy enforcement messages that appear in the Platform UI:

* [Data usage policy violation](#data-usage-violation)
* [Consent policy evaluation](#consent-policy-evaluation)

### Data usage policy violation {#data-usage-violation} -->

Si une violation de politique se produit lors de la tentative d’activation d’un segment (ou de la [modification d’un segment déjà activé](#policy-enforcement-for-activated-segments)), l’action est bloquée et une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs politiques ont été violées. Une fois qu’une violation a été déclenchée, le bouton **[!UICONTROL Enregistrer]** est désactivé pour l’entité à modifier jusqu’à ce que les composants appropriés soient mis à jour pour se conformer aux stratégies d’utilisation des données.

Sélectionnez une violation de politique dans la colonne de gauche de la fenêtre contextuelle pour afficher les détails de celle-ci.

![](../images/enforcement/violation-policy-select.png)

Le message relatif à la violation présente un résumé de la stratégie enfreinte, y compris les conditions configurées pour être vérifiées par la stratégie, l’action spécifique qui a déclenché la violation ainsi qu’une liste de résolutions possibles pour le problème.

![](../images/enforcement/violation-summary.png)

Un graphique relatif à la parenté des données s’affiche sous le résumé de la violation. Cela vous permet de visualiser les jeux de données, les stratégies de fusion, les segments et les destinations impliqués dans la violation de la stratégie. L’entité que vous modifiez actuellement est mise en surbrillance dans le graphique, ce qui indique le point du flux à l’origine de la violation. Vous pouvez sélectionner un nom d’entité dans le graphique pour ouvrir la page de détails de l’entité en question.

![](../images/enforcement/data-lineage.png)

Vous pouvez également utiliser l’icône **[!UICONTROL Filtre]** (![](../images/enforcement/filter.png)) pour filtrer les entités affichées par catégorie. Au moins deux catégories doivent être sélectionnées pour que les données s’affichent.

![](../images/enforcement/lineage-filter.png)

Sélectionnez **[!UICONTROL Mode Liste]** pour afficher la parenté des données sous forme de liste. Pour revenir au graphique visuel, sélectionnez **[!UICONTROL Chemin parcouru]**.

![](../images/enforcement/list-view.png)

<!-- (TO INCLUDE FOR PHASE 2)
### Consent policy evaluation (Beta) {#consent-policy-evaluation}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

If you have [created consent policies](../policies/user-guide.md#consent-policy) and are activating a segment to a destination, you can see how your consent policies will affect the percentage of profiles that will be included in the activation.

Once you reach at the **[!UICONTROL Review]** step in the [activation workflow](../../destinations/ui/activation-overview.md), select **[!UICONTROL View applied policies]**.

A policy check dialog appears, showing you a preview of how your consent policies affect the addressable audience of the activated segment.
 -->

## Application des politiques pour les segments activés {#policy-enforcement-for-activated-segments}

L’application de la politique s’applique toujours aux segments une fois qu’ils ont été activés, ce qui limite toute modification apportée à un segment ou à sa destination qui entraînerait une violation de la politique. En raison du fonctionnement de la [parenté des données](#lineage) dans l’application des stratégies, l’une des actions suivantes peut potentiellement déclencher une violation :

* Mise à jour des libellés d’utilisation des données
* Modification des jeux de données d’un segment
* Modification des prédicats de segment
* Modification des configurations de destination

Si l’une des actions ci-dessus déclenche une violation, l’enregistrement de cette action est bloquée et un message de violation de politique s’affiche, ce qui vous permet de vérifier que les segments que vous avez activés continuent à respecter les politiques d’utilisation des données lors de leur modification.

## Étapes suivantes

Ce document vous a présenté le fonctionnement de l’application automatique des stratégies dans Experience Platform. Pour savoir comment intégrer par programmation l’application de stratégies dans vos applications à l’aide d’appels d’API, consultez le guide sur l’[application basée sur les API](./api-enforcement.md).
