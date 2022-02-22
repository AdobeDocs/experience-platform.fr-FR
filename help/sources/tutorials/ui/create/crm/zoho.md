---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Création d’une connexion source CRM Zoho dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Zoho CRM à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 11%

---

# Créez un [!DNL Zoho CRM] connexion source dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’ingérer des données CRM externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Zoho CRM] connecteur source à l’aide de [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Le cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel de l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un [!DNL Zoho CRM] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

Pour vous connecter [!DNL Zoho CRM] Pour Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| --- | --- |
| Point d’entrée | Le point de terminaison de [!DNL Zoho CRM] le serveur vers lequel vous effectuez votre demande. |
| URL des comptes | L’URL des comptes est utilisée pour générer vos jetons d’accès et d’actualisation. L’URL doit être spécifique au domaine. |
| Identifiant du client | L’identifiant client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| Secret du client | Le secret client qui correspond à votre [!DNL Zoho CRM] compte utilisateur. |
| Jeton d’accès | Le jeton d’accès autorise votre accès sécurisé et temporaire à votre [!DNL Zoho CRM] compte . |
| Actualiser le jeton | Un jeton d’actualisation est un jeton utilisé pour générer un nouveau jeton d’accès, une fois que votre jeton d’accès a expiré. |

Pour plus d’informations sur ces informations d’identification, consultez la documentation sur [[!DNL Zoho CRM] authentication](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connectez-vous à [!DNL Zoho CRM] account

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Zoho CRM] compte à [!DNL Platform].

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL CRM] catégorie, sélectionnez **[!UICONTROL Zoho CRM]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/zoho/catalog.png)

Le **[!UICONTROL Connexion au compte CRM Zoho]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL Zoho CRM] compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/zoho/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et votre [!DNL Zoho CRM] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir la nouvelle connexion.

>[!TIP]
>
>Votre domaine URL de compte doit correspondre à l’emplacement de domaine approprié. Vous trouverez ci-dessous les différents domaines et les URL de leurs comptes correspondants :<ul><li>États-Unis : https://accounts.zoho.com</li><li>Australie : https://accounts.zoho.com.au</li><li>Europe : https://accounts.zoho.eu</li><li>Inde : https://accounts.zoho.in</li><li>Chine : https://accounts.zoho.com.cn</li></ul>

![new](../../../../images/tutorials/create/zoho/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre [!DNL Zoho CRM] compte . Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données dans Platform](../../dataflow/crm.md).
