---
keywords: plateforme;destinations;espace de travail des destinations;espace de travail;ui;interface utilisateur des destinations;catalogue;catalogue des destinations
title: Espace de travail des destinations
description: 'L’espace de travail des destinations se compose de cinq sections : Aperçu, Catalogue, Parcourir, Comptes et Vue du système. Elles sont décrites dans les sections ci-dessous.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 19%

---

# Espace de travail des destinations {#destinations-workspace}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Destinations]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Destinations] workspace.

Le [!UICONTROL Destinations] workspace se compose de cinq sections : [!UICONTROL Présentation], [!UICONTROL Catalogue], [!UICONTROL Parcourir], [!UICONTROL Comptes], et [!UICONTROL Vue du système], décrits dans les sections ci-dessous.

![Présentation des destinations](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Présentation] {#overview}

Le **[!UICONTROL Présentation]** affiche le [!UICONTROL Destinations] tableau de bord, fournissant des mesures clés liées aux données de destination de votre entreprise. Pour en savoir plus, rendez-vous sur la page [[!UICONTROL Destinations] guide du tableau de bord](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si votre entreprise est une nouvelle société qui n’a pas encore de destinations principales, la variable [!UICONTROL Destinations] tableau de bord et [!UICONTROL Présentation] ne sont pas visibles. À la place, sélectionnez [!UICONTROL Destinations] dans le volet de navigation de gauche affiche le [[!UICONTROL Catalogue] tab](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogue] {#catalog}

Le **[!UICONTROL Catalogue]** affiche une liste de toutes les destinations disponibles dans [!DNL Platform], auquel vous pouvez envoyer des données.

Le [!DNL Platform] L’interface utilisateur propose plusieurs options de recherche et de filtrage sur la page de catalogue des destinations :

* Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique.
* Filtrage des destinations à l’aide de la fonction [!UICONTROL Catégories] contrôle.
* Basculer entre [!UICONTROL Toutes les destinations] et [!UICONTROL Mes destinations]. Lorsque vous sélectionnez **[!UICONTROL Toutes les destinations]**, toutes disponibles [!DNL Platform] les destinations s’affichent. Lorsque vous sélectionnez **[!UICONTROL Mes destinations]**, vous ne pouvez afficher que les destinations avec lesquelles vous avez établi une connexion.
* Sélectionner pour afficher **[!UICONTROL Connexions]** et/ou **[!UICONTROL Extensions]**. Pour comprendre la différence entre les deux catégories, voir [Types et catégories de destinations](../destination-types.md).

![Catalogue](../assets/ui/workspace/catalog.png)

Les cartes de destination contiennent soit un **[!UICONTROL Configuration]** ou **[!UICONTROL Activation des segments]** et un contrôle secondaire qui offre davantage d’options. Ces contrôles sont décrits ci-dessous :

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

Pour plus d’informations sur les catégories de destination et sur chaque destination, voir [Catalogue de destinations](../catalog/overview.md) et [Types et catégories de destination](../destination-types.md).

## [!UICONTROL Comptes] {#accounts}

Le **[!UICONTROL Comptes]** Cet onglet affiche des détails sur les connexions que vous avez établies avec différentes destinations et vous permet de mettre à jour ou de supprimer des détails de compte existants. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque compte de destination.

>[!TIP]
>
> * Sélectionnez les trois points dans le [!UICONTROL Plateforme] et utilisez la variable ![Bouton Activer les segments](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activation des segments ]**pour envoyer des segments vers cette destination.
> * Sélectionnez les trois points dans le [!UICONTROL Plateforme] et utilisez la variable ![Bouton Modifier les détails](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Modifier les détails ]**à [update](update-accounts.md) les détails d’un compte de destination existant ;
> * Sélectionnez les trois points dans le [!UICONTROL Plateforme] et utilisez la variable ![Bouton Supprimer](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Supprimer ]**à [delete](delete-destination-account.md) un compte de destination existant ;


![Onglet Comptes](../assets/ui/workspace/destination-account-options.png)

| Élément | Description |
|---|---|
| [!UICONTROL Plateforme] | La destination pour laquelle vous avez configuré la connexion. |
| [!UICONTROL Type de connexion] | Représente le type de connexion du compte à votre compartiment de stockage ou à votre destination. Selon la destination, les options d’authentification sont les suivantes : <ul><li>Pour les destinations de marketing par e-mail : Il peut s’agir de S3, FTP ou Azure Blob.</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur</li><li>Pour les destinations de stockage dans le cloud Amazon S3 : clé d’accès </li><li>Pour les destinations de stockage dans le cloud SFTP : authentification de base pour SFTP</li><li>Authentification OAuth 1 ou OAuth 2</li><li>Authentification du jeton porteur</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Le nom d’utilisateur que vous avez sélectionné dans l’[assistant de connexion à la destination](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Représente le nombre de flux de données de destination réussis uniques connectés aux informations de base créées pour une destination. |
| [!UICONTROL Autorisé] | La date à laquelle la connexion à cette destination a été autorisée. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Destinations avec la variable **[!UICONTROL Activé/Désactivé]** Activez cette option pour définir la destination sur principale ou inactive, respectivement. Vous pouvez également afficher les destinations où les données circulent en sélectionnant **[!UICONTROL Segments]** > **[!UICONTROL Parcourir]** et sélectionner un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans la variable [!UICONTROL Parcourir] tab :

>[!TIP]
>
> * Sélectionnez les trois points dans le [!UICONTROL Nom] et utilisez la variable ![Bouton Activer les segments](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activation des segments ]**pour envoyer des segments vers cette destination.
> * Sélectionnez les trois points dans le [!UICONTROL Nom] et utilisez la variable ![Bouton Supprimer](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Supprimer ]**à [remove](delete-destinations.md) une connexion existante à une destination.
> * Sélectionnez les trois points dans le [!UICONTROL Nom] et utilisez la variable ![Bouton Afficher dans la surveillance](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Afficher dans la surveillance ]**pour afficher les informations d’activation de cette destination dans le [tableau de bord de surveillance](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Sélectionnez les trois points dans le [!UICONTROL Nom] et utilisez la variable ![Abonner aux alertes ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Abonner aux alertes ]**pour vous abonner aux alertes de flux de données de destination. Vous pouvez vous abonner à des alertes pour recevoir des messages concernant l’état, la réussite ou l’échec de l’exécution du flux. Voir [Abonner aux alertes de destination contextuelles](alerts.md) pour obtenir des informations détaillées sur les alertes de flux de données de destination.


![Onglet Parcourir](../assets/ui/workspace/browse-tab.png)

| Élément | Description |
|---------|----------|
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. La même colonne comprend deux contrôles : [!UICONTROL Activer ] et [!UICONTROL Supprimer la destination]. |
| [!UICONTROL État de la dernière exécution de flux] | État de la dernière exécution du flux de données. Voir [Affichage des détails de destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Date d’exécution du dernier flux] | Heure et date de la dernière exécution du flux de données. Voir [Affichage des détails de destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : Peut être S3, FTP ou [!DNL Azure Blob].</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur.</li><li>Pour les destinations de diffusion en continu : Peut être [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Données d’activation] | Indique le nombre de segments activés vers cette destination. Sélectionnez ce contrôle pour en savoir plus sur les segments activés. Voir [Données d’activation](/help/destinations/ui/destination-details-page.md#activation-data) sur la page de détails des destinations pour plus d’informations sur les segments activés. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. Sélectionnez la flèche haut/bas pour trier les flux d’activation selon le plus récent ou le plus ancien en premier. |
| [!UICONTROL État] | `Enabled` ou `Disabled`. Indique si les données sont activées vers cette destination. |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](../assets/ui/workspace/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## [!UICONTROL Vue du système] {#system-view}

Le **[!UICONTROL Vue du système]** affiche une représentation graphique des flux d’activation que vous avez configurés dans Adobe Experience Platform.

![Flux de données 1](../assets/ui/workspace/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page, puis cliquez sur **[!UICONTROL Afficher les flux de données]** pour afficher des informations sur toutes les connexions que vous avez configurées pour chaque destination.

![Flux de données 2](../assets/ui/workspace/data-flows2.png)
