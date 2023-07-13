---
title: Type de données Détails du compte
description: Ce document présente un aperçu du type de données XDM (Account Details Experience Data Model).
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: 55f86fdd4fd36d21dcbd575d6da83df18abb631d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 19%

---

# [!UICONTROL Détails du compte] type de données

[!UICONTROL Détails du compte] est un type de données XDM (Experience Data Model) standard qui décrit les détails liés à une entreprise.

![Structure du type de données](../images/data-types/account-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Devise]](./currency.md) | Montant estimé des recettes annuelles de l’organisation. |
| `DUNSNumber` | Chaîne | Dun &amp; Bradstreet D-U-N-S Number de l&#39;organisation. Il s’agit d’un nombre à neuf chiffres non indicatif attribué à chaque emplacement commercial dans la base de données de Dun &amp; Bradstreet, qui fonctionne de manière unique, distincte et distincte. Il est conservé uniquement par Dun &amp; Bradstreet. |
| `NAICSCode` | Chaîne | La classification de l’organisation dans le Système de classification des industries de l’Amérique du Nord. |
| `NAICSDescription` | Chaîne | Brève description du secteur d’activité d’une organisation, basée sur son code NAICS. |
| `SICCode` | Chaîne | Code SIC (Standard Industrial Classification) de l’organisation. Il s’agit d’un code à quatre chiffres qui classe le secteur auquel appartiennent les entreprises en fonction de leurs activités commerciales. |
| `SICDescription` | Chaîne | Brève description du secteur d’activité d’une organisation, en fonction de son code SIC. |
| `companyProductAndServices` | Chaîne | Les produits et services dans lesquels l’organisation traite ou traite. |
| `facebookPageUrl` | Chaîne | Lien vers le compte Facebook de l’organisation. |
| `industry` | Chaîne | Le secteur dans lequel cette organisation fait partie. Il s’agit d’un champ de forme libre, et il est conseillé d’utiliser une valeur structurée pour les requêtes ou d’utiliser la propriété `xdm:classifier`. |
| `jigsaw` | Chaîne | Clé Data.com de l’organisation. |
| `linkedinPageUrl` | Chaîne | Lien vers le compte LinkedIn de l’organisation. |
| `logoUrl` | Chaîne | Un chemin à combiner avec l’URL d’une instance Salesforce (par exemple, `https://yourInstance.salesforce.com/`) pour générer une URL permettant de demander l’image de profil de réseau social associée à l’organisation. L’URL générée renvoie une redirection HTTP (code 302) vers l’image de profil de réseau social pour l’organisation. |
| `marketSegment` | Chaîne | audience de marché nommée à laquelle l’organisation participe. Il s’agit d’un champ de forme libre, et il est conseillé d’utiliser une valeur structurée pour les requêtes ou d’utiliser la propriété `xdm:identifier`. |
| `numberOfEmployees` | Nombre entier | Nombre d’employés de l’organisation. |
| `organizationType` | Chaîne | Libellé décrivant le type d’organisation. |
| `primaryEmailDomain` | Chaîne | Domaine de messagerie Principal utilisé par l’organisation pour son personnel. |
| `rating` | Double | Score calculé ou nombre d’étoiles pour cette organisation. `1` indique la note maximale possible, et `0` est la note minimale possible. |
| `tickerSymbol` | Chaîne | Le symbole boursier de ce compte. 20 caractères maximum. |
| `twitterHandleUrl` | Chaîne | Lien vers le gestionnaire twitter de l’organisation. |
| `website` | Chaîne | URL du site web de l’organisation. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
