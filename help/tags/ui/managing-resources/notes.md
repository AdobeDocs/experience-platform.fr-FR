---
title: Notes
description: Découvrez comment ajouter des annotations textuelles à certaines ressources de balises dans Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
TQID: https://experienceleague.adobe.com/I9AmjlJBcOIB8rwX4W76oC9rZyex53uQYGufaXYmOP0
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 264
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

Les notes sont des commentaires qui n’ont aucun impact sur le comportement des ressources auxquelles elles sont rattachées. Elles ne sont pas incluses dans les bibliothèques construites.  Vous pouvez utiliser des notes pour :

* Fournir des informations supplémentaires sur une ressource
* Servir de liste de tâches pour les améliorations futures à apporter à la ressource
* Transmettre à d’autres utilisateurs des conseils sur l’utilisation de la ressource
* Donner des instructions aux autres membres de l’équipe
* Enregistrer les informations d’historique
* Noter la fonction d’une ressource, pourquoi elle est construite d’une telle manière ou comment l’utiliser

## Création d’une note

Les ressources qui peuvent être annotées ont un rail fin sur le côté droit de l’écran.  Ce rail comprend une icône pour l’annotation.  Cette icône indique le nombre actuel de notes jointes à la ressource.

Cliquez sur l’icône **[!UICONTROL Notes]** pour développer le rail de droite et afficher les notes. Les notes les plus récentes sont affichées en haut.  Pour ajouter une nouvelle note, saisissez votre texte dans la zone située en haut et cliquez sur **[!UICONTROL Add Note]**.

## Autre

* Les notes sur les ressources de balises se comportent de la même manière que les notes dans DTM. Elles sont immuables et ne peuvent pas être modifiées ni supprimées.
* Lorsque vous affichez les anciennes révisions d’une ressource, seules les notes créées avant la date `created_at` de cette révision s’affichent.
* Lorsque vous supprimez une ressource, toutes les notes qui lui sont associées sont également supprimées.
