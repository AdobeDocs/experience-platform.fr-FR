---
title: Tri des réponses dans l’API Reactor
description: Découvrez comment filtrer les résultats lors de l’établissement de la liste des ressources dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: ht
source-wordcount: '123'
ht-degree: 100%

---

# Tri des réponses dans l’API Reactor

La liste des points d’entrée de l’API Reactor vous permet de trier les ressources renvoyées en fonction d’attributs spécifiés. Vous pouvez configurer l’ordre de tri de la réponse en fournissant un paramètre `sort` dans le chemin d’accès de la requête.

## Tri ascendant

Les ressources peuvent être triées par attribut dans l’ordre ascendant en spécifiant 
l’attribut par lequel trier et en lui ajoutant un préfixe `+` :

`GET /companies/:company_id/properties?sort=+name`

## Tri descendant

Les ressources peuvent être triées par attribut dans l’ordre descendant en spécifiant
l’attribut par lequel trier et en lui ajoutant un préfixe `-` :

`GET /companies/:company_id/properties?sort=-name`

## Tri multiple

Pour trier suivant plusieurs valeurs, indiquez les directives de tri sous la forme de liste
de termes séparés par des virgules :

`GET /companies/:company_id/properties?sort=+name,-org_id`
