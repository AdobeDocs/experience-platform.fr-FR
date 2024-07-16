---
solution: Experience Platform
title: Respect du consentement dans les segments
description: Découvrez comment honorer les préférences de consentement des clients pour la collecte et le partage de données personnelles dans les opérations de segmentation.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Respect du consentement dans les segments

>[!NOTE]
>
>Ce guide explique comment honorer les consentements dans les **définitions de segment**.

Les réglementations légales relatives à la confidentialité, telles que le [!DNL California Consumer Privacy Act] (CCPA), donnent aux consommateurs le droit de ne pas avoir leurs données personnelles collectées ou partagées avec des tiers. Adobe Experience Platform fournit des composants XDM (Experience Data Model) standard destinés à capturer ces préférences de consentement des clients dans les données Real-time Customer Profile.

Si un client a retiré ou refusé le consentement pour le partage de ses données personnelles, il est important que votre organisation respecte cette préférence lors de la génération d’audiences pour les activités marketing. Ce document décrit comment intégrer des valeurs de consentement du client dans vos définitions de segment à l’aide de l’interface utilisateur de l’Experience Platform.

## Commencer

Le respect des valeurs de consentement des clients nécessite une compréhension des différents services [!DNL Adobe Experience Platform] impliqués. Avant de commencer ce tutoriel, assurez-vous de bien connaître les services suivants :

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md) : cadre normalisé selon lequel Platform organise les données d’expérience client.
* [[!DNL Real-Time Customer Profile]](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md) : vous permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].

## Champs de schéma de consentement

Afin d’honorer les consentements et les préférences des clients, l’un des schémas qui fait partie de votre schéma d’union [!UICONTROL XDM Individual Profile] doit contenir le groupe de champs standard **[!UICONTROL Contenus et Préférences]**.

Pour plus d’informations sur la structure et le cas d’utilisation prévu de chacun des attributs fournis par le groupe de champs, consultez le [guide de référence des consentements et des préférences](../xdm/field-groups/profile/consents.md). Pour obtenir des instructions détaillées sur l’ajout d’un groupe de champs à un schéma, reportez-vous au [guide de l’interface utilisateur XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Une fois que le groupe de champs a été ajouté à un [schéma activé par le profil](../xdm/ui/resources/schemas.md#profile) et que ses champs ont été utilisés pour ingérer des données de consentement de votre application d’expérience, vous pouvez utiliser les attributs de consentement collectés dans vos règles de segment.

## Gestion du consentement dans la segmentation

Afin de garantir que les profils exclus ne sont pas inclus dans les définitions de segment, des champs spéciaux doivent être ajoutés aux définitions de segment existantes et inclus lors de la création de nouvelles définitions de segment.

Les étapes ci-dessous montrent comment ajouter les champs appropriés pour deux types d’indicateurs d’exclusion :

1. [!UICONTROL Collecte de données]
1. [!UICONTROL Partager des données]

>[!NOTE]
>
>Bien que ce guide se concentre sur les deux indicateurs d’exclusion ci-dessus, vous pouvez configurer vos définitions de segment afin d’incorporer des signaux de consentement supplémentaires. Le [guide de référence des consentements et préférences](../xdm/field-groups/profile/consents.md) fournit des informations supplémentaires sur chacune de ces options et sur les cas d’utilisation prévus.

Lors de la création d’une définition de segment dans l’interface utilisateur, sous **[!UICONTROL Attributs]**, accédez à **[!UICONTROL XDM Individual Profile]**, puis sélectionnez **[!UICONTROL Contenus et préférences]**. À partir de là, vous pouvez voir les options pour **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager des données]**.

![](./images/opt-outs/consents.png)

Sélectionnez tout d’abord la catégorie **[!UICONTROL Collecte de données]**, puis faites glisser **[!UICONTROL Valeur de choix]** dans le créateur de segments. Lors de l’ajout de l’attribut à la définition de segment, vous pouvez spécifier les [valeurs de consentement](../xdm/field-groups/profile/consents.md#choice-values) qui doivent être incluses ou exclues.

![](./images/opt-outs/consent-values.png)

Une méthode consiste à exclure les clients qui ont choisi de ne pas collecter leurs données. Pour ce faire, définissez l’opérateur sur **[!UICONTROL n’est pas égal à]** et sélectionnez les valeurs suivantes :

* **[!UICONTROL Non (opt-out)]**
* **[!UICONTROL Valeur par défaut de Non (opt-out)]**
* **[!UICONTROL Inconnu]** (si le consentement est supposé être refusé s&#39;il est inconnu)

![](./images/opt-outs/collect.png)

Sous **[!UICONTROL Attributs]** dans le rail de gauche, revenez à la section **[!UICONTROL Contenus et Préférences]**, puis sélectionnez **[!UICONTROL Partager les données]**. Faites glisser la **[!UICONTROL valeur de choix]** correspondante dans la zone de travail, puis sélectionnez les mêmes valeurs que celles de la valeur de choix [!UICONTROL Collecte de données] . Assurez-vous qu’une relation **[!UICONTROL Or]** est établie entre les deux attributs.

![](./images/opt-outs/share.png)

Avec les valeurs de consentement **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]** ajoutées à la définition de segment, tous les clients qui ont choisi de ne pas utiliser leurs données seront exclus de l’audience résultante. À partir de là, vous pouvez continuer à personnaliser la définition de segment avant de sélectionner **[!UICONTROL Enregistrer]** pour terminer le processus.

## Étapes suivantes

En suivant ce tutoriel, vous devriez mieux comprendre comment honorer les consentements et les préférences des clients lors de la création de définitions de segment dans Experience Platform.

Pour plus d&#39;informations sur la gestion du consentement dans Platform, consultez la documentation suivante :

* [Traitement du consentement à l’aide de la norme Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Traitement du consentement à l’aide du standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)