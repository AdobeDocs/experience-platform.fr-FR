---
keywords: extension du DIL d’Audience Manager;gestionnaire d’audience de destination;extension dil
title: Extension Audience Manager DIL
description: L’extension Audience Manager DIL est une destination de plateforme de gestion des données (DMP) dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 22%

---

# Extension Audience Manager DIL {#aam-dil-extension}

## Présentation {#overview}

Il s’agit de l’extension de la bibliothèque d’intégration des données (mise en œuvre côté client) d’Adobe Audience Manager. Remarque : cette extension n’est pas destinée à être utilisée pour le transfert côté serveur (SSF) des données Adobe Analytics. Pour SSF, utilisez l’extension Adobe Analytics. Important : À partir de la version 8.0, DIL dépend fortement de la variable [!DNL Experience Cloud] Service d’ID, version 3.3 ou ultérieure. Mettez en oeuvre les deux [!DNL Experience Cloud] Service d’ID et DIL pour un accès complet [!DNL Audience Manager] fonctionnalités d’intégration des données.

[!DNL Audience Manager] DIL est une extension de Data Management Platform (DMP) dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, voir [Page d’extension d’Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) dans la documentation sur les balises.

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions dans Platform, voir [Présentation des extensions de balise](../launch-extensions/overview.md).

![Extension Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans la [!DNL Destinations] catalogue pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans Adobe Experience Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre entreprise pour accéder aux balises et demandez-lui de vous accorder la variable **[!UICONTROL manage_properties]** pour pouvoir installer des extensions.

## Installation de l’extension {#install-extension}

Pour installer le [!DNL Audience Manager] Extension de DIL :

Dans [l’interface de Platform](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si la variable **[!UICONTROL Configurer]** Le contrôle est grisé, vous ne trouvez pas la variable **[!UICONTROL manage_properties]** autorisation. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété dans laquelle vous souhaitez installer l’extension. Vous avez également la possibilité de créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. En savoir plus sur les propriétés dans [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Le workflow vous guide tout au long des étapes nécessaires pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension, voir la section [Page d’extension d’Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) dans la documentation sur les balises.

Vous pouvez également installer l’extension directement dans le [Interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Consultez le guide sur la [ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) pour plus d’informations.

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la présentation de [rules](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de la collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur s’affiche toujours. **[!UICONTROL Installer]** pour l’extension . Démarrez le workflow d’installation comme décrit dans la section [Installer l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur la [processus de mise à niveau d&#39;extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
