---
title: Connectez votre compte PathFactory à Experience Platform via l’interface utilisateur
description: Découvrez comment connecter votre compte PathFactory à Experience Platform via l’interface utilisateur.
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 18%

---

# Connecter votre compte [!DNL PathFactory] à Experience Platform via l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour connecter vos données [!DNL PathFactory] Visiteurs, sessions et pages vues à Adobe Experience Platform via l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL PathFactory], vous pouvez ignorer le reste de ce document et passer au tutoriel sur [l’importation de données d’automatisation du marketing dans Experience Platform à l’aide de l’interface utilisateur](../../dataflow/marketing-automation.md).

### Collecter les informations d’identification requises {#gather-credentials}

Pour accéder à votre compte PathFactory sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Nom d’utilisateur | Nom d’utilisateur de votre compte PathFactory. Cela est essentiel pour identifier votre compte dans le système. |
| Mot de passe | Mot de passe associé à votre compte PathFactory. Assurez-vous que cela est sécurisé pour empêcher tout accès non autorisé. |
| Domaine | Domaine associé à votre compte PathFactory. Cela fait généralement référence à l’identifiant unique dans votre URL PathFactory. |
| Jeton d’accès | Jeton unique utilisé pour l’authentification de l’API afin de garantir une communication sécurisée entre vos systèmes et PathFactory. |
| Points d’entrée de l’API | Points d’entrée d’API spécifiques pour accéder aux données : visiteurs, sessions et pages vues. Chaque point d’entrée correspond à différents jeux de données que vous pouvez récupérer. **Remarque :** ils sont prédéfinis par [!DNL PathFactory] et sont spécifiques aux données auxquelles vous avez l’intention d’accéder : <ul><li>**Point d’entrée Visiteurs** : `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Point d’entrée Sessions** : `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Point d’entrée Pages vues** : `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Pour obtenir des instructions détaillées sur la sécurisation et l’utilisation de vos informations d’identification, ainsi que des informations sur l’obtention et l’actualisation de votre jeton d’accès, consultez le [Centre d’assistance PathFactory](https://support.pathfactory.com/categories/adobe/). Cette ressource propose des guides complets sur la gestion de vos informations d’identification et la garantie d’une intégration d’API efficace et sécurisée.


## Connecter votre compte [!DNL PathFactory]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Le [!UICONTROL Catalogue] affiche diverses sources prises en charge par Experience Platform.

Vous pouvez sélectionner la catégorie appropriée dans la liste des catégories. Vous pouvez également utiliser la barre de recherche pour filtrer une source spécifique.

Dans la catégorie [!UICONTROL Automatisation marketing], sélectionnez **[!UICONTROL PathFactory]** puis sélectionnez **[!UICONTROL Configurer]**.

![Le catalogue des sources avec la source PathFactory sélectionnée.](../../../../images/tutorials/create/pathfactory/catalog.png)

La page **[!UICONTROL Se connecter à PathFactory]** s’affiche. Sur cette page, vous pouvez créer un compte ou utiliser un compte existant.

### Nouveau compte

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** et indiquez un nom de compte, une description facultative et les informations d’authentification qui correspondent à votre compte [!DNL PathFactory].

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Nouvelle interface de compte dans laquelle vous pouvez authentifier un nouveau compte pour PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Compte existant

Si vous disposez déjà d’un compte, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste qui s’affiche.

![Interface du compte existant dans laquelle vous pouvez effectuer une sélection dans une liste de comptes PathFactory existants.](../../../../images/tutorials/create/pathfactory/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion entre votre compte [!DNL PathFactory] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer vos données d’automatisation du marketing dans Experience Platform](../../dataflow/marketing-automation.md).
