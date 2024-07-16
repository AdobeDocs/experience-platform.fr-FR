---
keywords: Experience Platform;accueil;rubriques populaires;CJA;journey analytics;customer journey analytics;orchestration des campagnes;orchestration;parcours client;parcours;journey orchestration;fonctionnalité;région
title: Exemple de workflow de bout en bout Adobe Experience Platform
description: Découvrez le workflow de base de bout en bout pour Adobe Experience Platform à un niveau élevé.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 10%

---

# Exemple de workflow de bout en bout Adobe Experience Platform

Adobe Experience Platform est l’un des meilleurs systèmes ouverts, flexibles et performants du marché permettant de créer et de gérer des solutions complètes qui optimisent l’expérience client. Platform permet aux entreprises de centraliser et de normaliser les données et le contenu des clients à partir de n’importe quel système et d’appliquer la science des données et l’apprentissage automatique afin d’améliorer considérablement la conception et la diffusion d’expériences riches et personnalisées.

Basée sur les API RESTful, Platform expose toutes les fonctionnalités du système aux développeurs, ce qui facilite l’intégration des solutions d’entreprise à l’aide d’outils courants. Platform vous permet d’obtenir une vue d’ensemble de vos clients en ingérant vos données client, en segmentant vos données vers les audiences que vous souhaitez cibler et en activant ces audiences vers une destination externe. Le tutoriel suivant présente un workflow de bout en bout, qui montre toutes les étapes, de l’ingestion via les sources à l’activation de l’audience via les destinations.

![Workflow Experience Platform de bout en bout](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Commencer

Ce workflow de bout en bout utilise plusieurs services Adobe Experience Platform. Voici une liste des services utilisés dans ce workflow avec des liens vers leurs vues d’ensemble :

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md) : offre une vue d’ensemble complète de vos clients et de leur comportement en rapprochant des identités entre appareils et systèmes.
- [Sources ](../sources/home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [[!DNL Segmentation Service]](../segmentation/home.md) : [!DNL Segmentation Service] permet de diviser les données stockées dans [!DNL Experience Platform] qui se rapportent aux individus (tels que les client(e)s, les prospects, les utilisateurs et utilisatrices ou les organisations) en groupes plus petits.
- [[!DNL Real-Time Customer Profile]](../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Jeux de données](../catalog/datasets/overview.md) : structure de stockage et de gestion pour la persistance des données dans [!DNL Experience Platform].
- [Destinations](../destinations/home.md) : les destinations sont des intégrations préconfigurées des applications courantes qui permettent l’activation transparente des données de Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Créer un schéma XDM

Avant d’ingérer des données dans Platform, vous devez d’abord créer un schéma XDM pour décrire la structure de ces données. Lorsque vous ingérez vos données à l’étape suivante, vous mappez vos données entrantes avec ce schéma. Pour savoir comment créer un exemple de schéma XDM, consultez le tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).

Le tutoriel ci-dessus montre comment définir des champs d’identité pour vos schémas. Un champ d’identité représente un champ qui peut être utilisé pour identifier une personne individuelle liée à un événement d’enregistrement ou de série temporelle. Les champs d’identité sont un composant essentiel de la manière dont les graphiques d’identités client sont créés dans Platform, ce qui affecte finalement la manière dont Real-Time Customer Profile fusionne des fragments de données disparates pour obtenir une vue d’ensemble complète du client. Pour plus d’informations sur la manière d’afficher les graphiques d’identités dans Platform, consultez le tutoriel sur [l’utilisation de la visionneuse de graphiques d’identités](../identity-service/features/identity-graph-viewer.md).

