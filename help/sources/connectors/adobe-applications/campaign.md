---
keywords: Experience Platform;accueil;rubriques populaires;Adobe Campaign Managed Cloud Services;campaign;campaign managed services
title: Adobe Campaign Managed Cloud Services
description: Découvrez comment connecter Campaign Managed Cloud Services à Experience Platform à l’aide de l’interface utilisateur
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 5%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Adobe Campaign Managed Cloud Services propose une plateforme Managed Services pour concevoir des expériences client cross-canal et propose un environnement pour l’orchestration visuelle de campagnes, la gestion d’interactions en temps réel et l’exécution cross-canal. Consultez la [documentation Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=fr) pour plus d’informations.

La source Adobe Campaign Managed Cloud Services vous permet d’importer les données des logs de diffusion et des logs de tracking Adobe Campaign v8 dans Adobe Experience Platform.

## Conditions préalables

Avant de pouvoir créer une connexion source pour importer votre Campaign v8 dans Experience Platform, vous devez d&#39;abord remplir les conditions préalables suivantes :

* [Configurer l&#39;import du journal des événements depuis la console cliente Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Création d’un schéma XDM ExperienceEvent](#create-a-schema)
* [Créer un jeu de données](#create-a-dataset)

### Affichage des données des logs de diffusion et de tracking {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Vous devez avoir accès à la console cliente Adobe Campaign v8 pour afficher vos données de journal dans Campaign. Consultez la [documentation de Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=fr) pour plus d’informations sur le téléchargement et l’installation de la console cliente.

Connectez-vous à votre instance Campaign v8 via la console cliente. Sous l’onglet [!DNL Explorer] , sélectionnez [!DNL Administration] puis [!DNL Configuration]. Sélectionnez ensuite [!DNL Data schemas] puis appliquez le filtre `broadLog` pour le nom ou le libellé. Dans la liste qui s&#39;affiche, sélectionnez le schéma source des logs de diffusion des destinataires intitulé `broadLogRcp`.

![La console cliente Adobe Campaign v8 avec l’onglet Explorateur sélectionné, les nœuds Administration, Configuration et Schémas de données développés et le filtrage défini sur « large ».](./images/campaign/explorer.png)

Sélectionnez ensuite l’onglet **Données**.

![Console cliente Adobe Campaign v8 avec l’onglet Données sélectionné.](./images/campaign/data.png)

Cliquez avec le bouton droit de la souris ou appuyez sur la touche dans le panneau de données pour ouvrir le menu contextuel. À partir de là, sélectionnez **Configurer la liste...**

![La console cliente Adobe Campaign v8 affiche le menu contextuel et l’option Configurer la liste est sélectionnée.](./images/campaign/configure.png)

La fenêtre de configuration de la liste s’affiche, vous fournissant une interface dans laquelle vous pouvez ajouter tous les champs souhaités à la liste préexistante pour afficher les données dans le panneau de données.

![Liste des configurations pour les logs de diffusion des destinataires qui peuvent être ajoutées pour l’affichage.](./images/campaign/list-configuration.png)

Vous pouvez maintenant afficher vos logs de diffusion des destinataires, y compris les champs de configuration ajoutés à l’étape précédente.

>[!TIP]
>
>Vous pouvez répéter les mêmes étapes, mais en filtrant par `tracking` les données de vos logs de tracking.

![Les logs de diffusion des destinataires affichés avec des informations sur leur nom modifié, leur canal de diffusion, leur nom de diffusion interne et leur libellé.](./images/campaign/recipient-delivery-logs.png)

### Créer un schéma {#create-a-schema}

Créez ensuite un schéma XDM ExperienceEvent pour les logs de diffusion et les logs de tracking. Vous devez appliquer le groupe de champs Logs de diffusion Campaign à votre schéma de logs de diffusion et le groupe de champs Logs de tracking Campaign à votre schéma de logs de tracking. Vous devez également définir le champ `externalID` comme identité principale de votre schéma.

>[!NOTE]
>
>Votre schéma XDM ExperienceEvent doit être activé pour le profil pour ingérer vos données Campaign dans [!DNL Real-Time Customer Profile].

Pour obtenir des instructions détaillées sur la création d’un schéma, consultez le guide sur la [création d’un schéma XDM dans l’interface utilisateur](../../../xdm/tutorials/create-schema-ui.md).

### Créer un jeu de données {#create-a-dataset}

Enfin, vous devez créer un jeu de données pour vos schémas. Pour obtenir des instructions détaillées sur la création d’un jeu de données, consultez le guide sur la [création d’un jeu de données dans l’interface utilisateur](../../../catalog/datasets/user-guide.md).

## Créer une connexion source Adobe Campaign Managed Cloud Services à l’aide de l’interface utilisateur d’Experience Platform

Maintenant que vous avez accédé à vos logs de données dans la console cliente Campaign, que vous avez créé un schéma et un jeu de données, vous pouvez passer à la création d’une connexion source pour importer vos données Managed Services Campaign dans Experience Platform.

Pour obtenir des instructions détaillées sur la manière d’importer vos données de logs de diffusion et de logs de tracking Campaign v8 dans Experience Platform, consultez le guide sur la [création d’une connexion source Managed Services gérée dans l’interface utilisateur](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Il existe un cas de figure où l’interaction d’un destinataire d’e-mail récemment supprimé avec un e-mail pourrait réingérer des informations personnelles dans Experience Platform. Dans certains cas, cela peut réactiver le marketing pour cet utilisateur.
>
>* Ce scénario n’est actif qu’entre le moment où une demande d’accès à des informations personnelles a été exécutée dans Experience Platform et celui où elle a été exécutée dans Adobe Campaign Classic. Une fois la demande exécutée dans Campaign, un contrôle est effectué pour s’assurer que l’enregistrement n’est pas exporté vers Campaign. Pour résoudre ce problème, envoyez à nouveau une demande conforme au RGPD 72 heures après l’exécution.