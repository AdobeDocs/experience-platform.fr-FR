---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; identité ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d'identité
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM d'identité.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 10%

---

# [!UICONTROL Type ] Identitydata

[!UICONTROL L’] identification est un type de données XDM standard utilisé pour distinguer clairement les personnes qui interagissent avec des expériences numériques. L&#39;identité est établie par un fournisseur d&#39;identité, qui est lui-même référencé dans un attribut `namespace`. Dans chaque `namespace`, l&#39;identité est unique.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `namespace` | Objet | Objet contenant un seul champ de chaîne (`code`), qui indique l’espace de nommage associé à l’attribut `id` fourni. |
| `authenticatedState` | Chaîne | État authentifié pour cette identité au moment du Événement d’expérience observé. Voir l&#39;[annexe](#authenticatedState) pour connaître les valeurs et les définitions acceptées. |
| `id` | Chaîne | L&#39;identité du consommateur dans l&#39;espace de nommage associé. |
| `primary` | Booléen | Indique s’il s’agit de l’identité Principale de l’individu. Chaque individu ne peut avoir qu&#39;une seule identité Principale. |
| `xid` | Chaîne | Lorsqu’elle est présente, cette valeur représente un identifiant d’espace de noms croisé unique pour tous les identifiants d’espace de noms inclus dans tous les espaces de noms. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Identity].

## Valeurs acceptées pour authenticatedState {#authenticatedState}

Le tableau suivant décrit les valeurs acceptées pour `authenticatedState` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `ambiguous` | L’état authentifié est ambigu. |
| `authenticated` | L’utilisateur a été identifié par une connexion ou une action similaire valide au moment de l’observation du événement. |
| `loggedOut` | L’utilisateur a été identifié par une action de connexion à un moment donné, mais n’a pas été connecté au moment de l’observation du événement. |
