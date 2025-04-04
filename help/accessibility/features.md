---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;Profil unifié;unifié;Profil;rtcp;graphiques XDM
title: Fonctionnalités d’accessibilité générales dans Experience Platform
type: Documentation
description: En savoir plus sur les fonctionnalités d’accessibilité générales prises en charge par Adobe Experience Platform, notamment la navigation au clavier, le contraste et les palettes de couleurs, ainsi que la prise en charge des technologies d’assistance.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 92%

---

# Fonctionnalités d’accessibilité dans Experience Platform

Adobe Experience Platform s’engage à fournir des fonctionnalités accessibles et inclusives à tous les individus, y compris les utilisateurs ayant recours à des appareils d’assistance tels que des logiciels de reconnaissance vocale et des lecteurs d’écran. Ce document décrit les fonctionnalités d’accessibilité générales prises en charge par Experience Platform, notamment la navigation au clavier, la structure sémantique, un contraste suffisant entre les éléments de premier plan et les éléments d’arrière-plan, ainsi que la prise en charge des technologies d’assistance.

## Technologies d’assistance

Les utilisateurs présentant un handicap dépendent fréquemment du matériel et des logiciels connus sous le nom de technologies d’assistance pour accéder au contenu numérique et utiliser des produits logiciels. Adobe Experience Platform prend en charge plusieurs types de technologies d’assistance (AT), telles que les lecteurs d’écran, le zoom et les logiciels de reconnaissance vocale, en appliquant les bonnes pratiques d’accessibilité comme l’utilisation de code sémantique, d’équivalents textuels, de libellés et d’attributs ARIA, le cas échéant. Les éléments interactifs de l’interface utilisateur (IU) d’Experience Platform utilisent des libellés, des noms accessibles et des rôles correspondants qui identifient à la fois leur objectif et leur état actuel. Les technologies d’assistance telles que les lecteurs d’écran peuvent ainsi lire les libellés et d’autres informations aux utilisateurs. Cela permet à ces derniers d’interagir facilement avec les commandes de l’application.

## Accessibilité à l’aide du clavier

Experience Platform s’efforce de prendre en charge l’accessibilité complète du clavier.

Les éléments de navigation suivants facilitent l’accessibilité :
* La touche de tabulation permet de se déplacer entre les éléments, les sections et les groupes de menus de l’interface utilisateur.
* Les touches fléchées permettent de se déplacer dans les groupes de menus pour définir le focus sur des éléments principaux individuels.
* Maj + tabulation permet de revenir en arrière dans l’ordre de tabulation.
* Les touches Retour (Entrée) et la barre d’espacement activent les éléments sélectionnés.
* La touche Échap (ESC) fait office de bouton d’annulation pour fermer une boîte de dialogue, le cas échéant.
* Experience Platform affiche une bordure bleue autour d’un élément sélectionné afin d’indiquer clairement sur quel élément de l’interface utilisateur se trouve actuellement le focus.

![Bordure bleue apparaissant autour d’un élément sélectionné pour indiquer que le focus est appliqué.](images/profile-overview-tab.png)

## Palettes et contraste des couleurs

Experience Platform s’efforce de respecter la norme [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/), y compris les exigences en matière de contraste des couleurs. L’interface utilisateur d’Experience Platform offre un contraste suffisant dans l’application pour garantir une expérience de visionnage accessible aux utilisateurs présentant une faible vision ou des défauts de vision des couleurs.

![Contraste et palette de couleurs présents sur la page d’accueil de l’interface utilisateur d’Experience Platform.](images/homepage.png)

## Validation des champs requis

Lors de l’ajout de données, de la création de schémas ou de la définition de segments, les champs requis sont indiqués visuellement, à l’aide d’un astérisque en regard du libellé de texte d’un champ, et par programme. Ces champs déclenchent une validation lorsque vous saisissez des données non valides ainsi que lors de l’enregistrement. Si un champ obligatoire n’est pas validé, il est signalé en rouge et est accompagné d’une icône d’erreur. Une description écrite du problème à corriger s’affiche également.

![Gros plan sur un champ obligatoire n’ayant pas été validé. Le champ apparaît en rouge et une icône d’erreur est présente.](images/field-validation.png)
