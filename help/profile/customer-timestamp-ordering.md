---
title: Commande d’horodatage client
description: Découvrez comment ajouter un ordre d’horodatage client à vos jeux de données pour garantir la cohérence de vos données de profil.
badgePrivateBeta: label="Beta privée" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Ordre des horodatages du client

Dans Adobe Experience Platform, l’ordre des données n’est pas garanti par défaut lors de l’ingestion de données par flux vers la banque de profils. Avec l’ordre des horodatages client, vous pouvez garantir que le dernier message, conformément à l’horodatage client fourni, sera conservé dans la banque de profils. Tous les messages obsolètes seront alors ignorés et seront **not** peut être utilisé dans les services en aval qui utilisent des données de profil telles que la segmentation et les destinations. Ainsi, vos données de profil seront cohérentes et vos données de profil resteront synchronisées avec vos systèmes sources.

Pour activer l’ordre d’horodatage des clients, utilisez la variable `extSourceSystemAudit.lastUpdatedDate` dans le champ [Type de données Attributs d’audit du système de source externe](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) et contactez votre gestionnaire de compte technique d’Adobe ou l’assistance clientèle d’Adobe avec vos informations de sandbox et de jeu de données.

## Contraintes

Lors de cette version bêta privée, les contraintes suivantes s’appliquent lors de l’utilisation de l’horodatage client :

- Vous pouvez uniquement utiliser l’ordre d’horodatage client avec **attributs de profil** ingéré avec **ingestion par flux** dans la banque de profils.
   - Il y a **non** commande des garanties fournies pour les données dans le lac de données ou Identity Service.
- Vous pouvez uniquement utiliser l’ordre d’horodatage client sur **hors production** environnements de test.
- Vous pouvez uniquement appliquer un ordre d’horodatage client à la variable **5** jeux de données par environnement de test.
- You **cannot** utilisez des upserts de diffusion en continu pour envoyer des mises à jour de lignes partielles dans un jeu de données pour lequel l’horodatage du client est activé.
- La variable `extSourceSystemAudit.lastUpdatedDate` field **must** être dans la variable [ISO 8601](https://www.iso.org/fr/iso-8601-date-and-time-format.html) format. Lorsque vous utilisez le format ISO 8601, **must** être une date et une heure complètes au format `yyyy-MM-ddTHH:mm:ss.sssZ` (par exemple, `2028-11-13T15:06:49.001Z`).
- Toutes les lignes de données ingérées **must** contain the `extSourceSystemAudit.lastUpdatedDate` comme groupe de champs de niveau supérieur. Cela signifie que ce champ **must** ne pas être imbriqué dans le schéma XDM. Si ce champ est manquant ou dans un format incorrect, l’enregistrement incorrect sera **not** sont ingérés et un message d’erreur correspondant est envoyé.
- Tout jeu de données activé pour l’horodatage client **must** être un nouveau jeu de données sans aucune donnée précédemment ingérée.
- Pour tout fragment de profil donné, seules les lignes contenant un fragment plus récent `extSourceSystemAudit.lastUpdatedDate` sera ingéré. Lignes contenant un `extSourceSystemAudit.lastUpdatedDate` qui est plus âgé ou dont le même âge sera ignoré.

## Recommandations

Lors de l’implémentation de l’horodatage des clients, veuillez tenir compte des points suivants :

- Vous êtes responsable de la synchronisation des horloges sur tous les systèmes internes qui envoient des données dans la banque de profils.
- Les horodatages au format ISO 8061 doivent avoir une précision de millisecondes.
