---
title: Groupe de champs de schéma des détails de publicité
description: Ce document fournit un aperçu du groupe de champs de schéma Détails de publicité .
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 22%

---

# [!UICONTROL Détails de la publicité] groupe de champs de schéma

[!UICONTROL Détails de la publicité] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `advertising` à un schéma, qui capture les informations liées aux impressions publicitaires, aux clics publicitaires et à l’attribution.

![Structure du groupe de champs](../../images/field-groups/advertising-details/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `adAssetReference` | Objet | Capture les informations sur les ressources de la publicité. Voir [sous-section](#adAssetReference) pour plus d’informations sur la structure de cet objet. |
| `adAssetViewDetails` | Objet | Capture les détails de la vue pour la lecture de publicité. Voir [sous-section](#adAssetViewDetails) pour plus d’informations sur la structure de cet objet. |
| `adViewability` | Objet | Capture le nombre d’impressions vues par les utilisateurs finaux, telles que le volume du lecteur, la version de la bibliothèque, l’état de la fenêtre et les dimensions de la fenêtre d’affichage des publicités. Voir [sous-section](#adViewability) pour plus d’informations sur la structure de cet objet. |
| `clicks` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre d’actions de clics sur la publicité. |
| `completes` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une ressource multimédia minutée a été visionnée jusqu’à la fin. Cela ne signifie pas nécessairement que l’utilisateur final a visionné l’ensemble de la vidéo, car il a peut-être ignoré. |
| `conversions` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une action prédéfinie (ou des actions) ont déclenché un événement pour l’évaluation des performances. |
| `federated` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Indique si un événement d’expérience a été créé par le biais d’une fédération de données, comme le partage de données entre les clients. |
| `firstQuartiles` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une publicité vidéo numérique a été lue pendant 25 % de sa durée à une vitesse normale. |
| `impressions` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre d’impressions publicitaires envoyées à un utilisateur final avec la possibilité d’être visualisées. |
| `midpoints` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une publicité vidéo numérique a été lue pendant 50 % de sa durée à une vitesse normale. |
| `starts` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une publicité vidéo numérique a commencé à être lue. |
| `thirdQuartiles` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Nombre de fois où une publicité vidéo numérique a été lue pendant 75 % de sa durée à une vitesse normale. |
| `timePlayed` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Durée passée par un utilisateur final sur une ressource multimédia minutée spécifique. |
| `downloadedPlayback` | Booléen | Lorsque la variable est définie sur `true`, indique que l’accès est généré en raison de la lecture d’une session de publicité téléchargée. |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

Le `adAssetReference` capture les informations sur les ressources de la publicité.

![Structure adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc.title` | Chaîne | Nom convivial et lisible de la ressource publicitaire. |
| `_xmpDM.duration` | Nombre entier | Durée ou durée de la ressource en secondes. |
| `_id` | Chaîne | Identifiant unique de la ressource publicitaire, selon la variable [Ad-ID standard](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Chaîne | Entreprise ou marque dont le produit apparaît dans la publicité. |
| `campaign` | Chaîne | ID de la campagne publicitaire. |
| `creativeID` | Chaîne | ID de l’élément créatif publicitaire. |
| `creativeURL` | Chaîne | URL de l’élément créatif publicitaire. |
| `placementID` | Chaîne | Identifiant de référencement de la publicité. |
| `siteID` | Chaîne | ID du site publicitaire. |

{style=&quot;table-layout:auto&quot;}

## `adAssetViewDetails` {#adAssetViewDetails}

Le `adAssetViewDetails` capture les détails d’affichage de la lecture de publicité.

![Structure adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Coupure publicitaire]](../../data-types/ad-break.md) | Décrit la manière dont une publicité minutée est insérée dans un média minuté. |
| `index` | Nombre entier | Index de la publicité dans la coupure publicitaire parente. Par exemple, la première publicité comporte l’index `0` et la deuxième publicité comporte l’index `1`. |
| `playerName` | Chaîne | Nom du lecteur responsable du rendu de la publicité. |

{style=&quot;table-layout:auto&quot;}

## `adViewability` {#adViewability}

Le `adViewability` capture le nombre d’impressions vues par les utilisateurs finaux, telles que le volume du lecteur, la version de la bibliothèque, l’état de la fenêtre et les dimensions de la fenêtre d’affichage des publicités.

![structure adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Détails d’implémentation]](../../data-types/implementation-details.md) | Nom et version de la bibliothèque instrumentée pour évaluer les mesures de visibilité. |
| `measuredAdNotVisible` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Indique que la publicité n’est pas visible comme mesuré par une bibliothèque de visibilité au moment de l’impression. |
| `measuredMuted` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Indique que la publicité est mutée comme mesurée par une bibliothèque de visibilité au moment de l’impression. |
| `unmeasurableIframe` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Indique que la publicité s’affiche dans une fenêtre inactive comme mesuré par une bibliothèque de visibilité au moment de l’impression. |
| `unmeasurableOther` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Indique que la bibliothèque de visibilité n’est pas en mesure d’exécuter correctement les mesures en raison de la publicité affichée dans un iFrame. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Impressions d’une publicité destinée à un utilisateur final avec une bibliothèque de visibilité instrumentée. |
| `viewabilityCompletes` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Fin d’une publicité destinée à un utilisateur final jugée visible au moment de l’achèvement par une bibliothèque de visibilité. |
| `viewableFirstQuartiles` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Premier quartile d’une publicité destinée à un utilisateur final jugée visible au premier quartile de lecture par une bibliothèque de visibilité. |
| `viewableImpressions` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Impressions d’une publicité destinée à un utilisateur final jugée visible après deux secondes de lecture par une bibliothèque de visibilité. |
| `viewableMidpoints` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Points médians d’une publicité destinée à un utilisateur final jugée visible au milieu de la lecture par une bibliothèque de visibilité. |
| `viewableThirdQuartiles` | [[!UICONTROL Mesure]](../../data-types/measure.md) | Troisième quartile d’une publicité destinée à un utilisateur final jugée visible au troisième quartile de lecture par une bibliothèque de visibilité. |
| `activeWindow` | Booléen | Indique si la publicité a été affichée dans la principale fenêtre de l’appareil de l’utilisateur. |
| `adHeight` | Nombre entier | Nombre de pixels verticaux du lecteur, mesuré au moment de l’exécution. Cette taille peut être supérieure à la taille de la publicité si le lecteur dispose de commandes ou de miniatures en supplément. |
| `adUnitDepth` | Nombre entier | Les éditeurs peuvent incorporer des unités publicitaires dans des conteneurs (iFrames) afin de limiter l’accès de la publicité uniquement au code de la page. Cette valeur décrit le nombre de conteneurs dans lesquels l’unité publicitaire est affichée. |
| `adWidth` | Nombre entier | Nombre de pixels horizontaux du lecteur, mesuré au moment de l’exécution. Cette taille peut être supérieure à la taille de la publicité si le lecteur dispose de commandes ou de miniatures en supplément. |
| `measurementEligible` | Booléen | Précise si la publicité était éligible à la mesure de la visibilité. Une publicité est éligible si le format de création et le type de balise de l’unité sont pris en charge. |
| `percentViewable` | Nombre entier | Pourcentage de pixels dans la publicité jugés visibles au moment de la mesure. |
| `playerVolume` | Nombre entier | Pourcentage du volume du lecteur, mesuré au moment de l’exécution, où `0` est muet et `100` est le volume maximal. |
| `viewable` | Booléen | Indique si la publicité était visible au moment de l’exécution. Les publicités affichées sont considérées comme visibles lorsqu’au moins 50 % de la publicité est visible pendant au moins une seconde. Les publicités vidéo sont considérées comme visibles lorsqu’au moins 50 % de la publicité est visible pendant la lecture de la vidéo pendant au moins deux secondes consécutives. |
| `viewportHeight` | Nombre entier | Taille verticale (en pixels) de la fenêtre dans laquelle l’expérience a été affichée, mesurée au moment de l’exécution. Pour un événement d’affichage web, cette valeur indique la hauteur de la fenêtre d’affichage du navigateur. |
| `viewportWidth` | Nombre entier | Taille horizontale (en pixels) de la fenêtre dans laquelle l’expérience a été affichée, mesurée au moment de l’exécution. Pour un événement d’affichage web, cette valeur indique la largeur de la fenêtre d’affichage du navigateur. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
