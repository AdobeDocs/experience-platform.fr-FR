---
title: Commande d’horodatage client
description: Découvrez comment ajouter un ordre d’horodatage client à vos jeux de données pour garantir la cohérence de vos données de profil.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Ordre des horodatages du client

Dans Adobe Experience Platform, l’ordre des données n’est pas garanti par défaut lors de l’ingestion de données par flux vers la banque de profils. Avec l’ordre des horodatages client, vous pouvez garantir que le dernier message, conformément à l’horodatage client fourni, sera conservé dans la banque de profils. Tous les messages obsolètes seront alors déposés et **not** seront disponibles pour une utilisation dans les services en aval qui utilisent des données de profil telles que la segmentation et les destinations. Ainsi, vos données de profil seront cohérentes et vos données de profil resteront synchronisées avec vos systèmes sources.

Pour activer l’horodatage des clients, utilisez le champ `extSourceSystemAudit.lastUpdatedDate` dans le [groupe de champs Attributs d’audit du système Source externe](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) et contactez votre gestionnaire de compte technique Adobe ou l’Adobe de l’assistance clientèle avec vos informations d’environnement de test et de jeu de données.

## Contraintes

Lors de cette version bêta privée, les contraintes suivantes s’appliquent lors de l’utilisation de l’horodatage client :

- Vous pouvez uniquement utiliser l’ordre d’horodatage client avec les **attributs de profil** ingérés avec l’ **ingestion par flux** sur la banque de profils.
   - **no** fournit des garanties de commande pour les données dans le lac de données ou Identity Service.
- Vous ne pouvez utiliser l’horodatage des clients que sur les environnements de test **hors production**.
- Vous pouvez uniquement appliquer un ordre d’horodatage client aux jeux de données **5** par environnement de test.
- Vous **ne pouvez pas** utiliser des upserts de diffusion en continu pour envoyer des mises à jour de lignes partielles dans un jeu de données pour lequel l’horodatage du client est activé.
- Le champ `extSourceSystemAudit.lastUpdatedDate` **doit** être au format [ISO 8601](https://www.iso.org/fr/iso-8601-date-and-time-format.html). Lors de l’utilisation du format ISO 8601, il **doit** être une date et une heure complètes au format `yyyy-MM-ddTHH:mm:ss.sssZ` (par exemple, `2028-11-13T15:06:49.001Z`).
- Toutes les lignes de données ingérées **must** contiennent le champ `extSourceSystemAudit.lastUpdatedDate` en tant que groupe de champs de niveau supérieur. Cela signifie que ce champ **ne doit pas être imbriqué dans le schéma XDM.** Si ce champ est manquant ou dans un format incorrect, l’enregistrement incorrect sera **not** ingéré et un message d’erreur correspondant sera envoyé.
- Tout jeu de données activé pour l’ordre d’horodatage des clients **doit** être un nouveau jeu de données sans aucune donnée précédemment ingérée.
- Pour tout fragment de profil donné, seules les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus récent seront ingérées. Les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus ancien ou ayant le même âge seront ignorées.

## Recommandations

Lors de l’implémentation de l’horodatage des clients, veuillez tenir compte des points suivants :

- Vous êtes responsable de la synchronisation des horloges sur tous les systèmes internes qui envoient des données dans la banque de profils.
- Les horodatages au format ISO 8061 doivent avoir une précision de millisecondes.
