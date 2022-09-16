---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;balise;détails d’interaction;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de balise
topic-legacy: overview
description: Ce document présente la classe XDM Individual Profile.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 12%

---

# [!UICONTROL Balise] type de données

[!UICONTROL Balise] est un type de données XDM standard qui décrit l’appareil sans fil qui communique des informations d’identité aux applications mobiles à mesure que les appareils mobiles sont en portée.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconMajor` | Double | Les valeurs majeures identifient et distinguent un groupe et des valeurs entières non signées comprises entre 1 et 65 535. |
| `beaconMinor` | Double | Les valeurs mineures identifient et distinguent une valeur entière individuelle et non signée entre 1 et 65 535. |
| `proximity` | Chaîne | Distance estimée de la balise. Voir [annexe](#proximity) pour les valeurs et définitions acceptées. |
| `proximityUUID` | Chaîne | Un UUID de proximité (Universally Unique Identifier) est un type spécial d’identifiant utilisé pour distinguer les balises de votre réseau de toutes les autres balises des réseaux hors de votre contrôle. L’UUID de proximité est configuré dans une balise, à transmettre aux appareils mobiles à portée afin d’identifier les balises d’une organisation. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur la variable [!UICONTROL Balise] type de données.

## Valeurs acceptées pour la proximité {#proximity}

Le tableau suivant décrit les valeurs acceptées pour `proximity` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `immediate` | Dans quelques centimètres. |
| `near` | À moins de 10 mètres. |
| `far` | Plus de 10 mètres plus loin. |
| `unknown` | La distance n&#39;a pas pu être établie, probablement à cause d&#39;un signal faible. |
