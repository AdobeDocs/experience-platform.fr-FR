---
keywords: Experience Platform;accueil;rubriques populaires;Application des politiques;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Application automatique des politiques
description: Ce document présente l’application automatique des politiques d’utilisation de données lors de l’activation d’audiences vers des destinations dans Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 70%

---

# Application automatique des politiques

Les libellés et politiques d’utilisation des données sont disponibles pour tous les utilisateurs de Adobe Experience Platform. Définissez des politiques d’utilisation des données et appliquez des libellés d’utilisation des données pour vous assurer que toutes les données sensibles, identifiables ou contractuelles sont traitées avec précision. Ces mesures permettent d’appliquer les règles de gouvernance des données de votre organisation en ce qui concerne la manière dont les données peuvent être accessibles, traitées, stockées et partagées.

Pour protéger votre entreprise des risques et responsabilités potentiels, Experience Platform applique automatiquement les politiques d’utilisation en cas de violation lors de l’activation des audiences vers les destinations.

>[!IMPORTANT]
>
>Les politiques de consentement et l’application automatique des politiques de consentement ne sont disponibles que pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

Ce document se concentre sur l’application des politiques de gouvernance des données et de consentement. Pour plus d’informations sur les politiques de contrôle d’accès, consultez la documentation sur le [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md).

## Conditions préalables

Ce guide nécessite une compréhension pratique des services Experience Platform impliqués dans l’application automatique. Consultez la documentation suivante pour en savoir plus avant de poursuivre avec ce guide :

* [Gouvernance des données de Adobe Experience Platform ](../home.md) : cadre en fonction duquel Experience Platform applique la conformité de l’utilisation des données à l’aide des libellés et des politiques.
* [Profil client en temps réel](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Segmentation Service d’Adobe Experience Platform](../../segmentation/home.md) : moteur de segmentation de [!DNL Experience Platform] utilisé pour créer des audiences à partir de vos profils clients en fonction du comportement et des attributs de la clientèle.
* [Destinations](../../destinations/home.md) : les destinations sont des intégrations préconfigurées aux applications couramment utilisées. Elles permettent l’activation transparente des données d’Experience Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée, etc.

## Flux d’application {#flow}

Le diagramme suivant illustre la procédure d’intégration des politiques dans le train de données de l’activation des audiences :

![Illustration de la manière dont l’application des stratégies est intégrée au train de données de l’activation des audiences.](../images/enforcement/enforcement-flow.png)

Lorsqu’une audience est activée pour la première fois, [!DNL Policy Service] vérifie les politiques applicables en fonction des facteurs suivants :

* Les libellés d’utilisation des données ont été appliqués aux champs et aux jeux de données de l’audience à activer.
* Objectif marketing de la destination.
* Les profils qui ont consenti à être inclus dans l’activation des audiences, sur la base de vos politiques de consentement configurées.

>[!NOTE]
>
>Si des libellés d’utilisation des données n’ont été appliqués qu’à certains champs, l’application de ces libellés au niveau du champ sur l’activation ne se produit que si au moins l’une des conditions suivantes est remplie :
>
>* Les champs sont utilisés dans l’audience.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination cible.

## Parenté des données {#lineage}

La parenté des données joue un rôle essentiel dans la manière dont les politiques sont appliquées dans Experience Platform. D’une façon générale, la parenté des données fait référence à l’origine d’un jeu de données ainsi qu’à son évolution (ou à son déplacement) au fil du temps.

Dans le cadre de la gouvernance des données, la parenté permet aux libellés d’utilisation des données de se propager des schémas aux services en aval qui utilisent leurs données, comme le profil client en temps réel et les destinations. Cela permet d’évaluer et d’appliquer les politiques à plusieurs points essentiels du parcours des données via Experience Platform et fournit un contexte aux consommateurs de données quant aux raisons pour lesquelles une violation de politique a eu lieu.

Dans Experience Platform, l’application des politiques est concernée par la parenté suivante :

1. Les données sont ingérées dans Experience Platform et stockées dans des **jeux de données**.
1. Les profils clients sont identifiés et construits à partir de ces jeux de données grâce à la fusion des fragments de données, conformément à la **politique de fusion**.
1. Les groupes de profils sont divisés en **audiences** en fonction d’attributs communs.
1. Les audiences sont activées pour les **destinations** en aval.

