---
title: Développer une extension
description: Ce document offre un aperçu général du processus de développement d’une extension de balises et contient des liens vers d’autres documents présentant des processus plus détaillés.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '531'
ht-degree: 100%

---

# Développer une extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une extension de balises doit être considérée comme un (petit) produit ayant ses propres besoins. Déterminer comment un utilisateur Adobe Experience Platform souhaite utiliser votre extension peut vous permettre de trier les fonctionnalités en fonction des types d’événement, de condition, d’action et d’éléments de données que votre extension doit fournir.

Ces connaissances vous permettent de planifier les composants qui doivent être fournis dans votre extension.

## Guides

Une fois que vous avez mis un plan en place, ces guides vous aideront à comprendre le processus de développement des extensions :

* Le [guide de prise en main](../getting-started.md) et d’autres documents sous **Développement d’extension** dans le volet de navigation de gauche sont de bons documents de référence pour comprendre les extensions. Ces documents contiennent des détails sur le rôle des extensions, sur la façon dont les informations utilisateur sont stockées et transmises entre votre extension et Adobe Experience Platform. Ils expliquent aussi comment votre code est regroupé en bibliothèques et comment votre code d’extension est interprété et utilisé au moment de l’exécution dans le navigateur.
* Le [tutoriel vidéo de présentation des extensions](https://youtu.be/rxjtC9o4rl0) récemment mis à jour constitue un bon début.
* La playlist YouTube [Introduction to Extensions](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) passe en revue le processus de création de packages d’extension.
* Présentation de l’article [Understanding JSON Schema](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [JSON Lint/Validator](http://jsonlint.com/).
* Extension Chrome [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) pour visualiser et imprimer des fichiers JSON et JSONP.
* Éditeur [jsonschema.net](https://jsonschema.net/#/editor) pour créer un schéma JSON à partir de votre objet..
* [JSON Schema Validator](http://www.jsonschemavalidator.net/), validateur de schémas JSON interactif en ligne.

## Outils

Il existe également un certain nombre d’outils npm pour vous aider à développer votre package d’extensions :

* L’application [Tag Extension Scaffold Tool](https://www.npmjs.com/package/@adobe/reactor-scaffold) vous permet de créer facilement un projet de démarrage sur votre ordinateur local.
* L’application [Tag Extension Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) vous permet de valider vos vues et modules d’extension sur votre ordinateur local.
* L’application [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) est un utilitaire de ligne de commande permettant de transformer une extension de balises en fichier zip.
* L’application [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader) est un outil interactif de ligne de commande qui vous permet de saisir les informations d’identification de votre compte technique et de télécharger votre module d’extension vers les balises.
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) est un outil de ligne de commande interactif qui vous permet de déployer votre extension pour une disponibilité privée.

## Exemples d’extensions

Vous pouvez consulter les exemples d’extensions présents sur GitHub ou les utiliser comme projets de démarrage :

* [Exemple d’extension Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Exemple d’extension Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Exemple d’extension Typekit](https://github.com/jeffchasin/extension-typekit)
* [Exemple d’extension Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espace de travail Slack

Vous pouvez demander l’accès à l’espace de travail de la communauté Slack où les créateurs d’extensions peuvent se soutenir mutuellement. Pour ce faire, utilisez ce [formulaire de demande](http://join.launchdevelopers.chat).

**Veuillez noter** : bien que cet espace de travail Slack contienne des membres de l’équipe Adobe, il s’agit d’une ressource communautaire qui n’est ni parrainée ni modérée par Adobe.
