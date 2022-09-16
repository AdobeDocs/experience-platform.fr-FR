---
title: Tri des réponses dans l’API Reactor
description: Découvrez comment filtrer les résultats lorsque les ressources sont répertoriées dans l’API Reactor.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---

# Tri des réponses dans l’API Reactor

Répertorier les points d’entrée de l’API Reactor vous permet de trier les ressources renvoyées en fonction d’attributs spécifiés. Vous pouvez configurer l’ordre de tri de la réponse en fournissant un paramètre `sort` dans le chemin de la requête.

## Tri croissant

Les ressources peuvent être triées par attribut dans l’ordre croissant en spécifiant
l’attribut avec lequel trier et en lui ajoutant un préfixe `+` :

`GET /companies/:company_id/properties?sort=+name`

## Tri décroissant

Les ressources peuvent être triées par attribut dans l’ordre décroissant en spécifiant
l’attribut avec lequel trier et en lui ajoutant un préfixe `-` :

`GET /companies/:company_id/properties?sort=-name`

## Tris multiples

Pour trier par plusieurs valeurs, indiquez les directives de tri sous la forme d’une liste
aux termes séparés par des virgules :

`GET /companies/:company_id/properties?sort=+name,-org_id`
