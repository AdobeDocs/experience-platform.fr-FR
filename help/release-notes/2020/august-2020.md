---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform 10 août 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 23%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour libérer des informations de vos données. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations des machines virtuelles dans [!DNL JupyterLab] | Stabilité des machines [!DNL JupyterLab notebook] virtuelles à long terme améliorée. |

Pour plus d&#39;informations sur [!DNL JupyterLab]cette application, consultez le guide [[!DNL JupyterLab] d&#39;](../../data-science-workspace/jupyterlab/overview.md)utilisation.

## Destinations {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), destinations are pre-built integrations with destination platforms that activate data to those partners in a seamless way.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| [!DNL Google Customer Match] | La Correspondance avec les clients de Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, comme : [!DNL Search], [!DNL Shopping], Gmail et YouTube. <br><br> Consultez la [!DNL Google Customer Match] page [](/help/rtcdp/destinations/google-customer-match-destination.md) du catalogue de destinations pour en savoir plus sur la destination et sur la façon de la configurer dans le CDP en temps réel Adobe. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Editeur de nom de fichier personnalisé | Mettez à jour le processus d’activation des données pour les destinations de marketing par courrier électronique et les destinations d’enregistrement cloud, ce qui vous permet de modifier le nom des fichiers exportés. Pour plus d&#39;informations, reportez-vous à l&#39;étape [](/help/rtcdp/destinations/activate-destinations.md#configure) Configurer du processus d&#39;activation. |
| Attributs recommandés | Mettez à jour le processus d’activation des données pour les destinations de marketing par courrier électronique et les destinations d’enregistrement cloud qui affichent les attributs recommandés à ajouter aux fichiers exportés. Pour plus d&#39;informations, reportez-vous à l&#39;étape [](/help/rtcdp/destinations/activate-destinations.md#select-attributes) Sélectionner des attributs dans le processus d&#39;activation. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Built on Experience Platform, Real-time Customer Data Platform ([!DNL Real-time CDP]) helps companies bring together known and unknown data to activate customer profiles with intelligent decisioning throughout the customer journey. [!DNL Real-time CDP] combine plusieurs sources de données d’entreprise pour créer des profils clients en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences client personnalisées un à un sur tous les canaux et périphériques.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge d’IAB TCF 2.0 | [!DNL Real-time CDP] est maintenant un fournisseur enregistré pour la version 2.0 du [!DNL Transparency & Consent Framework] (TCF), comme indiqué par le [!DNL Interactive Advertising Bureau] (IAB). Vous pouvez configurer vos opérations de données et vos schémas de profil pour accepter les données de consentement des clients générées par un CMP et appliquer les préférences de consentement de vos clients lors de l’activation de segments vers des destinations en aval. Pour plus d’informations, consultez l’aperçu de la prise en charge [d’IAB TCF 2.0 dans le CDP](../../rtcdp/privacy/iab/overview.md) en temps réel. |

Pour plus d&#39;informations sur [!DNL Real-time CDP]cette application, consultez la [[!DNL Real-time CDP] présentation](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de l&#39;exécution du flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et voir une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Pour plus d&#39;informations, consultez le document des flux [de données de](../../sources/tutorials/ui/monitor.md) surveillance. |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des hameçons Web pour recevoir des notifications en temps réel sur l’état, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue de l’interface utilisateur | Mises à jour de l’écran du catalogue de sources pour faciliter l’accès aux actions Principales des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).