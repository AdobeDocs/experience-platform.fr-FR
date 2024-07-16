---
title: Notes de mise à jour de l’extension Google de couche de données
description: Notes de mise à jour les plus récentes pour l’extension Google de couche de données pour les balises dans Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: c1bad7d5414e62f4d77f7d5903f4b2bf4d9081f8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 100%

---

# Notes de mise à jour de l’extension Google de couche de données

## Version 1.0.4

* Version bêta publique de l’extension.

## Version 1.0.6

* Ajout d’une action pour réinitialiser la couche de données à l’état calculé.
* Correction de bugs dans l’élément de données qui empêchent la récupération des valeurs à partir de l’état calculé.

## Version 1.1.1

Version comportant une amélioration significative et une correction de bugs résultant des commentaires de test de la version bêta.

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