Vous devez activer votre schéma pour l’utiliser dans Real-time Customer Profile afin que les profils client puissent être créés à partir des données basées sur votre schéma. Pour plus d’informations, consultez la section sur l’ [activation d’un schéma pour Profile](../xdm/ui/resources/schemas.md#profile) dans le guide de l’interface utilisateur des schémas.

## Ingestion de vos données dans Platform

Une fois que vous avez créé un schéma XDM, vous pouvez commencer à intégrer vos données dans le système.

Toutes les données importées dans Platform sont stockées dans des jeux de données individuels lors de l’ingestion. Un jeu de données est un ensemble d’enregistrements de données qui correspondent à un schéma XDM spécifique. Avant que vos données puissent être utilisées par [!DNL Real-Time Customer Profile], le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes sur l’activation d’un jeu de données pour Profile, consultez le [guide sur l’interface utilisateur des jeux de données](../catalog/datasets/user-guide.md#enable-profile) et le [ tutoriel sur l’API de configuration des jeux de données](../profile/tutorials/dataset-configuration.md). Une fois le jeu de données configuré, vous pouvez commencer à y ingérer des données.

Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, les bases de données, etc. Par exemple, vous pouvez ingérer vos données à l’aide de [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Vous trouverez une liste complète des sources disponibles dans la [présentation des connecteurs source](../sources/home.md).

Si vous utilisez Amazon S3 comme connecteur source, vous pouvez suivre les instructions du tutoriel de l’API sur la [création d’un connecteur Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) ou du tutoriel de l’interface utilisateur sur la [création d’un connecteur Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) pour apprendre à créer, à vous connecter et à ingérer des données dans le connecteur.

Pour des instructions plus détaillées sur les connecteurs source, consultez la [présentation des connecteurs source](../sources/home.md). Pour en savoir plus sur le service de flux, l’API à partir de laquelle sont basées les sources, consultez la [référence de l’API de service de flux](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Une fois vos données importées dans Platform par le biais du connecteur source et stockées dans votre jeu de données activé pour Profile, les profils client sont automatiquement créés en fonction des données d’identité que vous avez configurées dans votre schéma XDM.

Lors du premier chargement de données vers un nouveau jeu de données ou lors de la configuration d’un nouveau processus ETL ou d’une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées et que les profils générés contiennent les données attendues. Pour plus d’informations sur l’accès aux profils client dans l’interface utilisateur de Platform, consultez le [guide de l’interface utilisateur de profil client en temps réel](../profile/ui/user-guide.md). Pour plus d’informations sur l’accès aux profils à l’aide de l’API Real-Time Customer Profile, consultez le guide sur [l’utilisation du point d’entrée Entités](../profile/api/entities.md).

## Évaluation de vos données

Une fois que vous avez généré des profils à partir des données ingérées, vous pouvez évaluer vos données à l’aide de la segmentation. La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble d’individus de votre banque de profils, afin de distinguer un groupe de clients potentiels de votre base. Pour en savoir plus sur la segmentation, consultez la [présentation de segmentation service](../segmentation/home.md).

### Création d’une définition de segment

Pour commencer, vous devez créer une définition de segment pour regrouper vos clients afin de créer votre audience cible. Une définition de segment est un ensemble de règles que vous pouvez utiliser pour définir l’audience que vous souhaitez cibler. Pour créer une définition de segment, vous pouvez suivre les instructions du guide de l’interface utilisateur sur l’utilisation du [créateur de segments](../segmentation/ui/segment-builder.md) ou du tutoriel de l’API sur la [création d’un segment](../segmentation/tutorials/create-a-segment.md).

Une fois que vous avez créé une définition de segment, veillez à tenir compte de l’identifiant de définition de segment.

### Évaluation de la définition de segment

Après avoir créé votre définition de segment, vous pouvez créer une tâche de segmentation pour évaluer le segment comme une instance unique ou créer une planification pour évaluer le segment de manière continue.

Pour évaluer une définition de segment à la demande, vous pouvez créer une tâche de segmentation. Une tâche de segmentation est un processus asynchrone qui crée un segment d’audience en fonction de la définition de segment référencé et des stratégies de fusion. Une stratégie de fusion est un ensemble de règles utilisé par Platform pour déterminer les données qui seront utilisées pour créer des profils client et les données qui seront hiérarchisées en cas d’incohérences entre les sources. Pour savoir comment utiliser des stratégies de fusion, consultez le [guide d’interface utilisateur des stratégies de fusion](../profile/merge-policies/ui-guide.md).

Une fois la tâche de segmentation créée et évaluée, vous pouvez obtenir des informations sur le segment, telles que la taille de votre audience ou les erreurs qui se sont produites au cours du traitement. Pour savoir comment créer une tâche de segmentation, y compris tous les détails que vous devez fournir, consultez le [guide de développement de tâche de segmentation](../segmentation/api/segment-jobs.md).

Pour évaluer une définition de segment de manière continue, vous pouvez créer et activer un planning. Un planning est un outil qui peut être utilisé pour exécuter automatiquement une tâche de segmentation une fois par jour à une heure donnée. Pour savoir comment créer et activer une planification, vous pouvez suivre les instructions du guide d’API sur le [point de terminaison de plannings](../segmentation/api/schedules.md).

## Exportation des données évaluées

Après avoir créé votre tâche de segmentation ponctuelle ou votre planification en cours, vous pouvez créer une tâche d’exportation de segments pour exporter les résultats vers un jeu de données ou exporter les résultats vers une destination. Les sections suivantes fournissent des conseils sur ces deux options.

### Exportation des données évaluées dans un jeu de données

Après avoir créé votre tâche de segmentation ponctuelle ou votre planification en cours, vous pouvez exporter les résultats en créant une tâche d’exportation de segments. Une tâche d’exportation de segments est une tâche asynchrone qui envoie des informations sur l’audience évaluée à un jeu de données.

Avant de créer une tâche d’exportation, vous devez d’abord créer un jeu de données dans lequel exporter les données. Pour savoir comment créer un jeu de données, reportez-vous à la section sur la [création d’un jeu de données cible](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) du tutoriel sur l’évaluation d’un segment, en vous assurant de noter l’identifiant du jeu de données après sa création. Après avoir créé un jeu de données, vous pouvez créer une tâche d’exportation. Pour savoir comment créer une tâche d’exportation, vous pouvez suivre les instructions du guide d’API sur le [point de terminaison des tâches d’exportation](../segmentation/api/export-jobs.md).

### Exporter vos données évaluées vers une destination

Vous pouvez également, après avoir créé votre tâche de segmentation ponctuelle ou votre planification en cours, exporter les résultats vers une destination. Une destination est un point de terminaison, par exemple une application d’Adobe sur un service externe, où une audience peut être activée et diffusée. Une liste complète des destinations disponibles se trouve dans le [catalogue des destinations](../destinations/catalog/overview.md).

Pour plus d’informations sur l’activation des données vers des destinations de marketing par lots ou par e-mail, consultez le tutoriel [sur l’activation des données d’audience vers des destinations d’exportation de profils par lots à l’aide de l’interface utilisateur de Platform](../destinations/ui/activate-batch-profile-destinations.md) et le [ guide sur la connexion aux destinations par lots et l’activation des données à l’aide de l’API de service de flux](../destinations/api/connect-activate-batch-destinations.md).

## Surveillance de vos activités de données Platform

Platform vous permet de suivre le mode de traitement des données à l’aide de flux de données, qui sont des représentations de tâches qui déplacent des données entre les différents composants de Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, où elles sont ensuite utilisées par [!DNL Identity Service] et [!DNL Real-Time Customer Profile] avant d’être finalement activées vers les destinations. Le tableau de bord de surveillance vous fournit une représentation visuelle du parcours d’un flux de données. Pour savoir comment surveiller les flux de données dans l’interface utilisateur de Platform, consultez les tutoriels sur la [surveillance des flux de données pour les sources](../dataflows/ui/monitor-sources.md) et la [surveillance des flux de données pour les destinations](../dataflows/ui/monitor-destinations.md).

Vous pouvez également surveiller les activités de Platform à l’aide de mesures statistiques et de notifications d’événement à l’aide de [!DNL Observability Insights]. Vous pouvez vous abonner aux notifications d’alerte via l’interface utilisateur de Platform ou les envoyer à un webhook configuré. Pour plus d’informations sur la manière d’afficher, d’activer, de désactiver et de s’abonner aux alertes disponibles à partir de l’interface utilisateur de l’Experience Platform, consultez le [[!UICONTROL guide d’utilisation des alertes]](../observability/alerts/ui.md). Pour plus d’informations sur la façon de recevoir des alertes par le biais de webhooks, consultez le guide sur l’ [abonnement aux notifications d’événement d’Adobe I/O](../observability/alerts/subscribe.md).

## Étapes suivantes

En lisant ce tutoriel, vous avez reçu une introduction de base à un flux de bout en bout simple pour Platform. Pour en savoir plus sur Adobe Experience Platform, consultez la [présentation de Platform](./home.md). Pour en savoir plus sur l’utilisation de l’interface utilisateur de Platform et de l’API de Platform, consultez respectivement le [guide de l’interface utilisateur de Platform](./ui-guide.md) et le [ guide de l’API de Platform](./api-guide.md).
