---
keywords: personnalisation;cible;destination;destinations de personnalisation;configurer les destinations de personnalisation;même page;page suivante;
title: Configurez des destinations de personnalisation pour la personnalisation de la même page et de la page suivante.
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Découvrez comment configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 99a60621bca43ecf2dacb6202e005bbd8f191c99
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 95%

---

# Configurez des destinations de personnalisation pour la personnalisation de la même page et de la page suivante.

## Présentation {#overview}

>[!NOTE]
>
>When [configuration de la connexion Adobe Target](../catalog/personalization/adobe-target-connection.md) sans utiliser d’identifiant de flux de données, les cas d’utilisation décrits dans cet article ne sont pas pris en charge.

Adobe Experience Platform utilise la [segmentation Edge](../../segmentation/ui/edge-segmentation.md) pour permettre aux clients de créer et de cibler des segments d’audience à grande échelle et en temps réel.

Cette fonctionnalité vous permet de configurer des cas d’utilisation de personnalisation de la même page et de la page suivante.

Cet article fournit des instructions étape par étape sur la configuration d’Experience Platform et de vos destinations de personnalisation pour ces cas d’utilisation.

Regardez également la vidéo ci-dessous pour un aperçu du processus de configuration dans son ensemble.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous aux étapes de configuration décrites dans les sections ci-dessous.

## Étape 1 : configurer un flux de données dans l’interface utilisateur de la collecte de données. {#configure-datastream}

La première étape de la configuration de votre destination de personnalisation consiste à configurer un flux de données pour le SDK web Experience Platform. Cette opération est effectuée dans l’interface utilisateur de la collecte de données.

Lors de la configuration du flux de données, sous **[!UICONTROL Adobe Experience Platform]** assurez-vous que la **[!UICONTROL Segmentation Edge]** et les **[!UICONTROL Destinations de personnalisation]** sont bien sélectionnées.

![Configurer le flux de données](../assets/ui/configure-personalization-destinations/datastream-config.png)

Pour plus d’informations sur la configuration d’un flux de données, suivez les instructions décrites dans la section [Documentation du SDK web Platform](../../edge/datastreams/overview.md).

## Étape 2 : configurer votre destination de personnalisation {#configure-destination}

Après avoir configuré votre flux de données, vous pouvez commencer à configurer votre destination de personnalisation.

Suivez le [tutoriel sur la création de connexion de destination](../ui/connect-destination.md) pour obtenir des instructions détaillées sur la création d’une connexion de destination.

Selon la destination configurée, reportez-vous aux articles suivants pour connaître les conditions préalables spécifiques à une destination et les informations connexes :

* [Connexion Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Connexion de personnalisation personnalisée](../catalog/personalization/custom-personalization.md)

## Étape 3 : créer une stratégie de fusion [!DNL Active-On-Edge]. {#create-merge-policy}

Une fois votre connexion de destination créée, vous devez créer une stratégie de fusion [!DNL Active-On-Edge].

Suivez les instructions de la section [création d’une stratégie de fusion](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) et assurez-vous d’activer le bouton **[!UICONTROL Stratégie de fusion Active-On-Edge]**.

## Étape 4 : créer un segment dans Platform. {#create-segment}

Après avoir créé la stratégie de fusion [!DNL Active-On-Edge], vous devez créer un segment dans Platform.

Suivez le guide du [Créateur de segments](../../segmentation/ui/segment-builder.md) pour créer le segment et veillez à [y affecter](../../segmentation/ui/segment-builder.md#merge-policies) la stratégie de fusion [!DNL Active-On-Edge] créée à l’étape 3.

## Étape 5 : activer le segment vers votre destination.

La dernière étape du processus de configuration consiste à activer le segment créé à l’étape 4 pour la destination créée à l’étape 2.

Pour ce faire, suivez le [tutoriel sur l’activation](../ui/activate-profile-request-destinations.md).

## Valider la configuration {#validate-configuration}

Si les étapes ci-dessus ont été effectuées correctement, vos nouveaux segments apparaissent dans votre destination de personnalisation.
