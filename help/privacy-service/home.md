---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 5%

---


# Présentation des Adobes Experience Platform Privacy Service

Pour offrir de meilleures expériences client, vous devez collecter et stocker les données personnelles de vos clients. Lors de l’utilisation de ces données, il est important de comprendre et de respecter la confidentialité de vos clients. Les nouvelles réglementations légales et organisationnelles donnent aux utilisateurs le droit d&#39;accéder à vos données personnelles ou de les supprimer de vos entrepôts de données sur demande.

L&#39;Adobe Experience Platform Privacy Service a été développé en réponse à un changement fondamental dans la façon dont les entreprises sont tenues de gérer les données personnelles de leurs clients. L&#39;objectif central du Privacy Service est d&#39;automatiser la conformité aux réglementations sur la confidentialité des données qui, en cas de violation, peuvent entraîner des amendes importantes et perturber les opérations de données pour votre entreprise.

Le Privacy Service fournit une API RESTful et une interface utilisateur pour vous aider à gérer les requêtes de données client. Avec Privacy Service, vous pouvez envoyer des demandes d’accès aux données personnelles des clients et de suppression de celles-ci à partir des applications Adobe Experience Cloud, ce qui vous permet de respecter automatiquement les règles de confidentialité légales et organisationnelles.

## Prise en main du Privacy Service {#getting-started}

Pour utiliser le Privacy Service, plusieurs décisions clés doivent être prises en fonction des exigences de confidentialité de votre entreprise, des types de données d&#39;identité que vous collectez auprès de vos clients et de la meilleure façon d&#39;interagir avec votre système de gestion de la relation client avec le service.

Ces décisions peuvent être résumées par les questions suivantes :

