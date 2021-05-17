---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; Schéma design ; map ; Map ; union schéma ; union
solution: Experience Platform
title: Classe de Profil XDM
topic-legacy: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] est une classe standard de modèle de données d’expérience (XDM) qui forme une représentation unique (ou &quot;profil&quot;) d’une personne. Plus précisément, la classe (et ses mixins compatibles) capture les attributs et les intérêts des individus identifiés et partiellement identifiés qui interagissent avec votre marque.

Les profils peuvent aller des signaux comportementaux anonymes (tels que les cookies de navigateur) aux profils hautement identifiés contenant des informations détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse électronique. À mesure qu&#39;un profil se développe, il devient un solide référentiel de renseignements personnels, d&#39;identités, de coordonnées et de préférences de communication pour une personne. Pour plus d&#39;informations de haut niveau sur l&#39;utilisation de cette classe dans l&#39;écosystème de la plate-forme, consultez la [présentation de XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fournit elle-même plusieurs valeurs générées par le système qui sont automatiquement renseignées lorsque des données sont ingérées, alors que tous les autres champs doivent être ajoutés à l&#39;aide de groupes de champs de schéma [compatibles](#field-groups) :

![](../images/classes/individual-profile.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Objet contenant les champs [!UICONTROL DateTime] suivants : <ul><li>`createDate`: Date et heure de création de la ressource dans le magasin de données, par exemple, date à laquelle les données ont été ingérées pour la première fois.</li><li>`modifyDate`: Date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identificateur unique de l&#39;enregistrement. Ce champ permet de suivre l&#39;unicité d&#39;un enregistrement individuel, d&#39;éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Il est important de distinguer que ce champ  **ne** représente pas une identité liée à une personne, mais plutôt l&#39;enregistrement des données. Les données d&#39;identité relatives à une personne doivent être reléguées à [champs d&#39;identité](../schema/composition.md#identity). |
| `createdByBatchID` | ID du lot assimilé à l&#39;origine de la création de l&#39;enregistrement. |
| `modifiedByBatchID` | ID du dernier lot assimilé qui a provoqué la mise à jour de l&#39;enregistrement. |
| `personID` | Identificateur unique de la personne à laquelle ce dossier se rapporte. Ce champ ne représente pas nécessairement une identité liée à la personne, sauf s&#39;il est également désigné comme [champ d&#39;identité](../schema/composition.md#identity). |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |

## Groupes de champs compatibles {#field-groups}

>[!NOTE]
>
>Les noms de plusieurs groupes de champs ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../field-groups/name-updates.md).

Adobe fournit plusieurs groupes de champs standard à utiliser avec la classe [!DNL XDM Individual Profile]. Voici une liste de certains groupes de champs couramment utilisés pour la classe :

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Détails démographiques]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Coordonnées personnelles]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Détails du contact de travail]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Détails de l’abonnement au segment]](../field-groups/profile/segmentation.md)

Pour obtenir la liste complète de tous les groupes de champs compatibles pour [!DNL XDM Individual Profile], consultez le [repo GitHub XDM](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
