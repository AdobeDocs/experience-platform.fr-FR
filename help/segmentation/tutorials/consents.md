---
solution: Experience Platform
title: Respect du consentement dans les définitions de segment
description: Découvrez comment respecter les préférences de consentement des clients pour la collecte et le partage de données personnelles dans les opérations de segmentation.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
TQID: https://experienceleague.adobe.com/k-0Hlwpmsutz75q0X8fNal2bFtnFig6JvlqIO118uGY
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: b784da9a-7978-4766-bf1f-5ab2b23d894a
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: de9975b2-c43a-4287-9698-4f4cad92b83f
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 689
ht-degree: 2%

---

# Respect du consentement dans les définitions de segment

>[!NOTE]
>
>Ce guide explique comment honorer les consentements dans les **définitions de segment**.

Les réglementations légales relatives à la confidentialité, telles que le [!DNL California Consumer Privacy Act] (CCPA), donnent aux consommateurs le droit de refuser la collecte ou le partage de leurs données personnelles avec des tiers. Adobe Experience Platform fournit des composants XDM (Modèle de données d’expérience) standard destinés à capturer ces préférences de consentement des clients dans les données du profil client en temps réel.

Si un client ou une cliente a retiré ou refusé le consentement pour que ses données personnelles soient partagées, il est important que votre organisation respecte cette préférence lors de la génération d’audiences pour les activités marketing. Ce document décrit comment intégrer des valeurs de consentement client dans vos définitions de segment à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main

Le respect des valeurs de consentement du client ou de la cliente nécessite une compréhension des différents services [!DNL Adobe Experience Platform] impliqués. Avant de commencer ce tutoriel, assurez-vous de connaître les services suivants :

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].

## Champs du schéma de consentement

Pour respecter les consentements et préférences des clients, l’un des schémas qui fait partie de votre schéma d’union [!UICONTROL Profil individuel XDM] doit contenir le groupe de champs standard **[!UICONTROL Consentements et préférences]**.

Pour plus d’informations sur la structure et le cas d’utilisation prévu de chacun des attributs fournis par le groupe de champs, consultez le [&#x200B; guide de référence des consentements et des préférences &#x200B;](../../xdm/field-groups/profile/consents.md). Pour obtenir des instructions détaillées sur l’ajout d’un groupe de champs à un schéma, reportez-vous au guide de l’interface utilisateur [XDM](../../xdm/ui/resources/schemas.md#add-field-groups).

Une fois que le groupe de champs a été ajouté à un [schéma activé pour Profile](../../xdm/ui/resources/schemas.md#profile) et que ses champs ont été utilisés pour ingérer des données de consentement à partir de votre application d’expérience, vous pouvez utiliser les attributs de consentement collectés dans vos règles de segment.

## Gestion du consentement dans la segmentation

Pour vous assurer que les profils exclus ne sont pas inclus dans les définitions de segment, des champs spéciaux doivent être ajoutés aux définitions de segment existantes et inclus lors de la création de définitions de segment.

Les étapes ci-dessous montrent comment ajouter les champs appropriés pour deux types d&#39;indicateurs d&#39;opt-out :

1. [!UICONTROL Collecte de données]
1. [!UICONTROL Partage de données]

>[!NOTE]
>
>Bien que ce guide se concentre sur les deux indicateurs d’exclusion ci-dessus, vous pouvez configurer vos définitions de segment pour incorporer également des signaux de consentement supplémentaires. Le [guide de référence des consentements et des préférences](../../xdm/field-groups/profile/consents.md) fournit plus d’informations sur chacune de ces options et les cas d’utilisation prévus.

Lors de la création d’une définition de segment dans l’interface utilisateur, sous **[!UICONTROL Attributs]**, accédez à **[!UICONTROL Profil individuel XDM]**, puis sélectionnez **[!UICONTROL Consentements et préférences]**, suivi de **[!UICONTROL Spécifique à l’ID]**. À partir de là, vous pouvez voir les options **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]**.

![](../images/tutorials/opt-outs/consents.png)

Sélectionnez d’abord la catégorie **[!UICONTROL Collecte de données]**, puis faites glisser **[!UICONTROL Valeur de choix]** dans le créateur de segments. Lors de l’ajout de l’attribut à la définition de segment, vous pouvez spécifier les [valeurs de consentement](../../xdm/field-groups/profile/consents.md#choice-values) qui doivent être incluses ou exclues.

![](../images/tutorials/opt-outs/consent-values.png)

Une approche consiste à exclure tous les clients qui se sont désinscrits de la collecte de leurs données. Pour ce faire, définissez l’opérateur sur **[!UICONTROL n’est pas égal à]**, puis choisissez les valeurs suivantes :

* **[!UICONTROL Non (opt-out)]**
* **[!UICONTROL Valeur par défaut de Non (opt-out)]**
* **[!UICONTROL Inconnu]** (si l’on suppose que le consentement a été refusé, sinon inconnu)

![](../images/tutorials/opt-outs/collect.png)

Sous **[!UICONTROL Attributs]** dans le rail de gauche, revenez à la section **[!UICONTROL Consentements et préférences]** puis sélectionnez **[!UICONTROL Partager les données]**. Faites glisser la **[!UICONTROL valeur de choix]** correspondante dans la zone de travail et sélectionnez les mêmes valeurs que celles de la valeur de choix [!UICONTROL collecte de données]. Assurez-vous qu’une relation **[!UICONTROL Or]** est établie entre les deux attributs.

![](../images/tutorials/opt-outs/share.png)

Avec les valeurs de consentement **[!UICONTROL Collecte de données]** et **[!UICONTROL Partager les données]** ajoutées à la définition de segment, tous les clients qui ont choisi de ne pas utiliser leurs données seront exclus de l’audience résultante. À partir de là, vous pouvez continuer à personnaliser la définition de segment avant de sélectionner **[!UICONTROL Enregistrer]** pour terminer le processus.

## Étapes suivantes

Vous êtes arrivé au bout de ce tutoriel. À présent, vous devriez mieux comprendre comment respecter les consentements et préférences des clients lors de la création de définitions de segment dans Experience Platform.

Pour plus d’informations sur la gestion du consentement dans Experience Platform, consultez la documentation suivante :

* [Traitement du consentement à l’aide de la norme Adobe](../../landing/governance-privacy-security/consent/adobe/overview.md)
* [Traitement du consentement à l’aide de la norme IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)