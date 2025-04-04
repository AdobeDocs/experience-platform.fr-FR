---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2020
description: Les notes de mise à jour d’août 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 38%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utilise le machine learning et l’intelligence artificielle pour libérer des informations à partir de vos données. Intégré à Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de lʼensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations des machines virtuelles dans [!DNL JupyterLab] | Amélioration de la stabilité des machines virtuelles [!DNL JupyterLab notebook] de longue durée d’exécution. |

Pour plus d’informations sur [!DNL JupyterLab], veuillez consulter le [[!DNL JupyterLab] guide de l’utilisateur](../../data-science-workspace/jupyterlab/overview.md).

## Destinations {#destinations}

Dans [Real-Time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées à des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| [!DNL Google Customer Match] | Le ciblage par correspondance des clients de Google vous permet d’utiliser vos données en ligne et hors ligne pour contacter et réengager vos clients dans les propriétés détenues et exploitées par Google, telles que : [!DNL Search], [!DNL Shopping], Gmail et YouTube. <br><br> Consultez la [!DNL Google Customer Match] [page](../../destinations/catalog/advertising/google-customer-match.md) du catalogue des destinations pour plus d’informations sur la destination et sur la manière de la configurer dans Real-Time CDP. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Éditeur de nom de fichier personnalisé | Mettez à jour vers le workflow d’activation des données pour les destinations de marketing par e-mail et les destinations d’espace de stockage qui vous permet de modifier le nom des fichiers exportés. Pour plus d’informations, reportez-vous à l’étape [Configurer](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |
| Attributs recommandés | Mettez à jour vers le workflow d’activation des données pour les destinations de marketing par e-mail et les destinations d’espace de stockage qui affiche les attributs recommandés que vous pouvez ajouter aux fichiers exportés. Pour plus d’informations, reportez-vous à l’étape [Sélectionner des attributs](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basée sur Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) aide les entreprises à rassembler des données connues et inconnues pour activer les profils des clients et clientes avec une prise de décision intelligente tout au long du parcours client. [!DNL Real-Time CDP] associe plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences personnalisées et individuelles aux clients et clientes sur tous les canaux et appareils.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’IAB TCF 2.0 | [!DNL Real-Time CDP] est désormais un fournisseur enregistré pour la version 2.0 du [!DNL Transparency & Consent Framework] (TCF), comme indiqué par l’[!DNL Interactive Advertising Bureau] (IAB). Vous pouvez configurer vos opérations de données et schémas de profil pour accepter les données de consentement des clients générées par une CMP et appliquer les préférences de consentement de vos clients lors de l’activation de segments vers des destinations en aval. |

Pour plus d’informations sur [!DNL Real-Time CDP], consultez la présentation [[!DNL Real-Time CDP] ](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance d’exécution de flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et consulter une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Consultez le document [surveillance des flux de données](../../sources/tutorials/ui/monitor.md) pour plus d’informations. |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des webhooks pour recevoir des notifications en temps réel sur le statut, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue d’interfaces utilisateur | Mises à jour de l’écran de catalogue des sources pour faciliter l’accès aux actions principales des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
