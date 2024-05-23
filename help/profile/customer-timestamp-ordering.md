---
title: Commande d’horodatage client
description: Découvrez comment ajouter un ordre d’horodatage client à vos jeux de données pour garantir la cohérence de vos données de profil.
badgePrivateBeta: label="Beta privée" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Ordre des horodatages du client

Dans Adobe Experience Platform, l’ordre des données n’est pas automatiquement garanti lors de l’ingestion de données par flux vers la banque de profils. Avec l’ordre des horodatages client, vous pouvez garantir que le dernier message, conformément à l’horodatage client fourni, sera conservé dans la banque de profils. Ainsi, vos données de profil seront cohérentes et vos données de profil resteront synchronisées avec vos systèmes sources.

Pour activer l’ordre d’horodatage des clients, vous devez utiliser la variable `lastUpdatedDate` dans le champ [Type de données Attributs d’audit du système de source externe](../xdm/data-types/external-source-system-audit-attributes.md) et contactez votre gestionnaire de compte technique d’Adobe ou l’assistance clientèle d’Adobe avec vos informations de sandbox et de jeu de données.

## Contraintes

Lors de cette version bêta privée, les contraintes suivantes s’appliquent lors de l’utilisation de l’horodatage client :

- Vous pouvez uniquement utiliser l’ordre d’horodatage client avec **attributs de profil** ingéré avec **ingestion par flux**.
- Vous pouvez uniquement utiliser l’ordre d’horodatage client sur **hors production** environnements de test.
- Vous pouvez uniquement appliquer un ordre d’horodatage client à la variable **5** jeux de données par environnement de test.
- La variable `lastUpdatedDate` doit se trouver dans le champ [ISO 8601](https://www.iso.org/fr/iso-8601-date-and-time-format.html) format.
- Toutes les lignes de données ingérées **must** contain the `lastUpdatedDate` champ . Si ce champ est manquant ou est dans un format incorrect, l’ingestion échoue.
- Tout jeu de données activé pour l’horodatage client **must** être un nouveau jeu de données sans aucune donnée précédemment ingérée.
- Pour tout fragment de profil donné, seules les lignes contenant un fragment plus récent `lastUpdatedDate` sera ingéré. Si la ligne ne contient pas d’élément plus récent `lastUpdatedDate`, la ligne est ignorée.

## Recommandations

Lors de l’implémentation de l’horodatage des clients, veuillez tenir compte des points suivants :

- Vous êtes responsable de la synchronisation des horloges sur tous les systèmes internes qui envoient des données dans la banque de profils.
- Les horodatages au format ISO 8061 doivent avoir une précision de millisecondes.
- L’utilisation de la préparation de données en coordination avec l’ordre d’horodatage des clients est **fortement recommandé**, à l’étape , une copie de toutes les lignes ingérées et de leurs horodatages est créée, ce qui permet un meilleur débogage en cas de problème.
