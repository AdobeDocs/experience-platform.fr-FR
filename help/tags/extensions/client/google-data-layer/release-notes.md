---
title: Notes de mise à jour de l’extension de couche de données Google
description: Notes de mise à jour les plus récentes pour l’extension de balise de la couche de données Google dans Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Notes de mise à jour de l’extension de la couche de données Google

## Version 1.0.4

* Version bêta publique de l’extension.

## Version 1.0.6

* Ajout d’une action pour réinitialiser la couche de données à l’état calculé.
* Correction de bogues dans l’élément de données qui empêchent la récupération des valeurs à partir de l’état calculé.

## Version 1.1.1

Une amélioration significative et une version de correctif de bogues résultant des commentaires de test bêta.

* Correction d’un problème en raison duquel un élément de données Extension de couche de données Google vide utilisé dans une règle de couche de données autre que celle-ci (par exemple, Library Loaded (Bibliothèque chargée)) renvoyait l’objet de couche de données, et non l’état calculé.
* Correction d’un problème en raison duquel l’état calculé de la couche de données n’était pas transmis de l’assistant dans les événements au moment du déclenchement de l’événement, mais plutôt au moment de l’exécution de la règle.
* Ajoute une bascule à la boîte de dialogue de l’élément de données qui permet à l’utilisateur de choisir si seules les valeurs des événements doivent être renvoyées.
* Correction d’un problème en raison duquel l’historique des événements n’était pas correctement capturé par les écouteurs d’événements de règle.
* Améliorations mineures de la clarté du code.

## Version 1.2.0

* Ajoute une action à transmettre à la couche de données à l’aide d’une boîte de dialogue multichamp à valeur clé.
* Correction d’un bogue qui empêchait le chargement de l’extension lorsque les balises étaient déployées de manière synchrone.
* Correction d’un bogue qui provoquait une erreur lors de l’enregistrement d’un élément de données dans certains cas.
* Ajoute une documentation à la boîte de dialogue d’événement expliquant l’utilisation de l’objet d’événement Balises.
* Ajoute un avertissement à propos des boucles infinies dans la boîte de dialogue d’événement.
