---
title: Questions fréquentes sur les attributs calculés
description: Découvrez les réponses aux questions fréquentes sur l’utilisation des attributs calculés.
badge: « Version bêta »
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 4%

---


# Questions fréquentes

>[!IMPORTANT]
>
>Les attributs calculés se trouvent actuellement dans **bêta** et est **not** disponible pour tous les utilisateurs.

Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour agréger les données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Vous trouverez ci-dessous une liste des questions fréquemment posées concernant les attributs calculés.

## Quels jeux de données contribuent aux calculs d’attributs calculés ?

Les attributs calculés prennent en compte les jeux de données d’événement d’expérience activés pour Real-time Customer Profile pour calculer les attributs calculés.

## Quels champs de modèle de données d’expérience (XDM) peuvent être utilisés pour créer des attributs calculés ?

Tous les champs XDM de votre schéma d’union d’événement d’expérience peuvent être utilisés pour créer des attributs calculés.

## Que représente la &quot;dernière heure d’évaluation&quot; ?

La dernière heure d’évaluation signifie que les événements **before** à cet horodatage ont été pris en compte dans la dernière actualisation réussie de l’attribut calculé.

## Puis-je choisir la fréquence d’actualisation ? Comment est-ce décidé ?

La fréquence d’actualisation est automatiquement déterminée en fonction de la période de recherche en amont de votre attribut calculé. Pour plus d’informations à ce sujet, veuillez lire le [section sur la période de recherche arrière](./overview.md#lookback-periods) de la présentation des attributs calculés.

## Comment les calculs sont-ils affectés par l’expiration des données d’Experience Event ?

Les calculs d’attributs calculés sont basés sur la période de recherche en amont définie et les événements d’expérience compris dans cette période. Par conséquent, ces calculs sont : **not** affecté par les expirations de données d’événement d’expérience. Toutefois, pour garantir la précision de vos attributs calculés, votre période de recherche arrière doit rester **dans** les limites de vos expirations de données.

## Puis-je créer un attribut calculé basé sur un autre attribut calculé ?

Les attributs calculés étant créés à l’aide de champs Experience Event et résidant dans un champ Profile, il n’est pas possible d’utiliser directement un attribut calculé pour créer un autre attribut calculé.

## Le nombre d’attributs calculés que je peux créer est-il limité ?

Le nombre maximal actuel de **publié** les attributs calculés sont de 25.

## Existe-t-il des implications en aval pour désactiver un attribut calculé ?

Avant de désactiver votre attribut calculé, vous devez : **should** supprimez-les de vos systèmes en aval (comme la segmentation, les parcours ou les destinations), car des complications peuvent survenir si elles ne sont pas supprimées.

## Que se passe-t-il lorsque je désactive un attribut calculé ? {#inactive-status}

Lorsqu’un attribut calculé est désactivé ou rendu inactif, il n’est plus mis à jour. Par conséquent, cet attribut calculé **cannot** être utilisé dans la recherche de profil ou dans d’autres utilisations en aval.

## Comment les attributs calculés aident-ils à stimuler l’engagement ?

Les attributs calculés alimentent l’enrichissement de profil en agrégeant vos attributs d’événement à un niveau de profil fusionné. Vous pouvez par exemple personnaliser les emails marketing avec le dernier produit consulté.
