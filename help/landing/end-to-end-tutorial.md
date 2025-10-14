---
keywords: Experience Platform;accueil;rubriques populaires;CJA;journey analytics;customer journey analytics;orchestration des campagnes;orchestration;parcours client;parcours;journey orchestration;fonctionnalité;région
title: Exemple de workflow complet de Adobe Experience Platform
description: Découvrez le workflow de base de bout en bout pour Adobe Experience Platform à un niveau élevé.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 11%

---

# Exemple complet de workflow Adobe Experience Platform

Adobe Experience Platform est l’un des meilleurs systèmes ouverts, flexibles et performants du marché permettant de créer et de gérer des solutions complètes qui optimisent l’expérience client. Experience Platform permet aux entreprises de centraliser et de normaliser les données et le contenu des clients à partir de n’importe quel système et d’appliquer la science des données et le machine learning afin d’améliorer considérablement la conception et la diffusion d’expériences riches et personnalisées.

Basé sur des API RESTful, Experience Platform offre toutes les fonctionnalités du système aux développeurs, en facilitant l’intégration des solutions d’entreprise à l’aide d’outils courants. Experience Platform vous permet d’obtenir une vue d’ensemble de vos clients en ingérant vos données client, en segmentant vos données aux audiences que vous souhaitez cibler et en activant ces audiences vers une destination externe. Le tutoriel suivant présente un workflow de bout en bout, montrant toutes les étapes de l’ingestion par le biais de sources à l’activation d’audiences par le biais de destinations.

