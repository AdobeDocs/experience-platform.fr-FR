---
title: Connexion de votre compte PathFactory à un Experience Platform via l’interface utilisateur
description: Découvrez comment connecter votre compte PathFactory à Experience Platform via l’interface utilisateur.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Version Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 21%

---

# Connectez-vous à [!DNL PathFactory] compte à Experience Platform via l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL PathFactory] Données Visiteurs, sessions et Pages vues vers Adobe Experience Platform via l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL PathFactory] , vous pouvez ignorer le reste de ce document et passer au tutoriel sur [apport de données d’automatisation du marketing à Experience Platform à l’aide de l’interface utilisateur](../../dataflow/marketing-automation.md).

### Collecte des informations d’identification requises {#gather-credentials}

Pour accéder à votre compte PathFactory sur Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Nom d’utilisateur | Nom d’utilisateur de votre compte PathFactory. Ceci est essentiel pour identifier votre compte dans le système. |
| Mot de passe | Mot de passe associé à votre compte PathFactory. Veillez à ce que cette protection soit sécurisée pour empêcher tout accès non autorisé. |
| Domaine | Domaine associé à votre compte PathFactory. Cela fait généralement référence à l’identifiant unique dans votre URL PathFactory. |
| Jeton d’accès | Jeton unique utilisé pour l’authentification API afin d’assurer une communication sécurisée entre vos systèmes et PathFactory. |
| Points de terminaison API | Points de terminaison d’API spécifiques pour l’accès aux données : visiteurs, sessions et pages vues. Chaque point de terminaison correspond à différents jeux de données que vous pouvez récupérer. **Remarque :** Ils sont prédéfinis par [!DNL PathFactory] et sont spécifiques aux données auxquelles vous avez l’intention d’accéder : <ul><li>**Point de terminaison Visiteurs**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Point de terminaison des sessions**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Point de terminaison des pages vues**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Pour obtenir des instructions détaillées sur la manière de sécuriser et d’utiliser vos informations d’identification, ainsi que pour obtenir et actualiser votre jeton d’accès, consultez la page [Centre de support PathFactory](https://support.pathfactory.com/categories/adobe/). Cette ressource propose des guides complets sur la gestion de vos informations d’identification et sur l’intégration efficace et sécurisée de l’API.


## Connecter votre compte [!DNL PathFactory]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. La variable [!UICONTROL Catalogue] affiche diverses sources prises en charge par Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans la liste des catégories. Vous pouvez également utiliser la barre de recherche pour filtrer une source spécifique.

Sous , [!UICONTROL Automatisation du marketing] catégorie, sélectionnez **[!UICONTROL PathFactory]** puis sélectionnez **[!UICONTROL Configuration]**.

![Catalogue des sources avec la source PathFactory sélectionnée.](../../../../images/tutorials/create/pathfactory/catalog.png)

La variable **[!UICONTROL Connexion à PathFactory]** s’affiche. Sur cette page, vous pouvez créer un compte ou utiliser un compte existant.

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom pour votre compte, une description facultative et les informations d’authentification qui correspondent à votre [!DNL PathFactory] compte .

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte dans laquelle vous pouvez authentifier un nouveau compte pour PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Compte existant

Si vous disposez déjà d’un compte, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![Interface du compte existant dans laquelle vous pouvez effectuer une sélection dans une liste de comptes PathFactory existants.](../../../../images/tutorials/create/pathfactory/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion entre votre [!DNL PathFactory] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer vos données d’automatisation marketing dans Experience Platform ;](../../dataflow/marketing-automation.md).
