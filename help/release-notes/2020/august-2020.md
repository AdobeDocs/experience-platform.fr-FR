---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform 10 août 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 89531ad458bd41720090ef2c429376af4460d7c0
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 33%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[ ! Espace de travail scientifique des données DNL]](#dsw)
- [[ !Sources DNL]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour libérer des informations de vos données. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations des machines virtuelles dans [!DNL JupyterLab] | Stabilité des machines [!DNL JupyterLab notebook] virtuelles à long terme améliorée. |

Pour plus d&#39;informations sur [!DNL JupyterLab]cette application, consultez le guide [[!DNL JupyterLab] d&#39;](../../data-science-workspace/jupyterlab/overview.md)utilisation.

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de l&#39;exécution du flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et voir une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Pour plus d&#39;informations, consultez le document des flux [de données de](../../sources/tutorials/ui/monitor.md) surveillance. |
| Mise à jour du compte | Les utilisateurs peuvent mettre à jour les informations d’identification, le nom et la description de tout compte existant afin de fournir des informations plus significatives et de corriger les erreurs qui ont pu être créées. |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des hameçons Web pour recevoir des notifications en temps réel sur l’état, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue de l’interface utilisateur | Mises à jour de l’écran du catalogue de sources pour faciliter l’accès aux actions Principales des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
