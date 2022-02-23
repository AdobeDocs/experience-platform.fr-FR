---
title: Groupe de champs de schéma d’extension complète Adobe Analytics ExperienceEvent
description: Ce document présente un aperçu du groupe de champs Extension complète d’Adobe Analytics ExperienceEvent .
source-git-commit: bfdcee33fb2cbd28039633d1d981149c40aa1d68
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 8%

---

# [!UICONTROL Extension complète Adobe Analytics ExperienceEvent] groupe de champs de schéma

[!UICONTROL Extension complète Adobe Analytics ExperienceEvent] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), qui capture les mesures courantes collectées par Adobe Analytics.

Ce document décrit la structure et le cas d’utilisation du groupe de champs de l’extension Analytics.

>[!NOTE]
>
>En raison de la taille et du nombre d’éléments répétés dans ce groupe de champs, de nombreux champs affichés dans ce guide ont été réduits pour économiser de l’espace. Pour explorer la structure complète de ce groupe de champs, vous pouvez : [Recherche dans l’interface utilisateur de Platform ](../../ui/explore.md) ou consulter le schéma complet dans la [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Structure du groupe de champs

Le groupe de champs fournit une `_experience` à un schéma, qui contient lui-même une seule `analytics` .

![Champs de niveau supérieur pour le groupe de champs Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `customDimensions` | Objet | Capture les dimensions personnalisées qui font l’objet d’un suivi par Analytics. Voir [sous-section](#custom-dimensions) pour plus d’informations sur le contenu de cet objet. |
| `endUser` | Objet | Capture les détails de l’interaction web pour l’utilisateur final qui a déclenché l’événement. Voir [sous-section](#end-user) pour plus d’informations sur le contenu de cet objet. |
| `environment` | Objet | Capture des informations sur le navigateur et le système d’exploitation qui ont déclenché l’événement. Voir [sous-section](#environment) pour plus d’informations sur le contenu de cet objet. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Objet | Le groupe de champs fournit des champs d’objet pour capturer jusqu’à 1 000 événements personnalisés. Voir [sous-section](#events) pour plus d’informations sur ces champs. |
| `session` | Objet | Capture des informations sur la session qui a déclenché l’événement. Voir [sous-section](#session) pour plus d’informations sur le contenu de cet objet. |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` capture personnalisée [dimensions](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=fr) qui sont suivis par Analytics.

![champ customDimensions](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `eVars` | Objet | Objet qui capture jusqu’à 250 variables de conversion ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=fr)). Les propriétés de cet objet sont indexées. `eVar1` to `eVar250` et n’acceptent que les chaînes pour leur type de données. |
| `hierarchies` | Objet | Objet qui capture jusqu’à cinq variables de hiérarchie personnalisées ([hier](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=fr)). Les propriétés de cet objet sont indexées. `hier1` to `hier5`, qui sont eux-mêmes des objets avec les sous-propriétés suivantes :<ul><li>`delimiter`: Délimiteur d’origine utilisé pour générer la liste fournie sous `values`.</li><li>`values`: Liste délimitée de noms de niveau hiérarchie, représentés sous forme de chaîne.</li></ul> |
| `listProps` | Objet | Un objet qui capture jusqu’à 75 [props de liste](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). Les propriétés de cet objet sont indexées. `prop1` to `prop75`, qui sont eux-mêmes des objets avec les sous-propriétés suivantes :<ul><li>`delimiter`: Délimiteur d’origine utilisé pour générer la liste fournie sous `values`.</li><li>`values`: Liste délimitée de valeurs pour la prop, représentée sous la forme d’une chaîne.</li></ul> |
| `lists` | Objet | Un objet qui capture jusqu’à trois [lists](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). Les propriétés de cet objet sont indexées. `list1` to `list3`. Chacune de ces propriétés contient une seule `list` tableau de [[!UICONTROL Paire de valeurs clés]](../../data-types/key-value-pair.md) types de données. |
| `props` | Objet | Un objet qui capture jusqu’à 75 [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). Les propriétés de cet objet sont indexées. `prop1` to `prop75` et n’acceptent que les chaînes pour leur type de données. |
| `postalCode` | Chaîne | Code postal fourni par le client. |
| `stateProvince` | Chaîne | Emplacement de province ou d’état fourni par le client. |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` capture les détails de l’interaction web pour l’utilisateur final qui a déclenché l’événement.

![Champ endUser](../../images/field-groups/analytics-full-extension/endUser.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Informations web]](../../data-types/web-information.md) | Informations relatives à la page web, au lien et au référent du premier événement d’expérience pour cet utilisateur final. |
| `firstTimestamp` | Nombre entier | Horodatage Unix pour le premier ExperienceEvent pour cet utilisateur final. |

## `environment` {#environment}

`environment` capture les informations sur le navigateur et le système d’exploitation qui ont déclenché l’événement.

![champ d&#39;environnement](../../images/field-groups/analytics-full-extension/environment.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `browserIDStr` | Chaîne | L’identifiant Adobe Analytics du navigateur utilisé (autrement appelé [dimension de type de navigateur](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | Chaîne | Identifiant Adobe Analytics du système d’exploitation utilisé (également appelé [dimension de type de système d&#39;exploitation](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Champs d’événement personnalisés {#events}

Le groupe de champs d’extension Analytics fournit dix champs d’objet qui capturent jusqu’à 100 [mesures d’événement personnalisé](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) chacun, pour un total de 1000 pour le groupe de champs.

Chaque objet d’événement de niveau supérieur contient les objets d’événement individuels pour sa plage respective. Par exemple : `event101to200` contient les événements saisis à partir de `event101` to `event200`.

Chaque objet pair utilise la variable [[!UICONTROL Mesure]](../../data-types/measure.md) type de données, fournissant un identifiant unique et une valeur quantifiable.

![Champ d’événement personnalisé](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` capture les informations sur la session qui a déclenché l’événement.

![champ de session](../../images/field-groups/analytics-full-extension/session.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `search` | [[!UICONTROL Recherche]](../../data-types/search.md) | Capture les informations relatives à la recherche web ou mobile pour l’entrée de session. |
| `web` | [[!UICONTROL Informations web]](../../data-types/web-information.md) | Capture des informations sur les clics sur les liens, les détails de la page web, les informations sur le référent et les détails du navigateur pour l’entrée de session. |
| `depth` | Nombre entier | Profondeur de session actuelle (numéro de page, par exemple) pour l’utilisateur final. |
| `num` | Nombre entier | Numéro de session actuel de l’utilisateur final. |
| `timestamp` | Nombre entier | Horodatage Unix pour l’entrée de session. |

## Étapes suivantes

Ce document couvrait la structure et le cas d’utilisation du groupe de champs de l’extension Analytics. Pour plus d’informations sur le groupe de champs lui-même, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Si vous utilisez ce groupe de champs pour collecter des données Analytics à l’aide du SDK Web de Adobe Experience Platform, consultez le guide sur [configuration d’un flux de données](../../../edge/fundamentals/datastreams.md) pour savoir comment mapper des données à XDM côté serveur.
