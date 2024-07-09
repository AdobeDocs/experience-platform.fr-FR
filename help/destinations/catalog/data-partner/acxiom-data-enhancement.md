---
title: Amélioration des données d’Acrobat
description: Utilisez ce connecteur pour activer les profils d’Adobe propriétaires dans Real-Time CDP vers Acrobat afin d’enrichir les données et de les utiliser sur les canaux marketing. Vous pouvez ensuite utiliser la source Acxiom pour importer les profils contenant des données améliorées et travailler avec eux dans Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Version bêta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 28%

---

# [!DNL Acxiom Data Enhancement] connexion à la destination

>[!NOTE]
>
>La variable [!DNL Acxiom Data Enhancement] destination est en version bêta.  Ce connecteur de destination et cette page de documentation sont créés et conservés par l’équipe d’Acxiom. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse acxiom-adobe-help@acxiom.com.

## Vue d’ensemble {#overview}

Utilisez la variable [!DNL Acxiom Data Enhancement] connecteur pour fournir des données descriptives supplémentaires à vos profils client, à utiliser dans les applications d’analyse, de segmentation et de ciblage. Avec des centaines d’éléments disponibles, vous pouvez ainsi mieux segmenter et modéliser les données, ce qui se traduit par un ciblage et une modélisation prédictive plus précis.

![Diagramme marketing pour exporter des données propriétaires vers Acxiom, puis réimporter des données enrichies dans Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Acxiom Data Enhancement] connexion de destination et flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform. Ce connecteur est utilisé pour diffuser des données vers le service d’amélioration d’Acrobat à l’aide d’Amazon S3 comme point de dépôt.

![Le catalogue des destinations avec la destination Acxiom sélectionnée.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre comment et à quel moment utiliser la variable [!DNL Acxiom Data Enhancement] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Amélioration des données client {#enhance-customer-data}

Ce connecteur doit être utilisé par les professionnels du marketing visant à améliorer l’efficacité de leurs stratégies de sensibilisation en ajoutant des éléments descriptifs sélectionnés à leurs profils clients et en les utilisant pour mieux cibler les campagnes.

Par exemple, en tant que marketeur, vous pouvez approfondir votre compréhension de vos audiences existantes en enrichissant leurs profils avec des données supplémentaires. Cela permettra d’améliorer la segmentation et les stratégies de ciblage, ce qui stimulera la personnalisation et la conversion des campagnes.

Le cas d’utilisation est exécuté par une combinaison de connecteurs source et de destination.

Vous commencez par exporter vos enregistrements de client existants pour enrichissement à l’aide de ce connecteur de destination. Le service d’Acxiom recherche le fichier, le récupère, l’enrichit avec les données d’Acxiom et génère un fichier.

Le client utilisera alors la variable [Ingestion des données par l’intermédiaire d’Acxiom](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) carte source pour réingérer les profils client hydratés dans Adobe Real-Time CDP.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | x | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion et activation des destinations de jeu de données]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clé d’accès S3 | Identifiant de la clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Clé secrète S3 | Identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur à partir de la variable [!DNL Acxiom] l&#39;équipe. |

### Nouveau compte

Pour définir un nouvel emplacement Acxiom Managed S3 :

![Nouveau compte](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Compte existant

Comptes déjà définis à l’aide de la variable [!DNL Acxiom Data Enhancement] La destination apparaît dans une fenêtre contextuelle de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple dans l’interface utilisateur lorsque vous accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]**;

![Compte existant](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la destination](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nom (obligatoire)** : nom sous lequel la destination sera enregistrée.
* **Description** - brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin d’accès au dossier (requis)** - Si des sous-répertoires d’un compartiment sont utilisés, un chemin doit être défini ou &quot;/&quot; pour référencer le chemin racine.
* **Type de fichier** - Sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Actuellement, le seul type de fichier attendu par le traitement Acxiom est le format CSV.

>[!IMPORTANT]
>
>Lors de la sélection de l’option CSV, *Délimiteur*, *Caractère de citation*, *Caractère d’échappement*, *Valeur vide*, *Valeur nulle*, *Format de compression*, et *Inclure le fichier manifeste* Les options seront présentées. Le document suivant explique plus en détail ces paramètres. [configuration des options de formatage](../../ui/batch-destinations-file-formatting-options.md).

![Options CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

### Suggestions de mappage

Le traitement correct des fichiers du côté Acxiom nécessite des éléments de nom et d’adresse. Bien que tous les éléments ne soient pas nécessaires, fournir autant que possible contribue à une correspondance réussie.

Les suggestions de mappage sont fournies dans le tableau ci-dessous, qui répertorie les attributs du côté destination utilisés par le traitement Acxiom vers lesquels les clients peuvent mapper des attributs de profil. Traitez ces éléments comme des suggestions, car tous les éléments ne sont pas requis et les valeurs source dépendront des besoins du compte.

| Champ cible | Description Source |
|--------------|-------------------------------------------------------------|
| nom | La variable `person.name.fullName` dans Experience Platform. |
| Prénom | La variable `person.name.firstName` dans Experience Platform. |
| Nom | La variable `person.name.lastName` dans Experience Platform. |
| address1 | La variable `mailingAddress.street1` dans Experience Platform. |
| address2 | La variable `mailingAddress.street2` dans Experience Platform. |
| ville | La variable `mailingAddress.city` dans Experience Platform. |
| state | La variable `mailingAddress.state` dans Experience Platform. |
| zip | La variable `mailingAddress.postalCode` dans Experience Platform. |

>[!NOTE]
>
>Si vous mappez des champs supplémentaires non répertoriés ci-dessus dans le flux de données, ils seront inclus dans l’exportation des données, mais seront ignorés par le traitement Acxiom.

## Valider l’exportation des données {#exported-data}

Pour contrôler que l’exportation des données a bien réussi, vérifiez votre compartiment [!DNL Amazon S3 Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour exporter les données de profil de l’Experience Platform vers votre [!DNL Acxiom] emplacement S3 géré. Ensuite, vous devez contacter votre représentant Acxiom avec le nom du compte, les noms des fichiers et le chemin du compartiment afin que le traitement puisse être configuré.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Acxiom Infobase :* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
