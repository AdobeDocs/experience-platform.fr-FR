---
title: Connexion à  [!DNL Google Ad Manager 360]  (Version bêta)
description: Google Ad Manager 360 est une plateforme de diffusion des publicités de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, en vidéo et dans les applications mobiles.
exl-id: 3251145a-3e4d-40aa-b120-d79c8c9c7cae
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 61%

---

# Connexion à [!DNL Google Ad Manager 360] (Version bêta)

>[!IMPORTANT]
>
> Google publie des modifications sur l’ [API Google Ads](https://developers.google.com/google-ads/api/docs/start), la [correspondance client](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) et l’ [API Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies en vertu de la [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) dans l’Union européenne ([Stratégie de consentement de l’utilisateur de l’UE](https://www.google.com/about/company/user-consent-policy/)). L’application de ces modifications aux exigences de consentement est en ligne depuis le 6 mars 2024.
><br/>
>Pour respecter la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audiences pour les utilisateurs de l’Espace économique européen (EEE), les publicitaires et les partenaires doivent s’assurer qu’ils transmettent le consentement de l’utilisateur final lors du transfert des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.
><br/>
>Les clients qui ont acheté Adobe Privacy &amp; Security Shield et qui ont configuré une [politique de consentement](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non autorisés n’ont pas besoin d’agir.
><br/>
>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser les fonctionnalités [définition de segment](../../../segmentation/home.md#segment-definitions) du [créateur de segments](../../../segmentation/ui/segment-builder.md) pour filtrer les profils non autorisés, afin de continuer à utiliser sans interruption les destinations Real-Time CDP Google existantes.

La connexion à [!DNL Google Ad Manager 360] active le chargement par lots pour [!DNL publisher provided identifiers] (PPID) dans [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage].

Pour plus d’informations sur le fonctionnement des identifiants fournis par l’éditeur dans Google Ad Manager 360, consultez la section [documentation Google officielle](https://support.google.com/admanager/answer/2880055?hl=fr).

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et nʼest disponible que pour un nombre de clients limité. Pour demander l’accès à la connexion à [!DNL Google Ad Manager 360], contactez votre représentant Adobe et fournissez vos [!DNL organization ID].

La destination [!DNL Google Ad Manager 360] exporte des fichiers [!DNL CSV] vers votre compartiment [!DNL Google Cloud Storage]. Une fois que vous avez exporté les fichiers [!DNL CSV], vous devez les importer dans votre compte [!DNL Google Ad Manager 360].

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Ad Manager 360].

* Les audiences activées sont créées par programmation dans la plateforme Google et renseignées dans le fichier CSV.

## Identités prises en charge {#supported-identities}

[!DNL This integration] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| PPID | [!DNL Publisher provided ID] | Sélectionnez cette identité cible pour envoyer des audiences à [!DNL Google Ad Manager 360] |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables (par exemple votre PPID), tels que choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

### Liste autorisée {#allow-listing}

La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ad Manager 360] dans Platform. Veillez à terminer le processus de mise en liste autorisée décrit ci-dessous, avant de créer votre destination.

>[!NOTE]
>
>L’exception à cette règle concerne les clients [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=fr) existants. Si vous avez déjà créé une connexion à cette destination Google dans Audience Manager, il n’est pas nécessaire de passer à nouveau par le processus de liste autorisée et vous pouvez passer directement aux étapes suivantes.

1. Suivez les étapes décrites dans la [documentation de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=fr) pour ajouter l’Adobe en tant que plateforme de gestion des données liée (DMP).
2. Dans l’interface [!DNL Google Ad Manager], accédez à **[!UICONTROL Admin]** > **[!UICONTROL Paramètres globaux]** > **[!UICONTROL Paramètres réseau]**, puis activez le curseur **[!UICONTROL Accès API]**.


## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs obligatoires et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL ID de clé d’accès]** : chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform.
* **[!UICONTROL Clé d’accès secrète]** : chaîne codée en base64 de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] sur Platform.

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] Présentation de la source](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam360_appendSegmentID"
>title="Ajouter un identifiant d’audience au nom de l’audience"
>abstract="Sélectionnez cette option pour que le nom de l’audience dans cette destination inclue l’identifiant de l’audience d’Experience Platform, comme suit : `Audience Name (Audience ID)`."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui héberge les fichiers exportés.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du compartiment [!DNL Google Cloud Storage] que cette destination doit utiliser.
* **[!UICONTROL ID de compte]** : saisissez votre [!DNL Audience Link ID] à partir de votre compte [!DNL Google]. Il s’agit d’un identifiant spécifique associé à votre réseau [!DNL Google Ad Manager] (et non à votre [!DNL Network code]). Vous pouvez le trouver sous **[!UICONTROL Admin > Paramètres globaux]** dans l’interface [!DNL Google Ad Manager].
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte [!DNL Google] :
   * Utiliser `AdX buyer` pour [!DNL Google AdX]
   * Utiliser `DFP by Google` pour [!DNL DoubleClick] pour les éditeurs
* **[!UICONTROL Ajouter un ID d’audience au nom de l’audience]** : sélectionnez cette option pour que le nom de l’audience dans Google Ad Manager 360 inclue l’ID d’audience de l’Experience Platform, comme suit : `Audience Name (Audience ID)`.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activation des données d’audience vers des destinations d’exportation de profil de lot](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

Dans l’étape de mappage d’identité, vous pouvez voir les mappages prérenseignés suivants :

| Mappage prérenseigné | Description |
|---------|----------|
| `ECID` -> `ppid` | Il s’agit du seul mappage prérenseigné modifiable par l’utilisateur. Vous pouvez sélectionner n’importe lequel de vos attributs ou espaces de noms d’identité dans Platform et les mapper à `ppid`. |
| `metadata.segment.alias` -> `list_id` | Met en correspondance les noms d’audience Experience Platform avec les ID d’audience dans la plateforme Google. |
| `iif(${segmentMembership.ups.seg_id.status}=="exited", "1","0")` -> `delete` | Indique à la plateforme Google à quel moment supprimer des utilisateurs disqualifiés des segments. |

Ces mappages sont exigés par [!DNL Google Ad Manager 360] et sont automatiquement créés par Adobe Experience Platform pour toutes les connexions [!DNL Google Ad Manager 360].

![Image de l’interface utilisateur montrant l’étape de mappage pour Google Ad Manager 360.](../../assets/catalog/advertising/google-ad-manager-360/ad-manager-360-mapping.png)

## Données exportées {#exported-data}

Pour vérifier si l’exportation des données a été réalisée, vérifiez votre compartiment [!DNL Google Cloud Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Dépannage {#troubleshooting}

Si vous rencontrez des erreurs lors de l’utilisation de cette destination et que vous devez atteindre Adobe ou Google, gardez à portée de main les identifiants suivants.

Il s’agit des ID de compte Google de l’Adobe :

* **[!UICONTROL ID de compte]** : 87933855
* **[!UICONTROL ID de client]** : 89690775