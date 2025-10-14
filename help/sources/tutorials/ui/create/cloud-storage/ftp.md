---
keywords: Experience Platform;accueil;rubriques populaires;FTP;ftp
solution: Experience Platform
title: Création d’une connexion Source FTP dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source FTP à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 31%

---

# Créer une connexion source FTP dans l’interface utilisateur

>[!NOTE]
>
>Le connecteur FTP est en version bêta. Consultez la [&#x200B; Présentation des sources &#x200B;](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés Beta.

Ce tutoriel décrit les étapes à suivre pour créer une connexion source FTP à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion FTP valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [la configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Pour connecter à FTP, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur FTP. |
| `username` | Nom d’utilisateur ayant accès à votre serveur FTP. |
| `password` | Mot de passe de votre serveur FTP. |

## Connexion à votre serveur FTP

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour créer un compte FTP afin de vous connecter à Experience Platform.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte entrant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL FTP]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer une connexion FTP.

![catalogue](../../../../images/tutorials/create/ftp/catalog.png)

La page **[!UICONTROL Connexion à FTP]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![nouveau](../../../../images/tutorials/create/ftp/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ftp/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte FTP. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de votre espace de stockage dans Experience Platform](../../dataflow/batch/cloud-storage.md).
