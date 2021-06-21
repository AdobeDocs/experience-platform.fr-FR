---
keywords: Experience Platform;accueil;rubriques les plus consultées;exclusion;segmentation;service de segmentation;service de segmentation;droit d’opposition;droit d’opposition;droit d’opposition;droit d’opposition;consentement;partage;collecte;droit d’opposition
solution: Experience Platform
title: Respect du consentement dans les segments
topic-legacy: overview
description: Découvrez comment honorer les préférences de consentement des clients pour la collecte et le partage de données personnelles dans les opérations de segmentation.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 6d11a94d45b4a089ca6960aaf1ce78ae654ebc3f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# Respect du consentement dans les segments

Les réglementations légales relatives à la protection de la vie privée, telles que la loi sur la protection des données (CCPA), donnent aux consommateurs le droit de se désabonner de la collecte ou du partage de leurs données personnelles avec des tiers. [!DNL California Consumer Privacy Act] Adobe Experience Platform fournit des composants XDM (Experience Data Model) standard destinés à capturer ces préférences de consentement des clients dans les données Real-time Customer Profile.

Si un client a retiré ou refusé le consentement pour le partage de ses données personnelles, il est important que votre organisation respecte cette préférence lors de la génération d’audiences pour les activités marketing. Ce document décrit comment intégrer des valeurs de consentement du client dans vos définitions de segment à l’aide de l’interface utilisateur de l’Experience Platform.

## Prise en main

Le respect des valeurs de consentement des clients nécessite une compréhension des différents [!DNL Adobe Experience Platform] services impliqués. Avant de commencer ce tutoriel, assurez-vous de bien connaître les services suivants :

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des segments d’audience à partir de  [!DNL Real-time Customer Profile] données.

## Champs de schéma de consentement

Afin d’honorer les consentements et les préférences des clients, l’un des schémas qui fait partie de votre schéma d’union [!UICONTROL XDM Individual Profile] doit contenir le groupe de champs standard **[!UICONTROL Privacy/Personalization/Marketing Preferences (Consensus)]**.

Pour plus d’informations sur la structure et le cas d’utilisation prévu de chacun des attributs fournis par le groupe de champs, consultez le [guide de référence des consentements et des préférences](../xdm/field-groups/profile/consents.md). Pour obtenir des instructions détaillées sur l’ajout d’un groupe de champs à un schéma, reportez-vous au [guide de l’interface utilisateur XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Une fois que le groupe de champs a été ajouté à un [schéma activé par le profil](../xdm/ui/resources/schemas.md#profile) et que ses champs ont été utilisés pour ingérer les données de consentement de votre application d’expérience, vous pouvez utiliser les attributs de consentement collectés dans vos règles de segment.

## Gestion du consentement dans la segmentation

Afin de garantir que les profils exclus ne sont pas inclus dans les segments, des champs spéciaux doivent être ajoutés aux segments existants et inclus lors de la création de nouveaux segments.

Les étapes ci-dessous montrent comment ajouter les champs appropriés pour deux types d’indicateurs d’exclusion :

1. [!UICONTROL Collecte de données]
1. [!UICONTROL Partager les données]

>[!NOTE]
>
>Bien que ce guide se concentre sur les deux indicateurs d’exclusion ci-dessus, vous pouvez configurer vos segments afin d’incorporer d’autres signaux de consentement. Le [guide de référence des consentements et des préférences](../xdm/field-groups/profile/consents.md) fournit des informations supplémentaires sur chacune de ces options et sur les cas d’utilisation prévus.

Lors de la création d’un segment dans l’interface utilisateur, sous **[!UICONTROL Attributs]**, accédez à **[!UICONTROL XDM Individual Profile]**, puis sélectionnez **[!UICONTROL Contenus et Préférences]**. À partir de là, vous pouvez voir les options pour **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]**.

![](./images/opt-outs/consents.png)

Sélectionnez tout d’abord la catégorie **[!UICONTROL Collecte de données]**, puis faites glisser **[!UICONTROL Valeur de choix]** dans le créateur de segments. Lors de l’ajout de l’attribut au segment, vous pouvez spécifier les [valeurs de consentement](../xdm/field-groups/profile/consents.md#choice-values) qui doivent être incluses ou exclues.

![](./images/opt-outs/consent-values.png)

Une méthode consiste à exclure les clients qui ont choisi de ne pas collecter leurs données. Pour ce faire, définissez l’opérateur sur **[!UICONTROL n’est pas égal à]**, puis sélectionnez les valeurs suivantes :

* **[!UICONTROL Non (opt-out)]**
* **[!UICONTROL Valeur par défaut de Non (opt-out)]**
* **[!UICONTROL Inconnu]**  (si le consentement est supposé être refusé s’il est inconnu)

![](./images/opt-outs/collect.png)

Sous **[!UICONTROL Attributs]** dans le rail de gauche, revenez à la section **[!UICONTROL Contenus et Préférences]** , puis sélectionnez **[!UICONTROL Partager les données]**. Faites glisser la **[!UICONTROL Valeur de choix]** correspondante dans la zone de travail, puis sélectionnez les mêmes valeurs que celles de la valeur de choix [!UICONTROL Collecte de données] . Assurez-vous qu’une relation **[!UICONTROL Ou]** est établie entre les deux attributs.

![](./images/opt-outs/share.png)

Avec les valeurs de consentement **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]** ajoutées au segment, tous les clients qui ont choisi de ne pas utiliser leurs données seront exclus de l’audience résultante. À partir de là, vous pouvez continuer à personnaliser la définition de segment avant de sélectionner **[!UICONTROL Enregistrer]** pour terminer le processus.

## Étapes suivantes

En suivant ce tutoriel, vous devriez mieux comprendre comment honorer les consentements et les préférences des clients lors de la création de segments dans Experience Platform.

Pour plus d&#39;informations sur la gestion du consentement dans Platform, consultez la documentation suivante :

* [Traitement du consentement à l’aide de la norme Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Traitement du consentement à l’aide du standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)