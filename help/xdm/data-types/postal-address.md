---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;adresse;xdm:address;datatype;data-type;data type;data type;
solution: Experience Platform
title: Type de données d'adresse postale
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM d’adresse postale.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 22%

---

# [!UICONTROL Type de données d&#39;] adresse postale

[!UICONTROL L&#39;] adresse postale est un type de données XDM standard qui décrit les détails d&#39;une adresse postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propriété | Description |
| --- | --- |
| `city` | Nom de la ville. |
| `country` | Nom du territoire administré par un gouvernement. Il s’agit d’un champ de forme libre qui peut avoir le nom du pays dans n’importe quelle langue. |
| `countryCode` | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `createdByBatchID` | ID du fichier de commandes assimilé qui a créé l&#39;enregistrement d&#39;adresse. |
| `dmaID` | La recherche médiatique Nielsen a désigné zone de marché. |
| `label` | Nom de forme libre pour l’adresse. |
| `lastVerifiedDate` | Date à laquelle l&#39;adresse a été vérifiée pour la dernière fois comme toujours associée à la personne. |
| `modifiedByBatchID` | ID du fichier de commandes assimilé qui a modifié l&#39;enregistrement pour la dernière fois. |
| `msaID` | Zone statistique métropolitaine aux États-Unis où l&#39;observation s&#39;est produite. |
| `postOfficeBox` | Boîte postale de l&#39;adresse. |
| `postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `primary` | Valeur booléenne qui indique s’il s’agit de l’adresse Principale de l’individu. Un profil ne peut avoir qu&#39;une seule adresse `primary` à un moment donné. |
| `region` | Partie de l’adresse qui indique la région, le département ou le district. |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |
| `stateProvince` | Partie de l’état ou de la province de l’observation. Le format est conforme à la norme [ISO 3166-2 (pays et subdivisions)](http://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indique si l’adresse peut être utilisée actuellement. |
| `statusReason` | Description du `status` actif. |
| `street1` - `street4` | Ces quatre champs sont conçus pour contenir des renseignements Principaux sur la rue, le numéro d&#39;appartement, le numéro de rue et le nom de la rue. `street2` sont  `street4` facultatives. |

Pour plus d&#39;informations sur le type de données d&#39;adresse postale, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)
