---
title: Mise À Jour Des Critères D’Éligibilité De Segmentation
description: Découvrez les mises à jour des critères d’éligibilité de segmentation qui affectent les types d’audiences qui peuvent être évalués à l’aide de la segmentation Edge et en flux continu.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: e6deed1fe52a0a852f521100171323f0de23295b
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Mise à jour des critères d’éligibilité de la segmentation

À compter du 23 mai 2025, deux mises à jour seront effectuées qui affecteront l’éligibilité de la segmentation.

1. Types de requête de segmentation Edge et en flux continu
2. Politiques de fusion de segmentation Edge et de streaming

## Types de requête

Toutes les définitions de segment **nouvelles ou modifiées** qui correspondent aux types de requête suivants **ne seront plus** évaluées à l’aide de la segmentation Edge ou en flux continu. Au lieu de cela, elles seront évaluées à l’aide de la segmentation par lots.

- Un événement unique avec une fenêtre temporelle de plus de 24 heures.
   - Activez une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours.
- Un événement unique sans fenêtre temporelle
   - Activez une audience avec tous les profils qui ont consulté une page web.

Si vous devez évaluer une définition de segment à l’aide de la segmentation en flux continu ou Edge qui correspond au type de requête mis à jour, vous pouvez explicitement créer une requête par lots et en flux continu et les combiner à l’aide d’un segment de segments.

Par exemple, si vous devez activer une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours à l’aide de la segmentation en flux continu, vous pouvez créer les requêtes suivantes :

- Q1 (Streaming) : tous les profils qui ont consulté une page web au cours des dernières 24 heures
- T2 (lot) : tous les profils qui ont consulté une page web au cours des 3 derniers jours.

Vous pouvez ensuite les combiner en vous référant à Q1 ou Q2.

De même, si vous devez activer une audience avec tous les profils qui ont consulté une page web, vous pouvez créer les requêtes suivantes :

- Q3 (Streaming) : tous les profils qui ont consulté une page web au cours des dernières 24 heures
- Q4 (lot) : tous les profils qui ont consulté une page web.

Ensuite, vous pouvez les combiner en vous référant à Q3 ou Q4.

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui correspondent aux types de requête restent évaluées à l’aide de la segmentation Edge ou en flux continu jusqu’à ce qu’elles soient modifiées.
>
>En outre, toutes les définitions de segment existantes qui répondent actuellement aux autres critères d’évaluation de segmentation en flux continu ou Edge resteront évaluées avec la segmentation en flux continu ou Edge.

## Politique de fusion

Toutes les définitions de segment **nouvelles ou modifiées** qui remplissent les critères de segmentation Edge ou en flux continu **doivent** doivent être sur la politique de fusion « Active-on-Edge ».

Toutes les définitions de segment existantes qui sont évaluées à l’aide de la segmentation Edge ou en flux continu continueront à fonctionner en l’état.
