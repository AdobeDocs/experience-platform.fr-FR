---
title: Modèle de données du secteur des soins de santé ERD
description: Affichez un diagramme de relation d’entité (ERD) qui décrit un modèle de données normalisé pour le secteur de la santé. Ce modèle de données est compatible avec le modèle de données d’expérience (XDM) à utiliser dans Adobe Experience Platform.
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 8%

---

# [!UICONTROL Santé] modèle de données du secteur ERD

Le diagramme de relation d’entité suivant (ERD) représente un modèle de données normalisé pour le secteur de la santé. L’ERD est délibérément présenté de manière dénormalisée et en tenant compte de la manière dont les données sont stockées dans Adobe Experience Platform.

>[!NOTE]
>
>L’ERD tel que décrit est une recommandation sur la manière dont vous devez modéliser vos données pour ce cas d’utilisation du secteur. Pour utiliser ce modèle de données dans Experience Platform, vous devez créer vous-même les schémas recommandés et leurs relations. Consultez les guides sur la gestion des [schémas](../../ui/resources/schemas.md) et [relations](../../tutorials/relationship-ui.md) dans l’interface utilisateur pour plus d’informations.

Utilisez la légende suivante pour interpréter cet ERD :

* Chaque entité affichée dans est basée sur une classe [Modèle de données d’expérience (XDM)](../composition.md#class) sous-jacente.
* Les champs mis en retrait sous un champ parent représentent un champ enfant, ou sous-champ, appartenant au groupe de champs du parent.
* Les champs les plus importants pour une entité donnée sont surlignés en rouge.
* Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme « identité », l’une de ces propriétés étant marquée comme « identité principale ».
* Les relations d’entité sont marquées comme non dépendantes, car les événements basés sur des cookies ne peuvent souvent pas déterminer la personne ou l’individu qui a effectué la transaction.

![Exemple de modèle de données ERD pour le secteur de la santé](../../images/industries/healthcare.png)

>[!NOTE]
>
>Chaque entité comprend un champ « _ID », qui représente l’attribut d’identifiant de chaîne unique (`_id`) pour l’enregistrement ou l’événement en question. Ce champ permet de déterminer l’unicité de l’enregistrement ou de l’événement individuel, d’éviter la duplication des données et de rechercher ces données dans les services en aval. Dans certains cas, `_id` peut être un [Identifiant universel unique (UUID)](https://tools.ietf.org/html/rfc4122) ou un [Identifiant global unique (GUID)](https://docs.microsoft.com/fr-fr/dotnet/api/system.guid?view=net-5.0).<br><br>Il est important de distinguer que **ce champ ne représente pas une identité liée à une personne individuelle**, mais plutôt lʼenregistrement de données lui-même. Les données d’identité relatives à une personne, un événement ou une entité commerciale doivent plutôt être reléguées dans des [champs d’identité](../composition.md#identity) fournis par des groupes de champs compatibles.

## Cas d’utilisation de [!UICONTROL Healthcare]

Le tableau suivant décrit les classes et les groupes de champs de schéma recommandés pour plusieurs cas d’utilisation courants des services de santé.

| Cas d’utilisation | Classes et groupes de champs recommandés |
| --- | --- |
| Améliorez l’acquisition numérique et l’expérience des consommateurs qui achètent une assurance. Par exemple : <ul><li>Lorsque les personnes accèdent à une page contenant des informations générales (telles que les plans, les noms/niveaux de plan, medicaid, les programmes de bien-être, etc.), elles comprennent leur comportement et ce qu’elles recherchent afin d’envoyer des e-mails promotionnels ou de les cibler sur des plateformes tierces avec des annonces.</li><li>Lorsque les gens recherchent des renseignements sur la santé cardiaque et les vaccins, envoyez-leur des renseignements sur la santé cardiaque liés aux vaccins pour les sensibiliser à la marque ou demandez-leur de planifier la vaccination.</li></ul> | <ul><li>**[[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Informations sur le membre du secteur de la santé]](../../field-groups/profile/healthcare-member-details.md)</li><li>Champ(s) de relation établi(s) entre `planID` attributs et les schémas utilisant la classe [!UICONTROL Plan].</li></ul></li><li>**[[!UICONTROL Débiteur]](../../classes/payer.md)**</li><li>**[[!UICONTROL Planifier]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Informations relatives au plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Application]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Informations sur l’outil de site]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL &#x200B; les détails marketing de la campagne]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| Augmenter l&#39;acquisition numérique de patients par des publicités ciblées basées sur les données passées en ligne sur le comportement et la santé. | <ul><li>**[[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Informations sur le membre du secteur de la santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Fournisseur]](../../classes/provider.md)** :<ul><li>[[!UICONTROL Prestataire de soins de santé]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Améliorez les inscriptions et la création de comptes dans les plans de santé en suivant le marketing de l’assurance par différents canaux, afin de comprendre comment un client a découvert une compagnie d’assurance. | <ul><li>**[[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Informations sur le membre du secteur de la santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Débiteur]](../../classes/payer.md)**</li><li>**[[!UICONTROL Planifier]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Informations relatives au plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| Évitez les lacunes dans la couverture d’assurance médicale. | <ul><li>**[[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Informations sur le membre du secteur de la santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Planifier]](../../classes/plan.md)** :<ul><li>[[!UICONTROL Informations relatives au plan de soins de santé]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| Promouvoir l&#39;information sur les médicaments auprès des fournisseurs en utilisant des publicités directes au client (DTC). | <ul><li>**[[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md)** :<ul><li>[[!UICONTROL Informations sur le membre du secteur de la santé]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL Médicaments]](../../classes/medication.md)** :<ul><li>[[!UICONTROL Médicaments]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)** :<ul><li>[[!UICONTROL Détails Web]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL Détails Advertising]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |

