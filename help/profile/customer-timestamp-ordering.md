---
title: Commande d’horodatage client
description: Découvrez comment ajouter un ordre d’horodatage client à vos jeux de données pour garantir la cohérence de vos données de profil.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
TQID: https://experienceleague.adobe.com/aLG9NXX2dnBkavqylpkVSWLNtvGht37lD5AmdzjdC7Y
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 417
ht-degree: 2%

---

# Ordre de date et heure du client

Dans Adobe Experience Platform, l’ordre des données n’est pas garanti par défaut lors de l’ingestion de données par le biais de l’ingestion en flux continu vers la banque de profils. Grâce à l’ordre des horodatages client, vous pouvez garantir que le dernier message, conformément à l’horodatage client fourni, sera conservé dans la banque de profils. Tous les messages obsolètes seront alors ignorés et ne seront **pas** disponibles pour une utilisation dans les services en aval qui utilisent les données de profil comme la segmentation et les destinations. Par conséquent, cela permet à vos données de profil d’être cohérentes et de rester synchronisées avec vos systèmes sources.

Pour activer la commande d’horodatage client, utilisez le champ `extSourceSystemAudit.lastUpdatedDate` dans le groupe de champs [&#x200B; Attributs d’audit du système Source externe &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) et contactez votre gestionnaire de compte technique Adobe ou l’assistance clientèle Adobe avec votre sandbox et vos informations sur le jeu de données.

## Contraintes

Pendant cette version bêta privée, les contraintes suivantes s’appliquent lors de l’utilisation de l’ordre d’horodatage client :

- Vous pouvez uniquement utiliser l’ordre d’horodatage client avec des **attributs de profil** ingérés avec l’**ingestion par flux** sur la banque de profils.
   - Aucune garantie de commande **no** n’est fournie pour les données du lac de données ou du service d’identités.
- Vous pouvez uniquement utiliser l’ordre d’horodatage client sur les sandbox **hors production**.
- Vous pouvez uniquement appliquer l’ordre d’horodatage client aux jeux de données **5** par sandbox.
- Vous **ne pouvez pas** utiliser des upserts en flux continu pour envoyer des mises à jour de lignes partielles dans un jeu de données pour lequel l’ordre d’horodatage client est activé.
- Le champ `extSourceSystemAudit.lastUpdatedDate` **doit** être un horodatage UTC [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) avec une précision en millisecondes (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`).
- Toutes les lignes de données ingérées **doivent** contiennent le champ `extSourceSystemAudit.lastUpdatedDate` en tant que groupe de champs de niveau supérieur. Cela signifie que ce champ **doit** ne pas être imbriqué dans le schéma XDM. Si ce champ est manquant ou son format est incorrect, l’enregistrement incorrect n’est **pas** ingéré et un message d’erreur correspondant est envoyé.
- Tout jeu de données activé pour la commande d’horodatage client **doit** être un nouveau jeu de données sans données précédemment ingérées.
- Pour un fragment de profil donné, seules les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus récent seront ingérées. Les lignes contenant un `extSourceSystemAudit.lastUpdatedDate` plus ancien ou du même âge seront ignorées.

## Recommandations

Lors de l’implémentation de la commande d’horodatage client, tenez compte des points suivants :

- La synchronisation des horloges sur tous les systèmes internes envoie les données dans la banque de profils.
- Vos horodatages au format ISO 8061 doivent être précis au niveau de la milliseconde.
