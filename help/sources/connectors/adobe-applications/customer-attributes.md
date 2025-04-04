---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur Attributs du client
solution: Experience Platform
title: Présentation du connecteur Source des attributs du client
description: Découvrez comment connecter les attributs du client à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 12%

---

# Connecteur Attributs du client

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) dans Experience Cloud vous permet de télécharger vos données d’entreprise capturées à partir d’une base de données de gestion de la relation client (GRC). Vous pouvez charger les données dans une source de données d’attributs du client dans Experience Cloud, puis les utiliser dans Adobe Analytics et Adobe Target.

Experience Platform prend en charge l’ingestion de données de profil [!DNL Customer Attributes] dans Adobe Experience Platform.

## Jeux de données et schémas

La source de [!DNL Customer Attributes] crée automatiquement le jeu de données dans lequel les données doivent atterrir. Ce jeu de données créé automatiquement est fixe et ne peut pas être sélectionné manuellement. La source crée également automatiquement le schéma du jeu de données en fonction de la source de données d’entrée. Ce processus implique également la création automatique des mappages nécessaires entre le schéma et les données sources.

## Identités

L’identité principale d’un jeu de données est contenue dans la première colonne du fichier CSV des données sources. La source [!DNL Customer Attributes] suppose que l’identité est toujours mappée à l’espace de noms [`CORE`](../../../identity-service/features/namespaces.md), un espace de noms généré par le système et pris en charge par [[!DNL Identity Service]](../../../identity-service/home.md).

Vous ne pouvez pas sélectionner d’espace de noms existant pour l’identité lors de l’utilisation de [!DNL Customer Attributes] source, car [!DNL Customer Attributes] suppose que l’identité principale du schéma se trouve toujours dans le mappage d’identités. [!DNL Customer Attributes] crée ensuite le mappage de l’ID source à l’UUID de mappage d’identité de manière automatisée.

Pour que les données [!DNL Customer Attributes] soient liées à d’autres jeux de données [!DNL Profile], leurs données et identités doivent pouvoir être associées à un Experience Cloud ID.

Vous pouvez établir l’espace de noms `CORE` en définissant l’Experience Cloud ID pour le visiteur à l’aide de [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) ou de l’API [du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr).

Le fichier [!DNL Customer Attributes] ne renseigne pas d’autres relations d’identité. Par exemple, si un jeu de données source [!DNL Customer Attributes] contient un champ **E-mail** et **Identifiant de fidélité**, ces champs doivent être libellés comme des champs d’identité dans le schéma afin d’être traités en [!DNL Identity Service].

Pour plus d’informations, consultez le tutoriel sur la [création d’une connexion source [!DNL Customer Attributes] dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/customer-attributes.md).