Chaque étape de la chronologie ci-dessus représente une entité qui peut contribuer à l’application de la politique, comme indiqué dans le tableau ci-dessous :

| Étape relative à la parenté des données | Rôle dans l’application des politiques |
| --- | --- |
| Jeu de données | Les jeux de données contiennent des libellés d’utilisation des données (appliqués au niveau du champ de schéma ou du champ de l’intégralité du jeu de données) qui définissent les cas d’utilisation pour lesquels l’intégralité du jeu de données ou des champs spécifiques peut être utilisée. Des violations de politique se produisent si un jeu de données ou un champ contenant certains libellés est utilisé à des fins limitées par une politique.<br><br>Tous les attributs de consentement collectés auprès de vos clients sont également stockés dans des jeux de données. Si vous avez accès aux politiques de consentement, tous les profils qui ne répondent pas aux exigences d’attribut de consentement de vos politiques seront exclus des audiences qui sont activées vers une destination. |
| Politique de fusion | Les politiques de fusion sont les règles utilisées par Experience Platform pour déterminer quelle est la priorité des données lors de la fusion de fragments provenant de plusieurs jeux de données. Des violations de politique se produisent si vos politiques de fusion sont configurées de telle sorte que les jeux de données dotés de libellés limités sont activés pour une destination. Pour plus d’informations, consultez la [présentation des politiques de fusion](../../profile/merge-policies/overview.md). |
| Audience | Les règles de segmentation définissent les attributs à inclure dans les profils clients. En fonction des champs inclus dans une définition de segment, l’audience hérite des libellés d’utilisation appliqués pour ces champs. Des violations de politique se produisent si vous tentez d’activer une audience dont les libellés hérités sont limités par les politiques applicables de la destination cible, en fonction de son cas d’utilisation marketing. |
| Destination | Lors de la configuration d’une destination, une action marketing (parfois appelée cas d’utilisation marketing) peut être définie. Ce cas d’utilisation correspond à une action marketing telle que définie dans une politique. En d’autres termes, l’action marketing que vous définissez comme une destination détermine les politiques d’utilisation des données et de consentement applicables à cette destination.<br><br>Des violations de politique d’utilisation des données se produisent si vous tentez d’activer une audience dont les libellés d’utilisation sont limités pour l’action marketing de la destination cible.<br><br>(Version Beta) Lorsqu’une audience est activée, tous les profils qui ne contiennent pas les attributs de consentement requis pour l’action marketing (tels que définis par vos politiques de consentement) sont exclus de l’audience activée. |

>[!IMPORTANT]
>
>Certaines politiques d’utilisation des données peuvent spécifier plusieurs libellés avec une relation AND. Par exemple, une politique peut limiter une action marketing si les libellés `C1` ET `C2` sont tous deux présents. Toutefois, elle ne limite pas l’action en question si un seul de ces libellés est présent.
>
>En ce qui concerne l’application automatique, le cadre de gouvernance des données ne considère pas l’activation d’audiences distinctes vers une destination comme une combinaison de données. Par conséquent, la politique `C1 AND C2` d’exemple n’est **PAS** appliquée si ces libellés sont inclus dans des audiences distinctes. Au lieu de cela, cette politique n’est appliquée que lorsque les deux libellés sont présents dans la même audience lors de l’activation.

Lorsque des violations de politique se produisent, les messages qui s’affichent dans l’interface utilisateur fournissent des outils utiles à l’exploration de la parenté des données contribuant à la violation afin de résoudre le problème. Vous trouverez plus de détails dans la section suivante.

## Messages d’application de politique {#enforcement}

Les sections ci-dessous décrivent les différents messages d’application de politique qui apparaissent dans l’interface utilisateur d’Experience Platform :

