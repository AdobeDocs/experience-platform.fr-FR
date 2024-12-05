---
title: ERD du modèle de données du secteur des soins de santé
description: Affichez un diagramme des relations d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur de la santé. Ce modèle de données est compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 8f026501cf5c8087cc512ac374163908cebd17c6
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 8%

---

# [!UICONTROL Healthcare] modèle de données du secteur ERD

Le diagramme de relation des entités suivant (ERD) représente un modèle de données normalisé pour le secteur de la santé. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’identifiant d’utilisateur (ERD) tel que décrit est une recommandation pour la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Platform, vous devez construire vous-même les schémas recommandés et leurs relations. Pour plus d’informations, consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et des [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une [classe de modèle de données d’expérience (XDM)](../composition.md#class) sous-jacente.
* Les champs mis en retrait sous un champ parent représentent un champ enfant, ou sous-champ, qui appartient au groupe de champs du parent.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;identité principale&quot;.
* Les relations d’entité sont marquées comme étant non dépendantes, puisque les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![Exemple d’ERD pour un modèle de données du secteur de la santé](../../images/industries/healthcare.png)

>[!NOTE]
>
>Chaque entité comprend un champ &quot;_ID&quot;, qui représente l’attribut de chaîne unique (`_id`) pour l’enregistrement ou l’événement en question. Ce champ permet de suivre l’unicité de l’enregistrement ou de l’événement individuel, d’éviter la duplication des données et de rechercher ces données dans les services en aval. Dans certains cas, `_id` peut être un [Identifiant universel unique (UUID)](https://tools.ietf.org/html/rfc4122) ou un [Identifiant global unique (GUID)](https://docs.microsoft.com/fr-fr/dotnet/api/system.guid?view=net-5.0).<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne, un événement ou une entité commerciale doivent être reléguées aux [champs d’identité](../composition.md#identity) fournis à la place par des groupes de champs compatibles.

## Cas d’utilisation de [!UICONTROL Healthcare]

Le tableau suivant décrit les classes recommandées et les groupes de champs de schéma pour plusieurs cas d’utilisation de la santé courants.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Améliorez l’acquisition et l’expérience digitales des consommateurs qui achètent des assurances. Par exemple : <ul><li>Lorsque les visiteurs accèdent à une page contenant des informations générales (plans, noms et niveaux des plans, aide médicale, programmes de bien-être, etc.), ils comprennent leur comportement et ce qu’ils recherchent pour envoyer des emails promotionnels ou les cibler sur des plateformes tierces avec des publicités.</li><li>Lorsque les gens recherchent des informations sur la santé cardiaque et le vaccin, envoyez-leur des informations sur la santé cardiaque pour créer une prise de conscience de la marque ou demandez-leur de planifier des vaccins.</li></ul> | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails des membres du service de santé]](../../field-groups/profile/healthcare-member-details.md)</li><li>Champ(s) de relation établi(s) entre les attributs `planID` et les schémas qui utilisent la classe [!UICONTROL Plan].</li></ul></li><li>**[[!UICONTROL Payeur]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Détails du plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Application]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Détails Du Site]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  Détails du marketing de campagne ]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Accroître l’acquisition numérique de patients par le biais d’annonces ciblées basées sur les comportements en ligne et les données de santé passés. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails des membres du service de santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Provider]](../../classes/provider.md)** :<ul><li>[[!UICONTROL Prestataire De Soins De Santé]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Améliorer l’inscription et la création de comptes dans les plans de santé en suivant le marketing des assurances par différents canaux, afin de comprendre comment un client a découvert une société d’assurance. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails des membres du service de santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Payeur]](../../classes/payer.md)**</li><li>**[[!UICONTROL Plan]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Détails du plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Évitez les défaillances dans la couverture médicale. | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails des membres du service de santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Plan]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Détails du plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promouvoir les informations sur les médicaments auprès des fournisseurs à l’aide de publicités DTC (direct-to-customer). | <ul><li>**[[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Détails des membres du service de santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Medication]](../../classes/medication.md)** :<ul><li>[[!UICONTROL Médicaments de santé]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
