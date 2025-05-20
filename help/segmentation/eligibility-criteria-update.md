---
title: Mise À Jour Des Critères D’Éligibilité De Segmentation
description: Découvrez les mises à jour des critères d’éligibilité de segmentation qui affectent les types d’audiences qui peuvent être évalués à l’aide de la segmentation Edge et en flux continu.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: eafb7337edacc5d2b2aa9c38540aff946c8d39c0
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 4%

---

# Mise à jour des critères d’éligibilité de la segmentation

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui sont actuellement évaluées à l’aide de la segmentation Edge ou en flux continu continueront à fonctionner en l’état, sauf si elles sont modifiées ou mises à jour.

À compter du 20 mai 2025, trois mises à jour seront effectuées qui affecteront l’éligibilité de la segmentation.

1. Ensemble de règles éligible
2. Éligibilité de la fenêtre temporelle
3. Inclusion de données par lot dans des audiences en flux continu
4. Politiques de fusion actives

## Ensemble de règles {#ruleset}

Les définitions de segment **nouvelles ou modifiées** qui correspondent aux ensembles de règles suivants **plus** seront évaluées à l’aide de la segmentation Edge ou en flux continu. Au lieu de cela, elles seront évaluées à l’aide de la segmentation par lots.

- Un événement unique avec une fenêtre temporelle de plus de 24 heures.
   - Activez une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours.
- Un événement unique sans fenêtre temporelle
   - Activez une audience avec tous les profils qui ont consulté une page web.

## Fenêtre temporelle {#time-window}

Pour évaluer une audience avec segmentation en flux continu, elle **doit** être limitée dans une fenêtre temporelle de 24 heures.

## Inclusion de données par lot dans des audiences en flux continu {#include-batch-data}

Avant cette mise à jour, vous pouviez créer une définition d’audience de diffusion en continu qui combinait des sources de données par lots et en flux continu. Cependant, avec la dernière mise à jour, la création d’une audience avec des sources de données par lots et par flux sera évaluée à l’aide de la segmentation par lots.

Si vous devez évaluer une définition de segment à l’aide de la segmentation en flux continu ou Edge qui correspond à l’ensemble de règles mis à jour, vous devez créer explicitement un lot et un ensemble de règles en flux continu et les combiner à l’aide d’un segment de segments. Ce jeu de règles par lot **doit** est basé sur un schéma de profil.

Supposons, par exemple, que vous ayez deux audiences, avec une audience contenant des données de schéma de profil et l’autre des données de schéma d’événement d’expérience de logement :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Résidents californiens | Profile | Lot | L&#39;adresse personnelle est dans l&#39;état de la Californie | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Si vous souhaitez utiliser le composant par lot dans votre audience de diffusion en continu, vous devez faire référence à l’audience par lot à l’aide d’un segment de segments.

Voici un exemple d’ensemble de règles qui combine les deux audiences :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

L’audience résultante *sera* évaluée à l’aide de la segmentation en flux continu, car elle exploite l’appartenance de l’audience par lots en se référant au composant d’audience par lots.

Cependant, si vous souhaitez combiner deux audiences avec des données d’événement, vous **ne pouvez pas** vous contenter de combiner les deux événements. Vous devez créer les deux audiences, puis créer une autre audience qui utilise `inSegment` pour faire référence à ces deux audiences.

Supposons, par exemple, que vous ayez deux audiences, avec les deux audiences hébergeant des données de schéma d’événement d’expérience :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Abandons récents | Événement d’expérience | Lot | A au moins un événement d’abandon au cours des dernières 24 heures | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Dans ce cas, vous devez créer une troisième audience comme suit :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui correspondent aux ensembles de règles restent évaluées à l’aide de la segmentation en flux continu ou Edge jusqu’à ce qu’elles soient modifiées.
>
>En outre, toutes les définitions de segment existantes qui répondent actuellement aux autres critères d’évaluation de segmentation en flux continu ou Edge resteront évaluées avec la segmentation en flux continu ou Edge.

## Politique de fusion {#merge-policy}

Toutes les définitions de segment **nouvelles ou modifiées** qui remplissent les critères de segmentation Edge ou en flux continu **doivent** doivent être sur la politique de fusion « Active-on-Edge ».

S’il n’existe aucun jeu de politiques de fusion actif, vous devez [configurer votre politique de fusion](../profile/merge-policies/ui-guide.md#configure) et la définir sur Active-On-Edge (active sur le bord).