1. **Quelles sont les informations que je recueille auprès de mes clients ?**
   * Pour tirer le meilleur parti de votre Privacy Service, vous devez connaître en détail les types de données que vous collectez auprès de vos clients et savoir lesquelles sont assujetties aux règles de confidentialité. Consultez la section sur la [détermination des exigences](#requirements) en matière de confidentialité pour en savoir plus.
1. **Ai-je correctement étiqueté mes données ?**
   * Les données doivent être correctement étiquetées pour que le service puisse déterminer les champs à accéder ou à supprimer pendant les tâches de confidentialité. Consultez la section sur les données [d&#39;](#label) étiquetage pour en savoir plus.
1. **Est-ce que je sais quels identifiants envoyer au Privacy Service ?**
   * Lors de l’envoi de demandes de confidentialité, des ID de client individuels spécifiques à des applications Adobe particulières doivent être fournis. Pour plus d&#39;informations, consultez les sections sur la [fourniture de données](#identity) d&#39;identité et sur l&#39; [exécution de demandes](#requests) de confidentialité.
1. **Comment effectuer le suivi de mes tâches de confidentialité ?**
   * Une fois que vous avez effectué des demandes de confidentialité, il existe plusieurs options pour suivre leur état et leurs résultats. Pour plus d’informations, voir la section sur la [surveillance des tâches](#monitor) de confidentialité.

Les sections ci-dessous fournissent des orientations générales sur ces étapes préalables importantes et fournissent également des liens vers d&#39;autres documents Privacy Service pour plus de détails.

### Déterminer les exigences de confidentialité de votre entreprise {#requirements}

En fonction de la nature de votre entreprise et des juridictions sous lesquelles elle opère, vos opérations de données peuvent être assujetties à des règlements juridiques sur la protection des renseignements personnels. Ces réglementations donnent souvent à vos clients le droit de demander l&#39;accès aux données que vous leur collectez et le droit de demander la suppression de ces données stockées. Ces demandes de données personnelles de la part des clients sont appelées &quot;demandes de confidentialité&quot; dans toute la documentation.

Le tableau ci-dessous décrit la réglementation relative à la protection des renseignements personnels que le Privacy Service gère les demandes de renseignements, y compris les liens vers la documentation pour plus d’informations :

| Réglementation | Description |
| --- | --- |
| CCPA (Californie) | Le California Consumer Privacy Act (CCPA) protège la vie privée et les consommateurs pour les personnes résidant en Californie, États-Unis. L&#39;ACCP accorde de nouveaux droits à la confidentialité des données aux résidents californiens, y compris le droit d&#39;accéder et de supprimer leurs données personnelles, de savoir si leurs données personnelles sont vendues ou divulguées (et à qui), et le droit de opt-out leurs données d&#39;être vendues à des tiers.<br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://oag.ca.gov/privacy/ccpa)</li><li>[FAQ CCPA](ccpa/faq.md)</li></ul> |
| RGPD (Union européenne) | Le règlement général sur la protection des données (RGPD) a introduit plusieurs nouveaux droits à la confidentialité des données pour les membres de l’Union européenne, y compris le **droit d’accès** et le **droit à l’oubli**. Cela signifie que tout citoyen de l’UE dont les données personnelles ont été collectées par votre entreprise peut demander à accéder à ses données ou à les supprimer à tout moment. <br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://gdpr-info.eu/)</li><li>[FAQ relative au RGPD](gdpr/faq.md)</li><li>[Terminologie relative au règlement général sur la protection des données (RGPD)](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thaïlande) | La loi thaïlandaise sur la protection des données personnelles (PDPA) a été introduite pour protéger les propriétaires thaïlandais des données contre la collecte, l&#39;utilisation ou la divulgation illégales de leurs données personnelles. Inspirée par le RMR de l&#39;Union européenne, la réglementation accorde aux citoyens thaïlandais le droit de demander l&#39;accès à leurs données personnelles stockées ou de les supprimer.<br/><br/>Liens pour de plus amples informations : <ul><li>[Présentation juridique](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[FAQ sur PDPA_THA](pdpa-tha/faq.md)</li><li>[Terminologie PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Si vos opérations de données relèvent de l’une des réglementations ci-dessus, consultez leur documentation pour obtenir des informations importantes, telles que les droits de confidentialité spécifiques qu’ils accordent à vos clients, et des fenêtres de conformité pour répondre aux demandes de confidentialité. Ces informations doivent être prises en compte pour déterminer comment intégrer un Privacy Service dans votre système de gestion de la relation client et comment les clients doivent interagir avec votre site Web afin de faire des demandes de confidentialité.

En plus des règlements juridiques, toute norme organisationnelle ou industrielle applicable à votre organisation doit également être prise en compte lors de la prise de ces décisions.

### Étiqueter les données des demandes de confidentialité {#label}

En fonction des applications Experience Cloud que vous utilisez, vous devez étiqueter les champs de données spécifiques qui doivent être accessibles ou supprimés en réponse aux demandes de confidentialité. Le processus d&#39;étiquetage des données varie d&#39;une demande à l&#39;autre. Pour savoir comment étiqueter les données pour chaque application Adobe prise en charge, reportez-vous au document sur les applications [](./experience-cloud-apps.md)Experience Cloud.

### Déterminer les types de données d&#39;identité à envoyer au Privacy Service {#identity}

Pour que le Privacy Service puisse traiter une demande de confidentialité d&#39;un client, au moins une valeur d&#39;identité unique pour ce client doit être fournie dans la demande elle-même. Une valeur d&#39;identité unique est tout élément d&#39;information qui peut être utilisé pour identifier une personne et ses données personnelles stockées dans les entrepôts de données de votre Experience Cloud. Le Privacy Service utilise ces informations d&#39;identité pour localiser et traiter les données personnelles du client en fonction de la nature de la demande (accès, suppression ou exclusion).

Selon les applications Experience Cloud utilisées par votre système de gestion de la relation client, le type et le nombre de valeurs d’identité que vous devez fournir pour chaque client varieront. Certaines applications utilisent leurs propres valeurs d’ID de client internes (par exemple, des ID d’Adobe Target), tandis que d’autres solutions reposent sur des identifiants globaux d’Adobe Experience Cloud Identity Service (ECID) qui effectuent le suivi de l’activité de client dans toutes les applications Experience Cloud. En outre, des informations personnelles génériques telles qu&#39;une adresse électronique ou un numéro de téléphone peuvent également servir de données d&#39;identité valides.

Le document sur les données d&#39; [identité pour les demandes](./identity-data.md) de confidentialité fournit des informations plus détaillées sur les types d&#39;informations d&#39;identité qui sont acceptées par le Privacy Service. Le document fournit également des conseils sur la manière d&#39;exploiter les technologies Adobe pour récupérer efficacement les informations d&#39;identité appropriées de vos clients lorsqu&#39;ils interagissent avec votre site Web et envoyer ces données au Privacy Service dans les demandes d&#39;API.

### Début qui demande la confidentialité {#requests}

Une fois que vous avez déterminé les besoins en matière de confidentialité de votre entreprise et que vous avez décidé quelles valeurs d&#39;identité envoyer au Privacy Service, vous pouvez début de faire des demandes de confidentialité. Privacy Service vous permet d’envoyer des requêtes de confidentialité via l’API ou l’interface utilisateur.

>[!IMPORTANT]
>
>Les sections ci-dessous contiennent des liens vers la documentation qui explique comment effectuer des demandes de confidentialité génériques dans l’API ou l’interface utilisateur. Cependant, en fonction des applications Experience Cloud que vous utilisez, les champs que vous devez envoyer dans la charge utile de la demande peuvent être différents des exemples illustrés dans ces guides.
>
>Au fur et à mesure que vous suivez les guides de l’API ou de l’interface utilisateur, veuillez consulter le document sur les applications [de](./experience-cloud-apps.md) Privacy Service et d’Experience Cloud pour obtenir de plus amples informations sur la façon de formater les demandes de confidentialité pour vos applications Experience Cloud particulières.

#### Utilisation de l’API

L’API [du](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service fournit plusieurs points de terminaison pour la création et la gestion des tâches de confidentialité à l’aide des appels d’API RESTful, ce qui vous permet d’approcher par programmation la conformité à la réglementation de confidentialité pour vos applications Experience Cloud. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le guide [du développeur de l’API du](api/getting-started.md)Privacy Service.

#### Utilisation de l’interface utilisateur

>[!NOTE]
>
>Actuellement, l’interface utilisateur du Privacy Service ne prend en charge que les demandes d’accès et de suppression. Toutes les demandes d’exclusion doivent être effectuées par le biais de l’API à la place.

L’interface utilisateur du Privacy Service vous permet de créer et de surveiller des tâches de confidentialité à l’aide d’une interface graphique. L’interface utilisateur comprend un widget de rapport **d’** état qui fournit une représentation visuelle de l’état de toutes les requêtes actives et vous permet de créer de nouvelles requêtes à l’aide du créateur **de** requêtes intégré ou en téléchargeant des fichiers JSON. Pour plus d’informations sur l’utilisation de l’interface utilisateur, voir le guide [de l’utilisateur](ui/overview.md)Privacy Service.

### Surveillance des tâches de confidentialité {#monitor}

Une fois que vous avez effectué des tâches de confidentialité, vous disposez de plusieurs options pour contrôler leur état et leurs résultats :

| Méthode de surveillance | Description |
| --- | --- |
| Interface utilisateur Privacy Service | L’interface utilisateur du Privacy Service fournit un tableau de bord de surveillance qui vous permet de vue une représentation visuelle de l’état de toutes les requêtes actives. Pour plus d’informations, consultez le guide [de l’utilisateur](ui/overview.md) Privacy Service. |
| API Privacy Service | Vous pouvez contrôler par programmation l’état des tâches de confidentialité en utilisant les points de terminaison de recherche fournis par l’API du Privacy Service. Pour obtenir des instructions détaillées sur l’utilisation de l’API, consultez le guide [du développeur](./api/getting-started.md) Privacy Service. |
| Événements de confidentialité | Les Événements de confidentialité tirent parti des Événements d&#39;E/S Adobe envoyés à un crochet Web configuré afin de faciliter l&#39;automatisation efficace des demandes d&#39;emploi. Elles réduisent ou éliminent la nécessité de consulter l’API du Privacy Service afin de vérifier si une tâche est terminée ou si un certain jalon dans un processus a été atteint. Pour plus d’informations, consultez le didacticiel sur l’ [abonnement aux Événements](./privacy-events.md) de confidentialité. |

## Étapes suivantes

Ce document fournit un aperçu de haut niveau du Privacy Service et des principales étapes nécessaires au début en utilisant les capacités du service. Pour plus d&#39;informations sur les différents aspects de la collaboration avec le Privacy Service, veuillez consulter la documentation à laquelle vous avez accès tout au long de la présentation.
