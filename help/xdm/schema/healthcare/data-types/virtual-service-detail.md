---
title: Type de données de détails du service virtuel
description: Découvrez le type de données du modèle de données d’expérience (XDM) des détails du service virtuel.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
TQID: https://experienceleague.adobe.com/RNyZBglQGRj-B0-fO3PXMSSRnD05hdP-XhkaRdjH3fs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 6%

---

# Type de données [!UICONTROL Virtual Service Detail]

[!UICONTROL Virtual Service Detail] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails de contact du service virtuel. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure de type de données Détails du service virtuel](../../../images/healthcare/data-types/virtual-service-detail.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Address Contact Point] | `addressContactPoint` | [[!UICONTROL Contact Point]](../data-types/contact-point.md) | Détails d’un point de contact recourant à la technologie, tel qu’un téléphone, un fax ou un e-mail. |
| [!UICONTROL Address Extended Contact Detail] | `addressExtendedContactDetail` | [[!UICONTROL Extended Contact Detail]](../data-types/extended-contact-detail.md) | Coordonnées étendues. |
| [!UICONTROL Channel Type] | `channelType` | [[!UICONTROL Coding]](../data-types/coding.md) | Type de service virtuel auquel se connecter, tel que Teams, Zoom ou WhatsApp. |
| [!UICONTROL Additional Info] | `additionalInfo` | Tableau de chaînes | Adresse pour afficher les autres détails de connexion, représentés sous la forme d’un URI. |
| [!UICONTROL Address String] | `addressString` | Chaîne | Adresse à utiliser pour la connexion au service virtuel. |
| [!UICONTROL Address Url] | `addressUrl` | Chaîne | URL à utiliser pour la connexion au service virtuel, représentée sous la forme d’un URI. |
| [!UICONTROL Max Participants] | `maxParticipants` | Entier | Nombre maximal de participants pris en charge, avec une valeur minimale de `0`. |
| [!UICONTROL Session Key] | `sessionKey` | Chaîne | Clé de session requise par le service virtuel. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
