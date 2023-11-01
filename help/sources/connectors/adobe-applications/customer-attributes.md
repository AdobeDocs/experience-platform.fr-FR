---
keywords: Experience Platform;accueil;rubriques les plus consultées;connecteur Attributs du client
solution: Experience Platform
title: Présentation du connecteur source des attributs du client
description: Découvrez comment connecter les attributs du client à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 23%

---

# Connecteur Attributs du client

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=fr) dans Experience Cloud vous permet de charger vos données d’entreprise capturées à partir d’une base de données de gestion de la relation client (CRM). Vous pouvez charger les données dans une source de données d’attributs du client dans Experience Cloud, puis les utiliser dans Adobe Analytics et Adobe Target.

Experience Platform prend en charge l’ingestion [!DNL Customer Attributes] données de profil dans Adobe Experience Platform.

## Jeux de données et schémas

La variable [!DNL Customer Attributes] source crée automatiquement le jeu de données dans lequel les données doivent être envoyées. Ce jeu de données créé automatiquement est corrigé et ne peut pas être sélectionné manuellement. La source crée également automatiquement le schéma du jeu de données en fonction de la source de données d’entrée. Ce processus implique également la création automatique des mappages nécessaires entre le schéma et les données source.

## Identités

L’identité principale d’un jeu de données est contenue dans la première colonne du fichier CSV des données source. La variable [!DNL Customer Attributes] source suppose que l’identité est toujours mappée à la variable [`CORE` namespace](../../../identity-service/namespaces.md), un espace de noms généré par le système qui est pris en charge par [[!DNL Identity Service]](../../../identity-service/home.md).

Vous ne pouvez pas sélectionner un espace de noms existant pour l’identité lors de l’utilisation de [!DNL Customer Attributes] source car [!DNL Customer Attributes] suppose que l’identité principale du schéma figure toujours dans la carte d’identité. [!DNL Customer Attributes] crée ensuite le mappage de l’ID source à l’UUID de carte d’identité de manière automatisée.

Pour [!DNL Customer Attributes] données à lier à d’autres [!DNL Profile] les jeux de données, ses données et ses identités doivent pouvoir être associés à un identifiant Experience Cloud.

Vous pouvez définir la variable `CORE` en définissant l’ID d’Experience Cloud du visiteur à l’aide de [SDK Web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=fr), [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/), ou la variable [API du service d’ID Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr).

La variable [!DNL Customer Attributes] ne renseigne aucune autre relation d’identité. Par exemple, si une variable [!DNL Customer Attributes] Le jeu de données source contient un **Email** et un **Loyalty ID** , ces champs doivent ensuite être étiquetés comme champs d’identité dans le schéma pour être traités dans [!DNL Identity Service].

Voir le tutoriel sur [création d’un [!DNL Customer Attributes] connexion source dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/customer-attributes.md) pour plus d’informations.
