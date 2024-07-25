---
title: Présentation de l’extension Adobe Privacy
description: Découvrez lʼextension de balise Adobe Privacy dans Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 89%

---

# Présentation de l’extension Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’extension de balise d’Adobe Privacy vous permet de collecter et de supprimer les identifiants d’utilisateur affectés aux utilisateurs finaux par les solutions Adobe sur les appareils côté client. Les identifiants collectés peuvent alors être envoyés à [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) pour accéder ou supprimer les données personnelles de l’individu concerné dans les applications Adobe Experience Cloud prises en charge.

Ce guide explique comment installer et configurer l’extension Adobe Privacy dans l’interface utilisateur Experience Platform ou l’interface utilisateur de collecte de données.

>[!NOTE]
>
>Si vous préférez installer ces fonctionnalités sans utiliser de balises, reportez-vous à la [présentation de la bibliothèque Privacy JavaScript](../../../../privacy-service/js-library.md) pour obtenir des instructions sur la mise en oeuvre de l’utilisation du code brut.

## Installation et configuration de l’extension 

Sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, suivi de l’onglet **[!UICONTROL Catalogue]** . Utilisez la barre de recherche pour réduire la liste des extensions disponibles jusqu’à ce que vous trouviez Adobe Privacy. Sélectionnez **[!UICONTROL Installer]** pour continuer.

![Installer l’extension](../../../images/extensions/client/privacy/install.png)

L’écran suivant vous permet de configurer les sources et solutions à partir desquelles l’extension doit collecter les identifiants. Les solutions suivantes sont prises en charge pour l’extension :

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Service d’identités d’Adobe Experience Cloud (Visiteur ou ECID)
* Adobe Advertising Cloud (AdCloud)

Sélectionnez une ou plusieurs solutions, puis cliquez sur **[!UICONTROL Mettre à jour]**.

![Sélectionner des solutions](../../../images/extensions/client/privacy/select-solutions.png)

L’écran se met à jour afin d’afficher les entrées pour les paramètres de configuration requis en fonction des solutions que vous avez sélectionnées.

![Propriétés requises](../../../images/extensions/client/privacy/required-properties.png)

À l’aide du menu déroulant ci-dessous, vous pouvez également ajouter des paramètres supplémentaires spécifiques à une solution à la configuration.

