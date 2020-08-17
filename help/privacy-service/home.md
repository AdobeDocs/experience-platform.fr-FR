---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 15%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lorsque vous utilisez ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande.

Adobe Experience Platform [!DNL Privacy Service] was developed in response to a fundamental shift in how businesses are required to manage the personal data of their customers. The central purpose of [!DNL Privacy Service] is to automate compliance with data privacy regulations which, when violated, can result in major fines and disrupt data operations for your business.

[!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer les requêtes de données client. With [!DNL Privacy Service], you can submit requests to access and delete personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

## Getting started with [!DNL Privacy Service] {#getting-started}

Afin de pouvoir utiliser [!DNL Privacy Service]ces données, plusieurs décisions clés doivent être prises en fonction des exigences de confidentialité de votre entreprise, des types de données d&#39;identité que vous collectez auprès de vos clients et de la meilleure façon d&#39;interagir avec votre système de gestion de la relation client avec le service.

Ces décisions peuvent être résumées par les questions suivantes :

1. **Quelles sont les informations que je recueille auprès de mes clients ?**
   * Pour tirer le meilleur parti de [!DNL Privacy Service]ces données, vous devez avoir une compréhension détaillée des types de données que vous collectez auprès de vos clients et de ceux qui sont assujettis à la réglementation en matière de confidentialité. Consultez la section sur la [détermination des exigences](#requirements) en matière de confidentialité pour en savoir plus.
1. **Ai-je correctement étiqueté mes données ?**
   * Les données doivent être correctement étiquetées pour que le service puisse déterminer les champs à accéder ou à supprimer pendant les tâches de confidentialité. See the section on [labelling data](#label) for more information.
1. **Est-ce que je sais à quels identifiants envoyer[!DNL Privacy Service]?**
   * Lors de l’envoi de demandes de confidentialité, des ID de client individuels spécifiques à des applications d’Adobe particulières doivent être fournis. Pour plus d&#39;informations, consultez les sections sur la [fourniture de données](#identity) d&#39;identité et sur l&#39; [exécution de demandes](#requests) de confidentialité.
1. **Comment effectuer le suivi de mes tâches de confidentialité ?**
   * Une fois que vous avez effectué des demandes de confidentialité, il existe plusieurs options pour suivre leur état et leurs résultats. Pour plus d’informations, voir la section sur la [surveillance des tâches](#monitor) de confidentialité.

Les sections ci-dessous fournissent des orientations générales sur ces étapes préalables importantes et fournissent également des liens vers d&#39;autres [!DNL Privacy Service] documents pour plus de détails.

### Déterminer les exigences de confidentialité de votre entreprise {#requirements}

En fonction de la nature de votre entreprise et des juridictions sous lesquelles elle opère, vos opérations de données peuvent être assujetties à des règlements juridiques sur la protection des renseignements personnels. Ces réglementations donnent souvent à vos clients le droit de demander l&#39;accès aux données que vous leur collectez et le droit de demander la suppression de ces données stockées. Ces demandes de données personnelles de la part des clients sont appelées &quot;demandes de confidentialité&quot; dans toute la documentation.

Le tableau ci-dessous décrit la réglementation relative à la protection des renseignements personnels qui [!DNL Privacy Service] gère les demandes de renseignements, y compris les liens vers la documentation pour plus d&#39;informations :

| Réglementation | Description |
| --- | --- |
| CCPA (Californie) | The [!DNL California Consumer Privacy Act] (CCPA) enhances privacy rights and consumer protection for residents of California, United States. Le CCPA accorde plusieurs nouveaux droits à la confidentialité des données aux résidents de Californie, y compris le droit d’accéder et de supprimer leurs données personnelles, de savoir si ces données personnelles sont vendues ou divulguées (et à qui) et le droit de refuser que ces données soient vendues à des tiers.<br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://oag.ca.gov/privacy/ccpa)</li><li>[FAQ relative au CCPA](ccpa/faq.md)</li></ul> |
| RGPD (Union européenne) | The [!DNL General Data Protection Regulation] (GDPR) introduced several new data privacy rights for members of the European Union, including the **Right to Access** and the **Right to be Forgotten**. Cela signifie que tout citoyen de l’UE dont les données personnelles ont été collectées par votre entreprise peut demander à tout moment d’accéder à ses données ou de les supprimer. <br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://gdpr-info.eu/)</li><li>[FAQ relative au RGPD](gdpr/faq.md)</li><li>[Terminologie relative au RGPD](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thaïlande) | La loi thaïlandaise sur la protection des données personnelles (PDPA) a été introduite pour protéger les propriétaires thaïlandais des données contre la collecte, l&#39;utilisation ou la divulgation illégales de leurs données personnelles. Inspirée par le RMR de l&#39;Union européenne, la réglementation accorde aux citoyens thaïlandais le droit de demander l&#39;accès à leurs données personnelles stockées ou de les supprimer.<br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[FAQ sur PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologie PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Si vos opérations de données relèvent de l’une des réglementations ci-dessus, consultez leur documentation pour obtenir des informations importantes, telles que les droits de confidentialité spécifiques qu’ils accordent à vos clients, et des fenêtres de conformité pour répondre aux demandes de confidentialité. Ces informations doivent être prises en compte pour déterminer comment intégrer [!DNL Privacy Service] votre système de gestion de la relation client et comment les clients doivent interagir avec votre site Web afin de faire des demandes de confidentialité.

En plus des règlements juridiques, toute norme organisationnelle ou industrielle applicable à votre organisation doit également être prise en compte lors de la prise de ces décisions.

### Label data for privacy requests {#label}

En fonction des [!DNL Experience Cloud] applications que vous utilisez, vous devez étiqueter les champs de données spécifiques qui doivent être accessibles ou supprimés en réponse aux demandes de confidentialité. Le processus d&#39;étiquetage des données varie d&#39;une demande à l&#39;autre. Pour savoir comment étiqueter les données pour chaque application d’Adobe prise en charge, reportez-vous au document sur les applications [](./experience-cloud-apps.md)Experience Cloud.

### Déterminer les types de données d&#39;identité à envoyer [!DNL Privacy Service] {#identity}

Pour [!DNL Privacy Service] traiter une demande de confidentialité d&#39;un client, au moins une valeur d&#39;identité unique doit être fournie dans la demande elle-même. Une valeur d&#39;identité unique est tout élément d&#39;information qui peut être utilisé pour identifier une personne et ses données personnelles stockées dans vos [!DNL Experience Cloud] entrepôts de données. [!DNL Privacy Service] utilise ces informations d&#39;identité pour localiser et traiter les données personnelles du client en fonction de la nature de la demande (accès, suppression ou exclusion).

Selon les [!DNL Experience Cloud] applications utilisées par votre système de gestion de la relation client, le type et le nombre de valeurs d’identité que vous devez fournir à chaque client varieront. Certaines applications utilisent leurs propres valeurs d’ID client internes (tels que les ID Adobe Target), tandis que d’autres solutions reposent sur des identifiants globaux d’Adobe [!DNL Experience Cloud Identity Service] (ECID) qui effectuent le suivi de l’activité des clients dans toutes les [!DNL Experience Cloud] applications. En outre, des informations personnelles génériques telles qu&#39;une adresse électronique ou un numéro de téléphone peuvent également servir de données d&#39;identité valides.

Le document sur les données d&#39; [identité pour les demandes](./identity-data.md) de confidentialité fournit des informations plus détaillées sur les types d&#39;informations d&#39;identité qui sont acceptées [!DNL Privacy Service]. Le document fournit également des conseils sur la manière d&#39;exploiter les technologies d&#39;Adobe pour récupérer efficacement les informations d&#39;identité appropriées de vos clients lorsqu&#39;ils interagissent avec votre site Web et envoyer ces données [!DNL Privacy Service] dans des demandes d&#39;API.

### Début qui demande la confidentialité {#requests}

Une fois que vous avez déterminé les besoins en matière de confidentialité de votre entreprise et que vous avez décidé quelles valeurs d&#39;identité [!DNL Privacy Service]vous souhaitez envoyer, vous pouvez début à faire des demandes de confidentialité. [!DNL Privacy Service] vous permet d’envoyer des requêtes de confidentialité via l’API ou l’interface utilisateur.

>[!IMPORTANT]
>
>Les sections ci-dessous contiennent des liens vers la documentation qui explique comment effectuer des demandes de confidentialité génériques dans l’API ou l’interface utilisateur. Cependant, selon les [!DNL Experience Cloud] applications utilisées, les champs que vous devez envoyer dans la charge utile de la demande peuvent être différents des exemples illustrés dans ces guides.
>
>Au fur et à mesure que vous suivez les guides de l’API ou de l’interface utilisateur, consultez le document sur les applications [](./experience-cloud-apps.md) Privacy Service et Experience Cloud pour obtenir de plus amples informations sur la façon de formater les demandes de confidentialité pour votre ou vos [!DNL Experience Cloud] applications particulières.

#### Utilisation de l’API

Le [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) fournit plusieurs points de terminaison pour la création et la gestion des tâches de confidentialité à l’aide des appels d’API RESTful, ce qui vous permet d’approcher par programmation la conformité à la réglementation de confidentialité pour vos [!DNL Experience Cloud] applications. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le [guide de développement de l’API Privacy Service](api/getting-started.md).

#### Utilisation de l’interface utilisateur

>[!NOTE]
>
>Actuellement, l’ [!DNL Privacy Service] interface utilisateur ne prend en charge que les demandes d’accès et de suppression. Toutes les demandes d’exclusion doivent être effectuées par le biais de l’API à la place.

The [!DNL Privacy Service] UI allows you to create and monitor privacy jobs using a graphical interface. L’interface utilisateur comprend un widget **[!UICONTROL Rapport d’état]** qui fournit une représentation visuelle de l’état de toutes les requêtes actives et vous permet de créer des requêtes à l’aide du **[!UICONTROL Créateur de requêtes]** intégré, ou en chargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/overview.md).

### Surveillance des tâches de confidentialité {#monitor}

Une fois que vous avez effectué des tâches de confidentialité, vous disposez de plusieurs options pour contrôler leur état et leurs résultats :

| Méthode de surveillance | Description |
| --- | --- |
| [!DNL Privacy Service] L’nterface utilisateur | L’ [!DNL Privacy Service] interface utilisateur fournit un tableau de bord de surveillance qui vous permet de vue une représentation visuelle de l’état de toutes les demandes principales. See the [Privacy Service user guide](ui/overview.md) for more information. |
| [!DNL Privacy Service] API | Vous pouvez contrôler par programmation l’état des tâches de confidentialité en utilisant les points de terminaison de recherche fournis par l’ [!DNL Privacy Service] API. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le guide [du développeur](./api/getting-started.md) Privacy Service. |
| [!DNL Privacy Events] | [!DNL Privacy Events] exploiter les Événements d&#39;E/S d&#39;Adobe envoyés à un webhook configuré afin de faciliter l&#39;automatisation efficace des demandes d&#39;emploi. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached. Pour plus d’informations, consultez le didacticiel sur l’ [abonnement aux Événements](./privacy-events.md) de confidentialité. |

## Étapes suivantes

Ce document fournit un aperçu général [!DNL Privacy Service] et les principales étapes nécessaires au début en utilisant les capacités du service. Pour plus d&#39;informations sur les différents aspects de la collaboration, veuillez consulter la documentation à laquelle vous avez accès tout au long de la présentation. [!DNL Privacy Service]
