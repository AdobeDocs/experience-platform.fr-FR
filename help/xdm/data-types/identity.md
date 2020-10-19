---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: Type de données d'identité
topic: overview
description: Ce document présente un aperçu du type de données XDM d'identité.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 11%

---


# [!UICONTROL Type de données d&#39;identité]

[!UICONTROL Identity] est un type de données XDM standard qui permet de distinguer clairement les personnes qui interagissent avec des expériences numériques. L&#39;identité est établie par un fournisseur d&#39;identité, qui est lui-même référencé dans un `namespace` attribut. Dans chaque `namespace`cas, l&#39;identité est unique.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `namespace` | Objet | Objet contenant un seul champ de chaîne (`code`), qui indique l’espace de nommage associé à l’ `id` attribut fourni. |
| `authenticatedState` | Chaîne | État authentifié pour cette identité au moment du Événement d’expérience observé. Consultez l&#39; [annexe](#authenticatedState) pour connaître les valeurs et les définitions acceptées. |
| `id` | Chaîne | L&#39;identité du consommateur dans l&#39;espace de nommage associé. |
| `primary` | Booléen | Indique s’il s’agit de l’identité Principale de l’individu. Chaque individu ne peut avoir qu&#39;une seule identité Principale. |
| `xid` | Chaîne | Lorsqu’elle est présente, cette valeur représente un identifiant d’espace de noms croisé unique pour tous les identifiants d’espace de noms inclus dans tous les espaces de noms. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Identité] .

## Valeurs acceptées pour authenticatedState {#authenticatedState}

Le tableau suivant présente les valeurs acceptées pour `authenticatedState` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `ambiguous` | L’état authentifié est ambigu. |
| `authenticated` | L’utilisateur a été identifié par une connexion ou une action similaire valide au moment de l’observation du événement. |
| `loggedOut` | L’utilisateur a été identifié par une action de connexion à un moment donné, mais n’a pas été connecté au moment de l’observation du événement. |