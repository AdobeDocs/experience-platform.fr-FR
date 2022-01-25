---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 46%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 janvier 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Préparation de données](#data-prep)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide du [!UICONTROL Alertes] dans l’interface utilisateur de Platform et peut choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles règles d’alerte | Plusieurs nouvelles règles d’alerte sont désormais disponibles pour les workflows liés à l’ingestion de données, aux identités, aux profils, à la segmentation et à l’activation. Consultez la présentation sur [règles d’alerte](../../observability/alerts/rules.md) pour la liste mise à jour des types d’alerte. |

Pour plus d’informations sur les alertes dans Platform, reportez-vous à la section [aperçu des alertes](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM). 

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Expérience de mappage consolidé | La nouvelle interface de mappage de l’interface utilisateur de Platform vous offre une expérience de mappage cohérente pour tirer parti des recommandations de mappage intelligent, configurer manuellement les règles de mappage et déboguer les erreurs qui se produisent dans vos jeux de mappages. Pour plus d’informations, voir [[!DNL Data Prep] Guide de l’interface utilisateur](../../data-prep/home.md). |

Pour plus d’informations sur [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation de la ](../../data-prep/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance unique de Platform en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de l’interface utilisateur des environnements de test | L’indicateur sandbox est désormais intégré à l’en-tête de toutes les applications de l’interface utilisateur de Platform. L’indicateur sandbox affiche le nom, la région et le type de l’environnement de test et vous permet également d’accéder à un menu déroulant pour basculer entre les environnements de test. Pour plus d’informations, voir [guide de l’interface utilisateur des environnements de test](../../sandboxes/ui/user-guide.md). |

Pour plus d’informations sur les environnements de test, voir [Présentation des environnements de test](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Correspondance de segments | La correspondance de segment est un service de collaboration de données qui permet à deux utilisateurs ou plus de Platform d’échanger des données, en fonction d’identifiants communs, d’une manière sécurisée, gouvernée et respectueuse de la confidentialité. Pour plus d’informations, voir [Correspondance de segment - Aperçu](../../segmentation/ui/segment-match/overview.md). |

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).
