---
title: FAQ sur les configurations de flux de données dynamiques
description: Découvrez les questions courantes sur  [!DNL Dynamic Datastream Configurations], notamment le comportement des règles, le routage des événements, les interactions système, les performances et les limites.
source-git-commit: 19e297602d67a360a3b6bcdd6d5403fb6090de7f
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# FAQ sur les configurations des trains de données dynamiques

## Puis-je utiliser des remplacements de flux de données côté [!DNL Dynamic Datastream Configurations] et côté client ensemble ?

Non. Les configurations de train de données dynamiques et [ remplacements de configuration de train de données](/help/datastreams/overrides.md) s’excluent mutuellement par événement. Lorsqu’un événement est associé à un remplacement côté client (envoyé par le biais de Web SDK `sendEvent` ou `configure`), le remplacement est prioritaire et Edge Network ignore [!DNL Dynamic Datastream Configuration] règles pour cet événement.

Planifiez votre implémentation autour d’une approche pour chaque flux de données. Si vous migrez des remplacements vers [!DNL Dynamic Datastream Configurations], supprimez les `edgeConfigOverrides` de votre code SDK à mesure que vous activez les règles correspondantes.

## Que se passe-t-il si aucune règle de [!DNL Dynamic Datastream Configuration] ne correspond à un événement ?

Edge Network achemine l’événement selon la configuration de train de données statique par défaut : le jeu de données d’événement principal et tous les services activés.

Définissez le jeu de données principal sur un jeu de données non activé pour le profil. Les événements inattendus ou non classés arrivent ensuite dans le lac de données au lieu de gonfler votre banque de profils.

## Les [!DNL Dynamic Datastream Configurations] peuvent-ils supprimer ou ignorer entièrement les événements ?

Oui. Désactivez le service (par exemple, [!DNL Adobe Experience Platform]) dans la configuration de routage d’une règle. Edge Network n’envoie pas l’événement à ce service. Si vous désactivez tous les services pour une règle correspondante, l’événement n’atteint aucun traitement en aval.

Pour le filtrage du trafic de robots, Adobe recommande d’acheminer d’abord les événements vers un jeu de données de quarantaine ([cas d’utilisation 4](/help/datastreams/dynamic-configurations/use-cases.md#uc4)) afin de valider votre logique de détection de robots avant de passer à une configuration de suppression complète.

## Puis-je filtrer des champs individuels dans un événement à l’aide de [!DNL Dynamic Datastream Configurations] ?

Non. Les configurations de train de données dynamiques acheminent les événements entiers. Ils ne peuvent pas supprimer ni masquer des champs spécifiques dans une payload d’événement.

## Affecte-t-[!DNL Dynamic Datastream Configuration] les réponses de personnalisation de Target ou de Journey Optimizer ?

La désactivation des [!DNL Adobe Target] pour certains événements via une règle de [!DNL Dynamic Datastream Configuration] empêche ces événements de déclencher Target Decisioning et ne renvoie [!DNL Adobe Target] aucune personnalisation pour eux. Veillez à ne pas désactiver le [!DNL Adobe Target] pour les événements interactifs de chargement de page qui doivent être personnalisés.

La suppression des événements `decisioning.propositionFetch` (voir [cas d’utilisation 3](/help/datastreams/dynamic-configurations/use-cases.md#uc3)) empêche [!DNL Adobe Experience Platform] de stocker ces événements système dans ses jeux de données. Cela ne désactive pas l’appel de personnalisation lui-même. [!DNL Adobe Target] et [!DNL Adobe Journey Optimizer] évaluent et renvoient toujours les décisions de personnalisation, quelle que soit cette règle.

## Comment interagit-[!DNL Data Prep] avec [!DNL Dynamic Datastream Configurations] ?

La [préparation des données pour la collecte de données](/help/datastreams/data-prep.md) s’exécute avant [!DNL Dynamic Datastream Configuration]’évaluation des règles. [!DNL Data Prep] mappe vos données sources brutes (envoyées via l’objet [`data`](/help/collection/js/commands/sendevent/data.md)) dans des champs XDM. Les règles de configuration des trains de données dynamiques évaluent ensuite leurs conditions par rapport à la payload XDM résultante.

Cela signifie que vos conditions de règle peuvent référencer tout champ que [!DNL Data Prep] avez mappé, y compris les champs calculés ou dérivés. Si vous utilisez [!DNL Data Prep], vérifiez que le mappage inclut tous les champs que vous référencez dans vos règles.

Plus généralement, tous les services d’enrichissement, notamment la détection des robots, la géolocalisation et la recherche d’appareils, s’exécutent avant l’évaluation des règles de [!DNL Dynamic Datastream Configuration]. Leurs champs de sortie sont disponibles en tant que conditions de règle.

## Comment interagit-[!DNL Dynamic Datastream Configuration] avec la détection des robots ?

[Détection de robots](/help/datastreams/bot-detection.md) s’exécute avant [!DNL Dynamic Datastream Configuration]’évaluation des règles. La détection des robots balise les événements avec un champ `botDetection.score`. Les configurations de train de données dynamiques peuvent ensuite référencer ce champ en tant que condition dans les règles.

Ils sont complémentaires : la détection des robots identifie le trafic de robots ; [!DNL Dynamic Datastream Configurations] agit sur cette identification en routant ou en ignorant les événements signalés.

## Puis-je acheminer des événements vers des jeux de données dans différents sandbox ?

Non. Les configurations de train de données dynamiques acheminent les événements dans le même sandbox que le train de données. Le système ne prend pas en charge le routage entre sandbox.

## Combien de flux de données puis-je consolider avec [!DNL Dynamic Datastream Configurations] ?

La limite de 5 règles par service détermine la réponse. Si votre configuration actuelle multi-flux de données nécessite plus de 5 chemins de routage distincts par service, vous pouvez toujours avoir besoin de plusieurs flux de données. Cependant, la plupart des mises en œuvre estiment que 5 règles sont suffisantes pour consolider deux à quatre flux de données en un seul.

Consultez [Créer des configurations de flux de données dynamiques](/help/datastreams/dynamic-configurations/configure.md#guardrails) pour obtenir la liste complète des mécanismes de sécurisation, y compris le nombre maximal de règles par service et le nombre maximal de conditions par règle.

## Quel est l’impact de la [!DNL Dynamic Datastream Configurations] sur les performances ?

Les configurations de train de données dynamiques ajoutent une latence minimale. Le système applique un budget d’évaluation de 25 ms pour toutes les règles d’un flux de données. Les règles évaluées dans le cadre de ce budget n’ont aucun impact mesurable sur la latence des événements de bout en bout.

Pour respecter le budget, veillez à ce que les règles soient simples, utilisez le `eventType` comme condition principale et évitez les conditions complexes à champs multiples où des alternatives plus simples existent.

## Étapes suivantes

- Voir [Cas d’utilisation de la configuration dynamique des trains de données](/help/datastreams/dynamic-configurations/use-cases.md) pour obtenir des configurations de règles détaillées.
- Lisez [bonnes pratiques pour [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/best-practices.md) pour obtenir des conseils opérationnels.
- Revenez à [Créer des configurations de flux de données dynamiques](/help/datastreams/dynamic-configurations/configure.md) pour ajuster les conditions des règles ou l’ordre des règles.
