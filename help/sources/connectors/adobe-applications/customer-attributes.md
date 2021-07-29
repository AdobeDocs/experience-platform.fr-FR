---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur Attributs du client
solution: Experience Platform
title: Présentation du connecteur source des attributs du client
topic-legacy: overview
description: Découvrez comment connecter les attributs du client à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 11%

---

# Connecteur Attributs du client

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) dans Experience Cloud vous permet de charger vos données d’entreprise capturées à partir d’une base de données de gestion de la relation client (CRM). Vous pouvez charger les données dans une source de données Attribut client dans l’Experience Cloud, puis utiliser les données dans Adobe Analytics et Adobe Target.

Experience Platform prend en charge l’ingestion de données de profil [!DNL Customer Attributes] dans Adobe Experience Platform.

## Jeux de données et schémas

La source [!DNL Customer Attributes] crée automatiquement le jeu de données dans lequel les données doivent être envoyées. Ce jeu de données créé automatiquement est corrigé et ne peut pas être sélectionné manuellement. La source crée également automatiquement le schéma du jeu de données en fonction de la source de données d’entrée. Ce processus implique également la création automatique des mappages nécessaires entre le schéma et les données source.

## Identités

L’identité Principale d’un jeu de données est contenue dans la première colonne du fichier CSV des données source. La source [!DNL Customer Attributes] suppose que l’identité est toujours mappée à l’espace de noms [`CORE`](../../../identity-service/namespaces.md), un espace de noms généré par le système qui est pris en charge par [[!DNL Identity Service]](../../../identity-service/home.md).

Vous ne pouvez pas sélectionner un espace de noms existant pour l’identité lors de l’utilisation de la source [!DNL Customer Attributes] car [!DNL Customer Attributes] suppose que l’identité Principale du schéma figure toujours dans la carte d’identité. [!DNL Customer Attributes] crée ensuite le mappage de l’ID source à l’UUID de carte d’identité de manière automatisée.

Pour que les données [!DNL Customer Attributes] soient liées à d’autres jeux de données [!DNL Profile], leurs données et identités doivent pouvoir être associées à un identifiant Experience Cloud.

Vous pouvez établir l’espace de noms `CORE` en définissant l’ID Experience Cloud du visiteur à l’aide du [SDK Web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), du [SDK mobile](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) ou de l’[API du service d’ID Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

Le fichier [!DNL Customer Attributes] ne renseigne aucune autre relation d’identité. Par exemple, si un jeu de données source [!DNL Customer Attributes] contient un **Email** et un champ **Loyalty ID**, ces champs doivent être étiquetés comme champs d’identité dans le schéma pour être traités dans [!DNL Identity Service].

Pour plus d’informations, consultez le tutoriel sur la [création d’une connexion source  [!DNL Customer Attributes] dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/customer-attributes.md) .
