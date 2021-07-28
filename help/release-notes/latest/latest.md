---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour de l’Experience Platform pour le 28 juillet 2021.
doc-type: release notes
last-update: July 28, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: dc01e03975fdda375b31f44edc8459fa32b5a61b
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 65%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 28 juillet 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Data Science Workspace](#dsw)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sources](#sources)

## Data Science Workspace {#dsw}

Data Science Workspace utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour de bibliothèque et de système d’exploitation | Data Science Workspace a effectué d’importantes mises à jour de bibliothèque et de système d’exploitation afin d’améliorer les fonctionnalités et la convivialité. Cela inclut JupyterLab 1.2.20, Python 3.7, Pandas 1.2.4, Tensorflow 2.4.1 avec prise en charge de CUDA 11 et de CUDNN 8, etc. Pour découvrir comment afficher les bibliothèques disponibles dans JupyterLab, consultez la section [Bibliothèques prises en charge](../../data-science-workspace/jupyterlab/overview.md#supported-libraries) de la documentation de présentation des notebooks JupyterLab. |

Pour plus d’informations sur Data Science Workspace, consultez la [Présentation de Data Science Workspace](../../data-science-workspace/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

Le modèle de données d’expérience (XDM) est une spécification open source conçue pour améliorer la puissance des expériences digitales. Il fournit des structures et des définitions communes pour les données sous la forme de schémas, qui permettent à toute application de communiquer avec les services Platform.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Filtre de l&#39;industrie des télécommunications | Lors de l’ajout de groupes de champs à un schéma dans l’interface utilisateur, vous pouvez désormais filtrer selon le secteur des télécommunications. Consultez le [diagramme des relations d’entité du secteur des télécommunications (ERD)](../../xdm/schema/industries/telecom.md) pour afficher un modèle de données recommandé pour les cas d’utilisation des télécommunications. |

Pour plus d’informations sur XDM dans Platform, reportez-vous à la [Présentation du système XDM](../../xdm/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Amazon Redshift]](../../sources/connectors/databases/redshift.md)</li><li>[[!DNL Azure Table Storage]](../../sources/connectors/databases/ats.md)</li><li>[[!DNL PayPal]](../../sources/connectors/payments/paypal.md)</li></ul> |
| [!DNL Salesforce Marketing Cloud] (version bêta) | Vous pouvez désormais connecter [!DNL Salesforce Marketing Cloud] à Experience Platform à lʼaide de lʼAPI [!DNL Flow Service] ou de lʼinterface utilisateur. Pour plus d’informations, consultez la [[!DNL Salesforce Marketing Cloud] présentation du connecteur](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
