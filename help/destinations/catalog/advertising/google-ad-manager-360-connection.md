---
title: (Version bêta) [!DNL Google Ad Manager 360] connection
description: Google Ad Manager 360 est une plateforme de service publicitaire de Google qui permet aux éditeurs de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.
source-git-commit: 60ae86ed6e741bd7739086105bfe70952841d454
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 15%

---

# (Version bêta) [!DNL Google Ad Manager 360] connection

## Présentation {#overview}

Le [!DNL Google Ad Manager 360] La connexion active le chargement par lots pour [!DNL publisher provided identifiers] (PPID) dans [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Pour plus d’informations sur le fonctionnement des identifiants fournis par l’éditeur dans Google Ad Manager 360, voir la section [documentation Google officielle](https://support.google.com/admanager/answer/2880055?hl=en).

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et n’est disponible que pour un nombre limité de clients. Pour demander l’accès au [!DNL Google Ad Manager 360] connectez-vous, contactez votre représentant Adobe et fournissez vos [!DNL IMS Organization ID].

Le [!DNL Google Ad Manager 360] exports de destination [!DNL CSV] dans vos fichiers [!DNL Google Cloud Storage] du compartiment. Une fois que vous avez exporté la variable [!DNL CSV] fichiers, vous devez les importer dans vos [!DNL Google Ad Manager 360] compte .

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques à [!DNL Google Ad Manager 360] destinations.

* Les audiences activées sont créées par programmation dans la plateforme Google et renseignées dans le fichier CSV.

## Identités prises en charge {#supported-identities}

[!DNL This integration] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Sélectionnez cette identité cible pour envoyer des audiences à [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

### Liste autorisée {#allow-listing}

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première [!DNL Google Ad Manager] destination dans Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.

Avant de créer la variable [!DNL Google Ad Manager 360] destination dans Platform, vous devez contacter [!DNL Google] pour que l’Adobe soit placé sur la liste des fournisseurs de données autorisés et pour que votre compte soit ajouté à la liste autorisée. Contact [!DNL Google] et fournissez les informations suivantes :

* **Identifiant de compte**: Identifiant de compte de l’Adobe avec Google. ID de compte : 87933855.
* **ID de client**: Identifiant du compte client de l’Adobe avec Google. ID de client : 89690775.
* **Identifiant réseau** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* **Identifiant du lien d’audience** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* Votre type de compte. DFP de Google ou AdX buyer.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Nom du compartiment]**: saisissez le nom du [!DNL Google Cloud Storage] compartiment à utiliser par cette destination.
* **[!UICONTROL Chemin du dossier]**: saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Dans l’étape de mappage d’identité, vous pouvez voir les mappages préremplis suivants :

| Mappage prérenseigné | Description |
|---------|----------|
| `ECID` -> `ppid` | Il s’agit du seul mappage prérenseigné modifiable par l’utilisateur. Vous pouvez sélectionner n’importe lequel de vos attributs ou espaces de noms d’identité dans Platform et les mapper à `ppid`. |
| `metadata.segment.alias` -> `list_id` | Met en correspondance les noms de segment Experience Platform avec les ID de segment dans la plateforme Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indique à la plateforme Google à quel moment supprimer des utilisateurs disqualifiés des segments. |

Ces mappages sont requis par [!DNL Google Ad Manager 360] et sont automatiquement créés par Adobe Experience Platform pour tous. [!DNL Google Ad Manager 360] connexions.

![Image de l’interface utilisateur montrant l’étape de mappage pour Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Données exportées {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez votre [!DNL Google Cloud Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
