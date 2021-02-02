---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform 10 août 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 24%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour libérer des informations de vos données. Intégré dans Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions d’Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de la machine virtuelle dans [!DNL JupyterLab] | Stabilité des machines virtuelles [!DNL JupyterLab notebook] à long terme améliorée. |

Pour plus d&#39;informations sur [!DNL JupyterLab], consultez le [[!DNL JupyterLab] guide de l&#39;utilisateur](../../data-science-workspace/jupyterlab/overview.md).

## Destinations {#destinations}

Dans [Plate-forme de données client en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données à ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| [!DNL Google Customer Match] | La Correspondance avec les clients de Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, comme : [!DNL Search], [!DNL Shopping], Gmail et YouTube. <br><br> Consultez la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) page du catalogue de destinations pour en savoir plus sur la destination et sur la façon de la configurer dans le CDP en temps réel. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Editeur de nom de fichier personnalisé | Mettez à jour le processus d’activation des données pour les destinations de marketing par courrier électronique et les destinations d’enregistrement cloud, ce qui vous permet de modifier le nom des fichiers exportés. Pour plus d&#39;informations, consultez l&#39;[ étape de configuration](../../destinations/ui/activate-destinations.md#configure) dans le processus d&#39;activation. |
| Attributs recommandés | Mettez à jour le processus d’activation des données pour les destinations de marketing par courrier électronique et les destinations d’enregistrement cloud qui affichent les attributs recommandés à ajouter aux fichiers exportés. Pour plus d&#39;informations, reportez-vous à l&#39;[étape de sélection des attributs](../../destinations/ui/activate-destinations.md#select-attributes) dans le processus d&#39;activation. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basée sur la plate-forme de données client en temps réel des Experience Platform ([!DNL Real-time CDP]), elle permet aux sociétés de rassembler des données connues et inconnues pour activer les profils clients avec une prise de décision intelligente dans tout le parcours client. [!DNL Real-time CDP] combine plusieurs sources de données d’entreprise pour créer des profils clients en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences client personnalisées un à un sur tous les canaux et périphériques.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge d’IAB TCF 2.0 | [!DNL Real-time CDP] est maintenant un fournisseur enregistré pour la version 2.0 du  [!DNL Transparency & Consent Framework] (TCF), comme l&#39;indique le  [!DNL Interactive Advertising Bureau] (IAB). Vous pouvez configurer vos opérations de données et vos schémas de profil pour accepter les données de consentement des clients générées par un CMP et appliquer les préférences de consentement de vos clients lors de l’activation de segments vers des destinations en aval. |

Pour plus d&#39;informations sur [!DNL Real-time CDP], voir [[!DNL Real-time CDP] overview](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de l&#39;exécution du flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et voir une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Pour plus d&#39;informations, consultez le document [surveillance des flux de données](../../sources/tutorials/ui/monitor.md). |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des hameçons Web pour recevoir des notifications en temps réel sur l’état, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue de l’interface utilisateur | Mises à jour de l’écran du catalogue de sources pour faciliter l’accès aux actions Principales des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).