---
keywords: Experience Platform;accueil;rubriques populaires;RGPD;rgpd;ccpa;CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Présentation de Privacy Service
description: Privacy Service vous permet de faciliter votre mise en conformité automatisée aux réglementations légales liées à la confidentialité dans vos opérations de données Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 3296209a15a5f88ab14e16de25d554b9df712445
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 100%

---

# Présentation de [!DNL Privacy Service]

>[!IMPORTANT]
>
>Les autorisations pour Adobe Experience Platform Privacy Service ont été améliorées afin d’augmenter leur niveau de granularité. Ces modifications permettent aux administrateurs et administratrices de l’organisation d’accorder l’accès à plus d’utilisateurs et d’utilisatrices avec le rôle et le niveau d’autorisation souhaités.Les utilisateurs et utilisatrices de comptes techniques doivent mettre à jour leurs autorisations de Privacy Service, car cette mise à jour imminente constitue une modification irréversible.L’application de la modification de ces autorisations aura lieu le **13 avril 2023**. Consultez la documentation relative à la [migration des informations d’identification d’API héritées](./permissions.md#migrate-tech-accounts) pour obtenir des conseils sur la résolution de ce problème.
>
>Les comptes techniques sont disponibles pour les clientes et clients d’entreprise et créés via l’Adobe Developers Console. L’Adobe ID d’une personne titulaire de compte technique se termine par `@techacct.adobe.com`. Si vous ne savez pas si vous êtes titulaire d’un compte technique, contactez l’administrateur ou l’administratrice de votre organisation.

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lorsque vous utilisez ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande.

Adobe Experience Platform [!DNL Privacy Service] a été développé en réponse à un changement fondamental dans la façon dont les entreprises sont tenues de gérer les données personnelles de leurs clients. Le principal objectif de [!DNL Privacy Service] est d’automatiser la conformité aux réglementations de confidentialité des données qui, en cas de violation, peuvent entraîner des amendes importantes et perturber les opérations de données de votre entreprise.

[!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer les requêtes liées aux données des clients. Grâce à [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clients personnelles depuis les applications Adobe Experience Cloud. Cela facilite l’automatisation de la mise en conformité concernant les réglementations légales et organisationnelles liées à la confidentialité.

>[!IMPORTANT]
>
>Privacy Service est destiné uniquement aux requêtes relatives aux titulaires de données et aux droits des clientes et clients. Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée. Adobe a l’obligation légale d’y répondre dans les délais impartis. Par conséquent, le test de chargement sur Privacy Service n’est pas autorisé, car il s’agit d’un environnement de production uniquement qui crée une liste d’attente inutile de requêtes d’accès à des informations personnelles valides.
>
>Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service. Les utilisateurs et utilisatrices qui abusent du système verront leur accès au service désactivé. Une réunion ultérieure sera ensuite organisée avec ces utilisateurs et utilisatrices afin d’aborder leurs actions et de discuter de l’utilisation acceptable de Privacy Service.

## Prise en main de [!DNL Privacy Service] {#getting-started}

Afin d’utiliser [!DNL Privacy Service], plusieurs décisions essentielles doivent être prises en fonction des exigences de confidentialité de votre organisation, des types de données d’identité que vous collectez auprès de vos clients et du meilleur moyen de connecter votre système de gestion de la relation client (CRM) avec ce service.

Ces décisions peuvent être résumées par le biais des questions suivantes :

1. **Quelles sont les informations que je recueille auprès de mes clients ?**
   * Pour tirer le meilleur parti de [!DNL Privacy Service], vous devez posséder une forte compréhension des types de données que vous collectez auprès de vos clients et savoir lesquelles sont assujetties aux réglementations liées à la confidentialité. Pour plus d’informations, consultez la section consacrée à la [détermination des exigences relatives à la confidentialité](#requirements).
1. **Ai-je appliqué les libellés corrects à mes données ?**
   * Les données doivent disposer de libellés appropriés afin que le service puisse déterminer les champs auxquels accéder ou ceux qu’il doit supprimer au cours des tâches relatives à la confidentialité. Pour plus d’informations, consultez la section consacrée aux [libellés des données](#label).
1. **Est-ce que je connais les ID à envoyer à [!DNL Privacy Service] ?**
   * Lors de l’envoi de demandes d’accès à des informations personnelles, il est nécessaire de fournir tous les ID de client spécifiques à des applications Adobe particulières. Pour plus d’informations, consultez les sections consacrées à la [production de données d’identité](#identity) et aux [demandes d’accès à des informations personnelles](#requests).
1. **Comment effectuer le suivi des tâches relatives à la confidentialité ?**
   * Une fois les demandes d’accès à des informations personnelles effectuées, il existe plusieurs options pour suivre leur statut et leurs résultats. Pour plus d’informations, consultez la section sur la [surveillance des tâches de confidentialité](#monitor).

Les sections ci-dessous fournissent des instructions générales sur ces étapes préalables importantes ainsi que des liens vers davantage de documentation offrant plus de détails sur [!DNL Privacy Service].

### Détermination des exigences de confidentialité de votre organisation {#requirements}

En fonction de la nature de votre entreprise et des juridictions sous lesquelles elle opère, vos opérations de données peuvent être assujetties à des règlements juridiques sur la confidentialité. Généralement, ces règlements donnent à vos clients le droit de demander l’accès aux données que vous collectez et qui les concernent. Ils peuvent également demander la suppression de ces données stockées. Ces demandes de données personnelles de la part des clients sont appelées « demandes d’accès à des informations personnelles » dans toute la documentation.

Pour plus d’informations sur les différents règlements juridiques en matière de confidentialité pour lesquels [!DNL Privacy Service] gère les demandes, y compris les termes clés et les réponses aux questions les plus fréquentes, reportez-vous à la [documentation sur les règlements en matière de confidentialité](./regulations/overview.md).

Si vos opérations de données relèvent de l’un des règlements pris en charge, consultez leur documentation pour obtenir des informations importantes, telles que les droits spécifiques relatifs à la confidentialité qu’ils accordent à vos clients, et les fenêtres de conformité permettant de répondre aux demandes d’accès à des informations personnelles. Ces informations doivent être prises en compte pour déterminer comment intégrer [!DNL Privacy Service] dans votre système CRM et comment les clients doivent interagir avec votre site web pour leurs demandes d’accès à des informations personnelles.

En plus des règlements juridiques, toute norme organisationnelle ou industrielle applicable à votre organisation doit également être considérée lorsque vous prenez ces décisions.

### Libellés des données pour les demandes d’accès à des informations personnelles {#label}

En fonction des applications [!DNL Experience Cloud] que vous utilisez, vous devez créer des libellés pour les champs de données spécifiques auxquels accéder ou que vous devez supprimer en réponse aux demandes d’accès à des informations personnelles. Le processus de création de libellés pour les données varie d’une application à l’autre. Pour savoir comment appliquer des libellés aux données de chaque application Adobe prise en charge, consultez le document sur les [applications Experience Cloud](./experience-cloud-apps.md).

### Détermination des types de données d’identité à envoyer à [!DNL Privacy Service] {#identity}

Pour que [!DNL Privacy Service] puisse traiter une demande d’accès à des informations personnelles émanant d’un client, il faut qu’au moins une valeur d’identité unique soit fournie pour ce client dans la demande elle-même. Une valeur d’identité unique désigne tout élément d’information pouvant être utilisé pour identifier une personne et ses données personnelles stockées dans vos magasins de données [!DNL Experience Cloud]. Le [!DNL Privacy Service] utilise ces informations d’identité pour localiser et traiter les données personnelles du client en fonction de la nature de la demande (accès, suppression ou désinscription).

Le type et le nombre de valeurs d’identité que vous devez fournir pour chaque client varient en fonction des applications [!DNL Experience Cloud] utilisées par votre système CRM. Certaines applications utilisent leurs propres valeurs d’ID client internes (tels que les ID Adobe Target), tandis que d’autres solutions reposent sur des identifiants globaux du [!DNL Experience Cloud Identity Service] (ECID) d’Adobe, qui effectuent le suivi de l’activité client dans toutes les applications [!DNL Experience Cloud]. En outre, des informations personnelles génériques telles qu’une adresse e-mail ou un numéro de téléphone peuvent également servir de données d’identité valides.

Le document sur les [données d’identité pour les demandes d’accès à des informations personnelles](./identity-data.md) fournit des informations plus détaillées sur les types d’informations relatives à l’identité acceptées pour [!DNL Privacy Service]. Le document fournit également des instructions sur la manière d’exploiter les technologies Adobe pour récupérer efficacement les informations d’identité appropriées de vos clients lorsqu’ils interagissent avec votre site web et envoyer ces données à [!DNL Privacy Service] dans des demandes d’API.

### Commencer à envoyer des demandes d’accès à des informations personnelles {#requests}

Une fois que vous avez déterminé les besoins en matière de confidentialité de votre entreprise et que vous avez décidé quelles valeurs d’identité envoyer à [!DNL Privacy Service], vous pouvez commencer à envoyer des demandes d’accès à des informations personnelles. [!DNL Privacy Service] vous permet d’envoyer des demandes d’accès à des informations personnelles par l’intermédiaire de l’API ou de l’interface utilisateur.

>[!IMPORTANT]
>
>Les sections ci-dessous contiennent des liens menant à la documentation qui explique comment effectuer des demandes d’accès à des informations personnelles génériques dans l’API ou l’interface utilisateur. Toutefois, en fonction des applications [!DNL Experience Cloud] que vous utilisez, les champs à envoyer dans la payload de requête peuvent différer des exemples qui se trouvent dans ces guides.
>
>Tout en suivant les instructions des guides relatifs à l’API ou à l’interface utilisateur, reportez-vous au document sur [Privacy Service et les applications Experience Cloud](./experience-cloud-apps.md) pour obtenir de plus amples informations sur la façon de formater les demandes d’accès à des informations personnelles pour une ou plusieurs de vos applications [!DNL Experience Cloud].
>
>Il est également important de noter que les demandes d’accès à des informations personnelles sont traitées de manière asynchrone dans les applications Experience Cloud. Lorsqu’une demande est reçue par Privacy Service, quelques minutes à plusieurs semaines peuvent être nécessaires à chaque application pour répondre à la requête. Le temps nécessaire à l’exécution de chaque demande est spécifique à l’application que vous utilisez et dépend également de la quantité de données à traiter.

#### Utilisation de l’API

[[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) fournit plusieurs points d’entrée pour la création et la gestion des tâches relatives à la confidentialité à l’aide des appels d’API RESTful. Cela vous permet d’avoir une approche automatisée de la conformité aux règlements relatifs à la confidentialité sur vos applications [!DNL Experience Cloud]. Pour obtenir des instructions détaillées sur lʼutilisation de lʼAPI, consultez le [guide de lʼAPI Privacy Service](api/overview.md).

#### Utilisation de l’interface utilisateur

>[!NOTE]
>
>L’interface utilisateur de [!DNL Privacy Service] ne prend actuellement en charge que les demandes d’accès et de suppression. Toutes les demandes de désinscription doivent être effectuées par le biais de l’API.

L’interface utilisateur de [!DNL Privacy Service] vous permet de créer et de surveiller des tâches de confidentialité à l’aide d’une interface graphique. L’interface utilisateur comprend un widget **[!UICONTROL Rapport d’état]** qui fournit une représentation visuelle de l’état de toutes les requêtes actives et vous permet de créer des requêtes à l’aide du **[!UICONTROL Créateur de requêtes]** intégré, ou en chargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/overview.md).

### Surveillance des tâches de confidentialité {#monitor}

Une fois les tâches de confidentialité effectuées, plusieurs options vous permettent de surveiller leur statut et leurs résultats :

| Méthode de surveillance | Description |
| --- | --- |
| [!DNL Privacy Service] Interface utilisateur | L’interface utilisateur de [!DNL Privacy Service] s’accompagne d’un tableau de bord de surveillance qui vous permet d’afficher une représentation visuelle reprenant le statut de chaque demande active. Pour plus d’informations, consultez le [guide d’utilisation de Privacy Service](ui/overview.md). |
| [!DNL Privacy Service] API | Vous pouvez surveiller le statut des tâches de confidentialité à l’aide d’un programme, en utilisant les points d’entrée de recherche fournis par l’API [!DNL Privacy Service]. Consultez le [guide de lʼAPI Privacy Service](./api/overview.md) pour obtenir des instructions détaillées sur lʼutilisation de lʼAPI. |
| [!DNL Privacy Events] | [!DNL Privacy Events] tire parti des événements d’Adobe I/O envoyés à un webhook configuré afin de faciliter l’automatisation efficace des demandes de traitement. Ils réduisent ou éliminent la nécessité de consulter l’API [!DNL Privacy Service] pour savoir si une tâche est terminée ou si un certain jalon a été atteint dans un workflow. Pour plus d’informations, consultez le tutoriel sur l’[abonnement aux Événements relatifs à la confidentialité](./privacy-events.md). |

## Étapes suivantes

Ce document offre un aperçu général de [!DNL Privacy Service] et des principales étapes à suivre pour commencer à utiliser les fonctionnalités du service. Pour obtenir de plus amples informations sur les divers aspects liés à l’utilisation de [!DNL Privacy Service], reportez-vous à la documentation référencée tout au long de la présentation.
