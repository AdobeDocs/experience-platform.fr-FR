---
title: Groupe de champs de schéma des composants de personne professionnelle XDM
description: Découvrez le groupe de champs de schéma XDM Business Person Components.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# [!UICONTROL Groupe de champs de schéma XDM Business Person Components]

[!UICONTROL XDM Business Person Components] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui capture plusieurs enregistrements source pour une personne, ainsi que d’autres attributs requis pour la segmentation des personnes.

Lorsqu’un profil est créé pour une personne via [Real-time Customer Profile](../../../profile/home.md) dans l’édition B2B de Real-Time CDP, les informations utilisées pour créer ce profil peuvent potentiellement provenir de nombreux enregistrements source. Par exemple, si une personne travaille pour deux sociétés différentes, de nombreux systèmes de gestion de la relation client créent intentionnellement une copie en double de cette personne afin qu’une copie soit liée à la Société A, tandis que l’autre est liée à la Société B. Lorsque vous incorporez ces données dans Adobe Experience Platform, ce groupe de champs est utilisé pour fusionner ces différents enregistrements source en une seule représentation.

Le groupe de champs fournit un champ `personComponents` de niveau racine, qui est un tableau d’objets. Chaque objet du tableau représente un enregistrement source différent.

>[!IMPORTANT]
>
>Vous devez suivre les modèles d’ingestion comme décrit dans la [documentation sur les sources](../../../rtcdp/sources/b2b.md). Il n’est pas garanti que les autres méthodes de mappage de champs fonctionnent.
>
>Par exemple, chaque objet du tableau `personComponents` est envoyé individuellement lors des modèles d’ingestion standard, puis ajouté au tableau par Platform. L’ajout manuel d’un tableau d’objets au composant Personne active renvoie une erreur.
>Vous devez utiliser l’utilitaire de génération automatique lors de la création de schémas pour vos données B2B. Consultez la documentation pour obtenir des instructions sur l’utilisation de l’espace de noms [B2B et de l’utilitaire de génération automatique de schéma](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Si vous n’utilisez pas l’utilitaire de génération automatique et envisagez de mapper manuellement votre modèle de données, veillez à lire la documentation sur les [classes XDM Adobe Real-Time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) avant de mapper vos données.
>
>Pour plus d’informations sur les workflows recommandés pour les données B2B, consultez le [tutoriel de bout en bout](../../../rtcdp/b2b-tutorial.md) .

![](../../images/field-groups/business-person-components.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte associé à la personne. |
| `sourceConvertedContactKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du contact associé si ce prospect a été converti. |
| `sourceExternalKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du système source d’où proviennent les données de la personne. |
| `sourcePersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne. |
| `workEmail` | [[!UICONTROL Adresse électronique]](../../data-types/b2b-source.md) | ID de l’adresse électronique professionnelle de la personne. |
| `personGroupID` | Chaîne | Identifiant de groupe de la personne. |
| `personScore` | Chaîne | Score généré pour la personne par un système CRM. |
| `personSource` | Chaîne | Identifiant unique basé sur des chaînes pour le système source d’où proviennent les données de la personne. |
| `personStatus` | Chaîne | État actuel du marketing ou des ventes de la personne. |
| `personType` | Chaîne | Type de personne dans un contexte B2B. |
| `sourceAccountID` | Chaîne | Identifiant unique basé sur des chaînes pour le compte dans le système source associé à la personne. Ce champ est utilisé comme clé étrangère par le système pour rechercher les différentes entreprises pour lesquelles cette personne travaille. |
| `sourceConvertedContactID` | Chaîne | Identifiant unique basé sur des chaînes pour le contact associé si cette piste a été convertie. |
| `sourceExternalID` | Chaîne | Identifiant unique basé sur des chaînes pour le système source d’où proviennent les données de la personne. |
| `sourcePersonID` | Chaîne | Identifiant unique basé sur des chaînes pour la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
