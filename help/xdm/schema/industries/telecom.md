---
solution: Experience Platform
title: Modèle de données du secteur des télécommunications ERD
description: Affichez un diagramme des relations d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur des télécommunications, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 11%

---

# [!UICONTROL Télécommunications] ERD du modèle de données du secteur

Le diagramme de relation des entités suivant (ERD) représente un modèle de données normalisé pour le secteur des télécommunications. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Consultez les guides de gestion [schémas](../../ui/resources/schemas.md) et [relations](../../tutorials/relationship-ui.md) pour plus d’informations.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans repose sur un sous-jacent [Classe de modèle de données d’expérience (XDM)](../composition.md#class).
* Pour une entité donnée, chaque ligne marquée dans **gras** représente un groupe de champs ou un type de données, avec les champs pertinents qu’il fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité Principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>L’entité Événement d’expérience comprend un champ &quot;_ID&quot;, qui représente l’identifiant unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

## [!UICONTROL Télécommunications] cas d’utilisation

Le tableau suivant décrit les classes et les groupes de champs de schéma recommandés pour plusieurs cas d’utilisation courants pour le secteur des télécommunications.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Comprendre les clients qui sont de bons candidats pour les opportunités de vente incitative ou croisée en fonction de leurs avoirs actuels et de leur comportement de navigation. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Informations sur les prestations supplémentaires]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Informations sur la mise à niveau]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abonnement aux télécommunications]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Reciblez les abandons de panier par le biais de publicités pertinentes et d’emails personnalisés automatisés. Supprimer les publicités lors de leur conversion. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Détails du commerce]](../../field-groups/event/upsell-details.md) (Pour capturer les abandons de panier)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abonnement aux télécommunications]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Lorsqu’un client est marqué comme susceptible de se produire (sur la base d’une interaction de l’employé ou d’un algorithme d’apprentissage automatique automatisé), envoyez les détails du client aux canaux numériques et non numériques. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Détails de la campagne marketing]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Informations sur le canal]](../../field-groups/event/channel-details.md)</li><li>Un groupe de champs personnalisé contenant du contenu personnalisé</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
