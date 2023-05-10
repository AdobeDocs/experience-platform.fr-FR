---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2020
description: Les notes de mise à jour d’août 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 31%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 12 août 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] dans utilise lʼapprentissage automatique et lʼintelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de lʼensemble des solutions Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Améliorations de la machine virtuelle dans [!DNL JupyterLab] | Amélioration de la stabilité des opérations de longue durée [!DNL JupyterLab notebook] machines virtuelles. |

Pour plus d’informations sur [!DNL JupyterLab], reportez-vous à la section [[!DNL JupyterLab] guide de l’utilisateur](../../data-science-workspace/jupyterlab/overview.md).

## Destinations {#destinations}

Dans [Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

De nouvelles destinations vous permettent d’activer vos données Adobe Experience Platform. Voir ci-dessous pour plus de détails :

| Destination | Description |
|--- | ---|
| [!DNL Google Customer Match] | La correspondance client Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées de Google, telles que : [!DNL Search], [!DNL Shopping], Gmail et YouTube. <br><br> Visitez le [!DNL Google Customer Match] [page](../../destinations/catalog/advertising/google-customer-match.md) dans le catalogue des destinations pour plus d’informations sur la destination et sur la manière de la configurer dans Real-Time CDP. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|------- | -----------|
| Éditeur de nom de fichier personnalisé | Mise à jour du workflow d’activation des données pour les destinations de marketing par e-mail et de stockage dans le cloud qui vous permet de modifier le nom des fichiers exportés. Pour plus d’informations, reportez-vous à la section [ Configuration de l’étape](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |
| Attributs recommandés | Mise à jour du workflow d’activation des données pour les destinations de marketing par e-mail et de stockage dans le cloud qui affiche les attributs recommandés à ajouter aux fichiers exportés. Pour plus d’informations, reportez-vous à la section [Étape Sélectionner des attributs](../../destinations/ui/activate-batch-profile-destinations.md) dans le workflow d’activation. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basé sur Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) permet aux entreprises de rassembler des données connues et inconnues pour activer les profils clients avec une prise de décision intelligente tout au long du parcours client. [!DNL Real-Time CDP] combine plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences client personnalisées et individuelles sur tous les canaux et appareils.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de l’IAB TCF 2.0 | [!DNL Real-Time CDP] est désormais un fournisseur enregistré pour la version 2.0 de la variable [!DNL Transparency & Consent Framework] (TCF), comme indiqué par [!DNL Interactive Advertising Bureau] (IAB). Vous pouvez configurer vos opérations de données et vos schémas de profil pour accepter les données de consentement du client générées par une CMP et appliquer les préférences de consentement de vos clients lors de l’activation de segments vers des destinations en aval. |

Pour plus d’informations sur [!DNL Real-Time CDP], reportez-vous à la section [[!DNL Real-Time CDP] aperçu](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de l’exécution du flux | Les utilisateurs peuvent surveiller toutes les exécutions de flux et afficher une vue détaillée de chaque exécution, y compris l’état d’achèvement, la durée d’exécution, la liste des fichiers traités, les erreurs et les mesures. Voir [suivi des flux de données](../../sources/tutorials/ui/monitor.md) pour plus d’informations. |
| Notifications d’exécution de flux | Les utilisateurs peuvent s’abonner à des événements et enregistrer des webhooks pour recevoir des notifications en temps réel sur l’état, les mesures et les erreurs concernant les exécutions de flux. |
| Améliorations du catalogue de l’interface utilisateur | Mises à jour de l’écran Catalogue de sources pour faciliter l’accès aux Principales actions des objets sélectionnés. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
