---
keywords: la personnalisation; cible; destination; les destinations de personnalisation ; configurer les destinations de personnalisation ; même page ; page suivante;
title: Configuration des destinations de personnalisation pour la personnalisation de la même page et de la page suivante
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Découvrez comment configurer des destinations de personnalisation pour la personnalisation de la même page et de la page suivante.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 69db8dbc315f97a0133bcc761ebf850d587dd7d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Configuration des destinations de personnalisation pour la personnalisation de la même page et de la page suivante

Utilisation de Adobe Experience Platform [segmentation de périphérie](../../segmentation/ui/edge-segmentation.md) pour permettre aux clients de créer et de cibler des segments d’audience à grande échelle, en temps réel.

Cette fonctionnalité vous permet de configurer des cas pratiques de personnalisation de la même page et de la page suivante.

Cet article fournit des instructions étape par étape sur la configuration d’Experience Platform et de vos destinations de personnalisation pour ces cas d’utilisation.

En outre, regardez la vidéo ci-dessous pour un aperçu du processus de configuration de bout en bout.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

## Étape 1 : Configuration d’un flux de données dans l’interface utilisateur de la collecte de données {#configure-datastream}

La première étape de la configuration de votre destination de personnalisation consiste à configurer un flux de données pour le SDK Web Experience Platform. Cette opération est effectuée dans l’interface utilisateur de la collecte de données.

Lors de la configuration du flux de données, sous **[!UICONTROL Adobe Experience Platform]** assurez-vous que les **[!UICONTROL Segmentation Edge]** et **[!UICONTROL Destinations de personnalisation]** sont sélectionnées.

![Configuration des flux de données](../assets/ui/configure-personalization-destinations/datastream-config.png)

Pour plus d’informations sur la configuration d’un flux de données, suivez les instructions décrites dans la section [Documentation du SDK Web Platform](../../edge/fundamentals/datastreams.md).

## Étape 2 : Configuration de votre destination de personnalisation {#configure-destination}

Après avoir configuré votre flux de données, vous pouvez commencer à configurer votre destination de personnalisation.

Suivez la [tutoriel sur la création de connexion à destination](../ui/connect-destination.md) pour obtenir des instructions détaillées sur la création d’une connexion de destination.

Selon la destination que vous configurez, reportez-vous aux articles suivants pour connaître les conditions préalables spécifiques à une destination et les informations connexes :

* [Connexion Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Connexion à la personnalisation personnalisée](../catalog/personalization/custom-personalization.md)

## Étape 3 : Créez un [!DNL Active-On-Edge] stratégie de fusion {#create-merge-policy}

Après avoir créé votre connexion de destination, vous devez créer une [!DNL Active-On-Edge] stratégie de fusion.

Suivez les instructions de la section [création d’une stratégie de fusion](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), et assurez-vous d’activer la variable **[!UICONTROL Stratégie de fusion principale sur le périphérique]** bascule.

## Étape 4 : Création d’un segment dans Platform {#create-segment}

Après avoir créé la variable [!DNL Active-On-Edge] stratégie de fusion, vous devez créer un segment dans Platform.

Suivez la [créateur de segments](../../segmentation/ui/segment-builder.md) pour créer votre segment et veillez à [affecter](../../segmentation/ui/segment-builder.md#merge-policies) la valeur [!DNL Active-On-Edge] stratégie de fusion que vous avez créée à l’étape 3.

## Étape 5 : Activation du segment vers votre destination

La dernière étape du processus de configuration consiste à activer le segment que vous avez créé à l’étape 4 vers la destination que vous avez créée à l’étape 2.

Pour ce faire, procédez comme suit : [tutoriel sur l’activation](../ui/activate-profile-request-destinations.md).

## Validation de la configuration {#validate-configuration}

Après avoir suivi les étapes ci-dessus, vous devriez voir vos nouveaux segments dans votre destination de personnalisation.
