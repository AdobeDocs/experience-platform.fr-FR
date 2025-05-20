---
keywords: platform;destinations;espace de travail des destinations;espace de travail;iu;interface utilisateur des destinations;catalogue;catalogue des destinations;
title: Espace de travail des destinations
description: 'L’espace de travail des destinations se compose de cinq sections : Vue d’ensemble, Catalogue, Parcourir, Comptes et Vue du système. Elles sont décrites dans les sections ci-dessous.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 75%

---

# Espace de travail des destinations {#destinations-workspace}

Dans Adobe Experience Platform, sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Destinations].

L’espace de travail [!UICONTROL Destinations] comprend cinq sections, [!UICONTROL Vue d’ensemble], [!UICONTROL Catalogue], [!UICONTROL Parcourir], [!UICONTROL Comptes] et [!UICONTROL Vue du système], décrites dans les sections ci-dessous.

![Tableau de bord de vue d’ensemble des destinations montrant trois widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Vue d’ensemble] {#overview}

L’onglet **[!UICONTROL Vue d’ensemble]** affiche le tableau de bord [!UICONTROL Destinations], fournissant des mesures clés liées aux données de destination de votre organisation. Pour en savoir plus, consultez le [[!UICONTROL guide du tableau de bord des destinations] ](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Si votre organisation est nouvelle sur Experience Platform et n’a pas encore de destinations actives, le tableau de bord [!UICONTROL Destinations] et l’onglet [!UICONTROL Vue d’ensemble] ne sont pas visibles. Au lieu de cela, la sélection de [!UICONTROL Destinations] dans la navigation de gauche affiche l’onglet [[!UICONTROL Catalogue]](#catalog).

![L’onglet Vue d’ensemble du tableau de bord des Destinations.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogue] {#catalog}

L’onglet **[!UICONTROL Catalogue]** affiche une liste de toutes les destinations disponibles dans [!DNL Experience Platform], auxquelles vous pouvez envoyer des données.

L’interface utilisateur de [!DNL Experience Platform] offre plusieurs options de recherche et de filtrage sur la page du catalogue des destinations :

* Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique.
* Filtrez les destinations à l’aide de la commande [!UICONTROL Catégories].
* Basculez entre [!UICONTROL Toutes les destinations] et [!UICONTROL Mes destinations]. Lorsque vous sélectionnez **[!UICONTROL Toutes les destinations]**, toutes les destinations [!DNL Experience Platform] disponibles s’affichent. Lorsque vous sélectionnez **[!UICONTROL Mes destinations]**, vous pouvez uniquement afficher les destinations avec lesquelles vous avez établi une connexion.
* Sélectionnez pour afficher les types de **[!UICONTROL Connexions]** et/ou d’**[!UICONTROL Extensions]**. Pour comprendre la différence entre ces deux catégories, lisez [Types et catégories de destinations](../destination-types.md).

![Catalogue des destinations présentant quelques destinations publicitaires et de stockage dans le cloud.](../assets/ui/workspace/catalog.png)

Les cartes de destination contiennent des options de commande principales et secondaires. Les commandes principales comprennent [!UICONTROL Configurer], [!UICONTROL Activer], [!UICONTROL Activer des audiences] ou [!UICONTROL Exporter des jeux de données]. Les commandes secondaires permettent d’afficher des options. Ces commandes sont décrites ci-dessous :

| Commande | Description |
|---------|----------|
| [!UICONTROL Configurer] | Permet de créer une connexion à la destination. |
| [!UICONTROL Activer] | Une fois que vous avez établi une connexion à la destination, vous pouvez activer des audiences ou exporter des jeux de données vers cette destination. |
| [!UICONTROL Activer les audiences] | Une fois que vous avez établi une connexion avec la destination, vous pouvez activer les audiences vers cette destination. |
| [!UICONTROL Exporter les jeux de données] | Une fois que vous avez établi une connexion à la destination, vous pouvez exporter des jeux de données vers cette destination. |
| [!UICONTROL Afficher le compte] | Affichez les comptes que vous avez connectés pour une destination. |
| [!UICONTROL Afficher les flux de données] | Affichez les flux d’activation de données qui existent pour une destination. |
| [!UICONTROL Afficher la documentation] | Ouvre un lien vers la page de documentation de cette destination spécifique, pour plus d’informations et pour vous aider à la configurer. |

{style="table-layout:auto"}

![Commandes sur la carte des destinations](../assets/ui/workspace/destination-card-options.png)

Sélectionnez une carte de destination dans le catalogue pour ouvrir le rail de droite. Vous pouvez voir ici une description de la destination. Le rail de droite fournit les mêmes commandes que ceux décrits dans le tableau ci-dessus, y compris une description de la destination, ainsi qu’une indication de la catégorie et du type de destination.

![Options du catalogue des destinations](../assets/ui/workspace/destination-right-rail.png)

Pour plus d’informations sur les catégories de destination et les informations sur chaque destination, consultez le [Catalogue des destinations](../catalog/overview.md) et les [Types et catégories de destination](../destination-types.md).

## [!UICONTROL Comptes] {#accounts}

L’onglet **[!UICONTROL Comptes]** vous montre les détails des connexions que vous avez établies avec diverses destinations, et vous permet de mettre à jour ou de supprimer les détails des comptes existants. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque compte de destination.

>[!TIP]
>
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Platform] et utilisez la commande ![Activer](/help/images/icons/data-add.png)**[!UICONTROL Activer &#x200B;]**/**[!UICONTROL &#x200B; Activer les audiences &#x200B;]**/**[!UICONTROL &#x200B; Exporter les jeux de données &#x200B;]**&#x200B;pour exporter des audiences ou des jeux de données vers cette destination.
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Platform] et utilisez la commande ![Modifier les détails](/help/images/icons/edit.png)**[!UICONTROL Modifier les détails &#x200B;]**&#x200B;pour [mettre à jour](update-accounts.md) les détails d’un compte de destination existant.
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Platform] et utilisez la ![commande Supprimer](/help/images/icons/delete.png)**[!UICONTROL Supprimer &#x200B;]**&#x200B;pour [supprimer](delete-destination-account.md) un compte de destination existant.

![Onglet Comptes](../assets/ui/workspace/destination-account-options.png)

| Élément | Description |
|---|---|
| [!UICONTROL Destination] | Connecteur de destination pour lequel vous avez configuré la connexion. |
| [!UICONTROL Type de connexion] | Représente le type de connexion de compte à votre compartiment de stockage ou à votre destination. Selon la destination, les options d’authentification sont les suivantes : <ul><li>Pour les destinations de marketing par e-mail : il peut s’agir de S3, FTP ou Azure Blob.</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur</li><li>Pour les destinations de stockage dans le cloud Amazon S3 : clé d’accès </li><li>Pour les destinations de stockage dans le cloud SFTP : authentification de base pour SFTP</li><li>Authentification OAuth 1 ou OAuth 2</li><li>Authentification par jeton porteur</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Nom d’utilisateur que vous avez sélectionné dans le [workflow de connexion à la destination](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connexions] | Représente le nombre de flux de données de destination uniques réussis et connectés avec des informations de base créées pour une destination. |
| [!UICONTROL Date d’autorisation] | La date à laquelle la connexion à cette destination a été autorisée. |
| [!UICONTROL Date d’expiration] | Date d’expiration de l’autorisation de connexion à cette destination. <br>**Important** : cette colonne est actuellement disponible uniquement pour la connexion [Facebook](../catalog/social/facebook.md). |

{style="table-layout:auto"}

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Les destinations dont le bouton (bascule) **[!UICONTROL Activer/Désactiver]** est sélectionné définissent la destination sur active ou inactive, respectivement. Vous pouvez également afficher les destinations où les données circulent en sélectionnant **[!UICONTROL Audiences]** > **[!UICONTROL Parcourir]** et en sélectionnant une audience à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet [!UICONTROL Parcourir] :

>[!TIP]
>
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Nom] et utilisez la commande ![Activer les audiences](/help/images/icons/data-add.png)**[!UICONTROL Activer &#x200B;]**&#x200B;pour exporter des audiences ou des jeux de données vers cette destination.
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Nom] et utilisez la commande ![Supprimer](/help/images/icons/delete.png)**[!UICONTROL Supprimer &#x200B;]**&#x200B;pour [supprimer](delete-destinations.md) une connexion existante à une destination.
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Nom] et utilisez la commande ![Affichage dans la surveillance](/help/images/icons/monitoring.png)**[!UICONTROL Affichage dans la surveillance &#x200B;]**&#x200B;pour afficher les informations d’activation de cette destination dans le [tableau de bord de la surveillance](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Sélectionnez les points de suspension (`...`) dans la colonne [!UICONTROL Nom] et utilisez la commande ![S’abonner aux alertes ](/help/images/icons/alert-add.png)**[!UICONTROL S’abonner aux alertes &#x200B;]**&#x200B;pour vous abonner aux alertes de flux de données de destination. Vous pouvez vous abonner à des alertes pour recevoir des messages concernant l’état, la réussite ou l’échec de votre exécution de flux. Consultez [S’abonner aux alertes de destination en contexte](alerts.md) pour des informations détaillées sur les alertes de flux de données de destination.

![Onglet Parcourir](../assets/ui/workspace/browse-tab.png)

| Élément | Description |
|---------|----------|
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. La même colonne comprend deux commandes : [!UICONTROL Activer] et [!UICONTROL Supprimer la destination]. |
| Type de données | Type de données pris en charge par la connexion de destination. Types de données pris en charge : <ul><li>**[!UICONTROL Clients]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Comptes]**</li><li>**[!UICONTROL Jeux de données]**</li></ul> |
| [!UICONTROL Statut de la dernière exécution du flux de données] | Statut de la dernière exécution du flux de données. Consultez [Afficher les détails de la destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Date de la dernière exécution du flux de données] | Date et heure de la dernière exécution du flux de données. Consultez [Afficher les détails de destination](destination-details-page.md) pour plus d’informations sur les exécutions de flux de données. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Date d’expiration du compte] | Date d’expiration de l’autorisation de connexion à cette destination. <br>**Important** : cette colonne est actuellement disponible uniquement pour la connexion [Facebook](../catalog/social/facebook.md). |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : il peut s’agir de S3, FTP ou [!DNL Azure Blob].</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur.</li><li>Pour les destinations en flux continu : il peut s’agir de [!DNL Azure Event Hubs] ou [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Données d’activation] | Indique le nombre d’audiences activées vers cette destination. Sélectionnez cette commande pour en savoir plus sur les audiences activées. Pour plus d’informations sur les audiences activées[&#128279;](/help/destinations/ui/destination-details-page.md#activation-data) reportez-vous à la section Données d’activation de la page de détails de la destination. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. Sélectionnez les flèches haut/bas pour trier les flux d’activation en fonction du plus récent ou du plus ancien. |
| [!UICONTROL État] | `Enabled` ou `Disabled`. Indique si les données sont activées vers cette destination. |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite, telles que l’identifiant de destination, la description, le nombre d’audiences activées, etc.

![Cliquer sur la ligne de destination](../assets/ui/workspace/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les audiences activées vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter des audiences aux audiences envoyées vers cette destination.

## [!UICONTROL Vue du système] {#system-view}

L’onglet **[!UICONTROL Vue du système]** affiche une représentation graphique des flux d’activation que vous avez configurés dans Adobe Experience Platform.

![Flux de données 1](../assets/ui/workspace/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page et cliquez sur **[!UICONTROL Afficher les flux de données]** pour afficher les informations sur toutes les connexions que vous avez configurées pour chaque destination.

![Flux de données 2](../assets/ui/workspace/data-flows2.png)
