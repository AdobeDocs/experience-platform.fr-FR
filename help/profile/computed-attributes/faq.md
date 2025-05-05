---
title: Questions fréquentes sur les attributs calculés
description: Trouvez des réponses aux questions fréquentes sur l’utilisation des attributs calculés.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 1%

---

# Questions fréquentes

Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Vous trouverez ci-dessous une liste de questions fréquentes concernant les attributs calculés.

## Comment puis-je accéder aux attributs calculés ?

Pour accéder aux attributs calculés, vous devez disposer des autorisations appropriées (**Afficher les attributs calculés** et **Gérer les attributs calculés**). Pour plus d’informations sur les autorisations requises, veuillez lire la [documentation sur le contrôle d’accès](../../access-control/home.md). Pour savoir comment appliquer ces autorisations, consultez le [guide de gestion des autorisations](../../access-control/ui/permissions.md).

## Quels jeux de données contribuent aux calculs d’attributs calculés ?

Les attributs calculés prennent en compte les jeux de données d’événements d’expérience activés pour Real-Time Customer Profile pour le calcul des attributs calculés.

## Quels champs de modèle de données d’expérience (XDM) peuvent être utilisés pour créer des attributs calculés ?

Tous les champs XDM de votre schéma d’union des événements d’expérience peuvent être utilisés pour créer des attributs calculés.

## Que représentent « dernière évaluation » et « dernier statut d’évaluation » ?

La dernière évaluation fait référence à la date et à l’heure auxquelles les événements sont pris en compte lors de la dernière exécution réussie. Le statut de la dernière évaluation indique si la dernière exécution d’évaluation a réussi ou non.

## Puis-je choisir la fréquence d’actualisation ? Comment en est-on arrivé à cette décision ?

