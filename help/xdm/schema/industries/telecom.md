---
solution: Experience Platform
title: Modèle de données du secteur des télécommunications ERD
topic-legacy: overview
description: Affichez un diagramme des relations d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur des télécommunications, compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 421b4a448370f9903b8bc826fd9be9e5b2e11c59
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

#  ERD du modèle de données du secteur des télécommunications

Le diagramme de relation des entités suivant (ERD) représente un modèle de données normalisé pour le secteur des télécommunications. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Pour plus d’informations, consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et des [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une classe [Modèle de données d’expérience (XDM) ](../composition.md#class) sous-jacente.
* Pour une entité donnée, chaque ligne marquée dans **bold** représente un groupe de champs ou un type de données, avec les champs pertinents qu’elle fournit ci-dessous dans le texte non en gras.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité Principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.


![](../../images/industries/telecom.png)

>[!NOTE]
>
>L’entité Événement d’expérience comprend un champ &quot;_ID&quot;, qui représente l’attribut unique (`_id`) fourni par la classe XDM ExperienceEvent. Consultez le document de référence sur [XDM ExperienceEvent](../../classes/experienceevent.md) pour plus d’informations sur ce qui est attendu pour cette valeur.

##  Cas d&#39;utilisation des télécommunications

Le tableau suivant décrit les classes et les groupes de champs de schéma recommandés pour plusieurs cas d’utilisation courants pour le secteur des télécommunications.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Comprendre les clients qui sont de bons candidats pour les opportunités de vente incitative ou croisée en fonction de leurs avoirs actuels et de leur comportement de navigation. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Détails de la mise à niveau]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL Détails de la mise à niveau]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL Abonnement aux télécommunications]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Reciblez les abandons de panier par le biais de publicités pertinentes et d’emails personnalisés automatisés. Supprimer les publicités lors de leur conversion. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails du commerce]](../../field-groups/event/upsell-details.md)  (pour capturer les abandons de panier)</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Abonnement aux télécommunications]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| Lorsqu’un client est marqué comme susceptible de se produire (sur la base d’une interaction de l’employé ou d’un algorithme d’apprentissage automatique automatisé), envoyez les détails du client aux canaux numériques et non numériques. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails du marketing de campagne]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL Détails du canal]](../../field-groups/event/channel-details.md)</li><li>Un groupe de champs personnalisé contenant du contenu personnalisé</li></ul></li><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails démographiques]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL Détails du contact personnel]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
