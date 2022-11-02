---
title: Destination de la zone d’entrée des données
description: Découvrez comment vous connecter à Data Landing Zone pour activer des segments et exporter des jeux de données.
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 26%

---

# (Version bêta) Destination de la zone d’entrée des données

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et n’est disponible que pour un nombre limité de clients. Pour demander l’accès à la connexion [!DNL Data Landing Zone], contactez votre représentant Adobe et fournissez vos [!DNL Organization ID].


## Présentation {#overview}

[!DNL Data Landing Zone] est un [!DNL Azure Blob] Interface de stockage configurée par Adobe Experience Platform, vous permettant d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers en dehors de Platform. Vous avez accès à une [!DNL Data Landing Zone] conteneur par environnement de test et le volume total de données sur tous les conteneurs est limité au total des données fournies avec votre licence Produits et Services Platform. Tous les clients de Platform et ses services d’application tels que [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], et [!DNL Real-time Customer Data Platform] sont configurés avec un [!DNL Data Landing Zone] conteneur par environnement de test. Vous pouvez lire et écrire des fichiers dans votre conteneur via [!DNL Azure Storage Explorer] ou votre interface de ligne de commande.

[!DNL Data Landing Zone] prend en charge l’authentification SAS et ses données sont protégées par la norme [!DNL Azure Blob] des mécanismes de sécurité du stockage au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre [!DNL Data Landing Zone] Conteneur via une connexion Internet publique. Aucune modification réseau n’est requise pour accéder à votre [!DNL Data Landing Zone] , ce qui signifie que vous n’avez pas besoin de configurer de listes autorisées ou de configurations inter-régions pour votre réseau.

Platform applique une durée de vie stricte de sept jours sur tous les fichiers chargés dans un [!DNL Data Landing Zone] conteneur. Tous les fichiers sont supprimés au bout de sept jours.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (votre PPID, par exemple), tels que choisis dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Gérez le contenu de vos [!DNL Data Landing Zone]

Vous pouvez utiliser [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) pour gérer le contenu de votre [!DNL Data Landing Zone] conteneur.

Dans le [!DNL Azure Storage Explorer] Dans l’interface utilisateur, sélectionnez l’icône de connexion dans la barre de navigation de gauche. Le **Sélectionner la ressource** s’affiche, vous permettant d’accéder à des options de connexion. Sélectionner **[!DNL Blob container]** pour vous connecter à [!DNL Data Landing Zone] stockage.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Ensuite, sélectionnez **URL de signature d’accès partagé (SAS)** comme méthode de connexion, puis sélectionnez **Suivant**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Après avoir sélectionné votre méthode de connexion, vous devez fournir un **nom d&#39;affichage** et le **[!DNL Blob]container SAS URL** qui correspond à votre [!DNL Data Landing Zone] conteneur.

>[!IMPORTANT]
>
>Vous devez utiliser les API Platform pour récupérer vos informations d’identification Data Landing Zone. Pour plus d’informations, voir [Récupération des informations d’identification Data Landing Zone](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/create/cloud-storage/data-landing-zone.html?lang=en#retrieve-data-landing-zone-credentials).
>
> Pour récupérer les informations d’identification et accéder aux fichiers exportés, vous devez remplacer le paramètre de requête `type=user_drop_zone` avec `type=dlz_destination` dans tout appel HTTP décrit dans la page ci-dessus.

Fournissez les [!DNL Data Landing Zone] URL SAS , puis sélectionnez **Suivant**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Le **Résumé** s’affiche, vous donnant ainsi une vue d’ensemble de vos paramètres, y compris des informations sur vos [!DNL Blob] point de terminaison et autorisations. Une fois prêt, sélectionnez **Connexion**.

![summary](/help/sources/images/tutorials/create/dlz/summary.png)

Une connexion réussie met à jour votre [!DNL Azure Storage Explorer] l’interface utilisateur de [!DNL Data Landing Zone] conteneur.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Avec votre [!DNL Data Landing Zone] conteneur connecté à [!DNL Azure Storage Explorer], vous pouvez maintenant commencer à exporter des fichiers de l’Experience Platform vers votre [!DNL Data Landing Zone] conteneur. Pour exporter des fichiers, vous devez établir une connexion au [!DNL Data Landing Zone] destination dans l’interface utilisateur de l’Experience Platform, comme décrit dans la section ci-dessous.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Parce que [!DNL Data Landing Zone] est un stockage configuré par Adobe, vous n’avez pas à effectuer d’étapes pour vous authentifier à la destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Chemin du dossier]**: Entrez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification

Dans le **[!UICONTROL Planification]** étape, vous pouvez [configuration du planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre [!DNL Data Landing Zone] destination et vous pouvez également [configurer le nom des fichiers exportés ;](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mise en correspondance des attributs et des identités {#map}

Dans le **[!UICONTROL Mappage]** vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir la [étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activation de l’interface utilisateur des destinations par lot .

## (Version bêta) Exportation de jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Validation de l’exportation des données réussie {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez votre [!DNL Data Landing Zone] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
