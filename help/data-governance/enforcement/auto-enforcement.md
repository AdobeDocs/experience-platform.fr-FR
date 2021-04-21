---
keywords: Experience Platform ; accueil ; rubriques populaires ; Application des stratégies ; Application automatique ; Application basée sur les API ; gouvernance des données
solution: Experience Platform
title: Application automatique de la stratégie
topic-legacy: guide
description: Ce document décrit comment les stratégies d’utilisation des données sont automatiquement appliquées lors de l’activation de segments vers des destinations dans l’Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 19%

---

# Application automatique des stratégies

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation des segments d’audience vers les destinations, Adobe Experience Platform applique automatiquement les stratégies d’utilisation en cas de violation.

## Conditions préalables

Ce guide nécessite une compréhension pratique des services de la Plateforme impliqués dans l&#39;application automatique. Veuillez consulter la documentation suivante pour en savoir plus avant de poursuivre avec ce guide :

* [Gouvernance](../home.md) des données Adobe Experience Platform : Cadre par lequel Plateforme applique la conformité à l&#39;utilisation des données en utilisant des étiquettes et des stratégies.
* [Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service](../../segmentation/home.md) de segmentation Adobe Experience Platform : Moteur de segmentation  [!DNL Platform] utilisé pour créer des segments d’audience à partir de vos profils clients en fonction du comportement et des attributs des clients.
* [Destinations](../../destinations/home.md) : Les destinations sont des intégrations préétablies avec les applications couramment utilisées qui permettent l’activation transparente des données de la plate-forme pour les campagnes marketing inter-canaux, les campagnes par courriel, la publicité ciblée, etc. Y.

## Flux d&#39;application {#flow}

Le diagramme suivant illustre la procédure d’intégration des politiques dans le flux de données de l’activation des segments :

![](../images/enforcement/enforcement-flow.png)

Lorsqu’un segment est activé pour la première fois, [!DNL Policy Service] recherche les violations de stratégie en fonction des facteurs suivants :

* Les libellés d’utilisation des données ont été appliquées aux champs et aux jeux de données du segment à activer.
* Objectif marketing de la destination.

>[!NOTE]
>
>Si des étiquettes d’utilisation de données n’ont été appliquées qu’à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu de données), l’application de ces étiquettes de niveau champ sur l’activation se fait uniquement dans les conditions suivantes :
>
>* Les champs sont utilisés dans la définition de segment.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination de la cible.


## Gamme de données {#lineage}

Le lignage des données joue un rôle clé dans la manière dont les stratégies sont appliquées dans Platform. En termes généraux, le lignage de données fait référence à l’origine d’un ensemble de données et à ce qui s’y passe (ou où il se déplace) au fil du temps.

Dans le contexte de [!DNL Data Governance], le lignage permet aux libellés d&#39;utilisation des données de se propager des jeux de données aux services en aval qui utilisent leurs données, tels que le Profil client en temps réel et les destinations. Cela permet d&#39;évaluer et d&#39;appliquer les politiques à plusieurs points clés du parcours des données via la plate-forme et fournit un contexte aux consommateurs de données quant aux raisons pour lesquelles une violation de la politique a eu lieu.

En Experience Platform, l&#39;application des politiques est concernée par la lignée suivante :

1. Les données sont ingérées dans la plate-forme et stockées dans **jeux de données**.
1. Les profils clients sont identifiés et construits à partir de ces jeux de données en fusionnant des fragments de données conformément à la **stratégie de fusion**.
1. Les groupes de profils sont divisés en **segments** en fonction d’attributs communs.
1. Les segments sont activés pour les **destinations** en aval.

Chaque étape du calendrier ci-dessus représente une entité qui peut contribuer à la violation d&#39;une politique, comme indiqué dans le tableau ci-dessous :

