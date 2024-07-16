---
title: Création d’une connexion source d’événements SugarCRM dans l’interface utilisateur
description: Découvrez comment créer une connexion source d’événements SugarCRM à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 43%

---

# Créer une connexion source [!DNL SugarCRM Events] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL SugarCRM Events] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL SugarCRM], vous pouvez ignorer le reste de ce document et passer au tutoriel expliquant comment [Configurer un flux de données](../../dataflow/crm.md).

### Collecter les informations d’identification requises

Pour connecter [!DNL SugarCRM Events] à Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Host` | Le point d’entrée de l’API SugarCRM auquel la source se connecte. | `developer.salesfusion.com` |
| `Username` | Nom d’utilisateur de votre compte de développeur SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Votre mot de passe du compte de développeur SugarCRM. | `123456789` |

### Création d’un schéma de plateforme pour [!DNL SugarCRM]

Avant de créer une connexion source [!DNL SugarCRM], vous devez également vous assurer de créer au préalable un schéma de plateforme à utiliser pour votre source. Consultez le tutoriel sur la [création d’un schéma de plateforme](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

![ Copie d’écran de l’interface utilisateur de Platform présentant un exemple de schéma pour les événements SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Lors du mappage du schéma, veillez également à mapper les champs `event_id` et `timestamp` obligatoires requis par Platform.

## Connecter votre compte [!DNL SugarCRM Events]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *CRM*, sélectionnez **[!UICONTROL SugarCRM Events]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Copie d’écran de l’interface utilisateur de Platform pour le catalogue avec carte Événements SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

La page **[!UICONTROL Se connecter au compte d’événements SugarCRM]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL SugarCRM Events] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![ Copie d’écran de l’interface utilisateur de Platform pour le compte Connect SugarCRM Events avec un compte existant ](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![ Copie d’écran de l’interface utilisateur de Platform pour le compte Connect SugarCRM Events avec un nouveau compte ](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL SugarCRM Events]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).

## Ressources supplémentaires

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL SugarCRM].

### Mécanismes de sécurisation {#guardrails}

Les taux de ralentissement de l’API [!DNL SugarCRM] sont de 90 appels par minute ou de 2 000 appels par jour, selon ce qui se produit en premier. Toutefois, cette restriction a été contournée en ajoutant un paramètre dans la spécification de connexion qui retardera le temps de demande afin que la limite de taux ne soit jamais atteinte.

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et que les données [!DNL SugarCRM Events] sont en cours d’ingestion, procédez comme suit :

* Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Afficher les flux de données]** en regard du menu de carte [!DNL SugarCRM Events] du catalogue des sources. Sélectionnez ensuite **[!UICONTROL Prévisualiser le jeu de données]** pour vérifier les données ingérées.

* Selon le type d’objet que vous utilisez, vous pouvez vérifier les données agrégées par rapport aux nombres visibles sur la page [!DNL SugarMarket] Events ci-dessous :

![Capture d&#39;écran de la page Comptes SugarMarket affichant la liste des comptes](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Les pages [!DNL SugarMarket] n’incluent pas le nombre d’objets supprimés. Toutefois, les données récupérées via cette source incluent également le nombre supprimé, qui sera marqué d’un indicateur supprimé.