![Propriétés facultatives](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Voir la section sur les [paramètres de configuration](../../../../privacy-service/js-library.md#config-params) dans la présentation de la bibliothèque JavaScript de confidentialité pour plus d’informations sur les valeurs de configuration acceptées pour chaque solution prise en charge.

Une fois que vous avez terminé d’ajouter des paramètres pour les solutions sélectionnées, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la configuration.

![Propriétés facultatives](../../../images/extensions/client/privacy/save-config.png)

## Utilisation de l’extension  {#using}

L’extension Adobe Privacy fournit trois types d’actions qui peuvent être utilisés dans une [règle](../../../ui/managing-resources/rules.md) lorsqu’un certain événement se produit et que les conditions sont remplies :

* **[!UICONTROL Récupération d’identités]** : les informations d’identité stockées de l’utilisateur sont récupérées.
* **[!UICONTROL Suppression d’identités]** : les informations d’identité stockées de l’utilisateur sont supprimées.
* **[!UICONTROL Récupération et suppression des identités]** : les informations d’identité stockées de l’utilisateur sont récupérées, puis supprimées.

Pour chacune des actions ci-dessus, vous devez fournir une fonction JavaScript de rappel qui accepte et gère les données d’identité récupérées en tant que paramètre d’objet. À partir de là, vous pouvez stocker ces identités, les afficher ou les envoyer au [API Privacy Service](../../../../privacy-service/api/overview.md) selon vos besoins.

Lors de l’utilisation de l’extension de balise d’Adobe Privacy, vous devez fournir la fonction de rappel requise sous la forme d’un élément de données. Reportez-vous à la section suivante pour savoir comment configurer cet élément de données.

### Définition d’un élément de données pour gérer les identités

Démarrez le processus de création d’un élément de données en sélectionnant **[!UICONTROL Data Elements]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Add Data Element]**. Une fois que vous êtes sur l’écran de configuration, sélectionnez **[!UICONTROL Core]** pour l’extension et **[!UICONTROL Code personnalisé]** pour le type d’élément de données. À partir de là, sélectionnez **[!UICONTROL Ouvrir l’éditeur]** dans le panneau de droite.

![Sélectionner le type d’élément de données](../../../images/extensions/client/privacy/data-element-type.png)

Dans la boîte de dialogue qui s’affiche, définissez une fonction JavaScript qui gérera les identités récupérées. Le rappel doit accepter un seul argument de type objet (`ids` dans l’exemple ci-dessous). La fonction peut ensuite gérer les identifiants comme vous le souhaitez et peut également appeler les variables et fonctions disponibles globalement sur votre site pour un traitement ultérieur.

>[!NOTE]
>
>Pour plus d’informations sur la structure de l’objet `ids` que la fonction de rappel doit traiter, reportez-vous à la section [exemples de code](../../../../privacy-service/js-library.md#samples) fourni dans la présentation de la bibliothèque JavaScript de confidentialité.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Définition de la fonction de rappel](../../../images/extensions/client/privacy/define-custom-code.png)

Vous pouvez continuer à créer d’autres éléments de données de code personnalisé si vous avez besoin de différents rappels pour différents événements.

### Création d’une règle avec une action de confidentialité

Après avoir configuré un élément de données de rappel pour gérer les identifiants récupérés, vous pouvez créer une règle qui invoque l’extension Adobe Privacy chaque fois qu’un événement spécifique se produit sur votre site, ainsi que toutes les autres conditions dont vous avez besoin.

Lors de la configuration de l’action pour la règle, sélectionnez **[!UICONTROL Adobe Privacy]** pour l’extension. Pour le type d’action, sélectionnez l’une des options suivantes : [trois fonctions](#using) fourni par l’extension.

![Sélectionner le type d’action](../../../images/extensions/client/privacy/action-type.png)

Le panneau de droite vous invite à sélectionner un élément de données qui servira de rappel à l’action. Sélectionnez l’icône de la base de données (![Icône de base de données](/help/images/icons/database.png)) et choisissez l’élément de données que vous avez créé précédemment dans la liste. Sélectionner **[!UICONTROL Conserver les modifications]** pour continuer.

![Sélectionner l’élément de données](../../../images/extensions/client/privacy/add-data-element.png)

À partir de là, vous pouvez continuer à configurer la règle afin que l’action Adobe Privacy se déclenche sous les événements et conditions dont vous avez besoin. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Enregistrer la règle](../../../images/extensions/client/privacy/save-rule.png)

Vous pouvez désormais ajouter la règle à une bibliothèque pour la déployer comme version sur votre site Web à des fins de test. Pour plus d’informations, consultez le guide sur le [flux de publication des balises](../../../ui/publishing/overview.md).

## Désactivation ou désinstallation de l’extension

Après avoir installé l’extension, vous pouvez la désactiver ou la supprimer. Cliquez sur **[!UICONTROL Configurer]** sur la carte Adobe Privacy des extensions installées, puis sélectionnez **[!UICONTROL Désactiver]** ou **[!UICONTROL Désinstaller]**.

## Étapes suivantes

Ce guide a porté sur l’utilisation de l’extension de balise de confidentialité Adobe dans l’interface utilisateur. Pour plus d’informations sur les fonctionnalités fournies par l’extension, y compris des exemples d’utilisation du code brut, voir la section [Présentation de la bibliothèque JavaScript de confidentialité](../../../../privacy-service/js-library.md) dans la documentation du Privacy Service.
