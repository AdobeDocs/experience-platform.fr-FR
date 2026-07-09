---
keywords: Experience Platform;accueil;rubriques populaires;RGPD;rgpd;ccpa;CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Présentation de Privacy Service
description: Découvrez comment Privacy Service peut faciliter la mise en conformité automatisée avec les réglementations légales en matière de confidentialité dans vos opérations de données Experience Cloud.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
TQID: https://experienceleague.adobe.com/Y-VDhBnsrSr-sFRAD8BHquyIt2BFAwKa6tjCoYHLkhI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 2f54212d8592c5ebc45b847c5f8269ddddfeb622
workflow-type: tm+mt
source-wordcount: 1674
ht-degree: 44%

---

# Présentation de Privacy Service

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lorsque vous utilisez ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles et de les supprimer de vos banques de données sur demande.

Adobe Experience Platform Privacy Service a été développé en réponse à un changement fondamental dans la façon dont les entreprises sont tenues de gérer les données personnelles de leurs clients. Le principal objectif de Privacy Service est d’automatiser la conformité aux réglementations de confidentialité des données qui, en cas de violation, peuvent entraîner des amendes importantes et perturber les opérations de données de votre entreprise.

Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer les demandes de données des clients. Vous pouvez utiliser Privacy Service pour envoyer des demandes d’accès et de suppression de données clients personnelles depuis les applications Adobe Experience Cloud. Cela facilite l’automatisation de la mise en conformité avec les réglementations légales et organisationnelles liées à la confidentialité.

>[!IMPORTANT]
>
>Privacy Service est destiné uniquement aux requêtes relatives aux titulaires de données et aux droits des clientes et clients. Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée. Adobe a l’obligation légale d’y répondre dans les délais impartis. Par conséquent, le test de chargement sur Privacy Service n’est pas autorisé, car il s’agit d’un environnement de production uniquement qui crée une liste d’attente inutile de requêtes d’accès à des informations personnelles valides.
>
>Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service. Les utilisateurs et utilisatrices qui abusent du système verront leur accès au service désactivé. Une réunion ultérieure sera ensuite organisée avec ces utilisateurs et utilisatrices afin d’aborder leurs actions et de discuter de l’utilisation acceptable de Privacy Service.

## Prise en main de Privacy Service {#getting-started}

Pour utiliser de manière optimale Privacy Service, plusieurs décisions importantes doivent être prises en fonction des exigences de confidentialité de votre organisation, des types de données d’identité que vous collectez auprès de vos clients et du meilleur moyen de connecter votre système de gestion de la relation client (CRM) avec ce service.

Ces décisions peuvent être résumées par le biais des questions suivantes :

