---
title: Notes De Mise À Jour De Adobe Experience Platform - Décembre 2019
description: Les notes de mise à jour de décembre 2019 pour Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
TQID: https://experienceleague.adobe.com/Lq2NtWy3vAL0ejPz7uBHVl5NW4ebRBgDSLGmfW7TfIk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2:
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 661
ht-degree: 64%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 11 décembre 2019**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service propose une interface utilisateur et une API RESTful qui vous permettent de créer des segments et de générer des audiences à partir des données [!DNL Real-Time Customer Profile]. Ces segments sont configurés et conservés de manière centralisée sur [!DNL Experience Platform], ce qui les rend facilement accessibles depuis n’importe quelle application Adobe.

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Onglet Audiences fusionnées dans [!DNL Segment Builder] | Les onglets [!UICONTROL Segments] et [!UICONTROL Audiences] du [!DNL Segment Builder] ont été combinés en un seul onglet [!UICONTROL Audiences]. Cet onglet vous permet de parcourir et de rechercher les audiences existantes, que vous pouvez ensuite faire glisser dans la zone de travail du créateur de règles pour créer une nouvelle définition de segment. En référençant une audience, il est possible d’ajouter l’un des jeux de logiques de règles suivants à la nouvelle définition de segment : l’appartenance à l’audience en tant que règle, le jeu complet de la logique de règle qui a défini l’audience référencée. |
| Nouvel emplacement du sélecteur de politique de fusion | L’emplacement du sélecteur de politique de fusion dans le [!DNL Segment Builder] a été modifié. Pour sélectionner une politique de fusion pour une définition de segment, sélectionnez l’icône en forme d’engrenage dans l’onglet **[!UICONTROL Fields]** , puis utilisez le menu déroulant **[!UICONTROL Merge Policy]** pour sélectionner la politique de fusion à utiliser. |

**Problèmes connus**

* Aucun

Pour plus d’informations, reportez-vous à la [présentation de Segmentation Service](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] permet de sélectionner intelligemment et par programmation la « meilleure expérience disponible » à partir d’un ensemble d’options défini pour une personne donnée, de la diffuser par le biais de n’importe quel canal ou application, ainsi que d’exécuter des analyses et de créer des rapports.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| -----------| ---------- |
| Fonctions de classement | L’ordre des offres pour les profils est désormais établi au moyen d’une fonction de classement, plutôt que d’un ensemble défini d’offres pour tous les profils. |

**Problèmes connus**

* Aucun.

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les solutions Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier auprès de vos services de gestion de la relation client et de vos systèmes de stockage, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ---------- | ------------ |
| Connexion en continu | L’ingestion par flux vous permet d’envoyer en temps réel des données à [!DNL Experience Platform] à partir d’appareils côté client et côté serveur. La version comprend une nouvelle interface utilisateur pour la connexion en continu. |
| Prise en charge des connecteurs pour [!DNL Google Cloud Store] | Prise en charge de la collecte de données à partir de [!DNL Google Cloud Store]. |

**Problèmes connus**

* Aucun.

Pour plus d’informations sur les sources, consultez la [présentation des sources](../../sources/home.md).

## Système d’[!DNL Experience Data Model] (XDM) {#xdm}

La normalisation et l&#39;interopérabilité sont les concepts clés de [!DNL Experience Platform]. [!DNL Experience Data Model] Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes à toutes les applications pour communiquer avec des services sur Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
|--- | ---|
| Amélioration de la validation des schémas | Nouvelles vérifications pour s’assurer que les références renvoient à des champs supplémentaires comme prévu. Ajout de vérifications supplémentaires aux champs définis comme un tableau d’objets pour s’assurer que les objets sont bien définis. Amélioration des messages d’erreur pour aider à identifier et à résoudre les problèmes. |

**Correctifs de bugs**

* Maintenance et améliorations relatives au contrôle d’accès et aux sandbox.
* Prise en charge de la `eTag` pour le point d’entrée `/descriptors` dans l’API [!DNL Schema Registry].

**Problèmes connus**

* Aucune

Pour en savoir plus sur l’utilisation de XDM à l’aide de l’API [!DNL Schema Registry] et de [!DNL Schema Editor]’interface utilisateur, consultez la [documentation du système XDM](../../xdm/home.md).
