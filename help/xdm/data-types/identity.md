---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;identité;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’identification
description: Ce document fournit un aperçu du type de données XDM d’identité.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 16%

---

# [!UICONTROL Identité] type de données

[!UICONTROL Identité] est un type de données XDM standard utilisé pour distinguer clairement les personnes qui interagissent avec des expériences numériques. L’identité est établie par un fournisseur d’identité, qui est lui-même référencé dans une variable `namespace` attribut. Dans chaque `namespace`, l’identité est unique.

<img src="../images/data-types/identity.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `namespace` | Objet | Objet contenant un seul champ de chaîne (`code`), qui indique l’espace de noms associé au fourni `id` attribut. |
| `authenticatedState` | Chaîne | État authentifié de cette identité au moment de l’événement d’expérience observé. Voir [annexe](#authenticatedState) pour les valeurs et définitions acceptées. |
| `id` | Chaîne | Identité du consommateur dans l’espace de noms associé. |
| `primary` | Booléen | Indique s’il s’agit de l’identité Principale de l’individu. Chaque individu ne peut avoir qu&#39;une seule identité Principale. |
| `xid` | Chaîne | Lorsqu’elle est présente, cette valeur représente un identifiant d’espace de noms croisé unique pour tous les identifiants d’espace de noms inclus dans tous les espaces de noms. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur la variable [!UICONTROL Identité] type de données.

## Valeurs acceptées pour authenticatedState {#authenticatedState}

Le tableau suivant décrit les valeurs acceptées pour `authenticatedState` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `ambiguous` | L’état authentifié est ambigu. |
| `authenticated` | L’utilisateur a été identifié par une connexion ou une action similaire qui était valide au moment de l’observation de l’événement. |
| `loggedOut` | L’utilisateur a été identifié par une action de connexion à un moment donné auparavant, mais n’a pas été connecté au moment de l’observation de l’événement. |
