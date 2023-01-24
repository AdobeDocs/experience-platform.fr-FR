---
title: Création d’une connexion source d’événements SugarCRM dans l’interface utilisateur
description: Découvrez comment créer une connexion source d’événements SugarCRM à l’aide de l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 47%

---

# (Version bêta) Créez un [!DNL SugarCRM Events] connexion source dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL SugarCRM Events] est en version Beta. Voir la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta. 

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL SugarCRM Events] connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

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

### Création d’un schéma Platform pour [!DNL SugarCRM]

Avant de créer un [!DNL SugarCRM] connexion source, vous devez également vous assurer de créer au préalable un schéma Platform à utiliser pour votre source. Voir le tutoriel sur [création d’un schéma Platform](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

![Copie d’écran de l’interface utilisateur de Platform présentant un exemple de schéma pour les événements SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Lors du mappage du schéma, veillez également à mapper le `event_id` et `timestamp` champs requis par Platform.

## Connecter votre compte [!DNL SugarCRM Events]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *CRM* catégorie, sélectionnez **[!UICONTROL Événements SugarCRM]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Copie d’écran de l’interface utilisateur de Platform pour le catalogue avec carte Événements SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

Le **[!UICONTROL Connexion au compte Événements SugarCRM]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL SugarCRM Events] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Copie d’écran de l’interface utilisateur de Platform pour le compte Connect SugarCRM Events avec un compte existant](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Copie d’écran de l’interface utilisateur de Platform pour le compte Connect SugarCRM Events avec un nouveau compte](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL SugarCRM Events]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).

## Ressources supplémentaires

Les sections ci-dessous contiennent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la variable [!DNL SugarCRM] source.

### Barrières de sécurité {#guardrails}

Le [!DNL SugarCRM] Les taux de ralentissement de l’API sont de 90 appels par minute ou de 2 000 appels par jour, selon ce qui se produit en premier. Toutefois, cette restriction a été contournée en ajoutant un paramètre dans la spécification de connexion qui retardera le temps de demande afin que la limite de taux ne soit jamais atteinte.

### Validation {#validation}

Pour vérifier que vous avez correctement configuré la source et [!DNL SugarCRM Events] en cours d’ingestion des données, procédez comme suit :

* Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Afficher les flux de données]** en regard de la variable [!DNL SugarCRM Events] menu de carte dans le catalogue des sources. Ensuite, sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]** pour vérifier les données ingérées.

* En fonction du type d’objet que vous utilisez, vous pouvez vérifier les données agrégées par rapport aux nombres visibles sur la variable [!DNL SugarMarket] Page Événements ci-dessous :

![Capture d&#39;écran de la page Comptes SugarMarket affichant la liste des comptes](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Le [!DNL SugarMarket] Les pages n’incluent pas le nombre d’objets supprimés. Toutefois, les données récupérées via cette source incluent également le nombre supprimé, qui sera marqué d’un indicateur supprimé.