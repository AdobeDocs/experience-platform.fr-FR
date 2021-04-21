---
keywords: 'Experience Platform ; accueil ; sujets populaires ; GDPR ; gdpr ; ccpa : CCPA ; pdpa ; PDPA ; pdpa_that ; PDPA_THA ; lgpd ; LGPD ; lgpd_bra ; LGPD_BRA ;'
solution: Experience Platform
title: Présentation du Privacy Service
topic-legacy: overview
description: Privacy Service vous permet de faciliter la conformité automatisée aux règles de confidentialité légales dans vos opérations de données Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 10%

---

# [!DNL Privacy Service] présentation

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lorsque vous utilisez ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande.

Adobe Experience Platform [!DNL Privacy Service] a été développé en réponse à un changement fondamental dans la façon dont les entreprises sont tenues de gérer les données personnelles de leurs clients. [!DNL Privacy Service] a pour principal objectif d&#39;automatiser le respect des règles de confidentialité des données, ce qui, en cas de violation, peut entraîner des amendes importantes et perturber les opérations de données pour votre entreprise.

[!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer les requêtes de données client. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d&#39;accès et de suppression de données personnelles sur les clients des applications Adobe Experience Cloud, ce qui facilite la conformité automatisée aux réglementations légales et de confidentialité de l&#39;entreprise.

## Prise en main de [!DNL Privacy Service] {#getting-started}

Afin d&#39;utiliser [!DNL Privacy Service], plusieurs décisions clés doivent être prises en fonction des exigences de confidentialité de votre entreprise, des types de données d&#39;identité que vous collectez auprès de vos clients et du meilleur moyen d&#39;interagir avec votre système de gestion de la relation client avec le service.

Ces décisions peuvent être résumées par les questions suivantes :

1. **Quelles sont les informations que je recueille auprès de mes clients ?**
   * Pour tirer le meilleur parti de [!DNL Privacy Service], vous devez avoir une compréhension détaillée des types de données que vous collectez auprès de vos clients et de ceux qui sont assujettis aux règles de confidentialité. Pour plus d&#39;informations, consultez la section [déterminer les exigences de confidentialité](#requirements).
1. **Ai-je correctement étiqueté mes données ?**
   * Les données doivent être correctement étiquetées pour que le service puisse déterminer les champs à accéder ou à supprimer pendant les tâches de confidentialité. Consultez la section [données d&#39;étiquetage](#label) pour plus d&#39;informations.
1. **Est-ce que je sais à quels identifiants envoyer  [!DNL Privacy Service]?**
   * Lors de l’envoi de demandes de confidentialité, des ID de client individuels spécifiques à des applications d’Adobe particulières doivent être fournis. Pour plus d&#39;informations, consultez les sections [Fourniture de données d&#39;identité](#identity) et [Demande de confidentialité](#requests).
1. **Comment effectuer le suivi de mes tâches de confidentialité ?**
   * Une fois que vous avez effectué des demandes de confidentialité, il existe plusieurs options pour suivre leur état et leurs résultats. Pour plus d&#39;informations, consultez la section [surveillance des tâches de confidentialité](#monitor).

Les sections ci-après fournissent des orientations générales sur ces étapes préalables importantes et fournissent également des liens vers d&#39;autres [!DNL Privacy Service] documents pour plus de détails.

### Déterminer les exigences de confidentialité de votre entreprise {#requirements}

En fonction de la nature de votre entreprise et des juridictions sous lesquelles elle opère, vos opérations de données peuvent être assujetties à des règlements juridiques sur la protection des renseignements personnels. Ces réglementations donnent souvent à vos clients le droit de demander l&#39;accès aux données que vous leur collectez et le droit de demander la suppression de ces données stockées. Ces demandes de données personnelles de la part des clients sont appelées &quot;demandes de confidentialité&quot; dans toute la documentation.

Pour plus d&#39;informations sur les différentes réglementations légales en matière de confidentialité que [!DNL Privacy Service] gère les demandes, y compris les termes clés et les réponses aux questions les plus fréquentes, consultez la [documentation sur les réglementations en matière de confidentialité](./regulations/overview.md).

Si vos opérations de données relèvent de l’une des réglementations prises en charge, consultez leur documentation pour obtenir des informations importantes, telles que les droits de confidentialité spécifiques qu’ils accordent à vos clients, et des fenêtres de conformité pour répondre aux demandes de confidentialité. Ces informations doivent être prises en compte pour déterminer comment intégrer [!DNL Privacy Service] dans votre système de gestion de la relation client et comment les clients doivent interagir avec votre site Web afin de faire des demandes de confidentialité.

En plus des règlements juridiques, toute norme organisationnelle ou industrielle applicable à votre organisation doit également être prise en compte lors de la prise de ces décisions.

### Étiqueter les données des demandes de confidentialité {#label}

En fonction des applications [!DNL Experience Cloud] que vous utilisez, vous devez étiqueter les champs de données spécifiques qui doivent être accessibles ou supprimés en réponse aux demandes de confidentialité. Le processus d&#39;étiquetage des données varie d&#39;une demande à l&#39;autre. Pour savoir comment étiqueter les données pour chaque application d&#39;Adobe prise en charge, consultez le document sur [les applications Experience Cloud](./experience-cloud-apps.md).

### Déterminer les types de données d&#39;identité à envoyer à [!DNL Privacy Service] {#identity}

Pour que [!DNL Privacy Service] puisse traiter une demande de confidentialité d&#39;un client, au moins une valeur d&#39;identité unique pour ce client doit être fournie dans la demande elle-même. Une valeur d&#39;identité unique est tout élément d&#39;information qui peut être utilisé pour identifier une personne et ses données personnelles stockées dans vos entrepôts de données [!DNL Experience Cloud]. [!DNL Privacy Service] utilise ces informations d&#39;identité pour localiser et traiter les données personnelles du client en fonction de la nature de la demande (accès, suppression ou exclusion).

Selon les applications [!DNL Experience Cloud] utilisées par votre système de gestion de la relation client, le type et le nombre de valeurs d&#39;identité que vous devez fournir pour chaque client varieront. Certaines applications utilisent leurs propres valeurs d&#39;ID client internes (tels que les ID Adobe Target), tandis que d&#39;autres solutions reposent sur des identifiants globaux de l&#39;Adobe [!DNL Experience Cloud Identity Service] (ECID) qui effectuent le suivi de l&#39;activité client dans toutes les applications [!DNL Experience Cloud]. En outre, des informations personnelles génériques telles qu&#39;une adresse électronique ou un numéro de téléphone peuvent également servir de données d&#39;identité valides.

Le document sur [les données d&#39;identité pour les demandes de confidentialité](./identity-data.md) fournit des informations plus détaillées sur les types d&#39;informations d&#39;identité qui sont acceptées pour [!DNL Privacy Service]. Le document fournit également des conseils sur la manière d&#39;exploiter les technologies d&#39;Adobe pour récupérer efficacement les informations d&#39;identité appropriées de vos clients lorsqu&#39;ils interagissent avec votre site Web et envoyer ces données à [!DNL Privacy Service] dans les demandes d&#39;API.

### Début qui adresse des demandes de confidentialité {#requests}

Une fois que vous avez déterminé les besoins en matière de confidentialité de votre entreprise et que vous avez décidé quelles valeurs d&#39;identité envoyer à [!DNL Privacy Service], vous pouvez début demander la confidentialité. [!DNL Privacy Service] vous permet d’envoyer des requêtes de confidentialité via l’API ou l’interface utilisateur.

>[!IMPORTANT]
>
>Les sections ci-dessous contiennent des liens vers la documentation qui explique comment effectuer des demandes de confidentialité génériques dans l’API ou l’interface utilisateur. Cependant, selon les applications [!DNL Experience Cloud] que vous utilisez, les champs que vous devez envoyer dans la charge utile de la demande peuvent être différents des exemples illustrés dans ces guides.
>
>Au fur et à mesure que vous suivez les guides de l&#39;API ou de l&#39;interface utilisateur, consultez le document sur [les applications Privacy Service et Experience Cloud](./experience-cloud-apps.md) pour obtenir de plus amples informations sur la façon de formater les demandes de confidentialité pour vos applications [!DNL Experience Cloud] particulières.
>
>Il est également important de noter que les demandes de confidentialité sont traitées de manière asynchrone dans les applications Experience Cloud. Une fois qu’une demande est reçue par le Privacy Service, chaque demande peut prendre de quelques minutes à plusieurs semaines pour la terminer. Le temps nécessaire à l’exécution de chaque demande est spécifique à l’application que vous utilisez et la quantité de données à traiter.

#### Utilisation de l’API

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) fournit plusieurs points de terminaison pour la création et la gestion des tâches de confidentialité à l&#39;aide des appels d&#39;API RESTful, ce qui vous permet d&#39;approcher par programmation la conformité de la réglementation de la confidentialité pour vos applications [!DNL Experience Cloud]. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le [guide de développement de l’API Privacy Service](api/getting-started.md).

#### Utilisation de l’interface utilisateur

>[!NOTE]
>
>L&#39;interface utilisateur [!DNL Privacy Service] ne prend actuellement en charge que les demandes d&#39;accès et de suppression. Toutes les demandes d’exclusion doivent être effectuées par le biais de l’API à la place.

L&#39;interface utilisateur [!DNL Privacy Service] vous permet de créer et de surveiller des tâches de confidentialité à l&#39;aide d&#39;une interface graphique. L’interface utilisateur comprend un widget **[!UICONTROL Rapport d’état]** qui fournit une représentation visuelle de l’état de toutes les requêtes actives et vous permet de créer des requêtes à l’aide du **[!UICONTROL Créateur de requêtes]** intégré, ou en chargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/overview.md).

### Surveillance des tâches de confidentialité {#monitor}

Une fois que vous avez effectué des tâches de confidentialité, vous disposez de plusieurs options pour contrôler leur état et leurs résultats :

| Méthode de surveillance | Description |
| --- | --- |
| [!DNL Privacy Service] Interface utilisateur | L&#39;interface utilisateur [!DNL Privacy Service] fournit un tableau de bord de surveillance qui vous permet de vue une représentation visuelle de l&#39;état de toutes les demandes principales. Pour plus d’informations, consultez le [guide de l’utilisateur Privacy Service](ui/overview.md). |
| [!DNL Privacy Service] API | Vous pouvez contrôler par programmation l’état des tâches de confidentialité en utilisant les points de terminaison de recherche fournis par l’API [!DNL Privacy Service]. Consultez le [guide du développeur Privacy Service](./api/getting-started.md) pour obtenir des instructions détaillées sur l&#39;utilisation de l&#39;API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] tirer parti des Événements d’Adobe I/O envoyés à un webhook configuré afin de faciliter l’automatisation des demandes d’emploi. Elles réduisent ou éliminent la nécessité de consulter l&#39;API [!DNL Privacy Service] afin de vérifier si une tâche est terminée ou si un certain jalon dans un flux de travail a été atteint. Pour plus d&#39;informations, consultez le didacticiel sur [l&#39;abonnement aux Événements de confidentialité](./privacy-events.md). |

## Étapes suivantes

Ce document fournit un aperçu général de [!DNL Privacy Service] et des principales étapes à suivre pour début en utilisant les capacités du service. Pour obtenir des informations plus détaillées sur les divers aspects de l&#39;utilisation de [!DNL Privacy Service], veuillez consulter la documentation à laquelle vous avez accès tout au long de la présentation.
