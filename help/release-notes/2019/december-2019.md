---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 décembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 64%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service fournit une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir de vos données [!DNL Real-time Customer Profile]. Ces segments sont configurés et gérés de manière centralisée sur [!DNL Platform], ce qui les rend facilement accessibles par toute application d&#39;Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Onglet Audiences fusionnées dans [!DNL Segment Builder] | Les onglets [!UICONTROL Segments] et [!UICONTROL Audiences] dans [!DNL Segment Builder] ont été combinés dans un seul onglet [!UICONTROL Audiences]. Cet onglet vous permet de parcourir et de rechercher les audiences existantes, que vous pouvez ensuite faire glisser dans le canevas du créateur de règles pour créer une nouvelle définition de segment. En référençant une audience, il est possible d’ajouter l’un des jeux de logiques de règles suivants à la nouvelle définition de segment : l’appartenance à l’audience en tant que règle, le jeu complet de la logique de règle qui a défini l’audience référencée. |
| Nouvel emplacement du sélecteur de stratégie de fusion | L&#39;emplacement du sélecteur de stratégies de fusion dans [!DNL Segment Builder] a été modifié. Pour sélectionner une stratégie de fusion pour une définition de segment, sélectionnez l&#39;icône d&#39;engrenage dans l&#39;onglet **[!UICONTROL Champs]**, puis utilisez le menu déroulant **[!UICONTROL Fusionner la stratégie]** pour sélectionner la stratégie de fusion que vous souhaitez utiliser. |

**Problèmes connus**

* Aucun

Pour plus d’informations, reportez-vous à la [présentation de Segmentation Service](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permet de sélectionner intelligemment et par programmation la &quot;prochaine meilleure expérience&quot; à partir d&#39;un ensemble d&#39;options disponibles pour une personne donnée, de la diffuser sur n&#39;importe quel canal ou application, et d&#39;effectuer des rapports et des analyses.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Fonctions de classement | L’ordre des offres pour les profils est désormais établi au moyen d’une fonction de classement, plutôt que d’un ensemble défini d’offres pour tous les profils. |

**Problèmes connus**

* Aucun.

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les solutions Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos services de gestion de la relation client et de vos systèmes de stockage, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Connexion en continu | L’assimilation en flux continu vous permet d’envoyer en temps réel des données des périphériques client et serveur à [!DNL Experience Platform]. La version comprend une nouvelle interface utilisateur pour la connexion en continu. |
| Prise en charge du connecteur pour [!DNL Google Cloud Store] | Prise en charge de la collecte de données auprès de [!DNL Google Cloud Store]. |

**Problèmes connus**

* Aucun.

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## [!DNL Experience Data Model] Système (XDM)  {#xdm}

La normalisation et l&#39;interopérabilité sont les concepts clés qui sous-tendent [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Amélioration de la validation des schémas | Nouvelles vérifications pour s’assurer que les références renvoient à des champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets pour s’assurer que les objets sont bien définis. Amélioration des messages d’erreur pour aider à identifier et à résoudre les problèmes. |

**Corrections de bogues**

* Maintenance et améliorations relatives au contrôle d’accès et aux environnements de test.
* Prise en charge de l’`eTag` pour le point de terminaison `/descriptors` dans l’API [!DNL Schema Registry]

**Problèmes connus**

* Aucun

Pour en savoir plus sur l&#39;utilisation de XDM à l&#39;aide de l&#39;API [!DNL Schema Registry] et de l&#39;interface utilisateur [!DNL Schema Editor], consultez la [documentation du système XDM](../../xdm/home.md).