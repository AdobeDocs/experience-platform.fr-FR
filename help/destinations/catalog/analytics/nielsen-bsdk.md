---
keywords: Nielsen BSDK;nielsen bsdk;nielsen BSDK
title: Extension Nielsen BSDK
description: L’extension Nielsen BSDK est une destination d’analyse dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: e1c10673-e3f4-474d-98d7-960124b2bfc7
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 92%

---

# Extension [!DNL Nielsen BSDK] {#nielsen-bsdk-extension}

## Présentation {#overview}

[!DNL Nielsen Digital SDK] l’extension de balise permet de mesurer l’audience à l’aide des produits de mesure numérique suivants :

DCR : une solution de mesure qui permet de mesurer quotidiennement le contenu numérique non linéaire, y compris le contenu comportant des publicités, et d’obtenir une vue exhaustive de la consommation du contenu numérique par l’audience sur les ordinateurs de bureau, les téléphones portables, les tablettes et les appareils connectés.

DTVR : cette solution tient compte du visionnage linéaire de la télévision sur les ordinateurs de bureau et les appareils mobiles pour les sources de programmation participantes. Il s’agit de la première solution ayant obtenu une accréditation du MRC pour sa contribution à la mesure de l’audience télévisuelle pour les programmes visionnés sur des ordinateurs et des appareils mobiles.

[!DNL Nielsen BSDK] est une extension d’analyse dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Platform, voir la [présentation des extensions de balises](../launch-extensions/overview.md).

![Extension Nielsen BSDK](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue [!DNL Destinations] pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez avoir accès aux balises dans Adobe Experience Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur ou l’administratrice de votre organisation pour accéder aux balises et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation l’extension {#install-extension}

Pour installer le [!DNL Nielsen BSDK] extension :

Dans l’[interface de Platform](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail droit. Si la commande **[!UICONTROL Configurer]** est grisée, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page propriétés](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentation sur les balises.

Le workflow vous guide tout au long des étapes nécessaires pour terminer l’installation.

Pour plus d’informations sur les options de configuration d’extension et la prise en charge de l’installation, consultez la [page consacrée à Nielsen BSDK sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, voir la section sur l’[ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) dans la documentation sur les balises.

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles.

Vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation sur les balises](../../../tags/ui/managing-resources/rules.md).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur de Platform continue d’afficher **[!UICONTROL Installer]** pour cette extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
