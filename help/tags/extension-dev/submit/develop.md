---
title: Développer une extension
description: Ce document donne un aperçu général du processus de développement de l’extension de balise avec des liens vers d’autres documents pour des processus plus détaillés.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 46%

---

# Développer une extension

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une extension de balise doit être considérée comme un (petit) produit ayant ses propres exigences. Déterminer comment un utilisateur Adobe Experience Platform souhaite utiliser votre extension peut vous permettre de trier les fonctionnalités en fonction des types d’événement, de condition, d’action et d’éléments de données que votre extension doit fournir.

Grâce à ces connaissances, vous pouvez planifier les composants qui doivent être fournis dans votre extension.

## Guides

Une fois que vous avez mis un plan en place, ces guides vous aideront à comprendre le processus de développement des extensions :

* Le [guide de prise en main](../getting-started.md) et d’autres documents sous **Développement d’extension** dans le volet de navigation de gauche sont de bons documents de référence pour comprendre les extensions. Elles incluent des détails sur ce que les extensions peuvent faire, comment les informations utilisateur sont stockées et transmises entre votre extension et Adobe Experience Platform, comment votre code est regroupé en bibliothèques et comment votre code d’extension est interprété et utilisé au moment de l’exécution dans le navigateur.
* Le [tutoriel vidéo sur l’extension](https://youtu.be/rxjtC9o4rl0) est un bon point de départ.
* La playlist YouTube [Introduction to Extensions](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) passe en revue le processus de création de packages d’extension.
* Présentation de l’article [Understanding JSON Schema](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](http://jsonlint.com/).
* Extension Chrome [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) pour visualiser et imprimer des fichiers JSON et JSONP.
* Éditeur [jsonschema.net](https://jsonschema.net/#/editor) pour créer un schéma JSON à partir de votre objet..
* [JSON Schema Validator](http://www.jsonschemavalidator.net/), validateur de schémas JSON interactif en ligne.

## Outils

Il existe également un certain nombre d’outils npm pour vous aider à développer votre package d’extensions :

* [Tag Extension Scaffold ](https://www.npmjs.com/package/@adobe/reactor-scaffold) Toolvous permet de créer facilement un projet de démarrage sur votre ordinateur local.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-sandbox) Sandbox vous aide à valider vos vues et modules d’extension sur votre ordinateur local.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-packager) Packagerest un utilitaire de ligne de commande permettant de transformer une extension de balise en fichier zip.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploaderer est un outil interactif de ligne de commande qui vous permet de saisir les informations d’identification de votre compte technique et de charger votre package d’extension vers des balises.
* [Tag Extension ](https://www.npmjs.com/package/@adobe/reactor-releaser) Releaser est un outil de ligne de commande interactif qui vous aide à déployer votre extension pour une disponibilité privée.

## Exemples d’extensions

Il existe des exemples d’extensions sur GitHub que vous pouvez consulter ou utiliser comme projets de démarrage :

* [Exemple d’extension Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Exemple d’extension Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Exemple d’extension Typekit](https://github.com/jeffchasin/extension-typekit)
* [Exemple d’extension Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espace de travail Slack

Vous pouvez demander l’accès à l’espace de travail de la communauté du Slack où les auteurs d’extensions peuvent s’entraider en utilisant ce [formulaire de demande](http://join.launchdevelopers.chat).

**Remarque** : bien qu’il y ait des membres de l’Adobe dans cet espace de travail de Slack, il s’agit d’une ressource communautaire qui n’est ni sponsorisée ni modérée par Adobe.
