---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2022
description: Les notes de mise à jour de janvier 2022 pour Adobe Experience Platform.
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 81%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 janvier 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte par le biais de l’onglet [!UICONTROL Alertes] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles règles d’alerte | Plusieurs nouvelles règles d’alerte sont désormais disponibles pour les workflows liés à l’ingestion de données, aux identités, aux profils, à la segmentation et à l’activation. Consultez la présentation des [règles d’alerte](../../observability/alerts/rules.md) pour obtenir la liste mise à jour des types d’alerte. |
| Alertes dans le contexte pour les flux de données des sources | Vous pouvez maintenant vous abonner pour recevoir des messages d’alerte concernant le statut de vos flux de données pendant le workflow d’ingestion. Pour plus d’informations, consultez le guide sur l’[abonnement aux alertes de sources dans l’interface utilisateur](../../sources/tutorials/ui/alerts.md). |

Pour plus d’informations sur les alertes dans Experience Platform, consultez la [présentation des alertes](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

| Fonctionnalité | Description |
| --- | --- |
| Légendes intelligentes | Un algorithme de machine learning fournit automatiquement des informations sur votre profil et vos données d’audience, et illustre les modèles et les tendances sur une période de 30 à 90 jours ou de 12 mois. Les légendes contiennent des informations sur les éléments suivants : <ul><li>Forme globale et statistiques</li><li>Tendances et modifications brusques</li><li>Modèles saisonniers</li><li>Anomalies inattendues</li></ul> Vous trouverez plus d’informations dans la documentation sur les [tableaux de bord des profils](../../dashboards/guides/profiles.md#profiles-count-trend) et les [tableaux de bord des segments](../../dashboards/guides/audiences.md#audience-size-trend). |
| Inventaire des tableaux de bord | Accédez aux rapports préconfigurés des tableaux de bord de profils, de segments et de destinations, y compris les intégrations installées telles que PowerBI, dans un emplacement centralisé. Pour plus d’informations, consultez la [[!DNL Dashboards] documentation de l’inventaire](../../dashboards/inventory.md). |
| Modèles de rapport PowerBI | Créez, personnalisez ou étendez les mesures à partir des modèles de données des rapports sur les profils, les segments et les destinations à l’aide de nouveaux graphiques PowerBI. Le workflow d’installation automatisée vous permet de partager vos informations marketing à travers votre organisation à partir de l’environnement PowerBI. Pour plus d’informations, consultez la [documentation sur le modèle de rapport PowerBI](../../dashboards/integrations/power-bi.md). |

Pour plus d’informations sur Query Service [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation](../../dashboards/home.md) de Query Service.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Expérience de mappage consolidée | La nouvelle interface de mappage de l’interface utilisateur d’Experience Platform vous offre une expérience de mappage cohérente qui vous permet de tirer parti des recommandations intelligentes en matière de mappage, de configurer manuellement les règles de mappage et de déboguer toute erreur survenant dans vos jeux de mappage. Pour plus d’informations, consultez le [[!DNL Data Prep] guide de l’interface utilisateur](../../data-prep/ui/mapping.md). |

Pour plus d’informations sur Query Service [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md) de Query Service.

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| Personnalisation de la même page et de la page suivante | La [fonctionnalité de personnalisation de la même page et de la page suivante](../../destinations/ui/activate-edge-personalization-destinations.md) fournit une vue partagée et ciblée des utilisateurs pour les applications sur Edge Network, afin d’assurer la cohérence entre les canaux marketing et client. Cette personnalisation est possible grâce à la [connexion Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) et à la [connexion de personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md). Pour configurer vos campagnes de personnalisation de la même page ou de la page suivante, reportez-vous au [tutoriel dédié](../../destinations/ui/activate-edge-personalization-destinations.md). |
| Surveillance des destinations par lots et mesures au niveau du segment | La fonctionnalité de surveillance des destinations est désormais étendue à partir des destinations de diffusion en continu pour inclure également les destinations par lots et les mesures au niveau du segment pour vos flux de données d’activation. Pour plus d’informations, lisez les sections [Tableau de bord de surveillance des destinations](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [Tableau de bord de surveillance des tâches de segment](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard) et [Affichage au niveau du segment](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| Modification du planning dans l’interface utilisateur pour les flux de données d’activation par lots existants | Cette version introduit l’option permettant de modifier le planning de vos flux de données d’activation existants vers des destinations par lots. Pour plus d’informations, lisez [Activation des données de profils vers les destinations de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Améliorations des destinations Marketo | Les clients d’Experience Platform qui utilisent Marketo Engage peuvent optimiser leur base de données Marketo grâce à la nouvelle possibilité d’envoyer des enregistrements de nouvelles personnes dans Marketo Engage depuis Experience Platform via le [connecteur de destination Marketo](/help/destinations/catalog/adobe/marketo-engage.md). <br> Lorsque vous envoyez des segments d’audience d’Experience Platform vers Marketo Engage, les personnes du segment qui n’existent pas encore dans votre base de données Marketo Engage peuvent y être automatiquement ajoutées. Pour plus d’informations, lisez [Envoi d’un segment Adobe Experience Platform vers une liste statique Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=fr) (l’étape 9 du tutoriel indique comment envoyer les enregistrements de nouvelles personnes dans Marketo). |

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [Connexion Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target est une application qui permet la personnalisation et l’expérimentation en temps réel, grâce à l’IA, au niveau de toutes les interactions avec les clients entrants sur les sites web, les applications mobiles, etc. Adobe Target est une connexion de personnalisation dans Adobe Experience Platform. |
| [Connexion de personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md) | Cette connexion de personnalisation permet de récupérer des informations sur les segments depuis Adobe Experience Platform vers des plateformes de personnalisation externes, des systèmes de gestion de contenu, des serveurs publicitaires et d’autres applications exécutées sur les sites web des clients. |

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Query Service {#query-service}

[!DNL Query Service] vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Bloc anonyme | La structure SQL du bloc anonyme permet de ventiler les tâches de préparation des données à grande échelle dans Query Service en tâches plus petites, puis de les réutiliser et de les exécuter en séquence pour le chargement incrémentiel des données. Pour plus d’informations, consultez la [documentation sur les exemples de requêtes pour les blocs anonymes](../../query-service/key-concepts/anonymous-block.md). |
| Organisation des jeux de données | Fournit une structure de données cohérente et logique pour organiser vos ressources de données à utiliser avec Query Service à mesure que la quantité de ressources de données dans le sandbox augmente. Pour plus d’informations, consultez la [documentation sur l’organisation des ressources de données](../../query-service/best-practices/organize-data-assets.md). |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations apportées à l’interface utilisateur des sandbox | L’indicateur sandbox est désormais intégré à l’en-tête de toutes les applications de l’interface utilisateur d’Experience Platform. L’indicateur sandbox affiche le nom, la région et le type du sandbox. Il vous offre également un accès à un menu déroulant afin de basculer entre les sandbox. Pour plus d’informations, consultez le [guide de l’interface utilisateur des sandbox](../../sandboxes/ui/user-guide.md). |

Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Segment Match | La correspondance de segments est un service de collaboration de données qui permet à deux utilisateurs d’Experience Platform ou plus d’échanger des données, basées sur des identifiants communs, d’une manière sécurisée, contrôlée et respectueuse de la vie privée. La correspondance de segments utilise les normes de confidentialité et les identifiants personnels d’Experience Platform tels que les e-mails hachés, les numéros de téléphone hachés et les identifiants d’appareils comme les IDFA et les GAID. Pour plus d’informations, consultez la [présentation de la Segment Match](../../segmentation/ui/segment-match/overview.md). |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| Améliorations de la source [!DNL Event Hubs] | La source [!DNL Event Hubs] prend désormais en charge le type d’authentification par clé SAS non racine pour se connecter et créer la connexion source. Pour plus d’informations, consultez la [[!DNL Event Hubs] présentation](../../sources/connectors/cloud-storage/eventhub.md). |
| Améliorations de la source [!DNL SFTP] | La source [!DNL SFTP] vous permet désormais d’établir un nombre défini de connexions simultanées maximales qu’un flux de données peut utiliser pour se connecter au serveur SFTP. Pour plus d’informations, consultez la [[!DNL SFTP] présentation](../../sources/connectors/cloud-storage/sftp.md). |
