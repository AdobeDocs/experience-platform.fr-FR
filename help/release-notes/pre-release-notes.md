---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 30%

---


# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : jeudi 18 juin 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Contrôle d’accès](#access-control)
- [Gestion avancée du cycle de vie des données](#advanced-data-lifecycle-management)
- [Tableaux de bord](#dashboards)
- [Gouvernance des données](#data-governance)
- [Destinations](#destinations)
- [Composition d’audiences fédérées](#fac)
- [Privacy Service](#privacy-service)
- [Service de requête](#query-service)
- [Sandbox](#sandboxes)
- [Sources](#sources)

## Contrôle d’accès {#access-control}

Experience Platform exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des sandbox. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités d’Experience Platform, notamment la modélisation des données, la gestion des profils et l’administration des sandbox.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Autorisation Exporter les données du tableau de bord | Les options **[!UICONTROL Télécharger CSV]** et **[!UICONTROL Envoyer par e-mail]** des tableaux de bord nécessitent désormais l’autorisation **[!UICONTROL Exporter les données du tableau de bord]**. Cette autorisation permet de s’assurer que seuls les utilisateurs autorisés peuvent exporter des données insight tabulées, ce qui permet de renforcer les politiques de gouvernance et de contrôle d’accès aux données. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform fournit un ensemble de fonctionnalités d’hygiène des données qui vous permettent de gérer vos données stockées par le biais de suppressions programmées d’enregistrements et de jeux de données de clients. En utilisant l’espace de travail Cycle de vie des données dans l’interface utilisateur ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| --- | --- |
| Disponibilité générale de la suppression des enregistrements | Vous pouvez désormais supprimer des enregistrements individuels en fonction de champs d’identité à l’aide de l’interface utilisateur ou de l’API. Cette fonctionnalité permet de réduire le stockage, d’appliquer la gouvernance et d’améliorer l’hygiène des données en autorisant les suppressions d’un seul jeu de données ou de tous les jeux de données. Des limites de volume et des exigences de droits s’appliquent. |

Pour plus d’informations, consultez la [présentation de la gestion avancée du cycle de vie des données](../hygiene/home.md).

## Tableaux de bord {#dashboards}

Experience Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes sur les données de votre organisation, telles quʼelles ont été capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Option Envoyer en tant qu’e-mail pour l’exportation | Vous pouvez désormais exporter jusqu’à 10 000 enregistrements des tableaux de bord du mode Query Pro en sélectionnant **[!UICONTROL Envoyer par e-mail]** dans le menu **[!UICONTROL En savoir plus]**. Cette option envoie en toute sécurité un lien de téléchargement à votre e-mail associé à Adobe pour des exportations plus importantes. |

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [présentation des tableaux de bord](../dashboards/home.md).

## Gouvernance des données {#data-governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes et configuration des Places sur la liste autorisée IP Azure CMK | Vous pouvez désormais placer sur la liste autorisée l’adresse IP statique d’Adobe dans Azure Key Vault pour garantir un accès continu lorsque les restrictions réseau sont activées. Cela permet d’éviter les perturbations des services Platform dues à un accès aux clés restreint. |
| Alertes et résolutions de configuration CMK | Experience Platform déclenche désormais des alertes lorsque les services Adobe perdent l’accès à votre coffre de clés Azure (par exemple, en raison d’entrées de place sur la liste autorisée IP supprimées ou de clés désactivées). Un nouveau guide vous aide à comprendre chaque alerte et à prendre des mesures correctives. |

Pour plus d’informations, consultez la [présentation de la gouvernance des données](../data-governance/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| Segments d’utilisateurs en Algérie | La destination Segments d’utilisateurs Algolia permet aux professionnels du marketing de fournir une personnalisation cohérente sur tous les sites, de la page d’accueil à la recherche. Créez des audiences enrichies à partir de plusieurs sources de données et partagez-les sur différents canaux pour améliorer les stratégies de ciblage et la personnalisation des campagnes. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Informations sur l’expiration du compte LinkedIn | Les informations d’expiration de compte pour les destinations LinkedIn sont désormais disponibles directement dans les vues [!UICONTROL Parcourir] et [!UICONTROL Comptes]. Auparavant, ces informations n’étaient disponibles que dans la documentation. Cette amélioration offre une meilleure visibilité sur le statut de l’authentification LinkedIn et la gestion des informations d’identification. |
| Correspondance client Google + disponibilité générale et amélioration de DV360 | La destination Correspondance client Google + DV360 est désormais disponible pour tous les utilisateurs Experience Platform. La documentation comprend désormais des conseils détaillés sur la liaison de comptes entre les comptes publicitaires Adobe et Google. |
| Prise en charge du chiffrement de destination Data Landing Zone (DLZ) | Ajout de la prise en charge du chiffrement pour la destination Data Landing Zone. Vous pouvez désormais joindre des clés publiques au format RSA pour ajouter un chiffrement à vos fichiers exportés. |
| Surveillance au niveau de l’audience pour les destinations d’entreprise | La surveillance au niveau de l’audience est désormais disponible pour les destinations d’entreprise suivantes : [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md) et [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../destinations/home.md).

## Composition d’audiences fédérées {#fac}

La composition de l’audience fédérée permet aux entreprises de composer des données pour une meilleure application dans divers cas d’utilisation. Grâce à cette nouvelle approche, en tant qu’utilisateur Adobe Real-Time Customer Data Platform et/ou Adobe Journey Optimizer, vous pouvez fédérer des jeux de données directement à partir de votre entrepôt de données existant afin de créer et d’enrichir des audiences et des attributs Adobe Experience Platform dans un seul système.

| Nouvelle fonctionnalité | Description |
| ----------- | ----------- |
| Conformité HIPAA | La composition de l’audience fédérée est désormais conforme à la loi HIPAA. Pour plus d’informations sur les mesures de confidentialité et de sécurité de la composition d’audiences fédérées, consultez la [présentation de la confidentialité et de la sécurité dans la composition d’audiences fédérées](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Pour plus d’informations sur la conformité HIPAA des produits Experience Platform en général, consultez la [ Présentation des produits et services HIPAA et Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Pour plus d’informations, consultez la [documentation sur la composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Plusieurs réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles ou de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite l’automatisation de la conformité aux réglementations de confidentialité légales et au sein de l’organisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Prise en charge des lois sur la protection de la vie privée du Tennessee et du Minnesota | Privacy Service prend désormais en charge le Tennessee Information Protection Act (`tipa_tn_usa`) et le Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Vous pouvez traiter les demandes d’accès et de suppression conformément à ces nouvelles réglementations au niveau de l’État. Pour plus d’informations, consultez la [présentation de la réglementation](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview). |

Voir la présentation de [Privacy Service](../privacy-service/home.md) pour plus d’informations sur le service.

## Service de requête {#query-service}

Interrogez des données dans le lac de données Adobe Experience Platform à l’aide de SQL standard avec le service de requête. Combinez facilement des jeux de données et générez de nouveaux jeux à partir des résultats de vos requêtes pour alimenter les rapports, activer les workflows de science des données ou faciliter l’ingestion dans le profil client en temps réel.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Fonctions statistiques avancées | **Intersection d’esquisse thêta** : nouvelle fonction permettant de calculer des intersections prédéfinies à l’aide d’esquisses thêta pour des opérations de comptage et de définition distinctes approximatives. **Histogrammes KLL** : fonctionnalités d’histogramme améliorées à l’aide d’esquisses KLL (Kth smallest, L large, Large items) pour l’estimation quantique et l’analyse de distribution. Ces fonctions sont disponibles pour les clients de Distiller de données. |
| Bibliothèque de modèles SQL | Une bibliothèque complète de modèles SQL pour les cas d’utilisation courants est désormais disponible. Cette fonctionnalité accélère le développement des requêtes en fournissant des modèles de bonnes pratiques pour les modèles analytiques fréquents, ce qui permet aux clients de Data Distiller d’implémenter des analyses complexes plus efficacement. |

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Exemple de modélisation RFM | Ajout d’un exemple complet de modélisation Récence, fréquence, monétaire (RFM) pour les clients de Data Distiller. Cela inclut une documentation détaillée et des guides de mise en œuvre pour la segmentation des clients et l’analyse de valeur à l’aide des techniques RFM. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../query-service/home.md) de Query Service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Migration des mises à jour de la configuration des objets | Vous pouvez désormais migrer les mises à jour de configuration d’objet itératif dans les sandbox après la réplication initiale. Cette amélioration prend en charge les workflows de développement pour lesquels les configurations doivent être mises à jour et propagées dans les environnements sans recréer l’ensemble de la configuration du sandbox. |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../sandboxes/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge d’un nouveau type d’authentification pour [!DNL Azure Synapse Analytics] | Désormais, le [!DNL Azure Synapse Analytics] prend également en charge l’authentification du principal de service, en plus de l’authentification de chaîne de connexion existante. |

**Mises à jour importantes de l’authentification**

| Mise à jour  | Description |
| --- | --- |
| [!DNL Salesforce] l’obsolescence de l’authentification de base | L’authentification de base pour Salesforce CRM et Salesforce Service Cloud sera abandonnée en janvier 2026. Les clients doivent migrer vers l’authentification OAuth 2.0 pour maintenir la connectivité. Cette modification affecte les deux connecteurs source et améliore la sécurité et la conformité aux normes d’authentification Salesforce. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../sources/home.md).
