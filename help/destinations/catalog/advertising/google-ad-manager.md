---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connexion Google Ad Manager
description: Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de diffusion des publicités de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 60%

---

# Connexion [!DNL Google Ad Manager]

>[!IMPORTANT]
>
> Google publie des modifications sur l’ [API Google Ads](https://developers.google.com/google-ads/api/docs/start), la [correspondance client](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) et l’ [API Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies en vertu de la [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) dans l’Union européenne ([Stratégie de consentement de l’utilisateur de l’UE](https://www.google.com/about/company/user-consent-policy/)). L’application de ces modifications aux exigences de consentement est en ligne depuis le 6 mars 2024.
><br/>
>Pour respecter la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audiences pour les utilisateurs de l’Espace économique européen (EEE), les publicitaires et les partenaires doivent s’assurer qu’ils transmettent le consentement de l’utilisateur final lors du transfert des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.
><br/>
>Les clients qui ont acheté Adobe Privacy &amp; Security Shield et qui ont configuré une [politique de consentement](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non autorisés n’ont pas besoin d’agir.
><br/>
>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser les fonctionnalités [définition de segment](../../../segmentation/home.md#segment-definitions) du [créateur de segments](../../../segmentation/ui/segment-builder.md) pour filtrer les profils non autorisés, afin de continuer à utiliser sans interruption les destinations Real-Time CDP Google existantes.


[!DNL Google Ad Manager], anciennement appelé [!DNL DoubleClick for Publishers] (DFP) ou [!DNL DoubleClick AdX], est une plateforme de diffusion des publicités de [!DNL Google] qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Ad Manager] :

* Les audiences activées sont créées par programmation dans la plateforme [!DNL Google].
* [!DNL Platform] n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.
* Après avoir mappé une audience sur une destination [!DNL Google Ad Manager], le nom de l’audience apparaît immédiatement dans l’interface utilisateur de [!DNL Google Ad Manager].
* La population de segments nécessite 24 à 48 heures pour apparaître dans [!DNL Google Ad Manager]. En outre, les audiences doivent avoir une taille d’audience d’au moins 50 profils pour être affichées dans [!DNL Google Ad Manager]. Les audiences dont la taille est inférieure à 50 profils ne seront pas renseignées dans [!DNL Google Ad Manager].

## Identités prises en charge {#supported-identities}

[!DNL Google Ad Manager] prend en charge l’activation des audiences en fonction des identités affichées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr), également appelé [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par Audience Manager à chaque appareil avec lequel il interagit. | Google utilise [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr) pour cibler les utilisateurs en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] utilise cet identifiant pour cibler les utilisateurs situés en dehors de la Californie. |
| RIDA | ID Roku pour la publicité. Cet identifiant identifie de manière unique les appareils Roku. |  |
| MAID | ID Microsoft Advertising. Cet identifiant identifie de manière unique les appareils exécutant Windows 10. |  |
| ID Amazon Fire TV | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

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
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez toutes les personnes membres d’une audience vers la destination Google. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Si vous souhaitez créer votre première destination avec [!DNL Google Ad Manager] sans jamais avoir activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service Experience Cloud ID dans le passé (avec Audience Manager ou d’autres applications), prenez contact avec Adobe Consulting ou l’assistance clientèle d’Adobe pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations [!DNL Google] dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Platform.

### Liste autorisée {#allow-listing}

La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ad Manager] dans Platform. Veillez à terminer le processus de mise en liste autorisée décrit ci-dessous, avant de créer votre destination.

1. Suivez les étapes décrites dans la [documentation de Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=fr) pour ajouter l’Adobe en tant que plateforme de gestion des données liée (DMP).
2. Dans l’interface [!DNL Google Ad Manager], accédez à **[!UICONTROL Admin]** > **[!UICONTROL Paramètres globaux]** > **[!UICONTROL Paramètres réseau]**, puis activez le curseur **[!UICONTROL Accès API]**.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Ajouter un identifiant d’audience au nom de l’audience"
>abstract="Sélectionnez cette option pour que le nom de l’audience dans Google Ad Manager inclue l’identifiant de l’audience d’Experience Platform, comme suit : `Audience Name (Audience ID)`"

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL ID de compte]** : saisissez votre [!DNL Audience Link ID] à partir de votre compte [!DNL Google]. Il s’agit d’un identifiant spécifique associé à votre réseau [!DNL Google Ad Manager] (et non à votre [!DNL Network code]). Vous pouvez le trouver sous **[!UICONTROL Admin > Paramètres globaux]** dans l’interface [!DNL Google Ad Manager].
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utiliser `DFP by Google` pour [!DNL DoubleClick] pour les éditeurs
   * Utiliser `AdX buyer` pour [!DNL Google AdX]
* **[!UICONTROL Ajouter un ID d’audience au nom de l’audience]** : sélectionnez cette option pour que le nom de l’audience dans Google Ad Manager inclue l’ID d’audience de l’Experience Platform, comme suit : `Audience Name (Audience ID)`.

>[!NOTE]
>
>Lorsque vous configurez une destination [!DNL Google Ad Manager], collaborez avec votre [!DNL Google Account Manager] ou votre représentant Adobe pour comprendre le type de compte dont vous disposez.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Ad Manager], vérifiez votre compte [!DNL Google Ad Manager]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.

## Dépannage {#troubleshooting}

Si vous rencontrez des erreurs lors de l’utilisation de cette destination et que vous devez atteindre Adobe ou Google, gardez à portée de main les identifiants suivants.

Il s’agit des ID de compte Google de l’Adobe :

* **[!UICONTROL ID de compte]** : 87933855
* **[!UICONTROL ID de client]** : 89690775