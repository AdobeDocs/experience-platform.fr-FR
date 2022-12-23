---
title: Connexion à  [!DNL Google Ad Manager 360]  (Version bêta)
description: Google Ad Manager 360 est une plateforme de diffusion d’annonces de Google qui donne aux éditeurs les moyens de gérer l’affichage des annonces sur leurs sites web, en vidéo et dans les applications mobiles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: ht
source-wordcount: '914'
ht-degree: 100%

---

# Connexion à [!DNL Google Ad Manager 360] (Version bêta)

## Présentation {#overview}

La connexion à [!DNL Google Ad Manager 360] active le chargement par lots pour [!DNL publisher provided identifiers] (PPID) dans [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Pour plus d’informations sur le fonctionnement des identifiants fournis par l’éditeur dans Google Ad Manager 360, consultez la section [documentation Google officielle](https://support.google.com/admanager/answer/2880055?hl=fr).

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et nʼest disponible que pour un nombre de clients limité. Pour demander l’accès à la connexion à [!DNL Google Ad Manager 360], contactez votre représentant Adobe et fournissez vos [!DNL IMS Organization ID].

La destination [!DNL Google Ad Manager 360] exporte des fichiers [!DNL CSV] vers votre compartiment [!DNL Google Cloud Storage]. Une fois que vous avez exporté les fichiers [!DNL CSV], vous devez les importer dans votre compte [!DNL Google Ad Manager 360].

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Ad Manager 360].

* Les audiences activées sont créées par programmation dans la plateforme Google et renseignées dans le fichier CSV.

## Identités prises en charge {#supported-identities}

[!DNL This integration] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Sélectionnez cette identité cible pour envoyer des audiences à [!DNL Google Ad Manager 360] |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (par exemple votre PPID), tels que choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

### Liste autorisée {#allow-listing}

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ad Manager] dans Platform. Veuillez vous assurer que [!DNL Google] a complété le processus de liste autorisée décrit ci-dessous avant de créer une destination.

>[!IMPORTANT]
>
>Google a simplifié le processus de connexion des plateformes de gestion d’audience externes à Google Ad Manager 360. Vous pouvez maintenant suivre le processus de liaison à Google Ad Manager 360 en libre-service. Lire [Segments des plateformes de gestion de données](https://support.google.com/admanager/answer/3289669?hl=fr) dans la documentation de Google. Vous devriez avoir à portée de main les identifiants répertoriés ci-dessous.

* **Identifiant de compte** : l’identifiant du compte Adobe avec Google. Identifiant de compte : 87933855.
* **Identifiant client** : l’identifiant client d’Adobe avec Google. Identifiant client : 89690775.
* **Code réseau** : il s’agit de votre identifiant réseau [!DNL Google Ad Manager], que l’on trouve sous **[!UICONTROL Admin > Paramètres globaux]** dans l’interface Google, ainsi que dans l’URL.
* **Identifiant du lien d’audience** : il s’agit d’un identifiant spécifique associé à votre réseau [!DNL Google Ad Manager] (et non votre [!DNL Network code]), que l’on trouve également sous **[!UICONTROL Admin > Paramètres globaux]** dans l’interface de Google.
* Votre type de compte. DFP de Google ou AdX buyer.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs obligatoires et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL ID de clé d’accès]** : chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform.
* **[!UICONTROL Clé d’accès secrète]** : chaîne codée en base64 de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform.

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] Présentation de la source](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du compartiment [!DNL Google Cloud Storage] que cette destination doit utiliser.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL ID de compte]** : renseignez votre ID de lien d’audience avec [!DNL Google].
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utiliser `DFP by Google` pour [!DNL DoubleClick] pour les éditeurs
   * Utiliser `AdX buyer` pour [!DNL Google AdX]

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Dans l’étape de mappage d’identité, vous pouvez voir les mappages prérenseignés suivants :

| Mappage prérenseigné | Description |
|---------|----------|
| `ECID` -> `ppid` | Il s’agit du seul mappage prérenseigné modifiable par l’utilisateur. Vous pouvez sélectionner n’importe lequel de vos attributs ou espaces de noms d’identité dans Platform et les mapper à `ppid`. |
| `metadata.segment.alias` -> `list_id` | Mappe les noms de segment Experience Platform sur les ID de segment dans la plateforme Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indique à la plateforme Google à quel moment supprimer des utilisateurs disqualifiés des segments. |

Ces mappages sont exigés par [!DNL Google Ad Manager 360] et sont automatiquement créés par Adobe Experience Platform pour toutes les connexions [!DNL Google Ad Manager 360].

![Image de l’interface utilisateur montrant l’étape de mappage pour Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Données exportées {#exported-data}

Pour vérifier si l’exportation des données a été réalisée, vérifiez votre compartiment [!DNL Google Cloud Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
