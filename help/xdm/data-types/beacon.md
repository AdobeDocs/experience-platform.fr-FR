---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Type de données de balise
topic: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---


# [!UICONTROL Type de données de balise]

[!UICONTROL La balise] est un type de données XDM standard qui décrit le périphérique sans fil qui communique des informations d&#39;identité aux applications mobiles lorsque les périphériques mobiles sont compris dans la plage définie.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `beaconMajor` | Double | Les valeurs principales identifient et distinguent un groupe et des entiers non signés entre 1 et 65 535. |
| `beaconMinor` | Double | Des valeurs mineures identifient et distinguent des valeurs entières individuelles et non signées comprises entre 1 et 65 535. |
| `proximity` | Chaîne | Distance estimée de la balise. Consultez l&#39; [annexe](#proximity) pour connaître les valeurs et les définitions acceptées. |
| `proximityUUID` | Chaîne | Un UUID de proximité (Universally Unique Identifier) est un type spécial d&#39;identifiant utilisé pour distinguer les balises de votre réseau de toutes les autres balises des réseaux qui ne sont pas sous votre contrôle. L&#39;UUID de proximité est configuré dans une balise, qui doit être transmise aux périphériques mobiles dans la plage pour identifier les balises d&#39;une organisation. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Balise] .

## Valeurs acceptées pour la proximité {#proximity}

Le tableau suivant présente les valeurs acceptées pour `proximity` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `immediate` | En quelques centimètres. |
| `near` | À moins de 10 mètres. |
| `far` | Plus de 10 mètres plus loin. |
| `unknown` | La distance n&#39;a pas pu être déterminée, probablement en raison d&#39;un signal faible. |