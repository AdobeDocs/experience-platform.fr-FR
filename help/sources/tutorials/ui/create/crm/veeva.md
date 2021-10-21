---
keywords: Experience Platform ; accueil ; sujets populaires ; Veeva CRM ; veeva
solution: Experience Platform
title: Créer une connexion source CRM Veeva dans l'interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Veeva CRM à l’aide de l’interface utilisateur Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: 8b4e3b9e95dd4c2ff8f3b5a1399eb7d114024bb6
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 13%

---

# Créer un [!DNL Veeva CRM] connexion source dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’assimiler des données CRM externes sur une base planifiée. Ce tutoriel explique comment créer une [!DNL Veeva CRM] connecteur source utilisant [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel sur l’éditeur de schéma](../../../../../xdm/tutorials/create-schema-ui.md): Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schéma.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’un [!DNL Veeva CRM] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d&#39;un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

| Informations d&#39;identification | Description |
| ---------- | ----------- |
| `environmentUrl` | L’URL de la [!DNL Veeva CRM] instance source. |
| `username` | Le nom d’utilisateur du [!DNL Veeva CRM] compte utilisateur. |
| `password` | Le mot de passe pour le [!DNL Veeva CRM] compte utilisateur. |
| `securityToken` | Le jeton de sécurité pour le [!DNL Veeva CRM] compte utilisateur. |

Pour plus d’informations sur la prise en main, reportez-vous à [[!DNL Veeva CRM] document](https://developer.veevacrm.com/api/#order-management-rest-api).

## Connectez-vous [!DNL Veeva CRM] compte

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Veeva CRM] compte [!DNL Platform].

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] espace de travail. Le [!UICONTROL Catalogue] affiche une variété de sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous [!UICONTROL CRM] catégorie, sélectionnez **[!UICONTROL Veeva CRM]**, puis sélectionnez **[!UICONTROL Ajout de données]**.

![catalogue](../../../../images/tutorials/create/veeva/catalog.png)

Le **[!UICONTROL Connexion d’un compte Veeva CRM]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez l’option [!DNL Veeva CRM] compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/veeva/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis indiquez un nom, une description facultative et votre [!DNL Veeva CRM] informations d&#39;identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis laissez un certain temps pour que la nouvelle connexion s&#39;établisse.

![new](../../../../images/tutorials/create/veeva/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre [!DNL Veeva CRM] compte. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/crm.md).
