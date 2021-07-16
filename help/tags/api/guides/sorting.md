---
title: Tri des réponses dans l’API Reactor
description: Découvrez comment filtrer les résultats lors de la liste des ressources dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Tri des réponses dans l&#39;API Reactor

Les points de terminaison de liste de l’API Reactor vous permettent de trier les ressources renvoyées en fonction d’attributs spécifiés. Vous pouvez configurer l’ordre de tri de la réponse en fournissant un paramètre `sort` dans le chemin de la requête.

## Tri croissant

Les ressources peuvent être triées par attribut dans l’ordre croissant en spécifiant la variable
par lequel trier et en lui ajoutant un préfixe `+` :

`GET /companies/:company_id/properties?sort=+name`

## Tri décroissant

Les ressources peuvent être triées par attribut dans l’ordre décroissant en spécifiant la variable
par lequel trier et en lui ajoutant un préfixe `-` :

`GET /companies/:company_id/properties?sort=-name`

## Plusieurs types

Pour trier par plusieurs valeurs, indiquez les directives de tri sous la forme d’une virgule.
list :

`GET /companies/:company_id/properties?sort=+name,-org_id`
