---
title: Notes de mise à jour d’octobre 2022 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2022 pour Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 90%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 octobre 2022**

- [Clés gérées par le client](#cmk)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience](#xdm)
- [Query Service](#query-service)

## Clés gérées par le client {#cmk}

Toutes les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Experience Platform, vous pouvez désormais choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

Consultez la présentation des [clés gérées par le client](../../landing/governance-privacy-security/customer-managed-keys/overview.md) pour plus d’informations sur la fonctionnalité.

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Gestion des données sensibles pour les flux de données | Les flux de données exploitent désormais plusieurs technologies Experience Platform pour gérer de manière appropriée les données sensibles selon les applications des réglementations telles que le Health Insurance Portability and Accountability Act (HIPAA). Consultez la section relative à la [gestion des données sensibles dans les flux de données](../../datastreams/overview.md#sensitive) pour plus d’informations. |
| Extension [!DNL Splunk] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Splunk] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Splunk] &#x200B;](../../tags/extensions/server/splunk/overview.md). |
| Extension [!DNL Zendesk] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Zendesk] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Zendesk] &#x200B;](../../tags/extensions/server/zendesk/overview.md). |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Exportations de jeux de données (version Beta) | La [fonctionnalité d’exportation des jeux de données en version Beta](/help/destinations/ui/export-datasets.md) vous permet d’exporter des données de première génération (comme défini dans la [description du produit Real-time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) depuis Adobe Experience Platform vers vos propres systèmes clients externes, via l’interface utilisateur des destinations. Vous pouvez ainsi extraire des données d’Experience Platform avec un workflow sans code, ou à faible code, vers six destinations de stockage dans le cloud (répertoriées dans le tableau ci-dessous) à des fins d’analyse et de conformité. |
| Amélioration des capacités d’exportation de fichiers (version Beta) | Vous pouvez désormais bénéficier d’une fonctionnalité de personnalisation améliorée lors de l’exportation de fichiers en dehors d’Experience Platform : <br><ul><li>[Options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) supplémentaires.</li><li>Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via l’[étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Possibilité de personnaliser le formatage des fichiers de données exportés au format CSV](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Cette fonctionnalité est prise en charge par les six nouvelles cartes de stockage cloud Beta répertoriées dans le tableau ci-dessous. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#new-or-updated-destinations}

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line est une plateforme de communication populaire qui connecte les personnes, les services et l’information et est passée d’une application de chat à un centre de divertissement, social et d’activités quotidiennes. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 est une plateforme d’applications métier cloud qui combine la planification des ressources de l’entreprise (ERP) et la gestion de la relation client (CRM), ainsi que des applications de productivité et des outils d’IA, afin d’offrir des opérations de bout en bout plus fluides et plus contrôlées, un meilleur potentiel de croissance et des coûts réduits. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Le connecteur de destination [!DNL (Beta) Adobe Commerce] vous permet de sélectionner un ou plusieurs segments Real-Time CDP à activer dans votre compte [!DNL Adobe Commerce] pour offrir une expérience personnalisée dynamique à vos clients. Dans [!DNL Adobe Commerce], vous pouvez ensuite sélectionner ces segments Real-Time CDP pour personnaliser les offres exceptionnelles du panier, telles que « Pour deux produits achetés, le troisième est offert ». Vous pouvez également afficher des bannières principales et modifier le prix des produits par le biais d’offres promotionnelles, toutes personnalisées en fonction des segments Adobe Real-Time CDP. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Créez une connexion sortante active vers [!DNL Azure Data Lake Storage Gen2] pour exporter régulièrement des fichiers de données d’Adobe Experience Platform vers votre propre emplacement de stockage. Cette nouvelle destination Beta fournit une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform. Elle vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers en dehors d’Experience Platform. Cette nouvelle destination Beta fournit une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Créez une connexion sortante active vers [!DNL Google Cloud Storage] pour exporter régulièrement des fichiers de données d’Adobe Experience Platform dans vos propres compartiments. Cette nouvelle destination Beta fournit une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Deux cartes de destination [!DNL Amazon S3] apparaissent désormais côte à côte dans le catalogue des destinations pour les personnes participant à la phase Beta. La nouvelle destination Beta offre une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Deux cartes de destination [!DNL Azure Blob] apparaissent désormais côte à côte dans le catalogue des destinations pour les personnes participant à la phase Beta. La nouvelle destination Beta offre une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Deux cartes de destination [!DNL SFTP] apparaissent désormais côte à côte dans le catalogue des destinations pour les personnes participant à la phase Beta. La nouvelle destination Beta offre une fonctionnalité améliorée d’exportation de fichiers et prend en charge les exportations de jeux de données. |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour**

| Documentation | Description |
| ----------- | ----------- |
| [Mécanismes de sécurisation des destinations](../../destinations/guardrails.md) | Cette page fournit des limites d’utilisation et de débit par défaut en ce qui concerne le comportement d’activation. |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Mise à jour du champ `authorized` d’un type booléen en une chaîne. `season` et `episode` ont été changés d’entiers en chaînes. |
| Type de données | [[!UICONTROL Informations détaillées sur la publicité]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` a été renommé `friendlyName` et `ID` a été renommé `name`. |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` a été renommé `name`. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [&#x200B; Présentation du système XDM &#x200B;](../../xdm/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Surveiller les requêtes via l’interface utilisateur d’Experience Platform | L’onglet [!UICONTROL Requêtes planifiées] de Query Service offre une visibilité améliorée du statut de tous les traitements de requêtes à travers l’interface utilisateur. Vous pouvez maintenant retrouver des informations importantes sur le statut de vos exécutions de requête, y compris des messages d’erreur et des codes en cas d’échec, depuis l’onglet [!UICONTROL Requêtes planifiées]. Via l’interface utilisateur, vous pouvez également vous abonner à des alertes pour n’importe laquelle de ces requêtes, en fonction de son statut. Consultez le [document sur la surveillance des requêtes](../../query-service/ui/monitor-queries.md) pour en savoir plus sur cette fonctionnalité. |
| Modèle de données d’informations de rapports accélérés par les requêtes | Dans le cadre du SKU Data Distiller, le magasin d’accélération des requêtes vous permet de réduire le temps et la puissance de traitement requis pour obtenir des informations importantes à partir de vos données. Avec le magasin d’accélération des requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre les modèles de données Adobe Real-time Customer Data Platform existants pour améliorer vos informations de rapports et leurs visualisations. Consultez le [document sur les informations de rapports du magasin d’accélération des requêtes](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) pour en savoir plus sur cette fonctionnalité. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la [présentation de Query Service](../../query-service/home.md).
Nouvelles fonctionnalités d’Adobe Experience Platform :

