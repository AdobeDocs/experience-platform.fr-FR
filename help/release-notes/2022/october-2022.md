---
title: Notes de mise à jour d’octobre 2022 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2022 pour Adobe Experience Platform.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
TQID: https://experienceleague.adobe.com/sjVeNejYDqY6CWOYJCQnc2K0AfyR-Hf7vTZ7GjGDbBc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: e08599ea-8888-4294-ba74-3ba0a7762a46id: ed0d8d0e-04b9-4326-be72-a0fbca265377
subfeature_v2: id: a230274e-7e6e-49eb-b817-514495a710acid: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6id: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1cid: de9975b2-c43a-4287-9698-4f4cad92b83fid: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1204
ht-degree: 87%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 octobre 2022**

- [Clés gérées par le client](#cmk)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Modèle de données d’expérience](#xdm)
- [Service de requête](#query-service)

## Clés gérées par le client {#cmk}

Toutes les données stockées sur Adobe Experience Platform sont chiffrées au repos à l’aide de clés au niveau du système. Si vous utilisez une application reposant sur Experience Platform, vous pouvez désormais choisir d’utiliser vos propres clés de chiffrement pour mieux contrôler la sécurité de vos données.

Consultez la présentation des [clés gérées par le client](../../landing/governance-privacy-security/customer-managed-keys/overview.md) pour plus d’informations sur la fonctionnalité.

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Gestion des données sensibles pour les flux de données | Les flux de données exploitent désormais plusieurs technologies Experience Platform pour gérer de manière appropriée les données sensibles selon les applications des réglementations telles que le Health Insurance Portability and Accountability Act (HIPAA). Consultez la section relative à la [gestion des données sensibles dans les flux de données](../../datastreams/overview.md#sensitive) pour plus d’informations. |
| Extension [!DNL Splunk] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Splunk] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Splunk] ](../../tags/extensions/server/splunk/overview.md). |
| Extension [!DNL Zendesk] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Zendesk] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Zendesk] ](../../tags/extensions/server/zendesk/overview.md). |

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

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Mise à jour du champ `authorized` d’un type booléen en une chaîne. `season` et `episode` ont été changés d’entiers en chaînes. |
| Type de données | [[!UICONTROL Informations détaillées sur ]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` a été renommé `friendlyName` et `ID` a été renommé `name`. |
| Type de données | [[!UICONTROL Informations détaillées sur les erreurs]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` a été renommé `name`. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [vue d’ensemble du système XDM](../../xdm/home.md).

## Service de requête {#query-service}

Le service de requête vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL Data Lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou pour l’ingestion dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Surveiller les requêtes via l’interface utilisateur d’Experience Platform | L’onglet [!UICONTROL Requêtes planifiées] de Query Service offre une meilleure visibilité du statut de tous les traitements de requête à travers l’interface utilisateur. Vous pouvez désormais trouver des informations importantes sur le statut de vos exécutions de requête, y compris des messages d’erreur et des codes en cas d’échec, à partir de l’onglet [!UICONTROL Requêtes planifiées]. Via l’interface utilisateur, vous pouvez également vous abonner à des alertes pour n’importe laquelle de ces requêtes, en fonction de son statut. Consultez le [document sur la surveillance des requêtes](../../query-service/ui/monitor-queries.md) pour en savoir plus sur cette fonctionnalité. |
| Modèle de données d’informations de rapports accélérés par les requêtes | Dans le cadre du SKU Data Distiller, le magasin d’accélération des requêtes vous permet de réduire le temps et la puissance de traitement requis pour obtenir des informations importantes à partir de vos données. Avec le magasin d’accélération des requêtes, vous pouvez créer un modèle de données personnalisé et/ou étendre les modèles de données Adobe Real-time Customer Data Platform existants pour améliorer vos informations de rapports et leurs visualisations. Consultez le [document sur les informations de rapports du magasin d’accélération des requêtes](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) pour en savoir plus sur cette fonctionnalité. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).
Nouvelles fonctionnalités de Adobe Experience Platform :

