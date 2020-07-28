---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur source d'Enregistrement Azure Table dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 14%

---


# Create an [!DNL Azure Table Storage] source connector in the UI

>[!NOTE]
>Le [!DNL Azure Table Storage] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Azure Table Storage] (ci-après dénommé &quot;ATS&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion ATS valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte ATS sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion à votre [!DNL Azure Table Storage] instance. Chaîne de connexion à l’instance ATS. Le modèle de chaîne de connexion pour ATS est `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)d&#39;Enregistrement de table Azure.

## Connecter votre [!DNL Azure Table Storage] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte ATS auquel vous connecter [!DNL Platform].

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">l’Adobe Experience Platform</a> , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui lui sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez Enregistrement **[!UICONTROL de table]** Azure pour afficher une barre d&#39;informations sur le côté droit de l&#39;écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion entrante, sélectionnez **[!UICONTROL Connexion source]**.

![catalogue](../../../../images/tutorials/create/ats/catalog.png)

La page *[!UICONTROL Se connecter à l&#39;Enregistrement]* de table Azure s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos informations d’identification ATS. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/ats/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte ATS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ats/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte ATS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/databases.md).