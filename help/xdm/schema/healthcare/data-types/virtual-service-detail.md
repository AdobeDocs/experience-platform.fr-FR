---
title: Type de données des détails du service virtuel
description: Découvrez le type de données XDM (Virtual Service Detail Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bde7363c-43b7-402d-96b2-7aa0160cd2ea
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# Type de données [!UICONTROL Virtual Service Detail]

[!UICONTROL Virtual Service Detail] est un type de données standard Experience Data Model (XDM) qui décrit les coordonnées du service virtuel. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Détails du service virtuel](../../../images/healthcare/data-types/virtual-service-detail.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Point de contact de l’adresse] | `addressContactPoint` | [[!UICONTROL Point de contact]](../data-types/contact-point.md) | Les détails d’un point de contact assisté par la technologie, tel qu’un téléphone, un fax ou un e-mail. |
| [!UICONTROL Adresse Extended Contact Detail] | `addressExtendedContactDetail` | [[!UICONTROL &#x200B; &lbrace;Extended Contact Detail]](../data-types/extended-contact-detail.md) | Coordonnées étendues. |
| [!UICONTROL Type de canal] | `channelType` | [[!UICONTROL Coding]](../data-types/coding.md) | Le type de service virtuel auquel se connecter, par exemple les équipes, le zoom ou WhatsApp. |
| [!UICONTROL Informations supplémentaires] | `additionalInfo` | Tableau de chaînes | Adresse permettant d’afficher d’autres détails de connexion, représentés sous forme d’URI. |
| [!UICONTROL Chaîne d’adresse] | `addressString` | Chaîne | Adresse à utiliser pour la connexion au service virtuel. |
| [!UICONTROL Adresse Url] | `addressUrl` | Chaîne | URL à utiliser pour la connexion au service virtuel, représenté sous la forme d’un URI. |
| [!UICONTROL Nombre max de participants] | `maxParticipants` | Nombre entier | Nombre maximal de participants pris en charge, avec une valeur minimale de `0`. |
| [!UICONTROL Clé de session] | `sessionKey` | Chaîne | Clé de session requise par le service virtuel. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
