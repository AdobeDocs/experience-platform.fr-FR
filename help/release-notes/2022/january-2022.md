---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: bcd52989-ef62-4ab9-866e-1d9e57b76a0c
source-git-commit: 78f9b8434d577909ccb1c62211a802e05c8291e1
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 37%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 janvier 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide du [!UICONTROL Alertes] dans l’interface utilisateur de Platform et peut choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles règles d’alerte | Plusieurs nouvelles règles d’alerte sont désormais disponibles pour les workflows liés à l’ingestion de données, aux identités, aux profils, à la segmentation et à l’activation. Consultez la présentation sur [règles d’alerte](../../observability/alerts/rules.md) pour la liste mise à jour des types d’alerte. |
| Alertes contextuelles pour les flux de données de sources | Vous pouvez maintenant vous abonner pour recevoir des messages d’alerte concernant l’état de vos flux de données pendant le processus d’ingestion. Pour plus d’informations, consultez le guide sur [abonnement aux alertes de sources dans l’interface utilisateur](../../sources/tutorials/ui/alerts.md). |

Pour plus d’informations sur les alertes dans Platform, reportez-vous à la section [aperçu des alertes](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform propose de nombreux tableaux de bord qui vous permettent dʼafficher des informations importantes concernant les données de votre entreprise. Celles-ci sont présentées telles quʼelles sont capturées lors dʼaperçus quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| Légendes intelligentes | Un algorithme d’apprentissage automatique fournit automatiquement des insights sur vos données de profil et d’audience, et illustre les schémas et tendances sur une période de 30 à 90 jours, ou de 12 mois. Les sous-titres contiennent des informations sur <ul><li>Forme globale et statistiques</li><li>Tendances et modifications brusques</li><li>Formats saisonniers</li><li>Les anomalies inattendues</li></ul> Vous trouverez plus d’informations sur la [tableaux de bord des profils](../../dashboards/guides/profiles.md#profiles-count-trend) et [tableaux de bord des segments](../../dashboards/guides/segments.md#audience-size-trend) documentation. |
| Inventaire des tableaux de bord | Accédez aux rapports préconfigurés des tableaux de bord des profils, des segments et des destinations, y compris les intégrations installées telles que PowerBI, à un emplacement centralisé. Pour plus d’informations, voir [[!DNL Dashboards] aperçu](../../dashboards/home.md). |
| Modèles de rapport PowerBI | Créez, personnalisez ou étendez des mesures à partir des modèles de données de rapports de profil, de segments et de destination à l’aide de nouveaux graphiques PowerBI. Le workflow d’installation automatisée vous permet de partager vos informations marketing dans l’ensemble de votre organisation à partir de l’environnement PowerBI. Pour plus d’informations, voir [[!DNL Dashboards] aperçu](../../dashboards/home.md). |

Pour plus d’informations sur [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation de la ](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Expérience de mappage consolidé | La nouvelle interface de mappage de l’interface utilisateur de Platform vous offre une expérience de mappage cohérente pour tirer parti des recommandations de mappage intelligent, configurer manuellement les règles de mappage et déboguer les erreurs qui se produisent dans vos jeux de mappages. Pour plus d’informations, voir [[!DNL Data Prep] Guide de l’interface utilisateur](../../data-prep/ui/mapping.md). |

Pour plus d’informations sur [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation de la ](../../data-prep/home.md).

<!--

## [!DNL Destinations] {#destinations}

[!DNL Destinations] are pre-built integrations with destination platforms that allow for the seamless activation of data from Adobe Experience Platform. You can use destinations to activate your known and unknown data for cross-channel marketing campaigns, email campaigns, targeted advertising, and many other use cases.

| Feature | Description |
| ----------- | ----------- |
| Placeholder for next-hit personalization | Description |
| Placeholder for batch monitoring | Description |
| Placeholder for re-introducing scheduling in the UI | Description |
| Placeholder for Marketo destination update | Description |


**New destinations**

| Destination | Description |
| ----------- | ----------- |
| Placeholder for Target | Description |
| Placeholder for Custom Personalization | Description |

For more general information on destinations, refer to the [destinations overview](../../destinations/home.md).

-->

## Query Service {#query-service}

[!DNL Query Service] vous permet d’utiliser SQL standard pour interroger des données dans Adobe Experience Platform. [!DNL Data Lake]. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête en tant que nouveau jeu de données à utiliser dans les rapports, Data Science Workspace ou pour ingestion dans Real-time Customer Profile.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Bloc anonyme | La structure SQL de bloc anonyme permet de ventiler les tâches de préparation de données à grande échelle dans Query Service en tâches plus petites, puis de les réutiliser et de les exécuter en séquence pour le chargement incrémentiel des données. Pour plus d’informations, voir [Présentation de Query Service](../../query-service/home.md). |
| Organisation du jeu de données | Fournit une structure de données logique et cohérente pour organiser vos ressources de données à utiliser avec Query Service à mesure que la quantité de ressources de données dans l’environnement de test augmente. Pour plus d’informations, voir [Présentation de Query Service](../../query-service/home.md). |

Pour plus d’informations sur [!DNL Query Service], consultez la [[!DNL Query Service] présentation de la ](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance unique de Platform en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’interface utilisateur des environnements de test | L’indicateur sandbox est désormais intégré à l’en-tête de toutes les applications de l’interface utilisateur de Platform. L’indicateur sandbox affiche le nom, la région et le type de l’environnement de test et vous permet également d’accéder à un menu déroulant pour basculer entre les environnements de test. Pour plus d’informations, voir [guide de l’interface utilisateur des environnements de test](../../sandboxes/ui/user-guide.md). |

Pour plus d’informations sur les environnements de test, voir [Présentation des environnements de test](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Correspondance de segments | La correspondance de segment est un service de collaboration de données qui permet à deux utilisateurs ou plus de Platform d’échanger des données, en fonction d’identifiants communs, d’une manière sécurisée, gouvernée et respectueuse de la confidentialité. La correspondance de segment utilise les normes de confidentialité de Platform et les identifiants personnels tels que les emails hachés, les numéros de téléphone hachés et les identifiants d’appareil comme les IDFA et les GAID. Pour plus d’informations, voir [Correspondance de segment - Aperçu](../../segmentation/ui/segment-match/overview.md). |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Améliorations de la source [!DNL Event Hubs] | Le [!DNL Event Hubs] source prend désormais en charge le type d’authentification de clé SAS non racine pour se connecter et créer une connexion source. Pour plus d’informations, voir [[!DNL Event Hubs] aperçu](../../sources/connectors/cloud-storage/eventhub.md). |
| Améliorations de la source [!DNL SFTP] | Le [!DNL SFTP] source vous permet désormais d’établir un nombre défini de connexions simultanées maximales qu’un flux de données peut utiliser pour se connecter au serveur SFTP. Pour plus d’informations, voir [[!DNL SFTP] aperçu](../../sources/connectors/cloud-storage/sftp.md). |
