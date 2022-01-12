---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;adresse;xdm:address;datatype;type de données;type de données;
solution: Experience Platform
title: Type de données d’adresse postale
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Postal Address (Adresse postale).
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 23%

---

# [!UICONTROL Adresse postale] type de données

[!UICONTROL Adresse postale] est un type de données XDM standard qui décrit les détails d’une adresse postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `city` | Nom de la ville. |
| `country` | Nom du territoire administré par un gouvernement. Il s’agit d’un champ de forme libre qui peut avoir le nom du pays dans n’importe quelle langue. |
| `countryCode` | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `createdByBatchID` | L’identifiant du fichier de commandes ingéré qui a créé l’enregistrement d’adresse. |
| `dmaID` | Zone de marché désignée pour la recherche sur les médias Nielsen. |
| `label` | Nom de forme libre pour l’adresse. |
| `lastVerifiedDate` | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme toujours associée à la personne. |
| `modifiedByBatchID` | L’identifiant du fichier de commandes ingéré qui a modifié l’enregistrement pour la dernière fois. |
| `msaID` | Zone statistique métropolitaine aux États-Unis où l’observation s’est produite. |
| `postOfficeBox` | Boîte postale de l’adresse. |
| `postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `primary` | Valeur boolean qui indique s’il s’agit de l’adresse Principale de l’individu. Un profil ne peut avoir qu’un seul `primary` adresse à un moment donné. |
| `region` | Partie de l’adresse qui indique la région, le département ou le district. |
| `repositoryCreatedBy` | L’identifiant de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | L’identifiant de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |
| `stateProvince` | Partie de l’état ou de la province de l’observation. Le format est conforme à la norme [ISO 3166-2 (pays et subdivisions)](https://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indique si l’adresse peut être actuellement utilisée. |
| `statusReason` | Description de la variable active `status`. |
| `street1` - `street4` | Ces quatre champs sont destinés à contenir des informations Principales sur les rues, le numéro d’appartement, le numéro de rue et le nom de la rue. `street2` to `street4` sont facultatives. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données des adresses postales, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
