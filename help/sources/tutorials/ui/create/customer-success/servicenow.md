---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source ServiceNow dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 16%

---


# Create a [!DNL ServiceNow] source connector in the UI

>[!NOTE]
>Le [!DNL ServiceNow] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur [!DNL ServiceNow] source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une [!DNL ServiceNow] connexion, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données.](../../dataflow/customer-success.md)

### Collecte des informations d’identification requises

Pour accéder à votre [!DNL ServiceNow] compte [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point de terminaison du [!DNL ServiceNow] serveur. |
| `username` | Nom d’utilisateur utilisé pour la connexion au [!DNL ServiceNow] serveur pour l’authentification. |
| `password` | Mot de passe de connexion au [!DNL ServiceNow] serveur pour l’authentification. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

## Connecter votre [!DNL ServiceNow] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau [!DNL ServiceNow] compte auquel vous connecter [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui lui sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie de succès ** client, sélectionnez **[!UICONTROL ServiceNow]** pour afficher une barre d’informations sur la droite de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer un compte, sélectionnez **[!UICONTROL Connexion source]**.

![](../../../../images/tutorials/create/servicenow/catalog.png)

La page *[!UICONTROL Se connecter à ServiceNow]* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos [!DNL ServiceNow] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![](../../../../images/tutorials/create/servicenow/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL ServiceNow] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre [!DNL ServiceNow] compte. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/customer-success.md).
