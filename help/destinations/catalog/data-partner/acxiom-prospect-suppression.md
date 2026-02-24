---
title: Suppression des prospects Acxiom
description: Exportez vos audiences propriétaires vers la destination Acxiom pour permettre à Acxiom de supprimer les clients connus ou convertis. Utilisez ensuite le connecteur source Acxiom pour ingérer et activer les listes de prospects à partir d’Acxiom, en supprimant vos clients connus ou convertis.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 23%

---

# [!DNL Acxiom Prospect-Suppression] la connexion de destination

>[!NOTE]
>
>La destination [!DNL Acxiom Prospect-Suppression] est en version bêta. Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe d’Acxiom. Pour toute demande ou information, contactez directement l&#39;équipe à l&#39;adresse acxiom-adobe-help@acxiom.com.

## Vue d’ensemble {#overview}

Utilisez [!DNL Acxiom Prospect-Suppression] pour offrir les audiences de prospects les plus productives possible. Ce connecteur exporte en toute sécurité des données propriétaires à partir de Real-Time Customer Data Platform et les exécute par le biais d’une hygiène primée et d’une résolution d’identité qui génère un fichier de données à utiliser comme liste de suppression. Ces données seront comparées à la base de données [!DNL Acxiom Global] qui permet de personnaliser les listes de prospects pour l’importation. Ensuite, utilisez le connecteur source [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) pour renvoyer les listes de prospects d’Acxiom dans Real-Time CDP, en supprimant vos clients connus ou convertis.

![Diagramme marketing pour exporter des données propriétaires vers Acxiom, puis importer les données des prospects dans Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom propose les audiences les plus performantes du secteur avec le plus grand catalogue de plus de 12 000 attributs de données mondiaux spécifiquement axés sur la fourniture d’expériences personnalisées. Tirez parti de combinaisons illimitées de données de haute qualité pour créer et distribuer des audiences afin de répondre à des besoins de campagne spécifiques.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de destination et un flux de données [!DNL Acxiom Prospect-Suppression] à l’aide de l’interface utilisateur de Adobe Experience Platform. Ce connecteur est utilisé pour diffuser des données au service de prospect Acxiom à l’aide d’Amazon S3 comme point de dépôt. Contactez votre représentant de compte Acxiom une fois que vous avez commencé à exporter des fichiers vers le point de dépôt Amazon S3.

![Le catalogue de destination avec la destination Acxiom sélectionnée.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Acxiom Prospect-Suppression], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Créer une liste de suppression pour la prospection de jeux de données {#create-suppression-list}

Les professionnels du marketing qui cherchent à améliorer l’efficacité de leurs stratégies de sensibilisation utilisent souvent la création d’une liste de suppression. Cette liste inclut les clients existants et des segments spécifiques, afin de garantir leur exclusion des activités de prospection lors des campagnes ciblées. Cette approche stratégique permet d’affiner l’audience, d’éviter les communications redondantes et de contribuer à un effort marketing plus ciblé et plus efficace.

Par exemple, en tant que spécialiste marketing, vous pouvez vouloir élargir la portée de votre campagne en ajoutant des profils de prospects ciblés à vos campagnes en fonction des critères de segmentation et de suppression que vous avez fournis.

Le cas d’utilisation est exécuté à l’aide d’une combinaison des connecteurs source et de destination.

Dans un premier temps, vous devez exporter vos profils clients existants à l’aide de ce connecteur de destination pour les utiliser comme fichier de suppression. Cela permet de s’assurer qu’aucun enregistrement client existant n’est inclus.

Le service d’Acxiom recherche le fichier, le récupère et l’utilise avec des critères de sélection supplémentaires et génère un fichier de prospect. Vous pouvez ensuite utiliser le connecteur source [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) correspondant pour ingérer les profils de prospects dans Adobe Real-Time CDP.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}




Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clé d’accès S3 | Identifiant de clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Clé secrète S3 | L’identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe [!DNL Acxiom]. |

### Nouveau compte

Pour définir un nouvel emplacement Acxiom Managed S3 :

![Nouveau compte](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination [!DNL Acxiom Prospect Suppression] apparaissent dans un pop-up de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple à partir de l’interface utilisateur, lorsque vous accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** :

![Compte existant](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la destination](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nom (obligatoire)** - Le nom sous lequel la destination sera enregistrée
* **Description** - Brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (obligatoire)** - si des sous-répertoires sont utilisés dans un compartiment, un chemin d’accès doit être défini, ou « / » pour référencer le chemin racine.
* **Type de fichier** - Sélectionnez le format qu’Experience Platform doit utiliser pour les fichiers exportés. Actuellement, le seul type de fichier attendu pour le traitement d’Acxiom est CSV

>[!IMPORTANT]
>
>Lors de la sélection de l’option CSV, les options *Délimiteur*, *Citation*, *Caractère d’échappement*, *Valeur vide*, *Valeur nulle*, *Format de compression* et *Inclure le fichier manifeste* sont présentées. Le document suivant explique ces paramètres de manière plus détaillée [configurer les options de formatage](../../ui/batch-destinations-file-formatting-options.md).

![&#x200B; Options CSV &#x200B;](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

### Suggestions de mappage

Le traitement nécessite des éléments de nom et d’adresse, tandis que tous les éléments ne sont pas requis, à condition que la mise en correspondance soit la plus facile possible.  Le tableau ci-dessous fournit des suggestions de mappage. Il répertorie les attributs de votre côté de destination utilisés par le traitement Acxiom auquel les clients peuvent mapper des attributs de profil.  Cela doit être traité comme des suggestions, car tous les éléments ne sont pas nécessaires et les valeurs sources dépendent des besoins du compte.

| Champ cible | Description du Source |
|--------------|-------------------------------------------------------------|
| nom | Valeur `person.name.fullName` dans Experience Platform. |
| Prénom | Valeur `person.name.firstName` dans Experience Platform. |
| Nom | Valeur `person.name.lastName` dans Experience Platform. |
| address1 | Valeur `mailingAddress.street1` dans Experience Platform. |
| address2 | Valeur `mailingAddress.street2` dans Experience Platform. |
| ville | Valeur `mailingAddress.city` dans Experience Platform. |
| state | Valeur `mailingAddress.state` dans Experience Platform. |
| fermeture éclair | Valeur `mailingAddress.postalCode` dans Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>Les champs supplémentaires non répertoriés ci-dessus seront inclus dans l’exportation, mais seront ignorés par le traitement Acxiom.

## Vérifier le flux de données

Utilisez la page de révision pour obtenir un résumé de votre flux de données avant l’envoi

![Révision](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Valider l’exportation des données {#exported-data}

Pour contrôler que l’exportation des données a bien réussi, vérifiez votre compartiment [!DNL Amazon S3 Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour exporter des données par lots d’Experience Platform vers votre emplacement S3 géré par [!DNL Acxiom]. Vous devez contacter votre représentant Acxiom avec le nom du compte, le nom de fichier et le chemin d’accès au compartiment afin que le traitement puisse s’installer.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Données et distribution de l’audience Acxiom :* https://www.acxiom.com/customer-data/audience-data-distribution/
