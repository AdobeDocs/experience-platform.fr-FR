---
keywords: plate-forme;destinations;destinations workspace;workspace;ui;destinations ui;catalog;destinations catalog;destinations catalog;destinations catalog;
title: Espace de travail des destinations
description: 'L’espace de travail Destinations se compose de quatre sections : Catalogue, Parcourir, Comptes et Vue système. Ils sont décrits dans les sections ci-dessous.'
seo-description: Dans Adobe Experience Platform, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
translation-type: tm+mt
source-git-commit: eaa4a7efc248104d823267eca574f2eca16edc3f
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 22%

---

# Espace de travail des destinations {#destinations-workspace}

## Présentation {#overview}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Destinations].

L&#39;espace de travail [!UICONTROL Destinations] comprend quatre sections, [!UICONTROL Catalogue], [!UICONTROL Parcourir], [!UICONTROL Comptes] et [!UICONTROL Vue système], décrites dans les sections ci-dessous.

![Présentation des destinations](../assets/ui/workspace/destinations-workspace.png)

## [!UICONTROL Catalogue] {#catalog}

L&#39;onglet **[!UICONTROL Catalogue]** affiche une liste de toutes les destinations disponibles dans [!DNL Platform], à laquelle vous pouvez envoyer des données.

L&#39;interface utilisateur [!DNL Platform] fournit plusieurs options de recherche et de filtrage sur la page de catalogue de destinations :

* Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique.
* Filtrez les destinations à l&#39;aide du contrôle [!UICONTROL Catégories].
* Basculez entre [!UICONTROL Toutes les destinations] et [!UICONTROL Mes destinations]. Lorsque vous sélectionnez **[!UICONTROL Toutes les destinations]**, toutes les destinations [!DNL Platform] disponibles s’affichent. Lorsque vous sélectionnez **[!UICONTROL Mes destinations]**, vous ne pouvez afficher que les destinations avec lesquelles vous avez établi une connexion.
* Sélectionnez **[!UICONTROL Connexions]** et/ou **[!UICONTROL Extensions]** pour la vue. Pour comprendre la différence entre les deux catégories, voir [Types et Catégories de destination](../destination-types.md).

![destinations filtrage et démonstration de recherche](../assets/ui/workspace/destinations-search-and-filter.gif)

Les cartes de destination contiennent soit un contrôle **[!UICONTROL Configurer]**, soit un contrôle **[!UICONTROL Activer]** et un contrôle secondaire qui affiche plus d&#39;options. Ces contrôles sont décrits ci-dessous :

| Contrôle | Description |
|---------|----------|
| [!UICONTROL Configuration] | Permet de créer une connexion à la destination. |
| [!UICONTROL Activer] | Une fois que vous avez établi une connexion à la destination, vous pouvez activer des segments. |
| [!UICONTROL Compte vue] | Vue des comptes que vous avez connectés pour une destination. |
| [!UICONTROL Flux de données de vue] | Vue des flux d’activation de données qui existent pour une destination. |
| [!UICONTROL Documentation sur la vue] | Ouvre un lien vers la page de documentation de cette destination spécifique, pour plus d’informations et pour vous aider à la configurer. |

{style=&quot;table-layout:auto&quot;}

![Contrôles sur la carte de destination](../assets/ui/workspace/destination-card-options.png)

Sélectionnez une carte de destination dans le catalogue pour ouvrir le rail de droite. Vous pouvez voir ici une description de la destination. Le rail droit fournit les mêmes commandes que celles décrites dans le tableau ci-dessus, y compris une description de la destination et une indication de la catégorie et du type de destination.

![Options du catalogue des destinations](../assets/ui/workspace/destination-right-rail.png)

Pour plus d&#39;informations sur les catégories de destination et les informations sur chaque destination, consultez les [Catalogue de destination](../catalog/overview.md) et [Types et catégories de destination](../destination-types.md).

## [!UICONTROL Comptes] {#accounts}

L&#39;onglet **[!UICONTROL Comptes]** affiche des détails sur les connexions que vous avez établies avec différentes destinations et vous permet de mettre à jour les détails de connexion existants. Voir [Mettre à jour les comptes](update-accounts.md) pour obtenir des instructions détaillées.

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Les destinations avec la bascule **[!UICONTROL Activé/Désactivé]** activée ont pour effet de définir la destination sur principal ou inactif, respectivement. Vous pouvez également vue les destinations vers lesquelles vos données circulent en sélectionnant **[!UICONTROL Segments]** > **[!UICONTROL Parcourir]** et en sélectionnant un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

>[!TIP]
>
> * Utilisez le bouton ![Ajouter les segments](../assets/ui/workspace/add-data-symbol.png) de la colonne **[!UICONTROL Nom]** pour [activer](activate-destinations.md) d&#39;autres segments vers cette destination.
> * Utilisez le bouton ![Supprimer les destinations](../assets/ui/workspace/delete-destination-symbol.png) de la colonne **[!UICONTROL Nom]** pour [supprimer](delete-destinations.md) une connexion existante à une destination.


![Onglet Parcourir](../assets/ui/workspace/browse-tab.png)

| Élément | Description |
|---------|----------|
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. La même colonne comprend deux contrôles : [!UICONTROL Activer ] et [!UICONTROL Supprimer la destination]. |
| [!UICONTROL État de la dernière exécution du flux] | Statut de la dernière exécution de flux de données. Voir [détails de destination de la Vue](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Date d&#39;exécution du dernier flux] | Heure et date de la dernière exécution du flux de données. Voir [détails de destination de la Vue](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par courriel : Peut être S3, FTP ou [!DNL Azure Blob].</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur.</li><li>Pour les destinations de diffusion en continu : Peut être [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Données d’Activation] | Indique le nombre de segments activés pour cette destination. Sélectionnez ce contrôle pour en savoir plus sur les segments activés. Pour plus d’informations sur les segments activés, voir [Données d’Activation](/help/destinations/ui/destination-details-page.md#activation-data) dans la page des détails de destination. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. |
| [!UICONTROL État] | `Active` ou `Inactive`. Indique si les données sont activées pour cette destination. Pour modifier le statut, consultez [Désactiver l’activation](./activate-destinations.md#disable-activation). |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](../assets/ui/workspace/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## [!UICONTROL Vue du système] {#system-view}

L&#39;onglet **[!UICONTROL Vue système]** affiche une représentation graphique des flux d&#39;activation que vous avez configurés dans le Adobe Experience Platform.

![Flux de données 1](../assets/ui/workspace/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page et cliquez sur **[!UICONTROL Flux de Vue]** pour afficher des informations sur toutes les connexions que vous avez configurées pour chaque destination.

![Flux de données 2](../assets/ui/workspace/data-flows2.png)
