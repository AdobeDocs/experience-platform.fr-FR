---
solution: Experience Platform
title: Respect du consentement dans les segments
description: Découvrez comment honorer les préférences de consentement des clients pour la collecte et le partage de données personnelles dans les opérations de segmentation.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# Respect du consentement dans les segments

>[!NOTE]
>
>Ce guide explique comment honorer les consentements dans **définitions de segment**.

Les réglementations légales relatives à la confidentialité, telles que [!DNL California Consumer Privacy Act] (CCPA) donne aux consommateurs le droit de s’exclure de la collecte ou du partage de leurs données personnelles avec des tiers. Adobe Experience Platform fournit des composants XDM (Experience Data Model) standard destinés à capturer ces préférences de consentement des clients dans les données Real-time Customer Profile.

Si un client a retiré ou refusé le consentement pour le partage de ses données personnelles, il est important que votre organisation respecte cette préférence lors de la génération d’audiences pour les activités marketing. Ce document décrit comment intégrer des valeurs de consentement du client dans vos définitions de segment à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Le respect des valeurs de consentement du client nécessite une compréhension des différentes [!DNL Adobe Experience Platform] les services impliqués. Avant de commencer ce tutoriel, assurez-vous de bien connaître les services suivants :

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md) : framework normalisé selon lequel Platform organise les données de l’expérience client.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des audiences à partir de [!DNL Real-Time Customer Profile] data.

## Champs de schéma de consentement

Pour honorer les consentements et les préférences des clients, l’un des schémas qui fait partie de votre [!UICONTROL XDM Individual Profile] le schéma d’union doit contenir le groupe de champs standard **[!UICONTROL Consentements et préférences]**.

Pour plus d’informations sur la structure et le cas d’utilisation prévu de chacun des attributs fournis par le groupe de champs, voir la section [Guide de référence des consentements et des préférences](../xdm/field-groups/profile/consents.md). Pour obtenir des instructions détaillées sur l’ajout d’un groupe de champs à un schéma, reportez-vous à la section [Guide de l’interface utilisateur XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Une fois que le groupe de champs a été ajouté à une [Schéma activé pour les profils](../xdm/ui/resources/schemas.md#profile) et ses champs ont été utilisés pour ingérer des données de consentement de votre application experience, vous pouvez utiliser les attributs de consentement collectés dans vos règles de segment.

## Gestion du consentement dans la segmentation

Afin de garantir que les profils exclus ne sont pas inclus dans les définitions de segment, des champs spéciaux doivent être ajoutés aux définitions de segment existantes et inclus lors de la création de nouvelles définitions de segment.

Les étapes ci-dessous montrent comment ajouter les champs appropriés pour deux types d’indicateurs d’exclusion :

1. [!UICONTROL Collecte de données]
1. [!UICONTROL Partager les données]

>[!NOTE]
>
>Bien que ce guide se concentre sur les deux indicateurs d’exclusion ci-dessus, vous pouvez configurer vos définitions de segment afin d’incorporer des signaux de consentement supplémentaires. Le [Guide de référence des consentements et des préférences](../xdm/field-groups/profile/consents.md) fournit des informations supplémentaires sur chacune de ces options et sur les cas d’utilisation prévus.

Lors de la création d’une définition de segment dans l’interface utilisateur, sous **[!UICONTROL Attributs]**, accédez à **[!UICONTROL XDM Individual Profile]**, puis sélectionnez **[!UICONTROL Consentements et préférences]**. À partir de là, vous pouvez voir les options pour **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]**.

![](./images/opt-outs/consents.png)

Commencez par sélectionner la variable **[!UICONTROL Collecte de données]** catégorie, puis faites glisser **[!UICONTROL Valeur de choix]** dans le créateur de segments. Lors de l’ajout de l’attribut à la définition de segment, vous pouvez spécifier la variable [valeurs de consentement](../xdm/field-groups/profile/consents.md#choice-values) qui doivent être inclus ou exclus.

![](./images/opt-outs/consent-values.png)

Une méthode consiste à exclure les clients qui ont choisi de ne pas collecter leurs données. Pour ce faire, définissez l’opérateur sur **[!UICONTROL n’est pas égal à]**, puis sélectionnez les valeurs suivantes :

* **[!UICONTROL Non (opt-out)]**
* **[!UICONTROL Valeur par défaut de Non (opt-out)]**
* **[!UICONTROL Inconnu]** (si le consentement est supposé être refusé s’il est inconnu)

![](./images/opt-outs/collect.png)

Sous **[!UICONTROL Attributs]** dans le rail de gauche, revenez à la **[!UICONTROL Consentements et préférences]** , puis sélectionnez **[!UICONTROL Partager les données]**. Faites glisser son correspondant **[!UICONTROL Valeur de choix]** dans la zone de travail, puis sélectionnez les mêmes valeurs que pour la [!UICONTROL Collecte de données] valeur de choix. Assurez-vous que la variable **[!UICONTROL Ou]** est établie entre les deux attributs.

![](./images/opt-outs/share.png)

Avec la fonction **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]** valeurs de consentement ajoutées à la définition de segment, tous les clients qui ont choisi de ne pas utiliser leurs données seront exclus de l’audience résultante. À partir de là, vous pouvez continuer à personnaliser la définition de segment avant de sélectionner **[!UICONTROL Enregistrer]** pour terminer le processus.

## Étapes suivantes

En suivant ce tutoriel, vous devriez mieux comprendre comment honorer les consentements et les préférences des clients lors de la création de définitions de segment dans Experience Platform.

Pour plus d&#39;informations sur la gestion du consentement dans Platform, consultez la documentation suivante :

* [Traitement du consentement à l’aide de la norme Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Traitement du consentement à l’aide du standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)