---
title: Notes de mise à jour de Adobe Experience Platform, décembre 2019
description: Notes de mise à jour de décembre 2019 pour Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 72%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Onglet Audiences fusionnées dans [!DNL Segment Builder] | Le [!UICONTROL Segments] et [!UICONTROL Audiences] dans les onglets [!DNL Segment Builder] ont été combinés en une seule [!UICONTROL Audiences] . Cet onglet vous permet de parcourir et de rechercher les audiences existantes, que vous pouvez ensuite faire glisser dans le canevas du créateur de règles pour créer une nouvelle définition de segment. En référençant une audience, il est possible d’ajouter l’un des jeux de logiques de règles suivants à la nouvelle définition de segment : l’appartenance à l’audience en tant que règle, le jeu complet de la logique de règle qui a défini l’audience référencée. |
| Nouvel emplacement du sélecteur de stratégie de fusion | L’emplacement du sélecteur de stratégie de fusion dans la variable [!DNL Segment Builder] a été modifié. Pour sélectionner une stratégie de fusion pour une définition de segment, cliquez sur l’icône d’engrenage sur la page **[!UICONTROL Champs]** , puis utilisez la fonction **[!UICONTROL Stratégie de fusion]** menu déroulant pour sélectionner la stratégie de fusion à utiliser. |

**Problèmes connus**

* Aucun

Pour plus d’informations, reportez-vous à la [présentation de Segmentation Service](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permet de sélectionner intelligemment et par programmation la &quot;meilleure expérience disponible&quot; à partir d’un ensemble d’options disponibles pour une personne donnée, de la diffuser sur n’importe quel canal ou application, ainsi que d’effectuer des rapports et des analyses.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Fonctions de classement | L’ordre des offres pour les profils est désormais établi au moyen d’une fonction de classement, plutôt que d’un ensemble défini d’offres pour tous les profils. |

**Problèmes connus**

* Aucun.

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les solutions Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos services de gestion de la relation client et de vos systèmes de stockage, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Connexion en continu | L’ingestion par flux vous permet d’envoyer des données depuis des périphériques côté client et côté serveur vers [!DNL Experience Platform] en temps réel. La version comprend une nouvelle interface utilisateur pour la connexion en continu. |
| Prise en charge des connecteurs pour [!DNL Google Cloud Store] | Prise en charge de la collecte de données à partir de [!DNL Google Cloud Store]. |

**Problèmes connus**

* Aucun.

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Système d’[!DNL Experience Data Model] (XDM) {#xdm}

La normalisation et l’interopérabilité sont des concepts clés pour [!DNL Experience Platform]. Le [!DNL Experience Data Model] (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Amélioration de la validation des schémas | Nouvelles vérifications pour s’assurer que les références renvoient à des champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets pour s’assurer que les objets sont bien définis. Amélioration des messages d’erreur pour aider à identifier et à résoudre les problèmes. |

**Corrections de bogues**

* Maintenance et améliorations relatives au contrôle d’accès et aux environnements de test.
* Prise en charge de l’`eTag` pour le point de terminaison `/descriptors` dans l’API [!DNL Schema Registry]

**Problèmes connus**

* Aucun

Pour en savoir plus sur l’utilisation de XDM à l’aide de la variable [!DNL Schema Registry] API et [!DNL Schema Editor] dans l’interface utilisateur, veuillez lire [Documentation du système XDM](../../xdm/home.md).
