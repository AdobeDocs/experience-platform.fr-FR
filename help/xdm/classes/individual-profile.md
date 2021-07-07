---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;profil individuel;champs;schémas;schéma;identityMap;identityMap;carte d’identité;carte d’identité;conception de schéma;carte;carte;schéma d’union;union
solution: Experience Platform
title: Classe XDM Individual Profile
topic-legacy: overview
description: Ce document présente la classe XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 79fcc44ec5e08f63bfd5eed6e90d7538273f4dab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] est une classe XDM (Experience Data Model) standard qui forme une représentation unique (ou &quot;profil&quot;) d’une personne. Plus précisément, la classe (et ses groupes de champs compatibles) capture les attributs et les intérêts des individus identifiés et partiellement identifiés qui interagissent avec votre marque.

Les profils peuvent aller des signaux comportementaux anonymes (tels que les cookies de navigateur) aux profils hautement identifiés contenant des informations détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse électronique. À mesure qu’un profil se développe, il devient un solide référentiel d’informations personnelles, d’identités, de coordonnées et de préférences de communication pour un individu. Pour plus d’informations de haut niveau sur l’utilisation de cette classe dans l’écosystème Platform, reportez-vous à la [présentation XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fournit elle-même plusieurs valeurs générées par le système qui sont automatiquement renseignées lorsque les données sont ingérées, alors que tous les autres champs doivent être ajoutés à l’aide des [groupes de champs de schéma compatibles](#field-groups) :

![](../images/classes/individual-profile.png)

| Propriété | Description |
| --- | --- |
| `_repo` | An object containing the following [!UICONTROL DateTime] fields: <ul><li>`createDate`: Date et heure de création de la ressource dans l’entrepôt de données, par exemple, date de la première ingestion des données.</li><li>`modifyDate`: Date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identifiant de chaîne unique pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval. Dans certains cas, `_id` peut être un [identifiant unique universel (UUID)](https://tools.ietf.org/html/rfc4122) ou [identifiant unique global (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données depuis une connexion source ou que vous ingérez directement à partir d’un fichier Parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rend l’enregistrement unique, comme un identifiant Principal, un horodatage, un type d’enregistrement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. Par la suite, la valeur concaténée doit être hachée à l’aide de SHA-256 ou d’un autre algorithme de votre choix.<br><br>Il est important de distinguer que  **ce champ ne représente pas une identité liée à une personne** individuelle, mais plutôt l’enregistrement des données lui-même. Les données d’identité relatives à une personne doivent être reléguées aux [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles à la place. |
| `createdByBatchID` | The ID of the ingested batch that caused the record to be created. |
| `modifiedByBatchID` | L’identifiant du dernier lot ingéré à l’origine de la mise à jour de l’enregistrement. |
| `personID` | Identifiant unique de la personne à laquelle cet enregistrement se rapporte. Ce champ ne représente pas nécessairement une identité liée à la personne, sauf s’il est également désigné comme [champ d’identité](../schema/composition.md#identity). |
| `repositoryCreatedBy` | L’identifiant de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | L’identifiant de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |

{style=&quot;table-layout:auto&quot;}

## Groupes de champs compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../field-groups/name-updates.md) .

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM Individual Profile]. Voici une liste de certains groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL Détails démographiques]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Détails de fidélité]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Détails du contact personnel]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Préférences marketing/confidentialité (consentement)]](../field-groups/profile/consents.md)
* [[!UICONTROL Détails de l’adhésion au segment]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Détails du contact professionnel]](../field-groups/profile/work-contact-details.md)

Pour obtenir la liste complète de tous les groupes de champs compatibles pour [!DNL XDM Individual Profile], consultez le [référentiel XDM GitHub](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
