---
title: Développement d’une extension
description: Ce document offre un aperçu général du processus de développement dʼune extension de balise et contient des liens vers dʼautres documents présentant des processus plus détaillés.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
TQID: https://experienceleague.adobe.com/Sqk2e7n7DRJ-wWn5HZT53eUbO0Eg380NcpZVr1gjWWA
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 443
ht-degree: 92%

---

# Développement d’une extension

Une extension de balise doit être considérée comme un (petit) produit ayant ses propres besoins. Déterminer comment un utilisateur Adobe Experience Platform souhaite utiliser votre extension peut vous permettre de trier les fonctionnalités en fonction des types d’événement, de condition, d’action et d’éléments de données que votre extension doit fournir.

Grâce à ces connaissances, vous pouvez planifier les composants qui doivent être fournis dans votre extension.

## Guides

Une fois que vous avez mis un plan en place, ces guides vous aideront à comprendre le processus de développement des extensions :

* Le [guide de prise en main](../getting-started.md) et dʼautres documents sous **Développement dʼextensions** dans le volet de navigation de gauche constituent un bon matériel de référence pour comprendre les extensions. Ces documents contiennent des détails sur le rôle des extensions, sur la façon dont les informations utilisateur sont stockées et transmises entre votre extension et Adobe Experience Platform. Ils expliquent aussi comment votre code est regroupé en bibliothèques et comment votre code d’extension est interprété et utilisé au moment de l’exécution dans le navigateur.
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

Vous pouvez consulter ou utiliser des exemples d’extensions provenant de GitHub, tels que l’exemple d’extension [Hello World](https://github.com/adobe/reactor-helloworld-extension), comme projets de démarrage.

## Espace de travail Slack

Vous pouvez demander lʼaccès à lʼespace de travail communautaire Slack où les auteurs dʼextensions peuvent sʼentraider en utilisant ce [formulaire de demande](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Remarque** : bien quʼil y ait des membres dʼAdobe dans cet espace de travail Slack, il sʼagit dʼune ressource communautaire ni sponsorisée ni modérée par Adobe.
