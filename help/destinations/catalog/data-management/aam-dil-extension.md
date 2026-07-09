---
keywords: extension Audience Manager DIL;destination audience manager;extension dil
title: Extension Audience Manager DIL
description: L’extension Audience Manager DIL est une destination de plateforme de gestion des données (DMP) dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
TQID: https://experienceleague.adobe.com/Bh74ytEjMwhanOa1hUaGZxmOx2dtZm8N9sf9Np5o69s
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: f5efb499-54f9-432b-ac5c-599dbac103afid: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2f54212d8592c5ebc45b847c5f8269ddddfeb622
workflow-type: tm+mt
source-wordcount: 508
ht-degree: 37%

---

# Extension Audience Manager DIL {#aam-dil-extension}

## Vue d’ensemble {#overview}

Il s’agit de l’extension de la bibliothèque d’intégration des données (mise en œuvre côté client) d’Adobe Audience Manager. Remarque : cette extension n’est pas destinée à être utilisée pour le transfert côté serveur (SSF) des données [!DNL Adobe Analytics]. Pour SSF, utilisez l’extension [!DNL Adobe Analytics]. Important : à partir de la version 8.0, DIL dépend fortement du service d’identification des visiteurs Adobe, version 3.3 ou ultérieure. Mettez en œuvre le service d’identification des visiteurs et DIL pour des fonctionnalités d’intégration de données [!DNL Audience Manager] complètes.

[!DNL Audience Manager] DIL est une extension de la plateforme de gestion des données (DMP) disponible dans [!DNL Adobe Experience Platform]. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension [](../../../tags/extensions/client/audience-manager/overview.md) dans la documentation sur les balises.

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions dans Experience Platform, consultez la [ présentation des extensions de balises](../launch-extensions/overview.md).

![Extension Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue [!DNL Destinations] pour tous les clients qui ont acheté Experience Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans [!DNL Adobe Experience Platform]. Les balises sont proposées aux clients [!DNL Adobe CX Enterprise] en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur ou l’administratrice de votre organisation pour accéder aux balises et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation l’extension {#install-extension}

Pour installer l’extension [!DNL Audience Manager] DIL :

Dans l’interface [](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Sélectionnez la destination, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si le contrôle **[!UICONTROL Configurer]** est grisé, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Le workflow vous guide tout au long des étapes nécessaires pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension, consultez la page de l’extension [](../../../tags/extensions/client/audience-manager/overview.md) dans la documentation sur les balises.

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, consultez le guide sur [l’ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de la collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la présentation de [rules](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur affiche toujours **[!UICONTROL Installer]** pour l’extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
