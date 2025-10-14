---
title: Suppression des prospects Acxiom
description: Exportez vos audiences propriétaires vers la destination Acxiom pour permettre à Acxiom de supprimer les clients connus ou convertis. Utilisez ensuite le connecteur source Acxiom pour ingérer et activer les listes de prospects à partir d’Acxiom, sans que vos clients connus ou convertis soient supprimés.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Version bêta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 27%

---

# [!DNL Acxiom Prospect-Suppression] connexion à la destination

>[!NOTE]
>
>La destination [!DNL Acxiom Prospect-Suppression] est en version bêta. Ce connecteur de destination et cette page de documentation sont créés et conservés par l’équipe d’Acxiom. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse acxiom-adobe-help@acxiom.com.

## Vue d’ensemble {#overview}

Utilisez [!DNL Acxiom Prospect-Suppression] pour fournir les audiences de prospects les plus productives possible. Ce connecteur exporte en toute sécurité des données propriétaires à partir de Real-Time Customer Data Platform et les exécute via une résolution d’identité et d’hygiène primée qui produit un fichier de données à utiliser comme liste de suppression. Cela sera comparé à la base de données [!DNL Acxiom Global] qui permet aux listes de prospects d&#39;être personnalisées pour l&#39;import. Ensuite, utilisez le connecteur source [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) pour créer des listes de prospects d’Acxiom vers Real-Time CDP, avec vos clients connus ou convertis supprimés.

![Diagramme marketing pour exporter des données propriétaires vers Acxiom, puis réimporter des données de prospects dans Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom propose les audiences les plus performantes du secteur avec le plus grand catalogue de plus de 12 000 attributs de données globaux spécifiquement axés sur la fourniture d’expériences personnalisées. Appuyez sur des combinaisons illimitées de données de haute qualité pour créer et distribuer des audiences afin de répondre à des besoins de campagne spécifiques.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de destination [!DNL Acxiom Prospect-Suppression] et un flux de données à l’aide de l’interface utilisateur de Adobe Experience Platform. Ce connecteur est utilisé pour diffuser des données vers le service prospect Acxiom à l’aide d’Amazon S3 comme point de dépôt. Contactez votre gestionnaire de compte Acxiom lorsque vous commencez à exporter des fichiers vers le point de dépôt Amazon S3.

![Catalogue de destinations avec la destination Acxiom sélectionnée.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Acxiom Prospect-Suppression], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Création d’une liste de suppression pour les jeux de données de prospection {#create-suppression-list}

Les professionnels du marketing qui visent à améliorer l’efficacité de leurs stratégies de sensibilisation utilisent souvent la création d’une liste de suppression. Cette liste comprend les clients existants et des segments spécifiques, ce qui garantit leur exclusion des activités de prospection lors des campagnes ciblées. Cette approche stratégique permet d’affiner l’audience, d’éviter les communications redondantes et contribue à un effort marketing plus ciblé et efficace.

En tant que marketeur, par exemple, vous pouvez élargir la portée de votre campagne en ajoutant des profils de prospects ciblés à vos campagnes en fonction des critères de segmentation et de suppression que vous avez fournis.

Le cas d’utilisation est exécuté par une combinaison de connecteurs source et de destination.

Vous commencez par exporter vos profils clients existants à l’aide de ce connecteur de destination à utiliser comme fichier de suppression. Cela permet de s’assurer qu’aucun enregistrement de client existant n’est inclus.

Le service d’Acxiom recherche le fichier, le récupère et l’utilise avec d’autres critères de sélection et génère un fichier de prospect. Vous utiliserez ensuite le connecteur source [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md) correspondant pour ingérer les profils de prospect dans Adobe Real-Time CDP.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL vues des destinations]** et **[!UICONTROL Gérer les destinations]**, **[!UICONTROL activer les destinations]**, **[!UICONTROL afficher les profils]** et **[!UICONTROL afficher les segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

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
>Pour vous connecter à la destination, vous avez besoin des **&#x200B;**&#x200B;et des **&#x200B;**&#x200B;[&#128279;](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
|---------------|----------------------------------------------------------------------------------------------------------|
| Clé d’accès S3 | Identifiant de la clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur de l’équipe [!DNL Acxiom]. |
| Clé secrète S3 | Identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur de l’équipe [!DNL Acxiom]. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur de l’équipe [!DNL Acxiom]. |

### Nouveau compte

Pour définir un nouvel emplacement Acxiom Managed S3 :

![Nouveau compte](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination [!DNL Acxiom Prospect Suppression] apparaissent dans une fenêtre contextuelle de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple dans l’interface utilisateur lorsque vous accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]** :

![Compte existant](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détail de la destination](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Nom (obligatoire)** - Nom sous lequel la destination sera enregistrée.
* **Description** - brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (requis)** - Si des sous-répertoires d’un compartiment sont utilisés, un chemin d’accès doit être défini ou &quot;/&quot; pour référencer le chemin d’accès racine.
* **Type de fichier** - Sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Actuellement, le seul type de fichier attendu par le traitement Acxiom est le format CSV.

>[!IMPORTANT]
>
>Lors de la sélection de l’option CSV, les options *Délimiteur*, *Caractère de citation*, *Caractère d’échappement*, *Valeur vide*, *Valeur nulle*, *Format de compression* et *Inclure le fichier manifeste* seront présentées, le document suivant explique ces paramètres plus de détails [configurez les options de formatage](../../ui/batch-destinations-file-formatting-options.md).

![Options CSV](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des **&#x200B;**, **[!UICONTROL Activer les destinations]**, **&#x200B;**&#x200B;et **&#x200B;**&#x200B;[&#x200B;  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

### Suggestions de mappage

Le traitement nécessite des éléments de nom et d’adresse, tandis que tous les éléments ne sont pas nécessaires si vous fournissez autant que possible pour faciliter la correspondance.  Les suggestions de mappage sont fournies dans le tableau ci-dessous, qui répertorie les attributs du côté destination utilisés par le traitement Acxiom vers lesquels les clients peuvent mapper des attributs de profil.  Cela doit être traité comme des suggestions, car tous les éléments ne sont pas requis et les valeurs source dépendront des besoins du compte.

| Champ cible | Description Source |
|--------------|-------------------------------------------------------------|
| nom | La valeur `person.name.fullName` en Experience Platform. |
| Prénom | La valeur `person.name.firstName` en Experience Platform. |
| Nom | La valeur `person.name.lastName` en Experience Platform. |
| address1 | La valeur `mailingAddress.street1` en Experience Platform. |
| address2 | La valeur `mailingAddress.street2` en Experience Platform. |
| ville | La valeur `mailingAddress.city` en Experience Platform. |
| state | La valeur `mailingAddress.state` en Experience Platform. |
| zip | La valeur `mailingAddress.postalCode` en Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>Les champs supplémentaires non répertoriés ci-dessus seront inclus dans l’exportation, mais seront ignorés par le traitement Acxiom.

## Vérifier le flux de données

Utilisez la page de révision pour obtenir un résumé de votre flux de données avant envoi.

![Révision](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Valider l’exportation des données {#exported-data}

Pour contrôler que l’exportation des données a bien réussi, vérifiez votre compartiment [!DNL Amazon S3 Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour exporter des données de lot de l’Experience Platform vers votre emplacement S3 géré [!DNL Acxiom]. Vous devez contacter votre représentant Acxiom avec le nom du compte, le nom du fichier et le chemin du compartiment afin que le traitement puisse être configuré.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Données et distribution d’audience Acxiom :* https://www.acxiom.com/customer-data/audience-data-distribution/