| Etape de la gamme de données | Rôle dans l&#39;application des politiques |
| --- | --- |
| Jeu de données | Les jeux de données contiennent des étiquettes d’utilisation des données (appliquées au niveau du jeu de données ou du champ) qui définissent les cas d’utilisation pour lesquels le jeu de données entier ou des champs spécifiques peuvent être utilisés. Des violations de stratégie se produisent si un jeu de données ou un champ contenant certaines étiquettes est utilisé à des fins restreintes par une stratégie. |
| Fusionner la stratégie | Les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées lors de la fusion de fragments provenant de plusieurs jeux de données. Des violations de stratégie se produiront si vos stratégies de fusion sont configurées de sorte que les jeux de données avec des étiquettes restreintes soient activés pour une destination. Pour plus d&#39;informations, consultez le guide [Fusionner les stratégies](../../profile/ui/merge-policies.md). |
| Segment | Les règles de segmentation définissent les attributs à inclure dans les profils client. En fonction des champs inclus par une définition de segment, le segment hérite des étiquettes d’utilisation appliquées pour ces champs. Des violations de stratégie se produiront si vous activez un segment dont les étiquettes héritées sont restreintes par les stratégies applicables de la destination de la cible, en fonction de son cas d’utilisation marketing. |
| Destination | Lors de la configuration d’une destination, une action marketing (parfois appelée cas d’utilisation marketing) peut être définie. Ce cas d’utilisation correspond à une action marketing telle que définie dans une stratégie d’utilisation des données. En d’autres termes, le cas d’utilisation marketing que vous définissez pour une destination détermine les stratégies d’utilisation des données applicables à cette destination. Des violations de stratégie se produiront si vous activez un segment dont les étiquettes d’utilisation sont restreintes par les stratégies applicables de la destination de la cible. |

Lorsque des violations de stratégie se produisent, les messages qui s’affichent dans l’interface utilisateur fournissent des outils utiles pour explorer la lignée de données de contribution de la violation afin de résoudre le problème. Vous trouverez plus de détails dans la section suivante.

## Messages de violation de politique  {#enforcement}

Si une violation de politique se produit lors de la tentative d’activation d’un segment (ou de la [modification d’un segment déjà activé](#policy-enforcement-for-activated-segments)), l’action est bloquée et une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs politiques ont été violées. Une fois qu&#39;une violation a été déclenchée, le bouton **[!UICONTROL Enregistrer]** est désactivé pour l&#39;entité que vous modifiez jusqu&#39;à ce que les composants appropriés soient mis à jour pour se conformer aux règles d&#39;utilisation des données.

Sélectionnez une violation de politique dans la colonne de gauche de la fenêtre contextuelle pour afficher les détails de celle-ci.

![](../images/enforcement/violation-policy-select.png)

Le message de violation fournit un résumé de la stratégie qui a été violée, y compris les conditions que la stratégie est configurée pour vérifier, l&#39;action spécifique qui a déclenché la violation et une liste de solutions possibles pour le problème.

![](../images/enforcement/violation-summary.png)

Un graphique de lignage de données s’affiche sous le résumé de la violation, ce qui vous permet de visualiser les jeux de données, les stratégies de fusion, les segments et les destinations impliqués dans la violation de la stratégie. L&#39;entité que vous modifiez actuellement est mise en surbrillance dans le graphique, ce qui indique le point du flux à l&#39;origine de la violation. Vous pouvez sélectionner un nom d&#39;entité dans le graphique pour ouvrir la page de détails de l&#39;entité en question.

![](../images/enforcement/data-lineage.png)

Vous pouvez également utiliser l&#39;icône **[!UICONTROL Filtrer]** (![](../images/enforcement/filter.png)) pour filtrer les entités affichées par catégorie. Au moins deux catégories doivent être sélectionnées pour que les données s’affichent.

![](../images/enforcement/lineage-filter.png)

Sélectionnez **[!UICONTROL vue de Liste]** pour afficher la lignée de données comme liste. Pour revenir au graphique visuel, sélectionnez **[!UICONTROL vue de chemin]**.

![](../images/enforcement/list-view.png)

## Application des politiques pour les segments activés   {#policy-enforcement-for-activated-segments}

L’application de la politique s’applique toujours aux segments une fois qu’ils ont été activés, ce qui limite toute modification apportée à un segment ou à sa destination qui entraînerait une violation de la politique. En raison de la manière dont [la lignée de données](#lineage) fonctionne dans l&#39;application des stratégies, l&#39;une des actions suivantes peut potentiellement déclencher une violation :

* Mise à jour des libellés d’utilisation des données
* Modification des jeux de données d’un segment
* Modification des prédicats de segment
* Modification des configurations de destination

Si l’une des actions ci-dessus déclenche une violation, l’enregistrement de cette action est bloquée et un message de violation de politique s’affiche, ce qui vous permet de vérifier que les segments que vous avez activés continuent à respecter les politiques d’utilisation des données lors de leur modification.

## Étapes suivantes

Ce document couvrait le fonctionnement de l&#39;application automatique de la stratégie en Experience Platform. Pour savoir comment intégrer par programmation l&#39;application de stratégies dans vos applications à l&#39;aide d&#39;appels d&#39;API, consultez le guide [Application basée sur les API](./api-enforcement.md).