La fréquence d’actualisation est automatiquement déterminée en fonction de la période de recherche en amont de votre attribut calculé. Pour plus d’informations à ce sujet, consultez la section [période de recherche en amont](./overview.md#lookback-periods) de la présentation des attributs calculés.

## Comment les calculs sont-ils affectés par l’expiration des données d’événements d’expérience ?

Les calculs d’attributs calculés sont renvoyés pour la durée de recherche en amont définie lors de la première évaluation et mis à jour en fonction d’événements incrémentiels pour les mises à jour ultérieures. Par conséquent, ces calculs ne sont **pas** affectés par l’expiration des données d’événements d’expérience des anciennes données après la première évaluation.

Par exemple, si vous créez un attribut calculé qui est évalué tous les mois avec une période de recherche arrière de trois mois, pour la première évaluation, l’attribut calculé calculera pour tous les événements de cette période de recherche arrière de trois mois. Même si l’expiration des données du jeu de données d’événement d’expérience est fixée à un mois, cette expiration de données n’affecte **pas** l’actualisation mensuelle de l’attribut calculé, car l’exécution d’évaluation du mois suivant agrège de manière incrémentielle les événements et met à jour le calcul.

>[!NOTE]
>
>Les données expirées **ne peuvent pas** peuvent pas être renvoyées ultérieurement par un attribut calculé. L’expiration des données du jeu de données d’événement **mai** a limité la possibilité de valider la valeur de l’attribut calculé à un moment ultérieur. Pour valider la valeur d’attribut calculée, votre période de recherche en amont doit rester **dans** les limites des expirations de données.

## Puis-je créer un attribut calculé en fonction d’un autre attribut calculé ?

Puisque les attributs calculés sont créés à l’aide de champs d’événement d’expérience et se trouvent dans un champ de profil, il n’est pas possible d’utiliser directement un attribut calculé pour créer un autre attribut calculé.

## Existe-t-il des limites au nombre d’attributs calculés que je peux créer ?

Oui, le nombre d’attributs calculés que vous pouvez créer est limité. Cette limite s’applique uniquement aux attributs calculés **actifs**. Reportez-vous à la description du produit ou contactez l’équipe du compte d’Adobe pour plus d’informations.

## La désactivation d’un attribut calculé a-t-elle des implications en aval ?

Avant de désactiver votre attribut calculé, vous **devez** le supprimer de vos systèmes en aval (tels que la segmentation, les parcours ou les destinations), car des complications peuvent se produire s’il n’est pas supprimé.

## Que se passe-t-il lorsque je désactive un attribut calculé ? {#inactive-status}

Lorsqu’un attribut calculé est désactivé ou rendu inactif, il n’est plus mis à jour. Par conséquent, cet attribut calculé **ne peut pas** être utilisé dans la recherche de profil ou d’autres utilisations en aval.

## Comment les attributs calculés favorisent-ils l’engagement ?

Les attributs calculés génèrent un enrichissement du profil en agrégeant vos attributs d’événement au niveau du profil fusionné. Par exemple, vous pouvez personnaliser les e-mails marketing avec le dernier produit consulté.

## À quelle fréquence les attributs calculés sont-ils évalués ? Est-ce lié au planning d’évaluation des audiences ?

Les attributs calculés sont évalués dans une fréquence **lot** qui est **indépendante** du planning d’évaluation de votre audience, de votre destination et de votre parcours. Cela signifie que, quel que soit le type de segmentation (segmentation par lots ou segmentation par flux), l’attribut calculé est évalué selon son propre planning (horaire, quotidien, hebdomadaire ou mensuel).

La première évaluation de votre attribut calculé se produit dans les 24 heures suivant sa **création**. Les évaluations par lots suivantes se produisent toutes les heures, tous les jours, toutes les semaines ou tous les mois, selon la période de recherche en amont définie.

Par exemple, si une première évaluation a lieu à 00 h 00 UTC le 9 octobre, les évaluations suivantes ont lieu aux heures suivantes :

- Prochaine actualisation quotidienne : 12 h UTC le 10 octobre
- Prochaine actualisation hebdomadaire : 12 h UTC le 15 octobre
- Prochaine actualisation mensuelle : 12 h UTC le 1er novembre

>[!IMPORTANT]
>
>Ce n’est le cas que si l’actualisation rapide n’est **pas** activée. Pour découvrir comment la période de recherche en amont change lorsque l’actualisation rapide est activée, consultez la section [Actualisation rapide](./overview.md#fast-refresh).

Les actualisations **hebdomadaire** et **mensuelle** ont lieu au début de la **semaine calendaire** (le dimanche de la nouvelle semaine) ou au début du **mois calendaire** (le premier du nouveau mois), par opposition à exactement une semaine ou un mois après la première date d’évaluation.

>[!NOTE]
>
>La valeur d’attribut calculée n’est **pas** immédiatement actualisée dans le profil après chaque exécution d’évaluation. Pour vous assurer que la valeur mise à jour se trouve dans vos profils, vous devez envisager une mémoire tampon de quelques heures entre l’heure d’évaluation et l’utilisation des attributs calculés. Le planning d’actualisation de l’attribut calculé est **déterminé par le système** et **ne peut pas** être modifié. Pour plus d’informations, contactez l’Assistance clientèle d’Adobe.

## Comment les attributs calculés interagissent-ils avec les audiences évaluées à l’aide de la segmentation en flux continu ?

Si une audience évaluée par segmentation en flux continu utilise un attribut calculé, elle utilise la **dernière valeur** de l’attribut calculé pendant l’évaluation de l’audience. Par exemple, si l’audience recherche des événements d’achat, elle se référera à la dernière valeur d’attribut calculée évaluée lorsque l’événement d’achat arrive.

## Puis-je utiliser des attributs calculés sur Edge ?

Comme tout autre attribut de profil, les attributs calculés sont disponibles et peuvent être utilisés sur les périphéries. Notez que les attributs calculés ne sont **pas** calculés sur Edge.

## Comment les libellés d’utilisation des données sont-ils appliqués aux attributs calculés ?

Les attributs calculés déduisent automatiquement les libellés d’utilisation des données des champs sources et des jeux de données utilisés pour définir les attributs calculés. Cela permet de s’assurer que vos données comportementales sont utilisées de manière appropriée.

## Comment utiliser les attributs calculés avec Adobe Journey Optimizer ?

Pour utiliser les attributs calculés dans les parcours, vous devez ajouter le groupe de champs `SystemComputedAttributes` à la source de données Experience Platform. Pour plus d&#39;informations sur la configuration de la source de données Experience Platform, veuillez lire le guide de la source de données de Adobe Experience Platform [&#128279;](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html).
