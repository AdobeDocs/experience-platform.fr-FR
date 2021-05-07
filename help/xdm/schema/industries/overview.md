---
solution: Experience Platform
title: Présentation des modèles de données du secteur
topic-legacy: overview
description: Découvrez les modèles de données normalisés pour divers secteurs verticaux qui peuvent être créés à l’aide de composants standard du modèle de données d’expérience (XDM).
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Présentation des modèles de données du secteur

Le modèle de données d’expérience (XDM) vous permet de créer des schémas hautement personnalisables pour capturer les données d’expérience client clés liées à votre entreprise. Pour simplifier le processus de modélisation de vos données pour les rendre conformes à XDM, Adobe Experience Platform fournit une suite polyvalente de composants XDM standard, qui capturent des concepts couramment utilisés dans plusieurs secteurs d’activité.

>[!NOTE]
>
>De nouveaux composants XDM standard sont continuellement mis à disposition pour répondre aux besoins des consommateurs. Pour obtenir une liste des composants les plus récents, vous pouvez [explorer les ressources existantes dans l&#39;interface utilisateur](../../ui/explore.md) ou consulter le [référentiel XDM officiel](https://github.com/adobe/xdm/tree/master/components) sur GitHub.

Selon le secteur d&#39;activité de votre entreprise, certains composants XDM seront plus adaptés à vos besoins que d&#39;autres. En outre, les relations que vous établissez entre vos schémas XDM varient selon votre secteur d&#39;activité.

Afin de vous aider à orienter votre stratégie de modélisation des données en fonction de votre secteur particulier, ce guide fournit une référence de diagrammes de relations d’entité (ERD) pour plusieurs secteurs verticaux pris en charge.

## Conditions préalables  

Pour lire les ERD référencées dans ce guide, vous devez avoir une bonne compréhension de la façon dont les composants XDM interagissent avec les schémas de formulaire et du fonctionnement des schémas XDM dans l&#39;Experience Platform dans son ensemble. Assurez-vous d’avoir lu la documentation d’aperçu suivante avant de continuer :

* [Présentation](../../home.md) du système XDM : Découvrez comment XDM fonctionne dans l’écosystème de la plate-forme.
* [Principes de base de la composition](../../schema/composition.md) des schémas : Découvrez comment les composants XDM (tels que les groupes de champs de schéma, les classes et les types de données) contribuent à la structure d&#39;un schéma, ainsi qu&#39;au rôle des champs d&#39;identité.

Il est également recommandé de consulter le [guide des meilleures pratiques de modélisation des données](../../schema/best-practices.md) pour obtenir des instructions générales sur la façon de mapper vos données à XDM.

## ERD du modèle de données du secteur {#erds}

Les modèles verticaux de l&#39;industrie représentés par les ERD ci-dessous sont créés intentionnellement de façon dénormalisée et en tenant compte de la façon dont les données sont stockées dans la plate-forme.

Pour une ERD donnée, chaque entité affichée dans est basée sur une classe XDM sous-jacente. Pour une entité donnée, chaque ligne indiquée dans **bold** représente un groupe de champs ou un type de données, avec les champs correspondants qu&#39;elle fournit ci-dessous dans du texte non gras. Les champs les plus importants pour une entité donnée sont surlignés en rouge.

>[!NOTE]
>
>Certaines entités peuvent inclure un champ &quot;_ID&quot;. Il s’agit de l’identifiant unique (`_id`) que Platform attribue automatiquement aux entités de événement ou de profil lorsqu’elles sont ingérées. Cependant, si vous le souhaitez, vous pouvez choisir d’utiliser vos propres valeurs d’ID uniques pour ce champ.

Toutes les propriétés pouvant être utilisées pour identifier des clients individuels sont marquées comme &quot;identité&quot;, l’une de ces propriétés étant marquée comme &quot;Principale identité&quot;.

Les relations d&#39;entité sont marquées comme non dépendantes, puisque les événements basés sur les cookies ne peuvent souvent pas déterminer la personne ou l&#39;individu qui a effectué la transaction.

Les ERD sont fournis pour les secteurs verticaux suivants :

* [[!UICONTROL Vente au détail]](./retail.md)
* [[!UICONTROL Services financiers]](./financial.md)
* [[!UICONTROL Voyages et hospitalité]](./travel-hospitality.md)

## Étapes suivantes

Ce document présente un aperçu des ERD du modèle de données du secteur et explique comment les interpréter. Pour vue d&#39;un ERD, sélectionnez-en un dans la liste ci-dessus.