1. **Quelles sont les informations que je recueille auprès de mes clients ?**
   * Pour tirer le meilleur parti de Privacy Service, vous devez posséder une bonne compréhension des types de données que vous collectez auprès de vos clients et savoir lesquelles sont assujetties aux réglementations liées à la confidentialité. Pour plus d’informations, consultez la section consacrée à la [détermination des exigences relatives à la confidentialité](#requirements).
1. **Ai-je appliqué les libellés corrects à mes données ?**
   * Les données doivent comporter des libellés appropriés pour le service afin de déterminer les champs auxquels accéder ou ceux qu’il faut supprimer lors des tâches relatives à la confidentialité. Pour plus d’informations, consultez la section sur [l’étiquetage des données](#label).
1. **Est-ce que je connais les ID à envoyer à Privacy Service ?**
   * Lors de l’envoi de demandes d’accès à des informations personnelles, il est nécessaire de fournir tous les ID de client spécifiques à des applications Adobe particulières. Pour plus d’informations, consultez les sections consacrées à la [production de données d’identité](#identity) et aux [demandes d’accès à des informations personnelles](#requests).
1. **Comment effectuer le suivi des tâches relatives à la confidentialité ?**
   * Une fois les demandes d’accès à des informations personnelles effectuées, il existe plusieurs options pour suivre leur statut et leurs résultats. Pour plus d’informations, consultez la section sur la [surveillance des tâches de confidentialité](#monitor).

Les sections ci-dessous fournissent des instructions générales sur ces étapes préalables importantes ainsi que des liens vers d’autres documents Privacy Service offrant plus de détails.

### Détermination des exigences de confidentialité de votre organisation {#requirements}

En fonction de la nature de votre entreprise et des juridictions sous lesquelles elle opère, vos opérations de données peuvent être assujetties à des règlements juridiques sur la confidentialité. Généralement, ces règlements donnent à vos clients le droit de demander l’accès aux données que vous collectez et qui les concernent. Ils peuvent également demander la suppression de ces données stockées. Ces demandes de données personnelles de la part des clients sont appelées « demandes d’accès à des informations personnelles » dans toute la documentation.

Pour plus d’informations sur les différents règlements juridiques en matière de confidentialité pour lesquels Privacy Service gère les demandes, y compris les termes clés et les réponses aux questions les plus fréquentes, reportez-vous à la documentation sur les [&#x200B; règlements en matière de confidentialité &#x200B;](./regulations/overview.md).

Si vos opérations de données relèvent de l’un des règlements pris en charge, consultez leur documentation pour obtenir des informations importantes, telles que les droits spécifiques relatifs à la confidentialité qu’ils accordent à vos clients, et les fenêtres de conformité permettant de répondre aux demandes d’accès à des informations personnelles. Ces informations doivent être prises en compte pour déterminer comment intégrer Privacy Service dans votre système CRM et comment les clients doivent interagir avec votre site web pour leurs demandes d’accès à des informations personnelles.

En plus des règlements juridiques, toute norme organisationnelle ou industrielle applicable à votre organisation doit également être considérée lorsque vous prenez ces décisions.

### Libellés des données pour les demandes d’accès à des informations personnelles {#label}

En fonction des applications [!DNL Experience Cloud] que vous utilisez, vous devez créer des libellés pour les champs de données spécifiques auxquels accéder ou que vous devez supprimer en réponse aux demandes d’accès à des informations personnelles. Le processus d’étiquetage des données varie d’une application à l’autre. Pour savoir comment appliquer des libellés aux données de chaque application Adobe prise en charge, consultez le document sur les [applications Experience Cloud](./experience-cloud-apps.md).

### Déterminer les types de données d’identité à envoyer à Privacy Service {#identity}

Pour que Privacy Service puisse traiter une demande d’accès à des informations personnelles émanant d’un client, il faut qu’au moins une valeur d’identité unique soit fournie pour ce client dans la demande elle-même. Une valeur d’identité unique désigne tout élément d’information pouvant être utilisé pour identifier une personne et ses données personnelles stockées dans vos magasins de données [!DNL Experience Cloud]. Privacy Service utilise ces informations d’identité pour localiser et traiter les données personnelles du client en fonction de la nature de la demande (accès, suppression ou désinscription).

Le type et le nombre de valeurs d’identité que vous devez fournir pour chaque client varient en fonction des applications [!DNL Experience Cloud] utilisées par votre système CRM. Certaines applications utilisent leurs propres valeurs d’ID client internes (tels que les ID Adobe Target), tandis que d’autres solutions reposent sur des identifiants globaux du [!DNL Visitor ID Service] Adobe (ECID) qui effectuent le suivi de l’activité client dans toutes les applications [!DNL Experience Cloud]. En outre, des informations personnelles génériques telles qu’une adresse e-mail ou un numéro de téléphone peuvent également servir de données d’identité valides.

Lisez le document sur [les données d’identité pour les demandes d’accès à des informations personnelles](./identity-data.md) pour plus d’informations sur les types d’informations d’identité acceptées pour Privacy Service. Le document fournit également des conseils sur l’application des technologies Adobe pour récupérer efficacement les informations d’identité appropriées de vos clients lorsqu’ils interagissent avec votre site web et envoyer ces données à Privacy Service dans des requêtes d’API.

### Commencer à envoyer des demandes d’accès à des informations personnelles {#requests}

Une fois que vous avez déterminé les besoins en matière de confidentialité de votre entreprise et que vous avez décidé quelles valeurs d’identité envoyer à Privacy Service, vous pouvez commencer à envoyer des demandes d’accès à des informations personnelles. Utilisez Privacy Service pour envoyer des demandes d’accès à des informations personnelles via l’API ou l’interface utilisateur.

#### Détails du fichier de demande d’accès {#access-requests}

En réponse à une demande d’accès réussie, une **URL de téléchargement** contient plusieurs fichiers. Un fichier est fourni pour chaque application Adobe pour laquelle des données ont été demandées. Notez que le format de fichier de chaque application peut différer en fonction de la structure de données de l’application.

#### Demandes de suppression - Aucune URL de téléchargement {#delete-requests}

La réponse à une **requête de suppression** ne contient **aucune URL de téléchargement**, car aucune donnée client n’est récupérée.

>[!IMPORTANT]
>
>Les sections ci-dessous contiennent des liens menant à la documentation qui explique comment effectuer des demandes d’accès à des informations personnelles génériques dans l’API ou l’interface utilisateur. Toutefois, en fonction des applications [!DNL Experience Cloud] que vous utilisez, les champs à envoyer dans la payload de requête peuvent différer des exemples qui se trouvent dans ces guides.
>
>Tout en suivant les instructions des guides relatifs à l’API ou à l’interface utilisateur, reportez-vous au document sur [les applications Privacy Service et Experience Cloud](./experience-cloud-apps.md) pour obtenir de plus amples informations sur la manière de formater les demandes d’accès à des informations personnelles pour vos applications [!DNL Experience Cloud] spécifiques.
>
>Il est également important de noter que les demandes d’accès à des informations personnelles sont traitées de manière asynchrone dans les applications Experience Cloud. Lorsqu’une demande est reçue par Privacy Service, quelques minutes à plusieurs semaines peuvent être nécessaires à chaque application pour répondre à la requête. Le temps nécessaire à l’exécution de chaque demande est spécifique à l’application que vous utilisez et dépend également de la quantité de données à traiter.

#### Utilisation de l’API {#api}

Pour approcher par programmation la conformité à la réglementation de confidentialité pour vos applications [!DNL Experience Cloud], vous pouvez utiliser des appels API RESTful pour [[!DNL Privacy Service API]](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) des points d’entrée afin de créer et de gérer des tâches de confidentialité. Pour obtenir des instructions détaillées sur lʼutilisation de lʼAPI, consultez le [guide de lʼAPI Privacy Service](api/overview.md).

#### Utilisation de l’interface utilisateur {#ui}

>[!NOTE]
>
>Actuellement, l’interface utilisateur de Privacy Service ne prend en charge que les demandes d’accès et de suppression. Toutes les demandes de désinscription doivent être effectuées par le biais de l’API.

Vous pouvez créer et surveiller les tâches de confidentialité à l’aide d’une interface graphique avec l’interface utilisateur de Privacy Service. L’interface utilisateur comprend un widget **[!UICONTROL Rapport de statut]** qui fournit une représentation visuelle du statut de toutes les requêtes actives. Vous pouvez également créer des requêtes avec le créateur de requêtes **[!UICONTROL intégré]** ou en chargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez le [guide d’utilisation de Privacy Service](ui/overview.md).

### Surveillance des tâches de confidentialité {#monitor}

Une fois les tâches de confidentialité effectuées, plusieurs options vous permettent de surveiller leur statut et leurs résultats :

| Méthode de surveillance | Description |
| --- | --- |
| Interface utilisateur de Privacy Service | Vous pouvez afficher une représentation visuelle du statut de toutes les requêtes actives avec le tableau de bord de surveillance de l’interface utilisateur de Privacy Service. Pour plus d’informations, consultez le [guide d’utilisation de Privacy Service](ui/overview.md). |
| API PRIVACY SERVICE | Vous pouvez surveiller par programmation le statut des tâches de confidentialité à l’aide des points d’entrée de recherche fournis par l’API Privacy Service. Consultez le [guide de lʼAPI Privacy Service](./api/overview.md) pour obtenir des instructions détaillées sur lʼutilisation de lʼAPI. |
| [!DNL Privacy Events] | [!DNL Privacy Events] utilisez des Adobe I/O Events qui sont envoyées à un webhook configuré afin de faciliter l’automatisation efficace des demandes de traitement. Ils réduisent ou éliminent la nécessité d’interroger l’API Privacy Service pour vérifier si une tâche est terminée ou si un certain jalon a été atteint dans un workflow. Pour plus d’informations, consultez le tutoriel sur l’[abonnement aux Événements relatifs à la confidentialité](./privacy-events.md). |

#### Réponses pour les utilisateurs non existants {#non-existing-users}

Lorsque vous soumettez une demande d’accès ou de suppression, même si les données utilisateur sont introuvables, la réponse renvoie toujours un `success` si l’appel a été effectué avec succès. Cela signifie que même si les données n’existent pas, un accès ou une suppression peut se terminer sans qu’aucune donnée ne soit récupérée ou supprimée.

## Étapes suivantes

Ce document offre une présentation générale de Privacy Service et des principales étapes à suivre pour commencer à utiliser les fonctionnalités du service. Pour obtenir de plus amples informations sur les différents aspects liés à l’utilisation de Privacy Service, reportez-vous à la documentation référencée tout au long de la présentation.