* [Violation de la politique d’utilisation des données](#data-usage-violation)
* [Évaluation des politiques de consentement](#consent-policy-evaluation)

### Violation de la politique d’utilisation des données {#data-usage-violation}

Si une violation de politique se produit lors de la tentative d’activation d’une audience (ou de la [modification d’une audience déjà activée](#policy-enforcement-for-activated-audiences)), l’action est bloquée et une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs politiques ont été violées. Une fois qu’une violation a été déclenchée, le bouton **[!UICONTROL Enregistrer]** est désactivé pour l’entité à modifier jusqu’à ce que les composants appropriés soient mis à jour pour se conformer aux politiques d’utilisation des données.

Sélectionnez un nom de politique pour afficher les détails de cette violation.

![Une boîte de dialogue indiquant qu’une violation de politique s’est produite avec le nom de la politique mis en surbrillance.](../images/enforcement/violation-policy-select.png)

Le message relatif à la violation présente un résumé de la politique enfreinte, y compris les conditions configurées pour être vérifiées par la politique, l’action spécifique qui a déclenché la violation ainsi qu’une liste de résolutions possibles pour le problème.

![Boîte de dialogue de violation de la politique avec le résumé de la violation mis en surbrillance.](../images/enforcement/violation-summary.png)

Un graphique relatif à la parenté des données s’affiche sous le résumé de la violation. Cela vous permet de visualiser les jeux de données, les politiques de fusion, les audiences et les destinations impliqués dans la violation de la politique. L’entité que vous modifiez actuellement est mise en surbrillance dans le graphique, ce qui indique le point du flux à l’origine de la violation. Vous pouvez sélectionner un nom d’entité dans le graphique pour ouvrir la page de détails de l’entité en question.

![Boîte de dialogue de violation de la politique avec le graphique de parenté des données mis en surbrillance.](../images/enforcement/data-lineage.png)

Vous pouvez également utiliser l’icône **[!UICONTROL Filtre]** (![Icône Filtrer.](/help/images/icons/filter.png)) pour filtrer les entités affichées par catégorie. Au moins deux catégories doivent être sélectionnées pour que les données s’affichent.

![Boîte de dialogue de violation de la politique avec le filtre de parenté des données et le menu déroulant en surbrillance.](../images/enforcement/lineage-filter.png)

Sélectionnez **[!UICONTROL Vue Liste]** pour afficher la parenté des données sous forme de liste. Pour revenir au graphique visuel, sélectionnez **[!UICONTROL Chemin parcouru]**.

![Boîte de dialogue de violation de la politique avec la vue de chemin de parenté des données mise en surbrillance.](../images/enforcement/list-view.png)

#### Libellés appliqués avec succès {#labels-successfully-applied}

Si vous créez des politiques d’utilisation des données avant d’étiqueter vos champs de schéma, vous pouvez rencontrer une boîte de dialogue de violation de la politique de gouvernance dès que vous appliquez des libellés à votre schéma. Dans ce cas, vous pouvez étiqueter correctement une partie de votre schéma. L’onglet [!UICONTROL &#x200B; Libellés appliqués avec succès &#x200B;] indique quels libellés ont été appliqués avec succès, car il n’existe aucune restriction de politique pour ce champ.

Utilisez le diagramme de parenté des données pour comprendre quelles autres modifications de configuration doivent être apportées avant de pouvoir ajouter le libellé à votre champ de schéma.

![Boîte de dialogue de violation de la politique avec l’onglet [!UICONTROL &#x200B; Libellés appliqués avec succès] mis en surbrillance.](../images/enforcement/labels-successfully-applied.png)

### Évaluation des politiques de consentement {#consent-policy-evaluation}

Lors de l’activation d’une audience vers une destination, vous pouvez voir comment vos [ politiques de consentement ](../policies/user-guide.md) affectent la portée de votre audience pendant l’étape de révision [ du workflow [!UICONTROL &#x200B; Activer des destinations &#x200B;]](#pre-activation-evaluation).

>[!NOTE]
>
>Les politiques de consentement ne sont disponibles que pour les organisations qui ont acheté Adobe Healthcare Shield ou Adobe Privacy &amp; Security Shield.

#### Amélioration de la stratégie de consentement pour les médias achetés {#consent-policy-enhancement}

Amélioration de l’application de la politique de consentement sur les destinations par [lots](../../destinations/destination-types.md#file-based) et de [streaming](../../destinations/destination-types.md#streaming-destinations), y compris les activations de médias achetés. Cette amélioration est disponible pour la clientèle de Privacy and Security Shield ou de Healthcare Shield. Elle supprime de manière proactive les profils des destinations par lots et de streaming à mesure que le statut du consentement change. Elle garantit également que les modifications du consentement sont propagées immédiatement afin que la bonne audience soit toujours ciblée.

Ces améliorations permettent une plus grande confiance dans votre stratégie marketing, car elles éliminent la nécessité pour les spécialistes marketing d’ajouter manuellement des attributs de consentement à l’expression de leur segment. Cela permet de s’assurer qu’aucun profil n’est ciblé par inadvertance pour une expérience marketing une fois que le consentement a été retiré ou qu’il n’est plus éligible pour une politique de consentement. Les politiques de consentement marketing qui définissent les règles de gestion des données de consentement ou de préférence dans divers workflows marketing sont désormais automatiquement appliquées dans les workflows d’activation dans les solutions en aval.

>[!NOTE]
>
>Cette amélioration n’a entraîné aucune modification de l’IU.

#### Évaluation préalable à l’activation {#pre-activation-evaluation}

Une fois que vous avez atteint l’étape **[!UICONTROL Réviser]** lors de l’[activation d’une destination](../../destinations/ui/activation-overview.md), sélectionnez **[!UICONTROL Afficher les politiques appliquées]**.

![Bouton Afficher les politiques appliquées dans le workflow d’activation de la destination](../images/enforcement/view-applied-policies.png)

Une boîte de dialogue de vérification de politique s’affiche, vous montrant un aperçu de la manière dont vos politiques de consentement affectent l’audience consentante des audiences à activer.

![Boîte de dialogue de vérification de la politique de consentement dans l’interface utilisateur d’Experience Platform](../images/enforcement/consent-policy-check.png)

La boîte de dialogue affiche l’audience consentante pour une audience à la fois. Pour afficher l’évaluation des politiques pour une autre audience, utilisez le menu déroulant situé au-dessus du diagramme pour en sélectionner une dans la liste.

![Sélecteur d’audience dans la boîte de dialogue de vérification des politiques.](../images/enforcement/audience-switcher.png)

Utilisez le rail de gauche pour basculer entre les politiques de consentement applicables pour l’audience sélectionnée. Les politiques qui ne sont pas sélectionnées sont représentées dans la section « [!UICONTROL Autres politiques] » du diagramme.

![Sélecteur de politique dans la boîte de dialogue de vérification des politiques](../images/enforcement/policy-switcher.png)

Le diagramme affiche le chevauchement entre trois groupes de profils :

1. Profils qui remplissent les critères de l’audience sélectionnée
1. Profils qui remplissent les critères de la politique de consentement sélectionnée
1. Profils qui remplissent les critères des autres politiques de consentement applicables pour l’audience (appelées « [!UICONTROL Autres politiques] » dans le diagramme)

Les profils qui remplissent les critères pour les trois groupes ci-dessus représentent l’audience consentante, résumée dans le rail de droite.

![Section résumé de la boîte de dialogue de vérification des politiques](../images/enforcement/summary.png)

Passez la souris sur l’une des audiences du diagramme pour afficher le nombre de profils qu’il contient.

![Mise en surbrillance d’une section de diagramme dans la boîte de dialogue de vérification des politiques](../images/enforcement/highlight-segment.png)

L’audience consentante est représentée par le chevauchement central du diagramme et peut être mise en surbrillance comme les autres sections.

![L’audience consentante mise en surbrillance dans le diagramme](../images/enforcement/consented-audience.png)

#### Application d’exécution de flux

Lorsque les données sont activées vers une destination, les détails de l’exécution du flux indiquent le nombre d’identités qui ont été exclues en raison de politiques de consentement actives.

![Mesures d’identités exclues pour une exécution de flux de données](../images/enforcement/dataflow-run-enforcement.png)

## Application des politiques pour les audiences activées {#policy-enforcement-for-activated-audiences}

L’application de la politique s’effectue toujours sur les audiences une fois qu’elles ont été activées, ce qui limite toute modification apportée à une audience ou à sa destination qui entraînerait une violation de la politique. En raison du fonctionnement de la [parenté des données](#lineage) dans l’application des politiques, l’une des actions suivantes peut potentiellement déclencher une violation :

* Mise à jour des libellés d’utilisation des données
* Modifier les jeux de données d’une audience
* Modifier les prédicats d’audience
* Modification des configurations de destination

Si l’une des actions ci-dessus déclenche une violation, l’enregistrement de cette action est bloqué et un message de violation de politique s’affiche, ce qui vous permet de vérifier que les audiences que vous avez activées continuent à respecter les politiques d’utilisation des données lors de leur modification.

## Étapes suivantes

Ce document vous a présenté le fonctionnement de l’application automatique des politiques dans Experience Platform. Pour savoir comment intégrer par programmation l’application de politiques dans vos applications à l’aide d’appels d’API, consultez le guide sur l’[application basée sur les API](./api-enforcement.md).
