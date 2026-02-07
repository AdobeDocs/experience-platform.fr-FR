---
title: Groupe de champs de schéma des composants Business Person XDM
description: Découvrez le groupe de champs de schéma Composants professionnels XDM .
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions" newtab=true
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 3fafccef44823b80938db96a7751edbff5a2fd02
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 4%

---

# [!UICONTROL XDM Business Person Components] groupe de champs de schéma

>[!AVAILABILITY]
>
>Ce groupe de champs n’est disponible que pour les organisations ayant accès au B2B edition Real-Time CDP.

[!UICONTROL XDM Business Person Components] est un groupe de champs de schéma standard pour la classe [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) qui capture plusieurs enregistrements sources pour une personne, ainsi que d’autres attributs requis pour la segmentation de la personne.

Lorsqu’un profil est créé pour une personne par l’intermédiaire du [profil client en temps réel](../../../profile/home.md) dans le B2B edition de Real-Time CDP, les informations utilisées pour créer ce profil peuvent provenir de nombreux enregistrements sources. Par exemple, si une personne travaille pour deux sociétés différentes, de nombreux systèmes de gestion de la relation client (CRM) dupliquent intentionnellement une copie de cette personne, de sorte qu’une copie est liée à la société A, tandis que l’autre est liée à la société B. Lors de l’importation de ces données dans Adobe Experience Platform, ce groupe de champs est utilisé pour fusionner ces différents enregistrements sources en une seule représentation.

Le groupe de champs fournit un champ de `personComponents` au niveau racine, qui est un tableau d’objets . Chaque objet du tableau représente un enregistrement source différent.

>[!IMPORTANT]
>
>Vous devez suivre les modèles d’ingestion comme décrit dans la [documentation sur les sources](../../../rtcdp/sources/b2b.md). Il n’est pas garanti que les autres méthodes de mappage de champs fonctionnent.
>
>Par exemple, chaque objet du tableau `personComponents` est envoyé individuellement lors des modèles d’ingestion standard, puis ajouté au tableau par Experience Platform. L’ajout manuel d’un tableau d’objets au composant Professionnel renvoie une erreur.
>Vous devez utiliser l’utilitaire de génération automatique lors de la création de schémas pour vos données B2B. Consultez la documentation pour obtenir des instructions sur l’utilisation de l’utilitaire de génération automatique de schémas et d’espaces de noms [B2B](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Si vous n’utilisez pas l’utilitaire de génération automatique et envisagez de mapper manuellement votre modèle de données, assurez-vous de lire la documentation sur les [classes XDM Adobe Real-Time Customer Data Platform B2B edition](../../../rtcdp/schemas/b2b.md) avant de mapper vos données.
>
>Consultez le [tutoriel complet](../../../rtcdp/b2b-tutorial.md) pour plus d’informations sur les workflows recommandés pour les données B2B.

![](../../images/field-groups/business-person-components.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Identifiant composite du compte associé à la personne. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Identifiant composite du contact associé si ce prospect a été converti. |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Identifiant composite du système source d’où proviennent les données de la personne. |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Identifiant composite de la personne. |
| `workEmail` | [[!UICONTROL Email address]](../../data-types/b2b-source.md) | ID d’e-mail professionnel de la personne. |
| `personGroupID` | Chaîne | Identifiant de groupe de la personne. |
| `personScore` | Chaîne | Score généré pour la personne par un système CRM. |
| `personSource` | Chaîne | Identifiant unique basé sur une chaîne pour le système source d’où proviennent les données de la personne. |
| `personStatus` | Chaîne | Statut actuel de vente ou de marketing de la personne. |
| `personType` | Chaîne | Type de personne dans un contexte B2B. |
| `sourceAccountID` | Chaîne | Identifiant unique basé sur une chaîne pour le compte dans le système source associé à la personne. Ce champ est utilisé comme clé étrangère par le système pour rechercher les différentes sociétés pour lesquelles cette personne travaille. |
| `sourceConvertedContactID` | Chaîne | Identifiant unique basé sur une chaîne pour le contact associé si ce prospect a été converti. |
| `sourceExternalID` | Chaîne | Identifiant unique basé sur une chaîne pour le système source d’où proviennent les données de la personne. |
| `sourcePersonID` | Chaîne | Identifiant unique basé sur une chaîne pour la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
