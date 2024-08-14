---
title: Mise à jour des critères d’éligibilité de la segmentation
description: Découvrez les mises à jour des critères d’éligibilité de la segmentation qui affectent les types d’audiences qui peuvent être évaluées à l’aide de la segmentation par flux et en périphérie.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Mise à jour des critères d’éligibilité de la segmentation

À compter du 24 septembre 2024, deux mises à jour seront effectuées, qui auront une incidence sur l’éligibilité à la segmentation.

1. Types de requête de segmentation par flux et par périphérie
2. Stratégies de fusion de segmentation par flux et par périphérie

## Types de requête

Toutes les **définitions de segment nouvelles ou modifiées** qui correspondent aux types de requête suivants **ne seront  plus** évaluées à l’aide de la segmentation par flux ou en périphérie. Ils seront plutôt évalués à l’aide de la segmentation par lots.

- Un seul événement avec une fenêtre temporelle de plus de 24 heures
   - Activez une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours.
- Un seul événement sans fenêtre temporelle
   - Activez une audience avec tous les profils qui ont consulté une page web.

Si vous devez évaluer une définition de segment à l’aide de la segmentation par flux ou de périphérie correspondant au type de requête mis à jour, vous pouvez créer explicitement une requête par lot et par flux et les combiner à l’aide d’un segment de segments.

Par exemple, si vous devez activer une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours à l’aide de la segmentation par flux, vous pouvez créer les requêtes suivantes :

- Q1 (Diffusion en continu) : Tous les profils ayant consulté une page web au cours des dernières 24 heures
- Q2 (par lot) : Tous les profils ayant consulté une page web au cours des 3 derniers jours

Vous pouvez ensuite les combiner en vous référant au premier trimestre ou au deuxième trimestre.

De même, si vous devez activer une audience avec tous les profils qui ont consulté une page web, vous pouvez créer les requêtes suivantes :

- Q3 (Diffusion en continu) : Tous les profils ayant consulté une page web au cours des dernières 24 heures
- Q4 (par lot) : tous les profils ayant consulté une page web.

Vous pouvez ensuite les combiner en faisant référence au 3e trimestre ou au 4e trimestre.

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui correspondent aux types de requête resteront évaluées à l’aide de la segmentation par flux ou en périphérie jusqu’à ce qu’elles soient modifiées.
>
>En outre, toutes les définitions de segment existantes qui répondent actuellement aux autres critères d’évaluation de segmentation par flux ou par périphérie resteront évaluées par la segmentation par flux ou par périphérie.

## Politique de fusion

Toutes les **définitions de segment nouvelles ou modifiées** qui remplissent les critères pour la segmentation par flux ou par périphérie **doivent** se trouver sur la stratégie de fusion &quot;Actif sur Edge&quot;.

Toutes les définitions de segment existantes qui sont évaluées à l’aide de la segmentation par flux ou de périphérie continueront à fonctionner en l’état.