![Workflow de bout en bout Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Commencer

Ce workflow de bout en bout utilise plusieurs services Adobe Experience Platform. Voici une liste des services utilisés dans ce workflow avec des liens vers leurs vues d’ensemble :

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md) : permet d’obtenir une vue d’ensemble complète de vos clients et de leur comportement en rapprochant des identités entre appareils et systèmes.
- [Sources &#x200B;](../sources/home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
- [[!DNL Segmentation Service]](../segmentation/home.md) : [!DNL Segmentation Service] permet de diviser les données stockées dans [!DNL Experience Platform] qui se rapportent aux individus (tels que les client(e)s, les prospects, les utilisateurs et utilisatrices ou les organisations) en groupes plus petits.
- [[!DNL Real-Time Customer Profile]](../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [Jeux de données](../catalog/datasets/overview.md) : structure de stockage et de gestion pour la persistance des données dans [!DNL Experience Platform].
- [Destinations](../destinations/home.md) : les destinations sont des intégrations préconfigurées aux applications couramment utilisées. Elles permettent l’activation transparente des données d’Experience Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

## Créer un schéma XDM

Avant d’ingérer des données dans Experience Platform, vous devez d’abord créer un schéma XDM pour décrire la structure de ces données. Lorsque vous ingérez vos données à l’étape suivante, vous allez mapper vos données entrantes à ce schéma. Pour savoir comment créer un exemple de schéma XDM, consultez le tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../xdm/tutorials/create-schema-ui.md).

Le tutoriel ci-dessus montre comment définir des champs d’identité pour vos schémas. Un champ d’identité représente un champ qui peut être utilisé pour identifier une personne individuelle liée à un enregistrement ou à un événement de série temporelle. Les champs d’identité sont un composant essentiel dans la construction des graphiques d’identités client dans Experience Platform, ce qui affecte finalement la manière dont le profil client en temps réel fusionne des fragments de données disparates pour obtenir une vue complète du client. Pour plus d’informations sur l’affichage des graphiques d’identités dans Experience Platform, consultez le tutoriel sur [comment utiliser la visionneuse de graphiques d’identités](../identity-service/features/identity-graph-viewer.md).

Vous devez activer votre schéma pour l’utiliser dans le profil client en temps réel afin que les profils client puissent être construits à partir des données en fonction de votre schéma. Pour plus d’informations, consultez la section sur [l’activation d’un schéma pour Profile](../xdm/ui/resources/schemas.md#profile) dans le guide de l’interface utilisateur des schémas.

## Ingestion de données dans Experience Platform

Une fois que vous avez créé un schéma XDM, vous pouvez commencer à importer vos données dans le système.

Toutes les données introduites dans Experience Platform sont stockées dans des jeux de données individuels lors de l’ingestion. Un jeu de données est un ensemble d’enregistrements de données qui correspondent à un schéma XDM spécifique. Avant que vos données puissent être utilisées par [!DNL Real-Time Customer Profile], le jeu de données en question doit être spécifiquement configuré. Pour obtenir des instructions complètes sur l’activation d’un jeu de données pour Profile, consultez le [guide de l’interface utilisateur des jeux de données](../catalog/datasets/user-guide.md#enable-profile) et le [tutoriel de l’API de configuration des jeux de données](../profile/tutorials/dataset-configuration.md). Une fois le jeu de données configuré, vous pouvez commencer à y ingérer des données.

Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, les stockages dans le cloud, les bases de données, etc. Par exemple, vous pouvez ingérer vos données à l’aide de [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Vous trouverez une liste complète des sources disponibles dans la [présentation des connecteurs source](../sources/home.md).

Si vous utilisez Amazon S3 comme connecteur source, vous pouvez suivre les instructions du tutoriel de l’API sur la [création d’un connecteur Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) ou du tutoriel de l’interface utilisateur sur la [création d’un connecteur Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) pour apprendre à créer des données dans le connecteur, à s’y connecter et à les ingérer.

Pour obtenir des instructions plus détaillées sur les connecteurs source, consultez la [présentation des connecteurs source](../sources/home.md). Pour en savoir plus sur le service de flux, l’API sur laquelle les sources sont basées, consultez la [référence de l’API du service de flux](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Une fois que vos données sont importées dans Experience Platform par le biais du connecteur source et stockées dans votre jeu de données activé pour Profil, les profils clients sont automatiquement créés en fonction des données d’identité que vous avez configurées dans votre schéma XDM.

Lors du premier chargement de données vers un nouveau jeu de données ou de la configuration d’un nouveau processus ETL ou d’une nouvelle source de données, il est recommandé de vérifier soigneusement les données afin de s’assurer qu’elles ont été correctement chargées et que les profils générés contiennent les données attendues. Pour plus d’informations sur l’accès aux profils client dans l’interface utilisateur d’Experience Platform, consultez le [guide de l’interface utilisateur du profil client en temps réel](../profile/ui/user-guide.md). Pour plus d’informations sur l’accès aux profils à l’aide de l’API Real-Time Customer Profile, consultez le guide sur l’[utilisation du point d’entrée d’entités](../profile/api/entities.md).

## Évaluation des données

Une fois que vous avez généré des profils à partir des données ingérées, vous pouvez évaluer les données à l’aide de la segmentation. La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble d’individus de votre banque de profils, afin de distinguer un groupe de clients potentiels de votre base de clients. Pour en savoir plus sur la segmentation, veuillez lire la [&#x200B; présentation du service de segmentation &#x200B;](../segmentation/home.md).

### Création d’une définition de segment

Pour commencer, vous devez créer une définition de segment pour regrouper vos clients afin de créer votre audience cible. Une définition de segment est un ensemble de règles que vous pouvez utiliser pour définir l’audience que vous souhaitez cibler. Pour créer une définition de segment, vous pouvez suivre les instructions du guide de l’interface utilisateur lors de l’utilisation du [créateur de segments](../segmentation/ui/segment-builder.md) ou du tutoriel de l’API sur la [création d’un segment](../segmentation/tutorials/create-a-segment.md).

Une fois que vous avez créé une définition de segment, veillez à conserver une note sur l’identifiant de définition de segment.

### Évaluation de votre définition de segment

Après avoir créé votre définition de segment, vous pouvez créer une tâche de segmentation pour évaluer le segment en tant qu’instance unique ou créer un planning pour évaluer le segment de manière continue.

Pour évaluer une définition de segment à la demande, vous pouvez créer une tâche de segmentation. Une tâche de segmentation est un processus asynchrone qui crée un segment d’audience en fonction de la définition de segment et des politiques de fusion référencées. Une politique de fusion est un ensemble de règles utilisé par Experience Platform pour déterminer quelles données seront utilisées pour créer des profils clients et quelles données seront prioritaires en cas d’incohérence entre les sources. Pour savoir comment utiliser les politiques de fusion, consultez le guide de l’interface utilisateur [politiques de fusion](../profile/merge-policies/ui-guide.md).

Une fois la tâche de segmentation créée et évaluée, vous pouvez obtenir des informations sur le segment, telles que la taille de votre audience ou les erreurs qui peuvent s’être produites pendant le traitement. Pour savoir comment créer une tâche de segmentation, y compris tous les détails que vous devez fournir, veuillez lire le guide de développement [tâche de segmentation](../segmentation/api/segment-jobs.md).

Pour évaluer une définition de segment de manière continue, vous pouvez créer et activer un planning. Une planification est un outil qui peut être utilisé pour exécuter automatiquement une tâche de segmentation une fois par jour à une heure donnée. Pour savoir comment créer et activer un planning, vous pouvez suivre les instructions du guide de l’API sur le point d’entrée [plannings](../segmentation/api/schedules.md).

## Exporter les données évaluées

Après avoir créé votre tâche de segmentation ponctuelle ou votre planification continue, vous pouvez créer une tâche d’exportation de segments pour exporter les résultats vers un jeu de données ou exporter les résultats vers une destination. Les sections suivantes fournissent des conseils sur ces deux options.

### Exporter vos données évaluées vers un jeu de données

Après avoir créé votre tâche de segmentation unique ou votre planification continue, vous pouvez exporter les résultats en créant une tâche d’exportation de segments. Une tâche d’exportation de segments est une tâche asynchrone qui envoie des informations sur l’audience évaluée à un jeu de données.

Avant de créer une tâche d’exportation, vous devez d’abord créer un jeu de données vers lequel exporter les données. Pour savoir comment créer un jeu de données, consultez la section sur la [création d’un jeu de données cible](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) dans le tutoriel sur l’évaluation d’un segment, en vous assurant de noter l’identifiant du jeu de données après sa création. Après avoir créé un jeu de données, vous pouvez créer une tâche d’exportation. Pour savoir comment créer une tâche d’exportation, vous pouvez suivre les instructions du guide de l’API relatif au point d’entrée [tâches d’exportation](../segmentation/api/export-jobs.md).

### Exporter vos données évaluées vers une destination

Vous pouvez également exporter les résultats vers une destination après avoir créé votre tâche de segmentation unique ou votre planning continu. Une destination est un point d’entrée, tel qu’une application Adobe sur un service externe, où une audience peut être activée et diffusée. Vous trouverez une liste complète des destinations disponibles dans le [catalogue des destinations](../destinations/catalog/overview.md).

Pour obtenir des instructions sur l’activation des données vers des destinations de marketing par lots ou par e-mail, consultez le tutoriel sur [comment activer les données d’audience vers des destinations d’exportation de profils par lots à l’aide de l’interface utilisateur d’Experience Platform](../destinations/ui/activate-batch-profile-destinations.md) et le [guide sur la connexion à des destinations par lots et l’activation de données à l’aide de l’API Flow Service](../destinations/api/connect-activate-batch-destinations.md).

## Surveillance des activités liées aux données d’Experience Platform

Experience Platform vous permet de suivre le traitement des données par l’utilisation des flux de données, qui sont des représentations des tâches qui déplacent les données entre les différents composants d’Experience Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, où elles sont ensuite utilisées par les [!DNL Identity Service] et les [!DNL Real-Time Customer Profile] avant d’être finalement activées vers les destinations. Le tableau de bord de surveillance vous fournit une représentation visuelle du parcours d’un flux de données. Pour découvrir comment surveiller les flux de données dans l’interface utilisateur d’Experience Platform, consultez les tutoriels sur [surveillance des flux de données pour les sources](../dataflows/ui/monitor-sources.md) et [surveillance des flux de données pour les destinations](../dataflows/ui/monitor-destinations.md).

Vous pouvez également surveiller les activités d’Experience Platform à l’aide de mesures statistiques et de notifications d’événement [!DNL Observability Insights]. Vous pouvez vous abonner aux notifications d’alerte par le biais de l’interface utilisateur d’Experience Platform ou les envoyer à un webhook configuré. Pour plus d’informations sur l’affichage, l’activation, la désactivation et l’abonnement aux alertes disponibles depuis l’interface utilisateur d’Experience Platform, consultez le guide de l’interface utilisateur [[!UICONTROL Alertes]](../observability/alerts/ui.md). Pour plus d’informations sur la réception d’alertes par le biais de Webhooks, consultez le guide sur [l’abonnement aux notifications d’événement d’Adobe I/O](../observability/alerts/subscribe.md).

## Étapes suivantes

Ce tutoriel vous a permis de bénéficier d’une introduction générale à un flux simple de bout en bout pour Experience Platform. Pour en savoir plus sur Adobe Experience Platform, veuillez lire la [présentation d’Experience Platform](./home.md). Pour en savoir plus sur l’utilisation de l’interface utilisateur d’Experience Platform et de l’API Experience Platform, veuillez lire respectivement le [guide de l’interface utilisateur d’Experience Platform](./ui-guide.md) et le [guide de l’API Experience Platform](./api-guide.md).
