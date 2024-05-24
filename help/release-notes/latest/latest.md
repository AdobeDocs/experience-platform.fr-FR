---
title: Notes de mise à jour d’Adobe Experience Platform - Mai 2024
description: Les notes de mise à jour de mai 2024 pour Adobe Experience Platform.
source-git-commit: e02892a2cbf5f65a1b9a0eec49722896bd061084
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 24%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : mercredi 21 mai 2024**

>[!TIP]
>
>La variable [Documentation de l’API Experience Platform](https://developer.adobe.com/experience-platform-apis/) est désormais interactif. Explorez les points de terminaison de l’API directement à partir des pages de documentation pour obtenir des commentaires immédiats et accélérer votre mise en oeuvre technique. [En savoir plus](#interactive-api-documentation) à propos de la nouvelle fonctionnalité.

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Service de catalogue](#catalog-service)
- [Tableaux de bord](#dashboards)
- [Gouvernance des données](#governance)
- [Destinations](#destinations)
- [Query Service](#query-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

Autres mises à jour dans Adobe Experience Platform :

- [Mises à jour de la documentation](#documentation-updates)

## Catalog Service {#catalog-service}

Le Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous la forme de fichiers et de répertoires, le catalogue contient les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Actions en bloc | L’inventaire des jeux de données prend désormais en charge les actions en bloc. Rationalisez vos processus de gestion des données et garantissez une gestion efficace de vos jeux de données avec des actions en bloc. Utilisez des actions en bloc pour gagner du temps en exécutant plusieurs actions simultanément sur de nombreux jeux de données.  Les actions en bloc incluent : [Déplacer vers le dossier](../../catalog/datasets/user-guide.md#move-to-folders), [Modifier les balises](../../catalog/datasets/user-guide.md#manage-tags), et [Supprimer](../../catalog/datasets/user-guide.md#delete) jeux de données. <br> ![Actions en bloc dans l’espace de travail de l’interface utilisateur des jeux de données.](../2024/assets/may/bulk-actions.png "Actions en bloc dans l’espace de travail de l’interface utilisateur des jeux de données."){width="100" zoomable="yes"} <br> Pour plus d’informations sur cette fonctionnalité, consultez la section [Guide de l’interface utilisateur des jeux de données](../../catalog/datasets/user-guide.md#bulk-actions). |

{style="table-layout:auto"}

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Informations personnalisables pour la création de rapports d’application étendue | En toute transparence [transition de la sortie de l’analyse SQL vers des formats visuels compréhensibles et conviviaux](../../dashboards/data-distiller/customizable-insights/overview.md). Utilisez des requêtes SQL personnalisées pour une manipulation de données précise et la création de graphiques dynamiques à partir de différents jeux de données structurés. Vous pouvez utiliser le mode query pro pour effectuer une analyse complexe avec SQL, puis partager cette analyse avec des utilisateurs non techniques par le biais de graphiques sur votre tableau de bord personnalisé ou les exporter dans des fichiers CSV. |

{style="table-layout:auto"}

## Gouvernance des données {#governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de mTLS pour les destinations d’API HTTP et les actions personnalisées de Adobe Journey Optimizer | Configurez la confiance des clients grâce aux mesures de sécurité renforcées du protocole mTLS (Mutual Transport Layer Security). La variable [Destination de l’API HTTP Experience Platform](../../destinations/catalog/streaming/http-destination.md#mtls-protocol-support) et [Actions personnalisées Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) prend désormais en charge le protocole mTLS lors de l’envoi de données à des points de terminaison configurés. Aucune configuration supplémentaire n’est requise dans votre action personnalisée ou votre destination d’API HTTP pour activer mTLS. Ce processus se produit automatiquement lorsqu’un point d’entrée compatible mTLS est détecté. Vous pouvez [télécharger le certificat public Adobe Journey Optimizer ici](../../landing/governance-privacy-security/encryption.md#download-certificates) et la variable [Certificat public du service Destinations ici](../../landing/governance-privacy-security/encryption.md#download-certificates).<br>Voir [Documentation sur le cryptage des données Experience Platform](../../landing/governance-privacy-security/encryption.md#mtls-protocol-support) pour plus d’informations sur les protocoles de connexion réseau lors de l’exportation de données vers des systèmes tiers. |

{style="table-layout:auto"}

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Réorganiser les champs de mappage pour les destinations par lots | Vous pouvez désormais modifier l’ordre des colonnes dans vos exportations CSV en faisant glisser les champs de mappage dans la variable [étape de mappage](../../destinations/ui/activate-batch-profile-destinations.md#mapping). L’ordre des champs mappés dans l’interface utilisateur se reflète dans l’ordre des colonnes du fichier CSV exporté, de haut en bas, la rangée supérieure étant la colonne la plus à gauche du fichier CSV. <br> ![Vue de la façon dont les mappages peuvent être réorganisés.](../2024/assets/may/reorder-mappings.gif "Vue de la façon dont les mappages peuvent être réorganisés."){width="100" zoomable="yes"} |
| Présélection des planifications d’exportation par défaut pour les destinations par lot | Experience Platform définit désormais automatiquement un planning par défaut pour chaque export de fichier. Consultez la documentation relative à [planification des exports d’audience](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) pour savoir comment modifier le planning par défaut. |
| Modification des plannings d’activation de plusieurs audiences pour les destinations par lots | Vous pouvez désormais modifier le planning d’activation de plusieurs audiences exportées vers une destination par lot (basée sur un fichier) à partir du **[!UICONTROL Données d’activation]** de la [page des détails de la destination](../../destinations/ui/destination-details-page.md#bulk-edit-schedule). <br> ![Vue de la sélection de plusieurs audiences et de la modification du planning d’exportation de fichiers.](../2024/assets/may/bulk-edit-schedule.gif "Vue de la sélection de plusieurs audiences et de la modification du planning d’exportation de fichiers."){width="100" zoomable="yes"} |
| Exportation de plusieurs audiences à la demande vers des destinations par lots | Vous pouvez désormais sélectionner et exporter plusieurs audiences vers les destinations par lot, au moyen de l’option [exporter des fichiers à la demande](../../destinations/ui/export-file-now.md) . |

{style="table-layout:auto"}

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Éditeur hérité obsolète | L’ancien éditeur est obsolète et n’est plus accessible. Vous pouvez utiliser le [fonctionnalités améliorées de Query Editor](../../query-service/ui/user-guide.md#query-authoring) pour écrire, valider et exécuter vos requêtes. |
| Délai d’exécution de requête | Contrôlez les heures de votre ordinateur en définissant des alertes pour les retards d’exécution des requêtes. Vous pouvez choisir de recevoir des alertes si l’état d’une requête ne change pas après une période spécifique. Il vous suffit de définir le délai souhaité dans l’interface utilisateur de Platform pour rester informé de la progression de votre requête. Pour savoir comment définir cette alerte dans l’interface utilisateur, reportez-vous à la section [documentation sur les plannings de requête](../../query-service/ui/query-schedules.md#alerts-for-query-status) ou le [guide des actions de requête intégrées](../../query-service/ui/monitor-queries.md#query-run-delay). |
| Inventaire des logs de requête rationalisé | Vous pouvez désormais utiliser une efficacité améliorée pour le dépannage et la surveillance des tâches avec un [interface utilisateur des journaux de requêtes simplifiés](../../query-service/ui/query-logs.md#filter-logs): <ul><li> Par défaut, l’interface utilisateur de Platform exclut toutes les &quot;requêtes système&quot; de l’onglet des journaux. </li><li> Afficher les requêtes système en décochant **Exclure les requêtes système**. </li></ul> <br> ![Onglet Journaux dans l’espace de travail de l’interface utilisateur des requêtes.](../2024/assets/may/query-log.png "Onglet Journaux dans l’espace de travail de l’interface utilisateur des requêtes."){width="100" zoomable="yes"} <br> Utilisez l’interface utilisateur des journaux de requêtes rationalisée pour obtenir une vue plus précise qui vous aide à identifier et à analyser rapidement les journaux pertinents. |
| Sélecteur de base de données | Utilisez le menu déroulant du nouveau sélecteur de base de données pour [accéder facilement aux vues de données du Customer Journey Analytics depuis Power BI ou Tableau ;](../../query-service/ui/credentials.md#connect-to-customer-journey-analytics). Vous pouvez désormais sélectionner la base de données de votre choix directement dans l’interface utilisateur de Platform pour une intégration plus transparente de vos outils de BI. <br> ![Onglet Informations d’identification dans l’espace de travail de l’interface utilisateur Requêtes.](../2024/assets/may/database-selector.png "Onglet Informations d’identification dans l’espace de travail de l’interface utilisateur Requêtes."){width="100" zoomable="yes"} <br> |

{style="table-layout:auto"}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Importation d’audiences générées en externe | L’import d’audiences générées en externe nécessite désormais l’autorisation &quot;Importer une audience&quot;. Pour en savoir plus sur les autorisations, lisez le [guide de l’interface utilisateur des autorisations](../../access-control/home.md#permissions). |

{style="table-layout:auto"}

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Authentification des informations d’identification client OAuth2 pour [!DNL Salesforce] source | Vous pouvez désormais utiliser les informations d’identification du client OAuth2 pour authentifier votre [!DNL Salesforce] sur Experience Platform. Lisez la section [!DNL Salesforce] source [Guide de l’API](../../sources/tutorials/api/create/crm/salesforce.md) et [Guide de l’interface utilisateur](../../sources/tutorials/ui/create/crm/salesforce.md) pour plus d’informations. |
| Prise en charge d’exemples de flux de données pour le [!DNL Marketo Engage] source | La variable [!DNL Marketo Engage] source prend désormais en charge les exemples de flux de données. Activez l’exemple de configuration de flux de données pour limiter votre taux d’ingestion, puis essayez des fonctionnalités Experience Platform sans avoir à ingérer de grandes quantités de données. Pour plus d’informations, consultez le guide sur [création d’un flux de données pour [!DNL Marketo Engage] dans l’interface utilisateur](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |
| Mises à jour de la liste autorisée d’adresses IP | Selon votre emplacement, vous devez ajouter un ensemble d’adresses IP à votre liste autorisée pour utiliser correctement les sources en continu. Pour obtenir une liste complète des nouvelles adresses IP, lisez le [Guide de liste autorisée des adresses IP](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour**

| Documentation mise à jour | Description |
| --- | --- |
| Mises à jour de la documentation pour [!DNL Google PubSub] | La variable [!DNL Google PubSub] mise à jour de la documentation source avec un guide prérequis complet - Utilisez la nouvelle section Conditions préalables pour savoir comment créer votre compte de service, accorder des autorisations au niveau de la rubrique ou de l’abonnement et définir des configurations afin d’optimiser l’utilisation de la variable [!DNL Google PubSub] source. Lisez la section [[!DNL Google PubSub] aperçu](../../sources/connectors/cloud-storage/google-pubsub.md) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Mises à jour de la documentation {#documentation-updates}

### Documentation de l’API d’Experience Platform interactif {#interactive-api-documentation}

La variable [Documentation de l’API Experience Platform](https://developer.adobe.com/experience-platform-apis/) est désormais interactif. Toutes les pages de référence d’API ont désormais une **Essayez-le** . Cette fonctionnalité vous permet de tester les appels d’API directement sur la page du site web de documentation. [Obtention des informations d’authentification requises](/help/landing/api-authentication.md) et commencez à utiliser la fonctionnalité pour explorer les points de terminaison de l’API.

Utilisez cette nouvelle fonctionnalité pour explorer les requêtes envoyées à et les réponses provenant des points de terminaison de l’API, afin d’obtenir des commentaires immédiats et d’accélérer votre mise en oeuvre technique. Par exemple, consultez la [API Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/) ou le [API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) points de terminaison pour explorer la nouvelle **Essayez-le** dans le rail de droite.

![Enregistrement d’écran montrant un appel API effectué directement à partir du site web de documentation.](../2024/assets/may/api-playground-demo.gif)

>[!CAUTION]
>
>Gardez à l’esprit qu’en utilisant la fonctionnalité d’API interactive sur les pages de documentation, vous effectuez de vrais appels d’API vers les points de terminaison . Gardez cela à l’esprit lorsque vous testez des environnements de test de production.

### Informations et engagement personnalisés {#personalized-insights-engagement}

Nouvelle page de documentation de cas d’utilisation de bout en bout pour [évolution de la valeur unique à la valeur de durée de vie](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/evolve-one-time-value-to-lifetime-value.md) est maintenant en ligne. Lisez cette documentation pour comprendre comment utiliser Real-Time CDP et Adobe Journey Optimizer pour convertir des visiteurs sporadiques en propriétés web en clients fidèles.
