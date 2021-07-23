---
solution: Experience Platform
title: Présentation des modèles de données du secteur
topic-legacy: overview
description: Découvrez les modèles de données normalisés pour divers secteurs verticaux qui peuvent être créés à l’aide des composants standard du modèle de données d’expérience (XDM).
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: e44da39dcdd4af4ab883b3ff8f61ca2fd44adb0b
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---

# Présentation des modèles de données du secteur

Le modèle de données d’expérience (XDM) vous permet de créer des schémas hautement personnalisables afin de capturer les données d’expérience client clés liées à votre entreprise. Pour simplifier le processus de modélisation de vos données afin qu’elles soient conformes à XDM, Adobe Experience Platform fournit une suite polyvalente de composants XDM standard, qui capturent des concepts généralement utilisés dans plusieurs secteurs d’activité.

>[!NOTE]
>
>De nouveaux composants XDM standard sont continuellement publiés pour répondre aux besoins des consommateurs. Pour obtenir la liste des composants les plus récents, vous pouvez [explorer les ressources existantes dans l’interface utilisateur](../../ui/explore.md) ou vous référer au [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components) sur GitHub.

Selon le secteur d’activité sous lequel votre entreprise opère, certains composants XDM seront plus pertinents que d’autres pour vos besoins. En outre, les relations que vous établissez entre vos schémas XDM varient en fonction de votre secteur d’activité.

Afin de vous aider à orienter votre stratégie de modélisation des données en fonction de votre secteur d’activité spécifique, ce guide fournit une référence des diagrammes de relation d’entité (ERD) pour plusieurs secteurs verticaux pris en charge.

## Conditions préalables

Pour lire les ERD référencés dans ce guide, vous devez avoir une compréhension pratique de la manière dont les composants XDM interagissent avec les schémas de formulaire et du fonctionnement des schémas XDM dans l’Experience Platform dans son ensemble. Assurez-vous d’avoir lu la documentation de présentation suivante avant de poursuivre :

* [Présentation](../../home.md) du système XDM : Découvrez comment XDM fonctionne dans l’écosystème Platform.
* [Principes de base de la composition](../../schema/composition.md) des schémas : Découvrez comment les composants XDM (tels que les groupes de champs de schéma, les classes et les types de données) contribuent à la structure d’un schéma, ainsi que le rôle des champs d’identité.

Il est également recommandé de consulter le [guide des bonnes pratiques de modélisation des données](../../schema/best-practices.md) pour obtenir des instructions générales sur la manière de mapper vos données à XDM.

## ERD de modèle de données du secteur {#erds}

Les ERD sont fournis pour les secteurs verticaux suivants :

* [[!UICONTROL Vente au détail]](./retail.md)
* [[!UICONTROL Services financiers]](./financial.md)
* [[!UICONTROL Télécommunications]](./telecom.md)
* [[!UICONTROL Voyage et hospitalité]](./travel-hospitality.md)

## Étapes suivantes

Ce document fournit un aperçu des ERD du modèle de données du secteur et de la manière de les interpréter. Pour afficher un ERD, sélectionnez-en un dans la liste ci-dessus.
