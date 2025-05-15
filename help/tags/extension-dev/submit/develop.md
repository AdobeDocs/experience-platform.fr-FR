---
title: Développement d’une extension
description: Ce document offre un aperçu général du processus de développement dʼune extension de balise et contient des liens vers dʼautres documents présentant des processus plus détaillés.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: cfcc70d66a34fa51bf0e21525539ba88de7fc367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 97%

---

# Développement d’une extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une extension de balise doit être considérée comme un (petit) produit ayant ses propres besoins. Déterminer comment un utilisateur Adobe Experience Platform souhaite utiliser votre extension peut vous permettre de trier les fonctionnalités en fonction des types d’événement, de condition, d’action et d’éléments de données que votre extension doit fournir.

Grâce à ces connaissances, vous pouvez planifier les composants qui doivent être fournis dans votre extension.

## Guides

Une fois que vous avez mis un plan en place, ces guides vous aideront à comprendre le processus de développement des extensions :

* Le [guide de prise en main](../getting-started.md) et dʼautres documents sous **Développement dʼextensions** dans le volet de navigation de gauche constituent un bon matériel de référence pour comprendre les extensions. Ces documents contiennent des détails sur le rôle des extensions, sur la façon dont les informations utilisateur sont stockées et transmises entre votre extension et Adobe Experience Platform. Ils expliquent aussi comment votre code est regroupé en bibliothèques et comment votre code d’extension est interprété et utilisé au moment de l’exécution dans le navigateur.
<!-- * The [extension tutorial video](https://youtu.be/rxjtC9o4rl0) is a great place to start. -->
* La playlist YouTube [Introduction to Extensions](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) passe en revue le processus de création de packages d’extension.
* Article de [Présentation du schéma JSON](https://spacetelescope.github.io/understanding-json-schema/index.html#).
* [Vignette/programme de validation JSON](https://jsonlint.com/).
* Extension Chrome [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) pour visualiser et imprimer des fichiers JSON et JSONP.
* Éditeur [jsonschema.net](https://jsonschema.net/#/editor) pour créer un schéma JSON à partir de votre objet.
* [JSON Schema Validator](https://www.jsonschemavalidator.net), validateur de schémas JSON interactif en ligne.

## Outils

Il existe également un certain nombre d’outils npm pour vous aider à développer votre package d’extensions :

* Lʼ[outil Tag Extension Scaffold](https://www.npmjs.com/package/@adobe/reactor-scaffold) vous aide à créer facilement un projet de démarrage sur votre ordinateur local.
* [Tag Extension Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) vous aide à valider vos vues et modules dʼextension sur votre ordinateur local.
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) est un utilitaire de ligne de commande permettant de transformer une extension de balise en fichier zip.
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader) est un outil interactif de ligne de commande qui vous permet de saisir les informations dʼidentification de votre compte technique et de télécharger votre package dʼextension vers les balises.
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser) est un outil de ligne de commande interactif qui vous permet de déployer votre extension pour une disponibilité privée.

## Exemples d’extensions

Il existe des exemples dʼextensions sur GitHub que vous pouvez consulter ou utiliser comme projets de démarrage :

* [Exemple d’extension Hello World](https://github.com/adobe/reactor-helloworld-extension)
* [Exemple d’extension Facebook](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Exemple d’extension Typekit](https://github.com/jeffchasin/extension-typekit)
* [Exemple d’extension Pinterest](https://github.com/jeffchasin/extension-pinterest)

## Espace de travail Slack

Vous pouvez demander lʼaccès à lʼespace de travail communautaire Slack où les auteurs dʼextensions peuvent sʼentraider en utilisant ce [formulaire de demande](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Remarque** : bien quʼil y ait des membres dʼAdobe dans cet espace de travail Slack, il sʼagit dʼune ressource communautaire ni sponsorisée ni modérée par Adobe.
