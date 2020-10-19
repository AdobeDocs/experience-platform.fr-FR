---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Classe de Profils individuels XDM
topic: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] est une classe XDM standard qui forme une représentation unique (ou &quot;profil&quot;) des attributs et des intérêts des individus identifiés et partiellement identifiés.

Les profils peuvent aller des signaux comportementaux anonymes (tels que les cookies de navigateur) aux profils hautement identifiés contenant des informations détaillées telles que le nom, la date de naissance, l’emplacement et l’adresse électronique. À mesure qu&#39;un profil se développe, il devient un solide référentiel de renseignements personnels, d&#39;identités, de coordonnées et de préférences de communication pour une personne. Pour plus d&#39;informations de haut niveau sur l&#39;utilisation de cette classe dans l&#39;écosystème de la plate-forme, consultez la présentation [de](../home.md#data-behaviors)XDM.

La [!DNL XDM Individual Profile] classe elle-même fournit plusieurs valeurs générées par le système qui sont automatiquement renseignées lors de l’assimilation des données, tandis que tous les autres champs doivent être ajoutés à l’aide de mixins [](#mixins)compatibles :

![](../images/classes/individual-profile.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Objet contenant les champs [!UICONTROL DateTime] suivants : <ul><li>`createDate`: Date et heure de création de la ressource dans le magasin de données, par exemple, date à laquelle les données ont été ingérées pour la première fois.</li><li>`modifyDate`: Date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identificateur de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l&#39;unicité d&#39;un enregistrement individuel, d&#39;éviter la duplication des données et de rechercher cet enregistrement dans les services en aval. Ce champ étant généré par le système, il ne doit pas être fourni de valeur explicite lors de l’assimilation des données.<br><br>Il est important de distinguer que ce champ ne **représente pas** une identité liée à une personne, mais plutôt l&#39;enregistrement des données proprement dites. Les données d&#39;identité relatives à une personne doivent être reléguées aux champs [d&#39;](../schema/composition.md#identity) identité. |
| `createdByBatchID` | ID du lot assimilé à l&#39;origine de la création de l&#39;enregistrement. |
| `modifiedByBatchID` | ID du dernier lot assimilé qui a provoqué la mise à jour de l&#39;enregistrement. |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |

## mixins compatibles {#mixins}

Adobe fournit plusieurs mixins standard à utiliser avec la [!DNL XDM Individual Profile] classe. Voici une liste des mixins les plus couramment utilisés pour la classe :

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Détails de la personne profil]](../mixins/profile/person-details.md)
* [[!UICONTROL Détails personnels du profil]](../mixins/profile/personal-details.md)
* [[!UICONTROL Détails du travail profil]](../mixins/profile/work-details.md)
* [[!UICONTROL Segmentation des profils]](../mixins/profile/segmentation.md)