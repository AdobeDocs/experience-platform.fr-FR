---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform 10 août 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 29%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] dans utilise lʼapprentissage automatique et lʼintelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de lʼensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de la machine virtuelle dans [!DNL JupyterLab] | Amélioration de la stabilité des machines virtuelles [!DNL JupyterLab notebook] à long terme. |

Pour plus d’informations sur [!DNL JupyterLab], consultez le [[!DNL JupyterLab] guide d’utilisation](../../data-science-workspace/jupyterlab/overview.md).

## Destinations  {#destinations}

Dans la [plateforme de données clients en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| [!DNL Google Customer Match] | La correspondance client Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre et réengager vos clients dans les propriétés détenues et exploitées de Google, telles que : [!DNL Search], [!DNL Shopping], Gmail et YouTube. <br><br> Consultez la  [!DNL Google Customer Match] [](../../destinations/catalog/advertising/google-customer-match.md) page du catalogue des destinations pour plus d’informations sur la destination et sur la manière de la configurer dans la plateforme de données clients en temps réel. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Éditeur de nom de fichier personnalisé | Mise à jour du workflow d’activation des données pour les destinations de marketing par e-mail et de stockage dans le cloud qui vous permet de modifier le nom des fichiers exportés. Pour plus d’informations, voir [ Configuration de l’étape](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |
| Attributs recommandés | Mise à jour du workflow d’activation des données pour les destinations de marketing par e-mail et de stockage dans le cloud qui affiche les attributs recommandés à ajouter aux fichiers exportés. Pour plus d’informations, reportez-vous à l’[étape Sélection des attributs](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Basée sur la plateforme de données clients en temps réel des Experience Platform ([!DNL Real-time CDP]), elle permet aux entreprises de rassembler des données connues et inconnues pour activer les profils clients avec une prise de décision intelligente tout au long du parcours client. [!DNL Real-time CDP] combine plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences client personnalisées et individuelles sur tous les canaux et appareils.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge du TCF 2.0 de l’IAB | [!DNL Real-time CDP] est désormais un fournisseur enregistré pour la version 2.0 du  [!DNL Transparency & Consent Framework] (TCF), comme indiqué par l’ [!DNL Interactive Advertising Bureau] (IAB). Vous pouvez configurer vos opérations de données et vos schémas de profil pour accepter les données de consentement du client générées par une CMP et appliquer les préférences de consentement de vos clients lors de l’activation de segments vers des destinations en aval. |

Pour plus d’informations sur [!DNL Real-time CDP], consultez la [[!DNL Real-time CDP] présentation](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de l’exécution du flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et afficher une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Pour plus d’informations, consultez le document [suivi des flux de données](../../sources/tutorials/ui/monitor.md) . |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des webhooks pour recevoir des notifications en temps réel sur l’état, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue de l’interface utilisateur | Mises à jour de l’écran Catalogue de sources pour faciliter l’accès aux Principales actions des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
