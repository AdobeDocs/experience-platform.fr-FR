---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;adresse;xdm:address;datatype;type de données;type de données;
solution: Experience Platform
title: Type de données d’adresse postale
description: Découvrez le type de données XDM Adresse postale .
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 32%

---

# Type de données [!UICONTROL Adresse postale]

[!UICONTROL Adresse postale] est un type de données XDM standard qui décrit les détails d’une adresse postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `city` | Nom de la ville. |
| `country` | Nom du territoire administré par un gouvernement. Il s’agit d’un champ de forme libre qui peut avoir le nom du pays dans n’importe quelle langue. |
| `countryCode` | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `createdByBatchID` | L’identifiant du fichier de commandes ingéré qui a créé l’enregistrement d’adresse. |
| `dmaID` | Zone de marché désignée par Nielsen Media Research. |
| `label` | Nom de forme libre pour l’adresse. |
| `lastVerifiedDate` | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme étant toujours associée à la personne. |
| `modifiedByBatchID` | L’identifiant du fichier de commandes ingéré qui a modifié l’enregistrement pour la dernière fois. |
| `msaID` | Région métropolitaine des États-Unis dans laquelle cette observation a été effectuée. |
| `postOfficeBox` | Boîte postale de l’adresse. |
| `postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `primary` | Une valeur booléenne qui indique s’il s’agit de l’adresse principale de l’individu. Un profil ne peut avoir qu’une seule adresse `primary` à un moment donné. |
| `region` | Partie de l’adresse qui indique la région, le département ou le district. |
| `repositoryCreatedBy` | L’identifiant de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | L’identifiant de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |
| `stateProvince` | Partie de l’état ou de la province de l’observation. Le format suit la norme [ISO 3166-2 (pays et subdivisions)](https://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indique si l’adresse peut être actuellement utilisée. |
| `statusReason` | Description du `status` actif. |
| `street1` - `street4` | Ces quatre champs sont destinés à contenir des informations principales sur la rue, le numéro d’appartement, le numéro de rue et le nom de la rue. `street2` à `street4` sont facultatifs. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données des adresses postales, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
