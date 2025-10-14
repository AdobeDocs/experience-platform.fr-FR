---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;identityMap;mappage d’identités;Mappage d’identités;conception de schéma;mappage;Mappage;schéma d’union;union
solution: Experience Platform
title: Classe XDM Individual Profile
description: En savoir plus sur la classe XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 29%

---

# Classe [!DNL XDM Individual Profile]

[!DNL XDM Individual Profile] est une classe XDM (modèle de données d’expérience) standard qui forme une représentation (ou « profil ») unique d’une personne individuelle. Plus précisément, la classe (et ses groupes de champs compatibles) capture les attributs et les centres d’intérêt des personnes identifiées partiellement et identifiées qui interagissent avec votre marque.

Les profils peuvent aller de signaux comportementaux anonymes (tels que des cookies de navigateur) à des profils hautement identifiés contenant des informations détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse e-mail. À mesure qu’un profil se développe, il devient un solide référentiel d’informations personnelles, d’identités, de coordonnées et de préférences de communication pour une personne. Pour plus d’informations détaillées sur l’utilisation de cette classe dans l’écosystème Experience Platform, reportez-vous à la [&#x200B; présentation de XDM](../home.md#data-behaviors).

![Schéma de la classe XDM Individual Profile.](../images/classes/individual-profile.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Objet contenant les champs [!UICONTROL DateTime] suivants : <ul><li>`createDate` : date et heure de création de la ressource dans l’entrepôt de données, par exemple la date de la première ingestion des données.</li><li>`modifyDate` : date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identifiant de chaîne unique pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval. Dans certains cas, `_id` peut être un [Identifiant universel unique (UUID)](https://tools.ietf.org/html/rfc4122) ou un [Identifiant global unique (GUID)](https://docs.microsoft.com/fr-fr/dotnet/api/system.guid?view=net-5.0).<br><br>Si vous diffusez des données à partir d’une connexion source ou si vous ingérez directement à partir d’un fichier Parquet, vous devez générer cette valeur en concaténant une certaine combinaison de champs qui rendent l’enregistrement unique, comme un identifiant principal, une date et heure, un type d’enregistrement, etc. La valeur concaténée doit être une chaîne formatée `uri-reference`, ce qui signifie que tout caractère deux-points doit être supprimé. La valeur concaténée doit ensuite être hachée à l’aide de lʼalgorithme SHA-256 ou d’un autre de votre choix.<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne doivent plutôt être reléguées dans des [champs d’identité](../schema/composition.md#identity) fournis par des groupes de champs compatibles. |
| `createdByBatchID` | L’identifiant du lot ingéré qui a provoqué la création de l’enregistrement. |
| `modifiedByBatchID` | L’identifiant du dernier lot ingéré qui a provoqué la mise à jour de l’enregistrement. |
| `personID` | Identifiant unique de la personne à laquelle cet enregistrement se rapporte. Ce champ ne représente pas nécessairement une identité liée à la personne, sauf s’il est également désigné comme [&#x200B; champ d’identité](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID du dernier utilisateur ayant modifié l’enregistrement. |

{style="table-layout:auto"}

## Groupes de champs compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../field-groups/name-updates.md).

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM Individual Profile]. Voici une liste de groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL &#x200B; Consentements et préférences &#x200B;]](../field-groups/profile/consents.md)
* [[!UICONTROL Détails démographiques]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL &#x200B; IdentityMap &#x200B;]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Détails de fidélité]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Coordonnées personnelles]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Détails de l’appartenance à un segment]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Abonnement télécom]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Détails du contact professionnel]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Composants professionnels XDM]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL Détails professionnels XDM]](../field-groups/profile/business-person-details.md)\*

*\*Ce groupe de champs n’est disponible que pour les organisations ayant accès au B2B edition d’Adobe Real-Time Customer Data Platform.*

Pour obtenir la liste complète de tous les groupes de champs compatibles pour [!DNL XDM Individual Profile], reportez-vous au [référentiel GitHub XDM](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
