---
title: Destination de Data Landing Zone
description: Découvrez comment vous connecter à Data Landing Zone pour activer des segments et exporter des jeux de données.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 95%

---

# Destination de Data Landing Zone (Version bêta)

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et nʼest disponible que pour un nombre de clients limité. Pour demander l’accès à la connexion [!DNL Data Landing Zone], contactez votre représentant Adobe et fournissez votre [!DNL Organization ID].


## Présentation {#overview}

[!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform et qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers hors de Platform. Vous avez accès à un conteneur [!DNL Data Landing Zone] par sandbox et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients de Platform et ses services d’application tels que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], et [!DNL Real-Time Customer Data Platform] sont configurés avec un conteneur [!DNL Data Landing Zone] par sandbox. Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité du stockage [!DNL Azure Blob] standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur [!DNL Data Landing Zone] via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre conteneur [!DNL Data Landing Zone], ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau.

Platform applique une durée de vie (TTL) stricte de sept jours sur tous les fichiers chargés dans un conteneur [!DNL Data Landing Zone]. Tous les fichiers sont supprimés au bout de sept jours.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (par exemple votre PPID), tels que choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Gérer le contenu de vos [!DNL Data Landing Zone]

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/fr-fr/products/storage/storage-explorer/) pour gérer le contenu de votre conteneur [!DNL Data Landing Zone].

Dans l’interface utilisateur [!DNL Azure Storage Explorer], sélectionnez l’icône de connexion dans la barre de navigation de gauche. La fenêtre **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionnez **[!DNL Blob container]** pour vous connecter à votre espace de stockage [!DNL Data Landing Zone].

![Sélection de ressource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![Sélection d’une méthode de connexion](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez fournir un **nom d’affichage** et l’URL du conteneur SAS **[!DNL Blob]** qui correspond à votre conteneur [!DNL Data Landing Zone].

>[!IMPORTANT]
>
>Vous devez utiliser les API Platform pour récupérer vos informations d’identification Data Landing Zone. Pour plus d’informations, voir [Récupération des informations d’identification Data Landing Zone](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=fr).
>
> Pour récupérer les informations d’identification et accéder aux fichiers exportés, vous devez remplacer le paramètre de requête `type=user_drop_zone` par `type=dlz_destination` dans tout appel HTTP décrit dans la page ci-dessus.

Fournissez votre URL SAS [!DNL Data Landing Zone], puis sélectionnez **Suivant**.

![Saisie des informations de connexion](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

La fenêtre **Résumé** s’affiche, vous donnant ainsi une présentation de vos paramètres, y compris des informations sur votre point d’entrée et vos autorisations [!DNL Blob]. Quand vous avez terminé, sélectionnez **Se connecter**.

![Résumé](/help/sources/images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour l’interface utilisateur [!DNL Azure Storage Explorer] avec votre conteneur [!DNL Data Landing Zone].

![Conteneur utilisateur DLZ](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Avec votre conteneur [!DNL Data Landing Zone] connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à exporter des fichiers d’Experience Platform vers votre conteneur [!DNL Data Landing Zone]. Pour exporter des fichiers, vous devez établir une connexion à la destination [!DNL Data Landing Zone] dans l’interface utilisateur Experience Platform, comme décrit dans la section ci-dessous.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Parce que [!DNL Data Landing Zone] est un stockage configuré par Adobe, vous n’avez aucune étape à effectuer pour vous authentifier auprès de la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui héberge les fichiers exportés.
* **[!UICONTROL Type de fichier]**: sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Lorsque vous sélectionnez la variable [!UICONTROL CSV] , vous pouvez également [configuration des options de formatage de fichier](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]**: sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activer des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification

Dans l’étape **[!UICONTROL Planifier]**, vous pouvez [configurer le planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre destination [!DNL Data Landing Zone] et vous pouvez également [configurer le nom de vos fichiers exportés](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapper les attributs et les identités {#map}

Dans l’étape **[!UICONTROL Mappage]**, vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## (Version bêta) Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Valider l’exportation des données avec succès {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez le stockage [!DNL Data Landing Zone] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
