---
title: Notes de mise à jour de l’extension Google de couche de données
description: Notes de mise à jour les plus récentes pour l’extension Google de couche de données pour les balises dans Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
TQID: https://experienceleague.adobe.com/mgFSNSvx-Gg1syMdsf6yv-YUbHvIRPXRUUo1s-503KA
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 100%

---

# Notes de mise à jour de l’extension Google de couche de données

## Version 1.0.4

* Version Beta publique de l’extension.

## Version 1.0.6

* Ajout d’une action pour réinitialiser la couche de données à l’état calculé.
* Correction de bugs dans l’élément de données qui empêchent la récupération des valeurs à partir de l’état calculé.

## Version 1.1.1

Version comportant une amélioration significative et une correction de bugs résultant des commentaires de test de la version Beta.

* Correction d’un problème en raison duquel un élément de données vide de l’extension Google de couche de données utilisé dans une règle de couche ne concernant pas des données (par exemple, « Library Loaded ») renvoyait l’objet de la couche de données, et non l’état calculé.
* Correction d’un problème en raison duquel l’état calculé de la couche de données n’était pas transmis de l’assistant vers les événements au moment du déclenchement de l’événement, mais au moment de l’exécution de la règle.
* Ajout d’un bouton à la boîte de dialogue de l’élément de données qui permet à l’utilisateur ou à l’utilisatrice de choisir si seules les valeurs des événements doivent être renvoyées.
* Correction d’un problème en raison duquel l’historique des événements n’était pas correctement capturé par les écouteurs d’événements/de règles.
* Améliorations mineures de la clarté du code.

## Version 1.2.0

* Ajout d’une action pour transmettre vers la couche de données à l’aide d’une boîte de dialogue à champs multiples clé-valeur.
* Correction d’un bug qui empêchait le chargement de l’extension lorsque des balises étaient déployées de manière synchrone.
* Correction d’un bug qui provoquait une erreur lors de l’enregistrement d’un élément de données dans certains cas.
* Ajout d’une documentation à la boîte de dialogue d’événement qui explique comment utiliser l’objet d’événement Balises.
* Ajout d’un avertissement à propos des boucles infinies dans la boîte de dialogue d’événement.

## Version 1.2.2

* Ajout de la prise en charge des événements gtag() Google Analytics.
