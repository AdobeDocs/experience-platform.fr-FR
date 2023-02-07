---
title: Création d’une connexion source Eloqua d’Oracle à l’aide de l’interface utilisateur de Platform
description: Découvrez comment connecter Adobe Experience Platform à Oracle Eloqua à l’aide de l’interface utilisateur de Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 59%

---

# Créez un [!DNL Oracle Eloqua] Connexion source à l’aide de l’interface utilisateur de Platform

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Oracle Eloqua] connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce guide nécessite une connaissance pratique des composants suivants de Platform :

* [Sources](../../../../home.md) : Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Platform fournit des sandbox virtuelles qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Si vous disposez déjà d’un compte authentifié [!DNL Oracle Eloqua] sur Platform, alors vous pouvez ignorer le reste de ce document et passer au tutoriel sur comment [créer un flux de données pour apporter les données d’automatisation du marketing à Platform](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises

Pour connecter [!DNL Oracle Eloqua] à Platform, vous devez fournir des valeurs pour les propriétés d’authentification suivantes :

| Informations d’identification | Description |
| --- | --- |
| Point d’entrée | Le point de terminaison de votre [!DNL Oracle Eloqua] serveur. [!DNL Oracle Eloqua] prend en charge plusieurs centres de données. Pour trouver votre point de terminaison, connectez-vous au [[!DNL Oracle Eloqua] interface](https://login.eloqua.com) avec vos informations d’identification, puis copiez la partie URL de base à partir de l’URL de redirection. Le format de votre modèle d’URL est le suivant : `xxx.xx.eloqua.com` et doivent être saisies sans `http` ou `https`. |
| Nom d’utilisateur | Le nom d’utilisateur de votre [!DNL Oracle Eloqua] serveur. Le nom d’utilisateur doit être formaté en tant que `siteName + \\ + username`où `siteName` est le nom de l’entreprise à laquelle vous vous êtes connecté. [!DNL Oracle Eloqua] et `username` est votre nom d’utilisateur. Par exemple, votre nom d’utilisateur de connexion peut être : `Eloqua\Andy`. **Remarque**: Vous devez utiliser une seule barre oblique inverse (`\`) lors de l’utilisation de l’interface utilisateur, car l’interface utilisateur Experience Platform ajoute automatiquement une barre oblique inverse supplémentaire (`\`) lors de la saisie d’un nom d’utilisateur. |
| Mot de passe | Le mot de passe correspondant à votre [!DNL Oracle Eloqua] nom d’utilisateur. |

Pour plus d’informations sur les informations d’authentification pour [!DNL Oracle Eloqua], consultez le [[!DNL Oracle Eloqua] guide sur l’authentification](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Oracle Eloqua] à Platform.

## Connecter votre compte [!DNL Oracle Eloqua]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL Oracle Eloqua]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Le **[!UICONTROL Connexion au compte Eloqua Oracle]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Oracle Eloqua] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et les valeurs appropriées pour votre [!DNL Oracle Eloqua] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![nouveau](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et avez créé une connexion source entre votre compte [!DNL Oracle Eloqua] et Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour apporter les données d’automatisation du marketing à Platform](../../dataflow/marketing-automation.md).
