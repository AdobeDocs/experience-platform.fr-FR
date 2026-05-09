---
title: Commande d’horodatage client
description: Découvrez comment ajouter un ordre d’horodatage client à vos jeux de données pour garantir la cohérence de vos données de profil.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 752e9939a7d141921330d5a52dd4299681d09205
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---

# Ordre de date et heure du client

Dans Adobe Experience Platform, l’ordre des données n’est pas garanti par défaut lors de l’ingestion de données par le biais de l’ingestion en flux continu vers la banque de profils. Grâce à l’ordre des horodatages client, vous pouvez garantir que le dernier message, conformément à l’horodatage client fourni, sera conservé dans la banque de profils. Tous les messages obsolètes seront alors ignorés et ne seront **pas** disponibles pour une utilisation dans les services en aval qui utilisent les données de profil comme la segmentation et les destinations. Par conséquent, cela permet à vos données de profil d’être cohérentes et de rester synchronisées avec vos systèmes sources.

Pour activer la commande d’horodatage client, utilisez le champ `extSourceSystemAudit.lastUpdatedDate` dans le groupe de champs [ Attributs d’audit du système Source externe ](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) et contactez votre gestionnaire de compte technique Adobe ou l’assistance clientèle Adobe avec votre sandbox et vos informations sur le jeu de données.

## Contraintes

Pendant cette version bêta privée, les contraintes suivantes s’appliquent lors de l’utilisation de l’ordre d’horodatage client :

- Vous pouvez uniquement utiliser l’ordre d’horodatage client avec des **attributs de profil** ingérés avec l’**ingestion par flux** sur la banque de profils.
   - Aucune garantie de commande **no** n’est fournie pour les données du lac de données ou du service d’identités.
- Vous pouvez uniquement utiliser l’ordre d’horodatage client sur les sandbox **hors production**.
- Vous pouvez uniquement appliquer l’ordre d’horodatage client aux jeux de données **5** par sandbox.
- Vous **ne pouvez pas** utiliser des upserts en flux continu pour envoyer des mises à jour de lignes partielles dans un jeu de données pour lequel l’ordre d’horodatage client est activé.
- Le champ `extSourceSystemAudit.lastUpdatedDate` **doit** doit être au format [ISO 8601](https://www.iso.org/fr/iso-8601-date-and-time-format.html). Lors de l’utilisation du format ISO 8601, il **doit** être une date-heure complète au format `yyyy-MM-ddTHH:mm:ss.sssZ` (par exemple, `2028-11-13T15:06:49.001Z`).
- Toutes les lignes de données ingérées **doivent** contiennent le champ `extSourceSystemAudit.lastUpdatedDate` en tant que groupe de champs de niveau supérieur. Cela signifie que ce champ **doit** ne pas être imbriqué dans le schéma XDM. Si ce champ est manquant ou son format est incorrect, l’enregistrement incorrect n’est **pas** ingéré et un message d’erreur correspondant est envoyé.
- Tout jeu de données activé pour la commande d’horodatage client **doit** être un nouveau jeu de données sans données précédemment ingérées.
- Pour un fragment de profil donné, seules les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus récent seront ingérées. Les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus ancien ou du même âge seront ignorées.

## Recommandations

Lors de l’implémentation de la commande d’horodatage client, tenez compte des points suivants :

- La synchronisation des horloges sur tous les systèmes internes envoie les données dans la banque de profils.
- Vos horodatages au format ISO 8061 doivent être précis au niveau de la milliseconde.
