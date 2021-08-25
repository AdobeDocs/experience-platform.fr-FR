---
keywords: plateforme;destinations;espace de travail des destinations;espace de travail;ui;interface utilisateur des destinations;catalogue;catalogue des destinations
title: Espace de travail des destinations
description: 'L’espace de travail des destinations se compose de quatre sections : Catalogue, Parcourir, Comptes et Vue du système. Elles sont décrites dans les sections ci-dessous.'
seo-description: In Adobe Experience Platform, select Destinations from the left navigation bar to access the destinations workspace.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 20%

---

# Espace de travail des destinations {#destinations-workspace}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Destinations].

L’espace de travail [!UICONTROL Destinations] se compose de cinq sections : [!UICONTROL Aperçu], [!UICONTROL Catalogue], [!UICONTROL Parcourir], [!UICONTROL Comptes] et [!UICONTROL Vue du système], décrites dans les sections ci-dessous.

![Présentation des destinations](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Présentation] {#overview}

L’onglet **[!UICONTROL Aperçu]** affiche le tableau de bord [!UICONTROL Destinations], fournissant des mesures clés liées aux données de destination de votre entreprise. Pour en savoir plus, consultez le guide de tableau de bord [[!UICONTROL Destinations]](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si votre entreprise est une nouvelle société Experience Platform qui ne possède pas encore de destinations principales, le tableau de bord [!UICONTROL Destinations] et l’onglet [!UICONTROL Aperçu] ne sont pas visibles. À la place, la sélection de [!UICONTROL Destinations] dans le volet de navigation de gauche affiche l’onglet [[!UICONTROL Catalogue]](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogue] {#catalog}

L’onglet **[!UICONTROL Catalogue]** affiche la liste de toutes les destinations disponibles dans [!DNL Platform], auxquelles vous pouvez envoyer des données.

L’interface utilisateur de [!DNL Platform] propose plusieurs options de recherche et de filtrage sur la page de catalogue des destinations :

* Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique.
* Filtrez les destinations à l’aide de la commande [!UICONTROL Catégories].
* Basculez entre [!UICONTROL Toutes les destinations] et [!UICONTROL Mes destinations]. Lorsque vous sélectionnez **[!UICONTROL Toutes les destinations]**, toutes les destinations [!DNL Platform] disponibles s’affichent. Lorsque vous sélectionnez **[!UICONTROL Mes destinations]**, vous ne pouvez afficher que les destinations avec lesquelles vous avez établi une connexion.
* Sélectionnez cette option pour afficher **[!UICONTROL Connexions]** et/ou **[!UICONTROL Extensions]**. Pour comprendre la différence entre les deux catégories, voir [Types de destination et Catégories](../destination-types.md).

![Catalogue](../assets/ui/workspace/catalog.png)

Les cartes de destination contiennent soit un contrôle **[!UICONTROL Configurer]** ou **[!UICONTROL Activer les segments]** et un contrôle secondaire qui affiche d’autres options. Ces contrôles sont décrits ci-dessous :

| Contrôle | Description |
|---------|----------|
| [!UICONTROL Configuration] | Permet de créer une connexion à la destination. |
| [!UICONTROL Activation des segments] | Une fois que vous avez établi une connexion à la destination, vous pouvez activer les segments. |
| [!UICONTROL Afficher le compte] | Affichez les comptes que vous avez connectés pour une destination. |
| [!UICONTROL Afficher les flux de données] | Affichez les flux d’activation de données qui existent pour une destination. |
| [!UICONTROL Afficher la documentation] | Ouvre un lien vers la page de documentation de cette destination spécifique pour plus d’informations et pour vous aider à la configurer. |

{style=&quot;table-layout:auto&quot;}

![Contrôles sur la carte des destinations](../assets/ui/workspace/destination-card-options.png)

Sélectionnez une carte de destination dans le catalogue pour ouvrir le rail de droite. Vous pouvez voir ici une description de la destination. Le rail de droite fournit les mêmes contrôles que ceux décrits dans le tableau ci-dessus, y compris une description de la destination, ainsi qu’une indication de la catégorie et du type de destination.

![Options du catalogue des destinations](../assets/ui/workspace/destination-right-rail.png)

Pour plus d’informations sur les catégories de destination et les informations sur chaque destination, voir [Catalogue des destinations](../catalog/overview.md) et [Types et catégories de destination](../destination-types.md).

## [!UICONTROL Comptes] {#accounts}

L’onglet **[!UICONTROL Comptes]** affiche des détails sur les connexions que vous avez établies avec différentes destinations et vous permet de mettre à jour les détails de connexion existants. Voir [Mise à jour de comptes](update-accounts.md) pour obtenir des instructions détaillées.

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Les destinations avec le bouton d’activation/désactivation **[!UICONTROL activé/désactivé]** activé/désactivé définissent la destination comme principale ou inactive, respectivement. Vous pouvez également afficher les destinations où les données circulent en sélectionnant **[!UICONTROL Segments]** > **[!UICONTROL Parcourir]** et en sélectionnant un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

>[!TIP]
>
> * Sélectionnez les trois points de la colonne [!UICONTROL Nom] et utilisez le bouton ![Ajouter des segments](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activer les segments ]**pour envoyer des segments vers cette destination.
> * Sélectionnez les trois points de la colonne [!UICONTROL Nom] et utilisez le bouton ![Supprimer les destinations](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Supprimer ]**pour [supprimer](delete-destinations.md) une connexion existante à une destination.


![Onglet Parcourir](../assets/ui/workspace/browse-tab.png)

| Élément | Description |
|---------|----------|
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. La même colonne comprend deux contrôles : [!UICONTROL Activez ] et [!UICONTROL Supprimez la destination]. |
| [!UICONTROL État de la dernière exécution de flux] | État de la dernière exécution du flux de données. Voir [Affichage des détails de destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Date d’exécution du dernier flux] | Heure et date de la dernière exécution du flux de données. Voir [Affichage des détails de destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : Peut être S3, FTP ou [!DNL Azure Blob].</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur.</li><li>Pour les destinations de diffusion en continu : Peut être [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Données d’activation] | Indique le nombre de segments activés vers cette destination. Sélectionnez ce contrôle pour en savoir plus sur les segments activés. Pour plus d’informations sur les segments activés, voir [Données d’activation](/help/destinations/ui/destination-details-page.md#activation-data) dans la page des détails de destination. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. |
| [!UICONTROL État] | `Active` ou `Inactive`. Indique si les données sont activées vers cette destination. |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](../assets/ui/workspace/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## [!UICONTROL Vue du système] {#system-view}

L’onglet **[!UICONTROL Vue du système]** affiche une représentation graphique des flux d’activation que vous avez configurés dans Adobe Experience Platform.

![Flux de données 1](../assets/ui/workspace/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page et cliquez sur **[!UICONTROL Afficher les flux de données]** pour afficher les informations sur toutes les connexions que vous avez configurées pour chaque destination.

![Flux de données 2](../assets/ui/workspace/data-flows2.png)
