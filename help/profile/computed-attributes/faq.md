---
title: Questions fréquentes sur les attributs calculés
description: Découvrez les réponses aux questions fréquentes sur l’utilisation des attributs calculés.
source-git-commit: fb5d3088b9fb330153bf64125df2f739eee80518
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# Questions fréquentes

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

Les calculs d’attributs calculés sont renvoyés pour la durée de recherche en amont définie lors de la première évaluation et mis à jour en fonction des événements incrémentiels pour les mises à jour suivantes. Par conséquent, ces calculs sont : **not** affecté par l’expiration des données de l’événement d’expérience des anciennes données après la première évaluation.

Par exemple, si vous créez un attribut calculé évalué tous les mois avec une période de recherche en amont de trois mois, pour la première évaluation, l’attribut calculé calculera pour tous les événements au cours de cette période de recherche en amont de trois mois. Même si le jeu de données d’événement d’expérience expire au bout d’un mois, cette expiration de données sera **not** affecte l’actualisation mensuelle des attributs calculés, puisque l’exécution de l’évaluation du mois suivant agrégera progressivement les événements et mettra à jour le calcul.

>[!NOTE]
>
>Données expirées **cannot** être renseigné ultérieurement par un attribut calculé. Expiration des données du jeu de données d’événement **may** la capacité de valider la valeur de l’attribut calculé à un moment ultérieur ; Pour valider la valeur d’attribut calculé, votre période de recherche arrière doit rester **dans** les limites des expirations de données.

## Puis-je créer un attribut calculé basé sur un autre attribut calculé ?

Les attributs calculés étant créés à l’aide de champs Experience Event et résidant dans un champ Profile, il n’est pas possible d’utiliser directement un attribut calculé pour créer un autre attribut calculé.

## Le nombre d’attributs calculés que je peux créer est-il limité ?

Oui, il existe une limite au nombre d’attributs calculés que vous pouvez créer. Pour plus d’informations, reportez-vous à la description du produit ou contactez l’équipe de compte d’Adobe.

## Existe-t-il des implications en aval pour désactiver un attribut calculé ?

Avant de désactiver votre attribut calculé, vous **should** supprimez-les de vos systèmes en aval (comme la segmentation, les parcours ou les destinations), car des complications peuvent survenir si elles ne sont pas supprimées.

## Que se passe-t-il lorsque je désactive un attribut calculé ? {#inactive-status}

Lorsqu’un attribut calculé est désactivé ou rendu inactif, il n’est plus mis à jour. Par conséquent, cet attribut calculé **cannot** être utilisé dans la recherche de profil ou dans d’autres utilisations en aval.

## Comment les attributs calculés aident-ils à stimuler l’engagement ?

Les attributs calculés alimentent l’enrichissement de profil en agrégeant vos attributs d’événement à un niveau de profil fusionné. Vous pouvez par exemple personnaliser les emails marketing avec le dernier produit consulté.

## À quelle fréquence les attributs calculés sont-ils évalués ? Est-ce lié au planning d’évaluation de l’audience ?

Les attributs calculés sont évalués par lots indépendamment du planning de segmentation. Cela signifie que, quel que soit le type de segmentation (segmentation par lots ou segmentation par flux), l’attribut calculé sera évalué selon son propre planning (horaire, quotidien, hebdomadaire ou mensuel).

Lorsque l’audience est évaluée, elle utilise la variable **dernier** valeur de l’attribut calculé disponible.

## Comment les attributs calculés interagissent-ils avec les audiences évaluées à l’aide de la segmentation par flux ?

Si une audience évaluée par segmentation en continu utilise un attribut calculé, la variable **dernière valeur** de l’attribut calculé pendant l’évaluation de l’audience. Par exemple, si l’audience recherche des événements d’achat, l’audience fait référence à la dernière valeur d’attribut calculée évaluée lorsque l’événement d’achat survient.

## Puis-je utiliser des attributs calculés sur Edge ?

Comme tout autre attribut de profil, les attributs calculés sont disponibles et peuvent être utilisés en périphérie. Notez que les attributs calculés sont **not** calculé sur Edge.

## Comment les libellés d’utilisation des données sont-ils appliqués aux attributs calculés ?

Les attributs calculés dérivés automatiquement des libellés d’utilisation des données des champs sources et des jeux de données qui ont été utilisés pour définir les attributs calculés. Cela permet de s’assurer que vos données comportementales sont correctement utilisées.

## Comment accéder aux attributs calculés ?

Pour accéder aux attributs calculés, vous devez disposer des autorisations appropriées. Pour plus d’informations sur les autorisations requises, consultez la section [documentation sur le contrôle d’accès](../../access-control/home.md).

## Comment utiliser les attributs calculés avec Adobe Journey Optimizer ?

Pour utiliser les attributs calculés dans les parcours, vous devez ajouter la variable `SystemComputedAttributes` groupe de champs vers la source de données Experience Platform. Pour plus d’informations sur la configuration de la source de données Experience Platform, veuillez lire le [Guide de source de données Adobe Experience Platform](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=en).
