---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;identité;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d’identité
description: Découvrez le type de données XDM d’identité.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 11%

---

# Type de données [!UICONTROL Identity]

[!UICONTROL Identité] est un type de données XDM standard utilisé pour distinguer clairement les personnes qui interagissent avec des expériences digitales. L’identité est établie par un fournisseur d’identité, qui est lui-même référencé dans un attribut `namespace`. Au sein de chaque `namespace`, l’identité est unique.

![](../images/data-types/identity.png){width=550}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `namespace` | Objet | Objet contenant un champ de chaîne unique (`code`), qui indique l’espace de noms associé à l’attribut `id` fourni. |
| `authenticatedState` | Chaîne | État authentifié de cette identité au moment de l’événement d’expérience observé. Voir l’[annexe](#authenticatedState) pour connaître les valeurs et définitions acceptées. |
| `id` | Chaîne | Identité du client dans l’espace de noms associé. |
| `primary` | Booléen | Indique s’il s’agit de l’identité principale de l’individu. Chaque individu ne peut avoir qu’une seule identité principale. |
| `xid` | Chaîne | Lorsqu’elle est présente, cette valeur représente un identifiant d’espace de noms croisé unique pour tous les identifiants d’espace de noms inclus dans tous les espaces de noms. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Identity].

## Valeurs acceptées pour authenticatedState {#authenticatedState}

Le tableau suivant décrit les valeurs acceptées pour les `authenticatedState` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `ambiguous` | L’état d’authentification est ambigu. |
| `authenticated` | L’utilisateur a été identifié par une connexion ou une action similaire valide au moment de l’observation de l’événement. |
| `loggedOut` | L’utilisateur a été identifié par une action de connexion à un moment précédent, mais n’était pas connecté au moment de l’observation de l’événement. |
