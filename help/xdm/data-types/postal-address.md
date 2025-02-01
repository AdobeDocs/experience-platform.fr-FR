---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;address;xdm:address;type de données;type de données;type de données;
solution: Experience Platform
title: Type De Données D’Adresse Postale
description: Découvrez le type de données XDM de l’adresse postale.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 32%

---

# [!UICONTROL Adresse postale] type de données

[!UICONTROL Adresse postale] est un type de données XDM standard qui décrit les détails d’une adresse de publipostage.

![](../images/data-types/postal-address.png){width=450}

| Propriété | Description |
| --- | --- |
| `city` | Nom de la ville. |
| `country` | Nom du territoire administré par un gouvernement. Il s’agit d’un champ à structure libre pouvant contenir le nom du pays dans n’importe quelle langue. |
| `countryCode` | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `createdByBatchID` | Identifiant du fichier de commandes ingéré qui a créé l’enregistrement d’adresse. |
| `dmaID` | Zone de marché désignée par Nielsen Media Research. |
| `label` | Nom de l’adresse sous forme libre. |
| `lastVerifiedDate` | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme étant toujours associée à la personne. |
| `modifiedByBatchID` | Identifiant du fichier de commandes ingéré qui a modifié l’enregistrement pour la dernière fois. |
| `msaID` | Région métropolitaine des États-Unis dans laquelle cette observation a été effectuée. |
| `postOfficeBox` | Boîte postale de l’adresse. |
| `postalCode` | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `primary` | Valeur booléenne qui indique s’il s’agit de l’adresse principale de l’individu. Un profil ne peut avoir qu’une seule adresse `primary` à un moment donné. |
| `region` | Partie de l’adresse qui indique la région, le département ou le district. |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID du dernier utilisateur ayant modifié l’enregistrement. |
| `stateProvince` | Partie de l’état ou de la province de l’observation. Le format suit la norme [ISO 3166-2 (pays et subdivisions)](https://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indique si l&#39;adresse peut être actuellement utilisée. |
| `statusReason` | Description de la `status` actuelle. |
| `street1` - `street4` | Ces quatre champs sont destinés à contenir des informations principales au niveau de la rue, le numéro de l’appartement, le numéro de la rue et le nom de la rue. Les `street2` à `street4` sont facultatives. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données d’adresse postale, consultez le référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
