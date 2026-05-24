---
keywords: extension publicitaire ; destination publicitaire
title: Extension Adobe Advertising
description: L’extension Adobe Advertising est une destination publicitaire dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
TQID: https://experienceleague.adobe.com/4hYx-JGJE4F7GP5JoI-JSPOp7NRNbGEvHzOrXAv8AGw
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: ae2cba0e-54f2-464b-a3b3-ad371e8a886a
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
  - id: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 414
ht-degree: 36%

---

# Extension [!DNL Adobe Advertising] {#adobe-advertising-cloud-extension}

## Vue d’ensemble {#overview}

Il s’agit de l’extension [!DNL Adobe Advertising] pour l’implémentation de la conversion publicitaire et des balises d’audience pour DSP et Search (DCO n’est actuellement pas pris en charge).

[!DNL Adobe Advertising] est une extension publicitaire en [!DNL Adobe Experience Platform].

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Experience Platform, consultez la [&#x200B; présentation des extensions de balises](../launch-extensions/overview.md).

![Extension &#x200B;](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour tous les clients qui ont acheté Experience Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans Experience Platform. Les balises sont proposées aux clients [!DNL Adobe CX Enterprise] en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur ou l’administratrice de votre organisation pour accéder aux fonctionnalités de collecte de données dans l’interface utilisateur et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer des extensions.

## Installation l’extension {#install-extension}

Pour installer l’extension [!DNL Adobe Advertising], procédez comme suit :

Dans l’interface d’[&#128279;](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Sélectionnez la destination, puis sélectionnez **[!UICONTROL Configure]** dans le rail de droite. Si le contrôle **[!UICONTROL Configure]** est grisé, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété de balise dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md).

Le workflow vous mène à l’interface utilisateur de la collecte de données pour terminer l’installation.

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, consultez le guide sur [l’ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de la collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la présentation de [rules](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur affiche toujours **[!UICONTROL Install]** pour cette extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
