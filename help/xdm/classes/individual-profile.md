---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; Schéma design ; map ; Map ; union schéma ; union
solution: Experience Platform
title: Classe de Profil XDM
topic-legacy: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] est une classe XDM standard qui forme une représentation unique (ou &quot;profil&quot;) des attributs et des intérêts des individus identifiés et partiellement identifiés.

Les profils peuvent aller des signaux comportementaux anonymes (tels que les cookies de navigateur) aux profils hautement identifiés contenant des informations détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse électronique. À mesure qu&#39;un profil se développe, il devient un solide référentiel de renseignements personnels, d&#39;identités, de coordonnées et de préférences de communication pour une personne. Pour plus d&#39;informations de haut niveau sur l&#39;utilisation de cette classe dans l&#39;écosystème de la plate-forme, consultez la [présentation de XDM](../home.md#data-behaviors).

La classe [!DNL XDM Individual Profile] fournit elle-même plusieurs valeurs générées par le système qui sont automatiquement renseignées lorsque des données sont ingérées, alors que tous les autres champs doivent être ajoutés à l&#39;aide de mixins [compatibles](#mixins) :

![](../images/classes/individual-profile.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Objet contenant les champs [!UICONTROL DateTime] suivants : <ul><li>`createDate`: Date et heure de création de la ressource dans le magasin de données, par exemple, date à laquelle les données ont été ingérées pour la première fois.</li><li>`modifyDate`: Date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identificateur de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l&#39;unicité d&#39;un enregistrement individuel, d&#39;éviter la duplication des données et de rechercher cet enregistrement dans les services en aval. Ce champ étant généré par le système, il ne doit pas être fourni de valeur explicite lors de l’assimilation des données.<br><br>Il est important de distinguer que ce champ  **ne** représente pas une identité liée à une personne, mais plutôt l&#39;enregistrement des données. Les données d&#39;identité relatives à une personne doivent être reléguées à [champs d&#39;identité](../schema/composition.md#identity). |
| `createdByBatchID` | ID du lot assimilé à l&#39;origine de la création de l&#39;enregistrement. |
| `modifiedByBatchID` | ID du dernier lot assimilé qui a provoqué la mise à jour de l&#39;enregistrement. |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |

## mixins compatibles {#mixins}

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../mixins/name-updates.md).

Adobe fournit plusieurs mixins standard à utiliser avec la classe [!DNL XDM Individual Profile]. Voici une liste des mixins les plus couramment utilisés pour la classe :

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Détails démographiques]](../mixins/profile/person-details.md)
* [[!UICONTROL Coordonnées personnelles]](../mixins/profile/personal-details.md)
* [[!UICONTROL Détails du contact de travail]](../mixins/profile/work-details.md)
* [[!UICONTROL Détails de l’abonnement au segment]](../mixins/profile/segmentation.md)
