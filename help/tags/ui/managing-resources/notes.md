---
title: Notes
description: Découvrez comment ajouter des annotations textuelles à certaines ressources de balises dans Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 99%

---

# Notes

Les notes sont des annotations textuelles que vous pouvez ajouter à certaines ressources de balises dans Adobe Experience Platform. Des notes peuvent être ajoutées aux ressources suivantes :

* Extensions
* Éléments de données
* Règles
* Composants de règle
* Bibliothèques
* Propriétés

Les notes peuvent contenir jusqu’à 512 caractères Unicode.

Les notes sont des commentaires qui n’ont aucun impact sur le comportement des ressources auxquelles elles sont rattachées. Elles ne sont pas incluses dans les bibliothèques construites. Vous pouvez utiliser des notes pour :

* Fournir des informations supplémentaires sur une ressource
* Servir de liste de tâches pour les améliorations futures à apporter à la ressource
* Transmettre à d’autres utilisateurs des conseils sur l’utilisation de la ressource
* Donner des instructions aux autres membres de l’équipe
* Enregistrer les informations d’historique
* Noter la fonction d’une ressource, pourquoi elle est construite d’une telle manière ou comment l’utiliser

## Création d’une note

Les ressources qui peuvent être annotées ont un rail fin sur le côté droit de l’écran. Ce rail comprend une icône pour l’annotation. Cette icône indique le nombre actuel de notes jointes à la ressource.

Cliquez sur l’icône **[!UICONTROL Notes]** pour développer le rail de droite et afficher les notes. Les notes les plus récentes sont affichées en haut.  Pour ajouter une nouvelle note, saisissez votre texte dans la zone située en haut et cliquez sur **[!UICONTROL Add Note]**.

## Autre

* Les notes sur les ressources de balises se comportent de la même manière que les notes dans DTM. Elles sont immuables et ne peuvent pas être modifiées ni supprimées.
* Lorsque vous affichez les anciennes révisions d’une ressource, seules les notes créées avant la date `created_at` de cette révision s’affichent.
* Lorsque vous supprimez une ressource, toutes les notes qui lui sont associées sont également supprimées.
