---
keywords: publicité ; bing ;
title: Connexion Microsoft Bing
description: Avec la destination de connexion Microsoft Bing, vous pouvez exécuter des campagnes numériques de reciblage et d’audience ciblées sur l’ensemble du réseau Microsoft Advertising, y compris l’affichage publicitaire, la recherche et le natif.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: b9713d5155f89ee895d9fb623088eda77b931d89
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 30%

---

# Connexion [!DNL Microsoft Bing] {#bing-destination}

## Vue d’ensemble {#overview}


>[!IMPORTANT]
>
>Suite à une mise à niveau interne vers le service de destinations à partir d’août 2025, il se peut que vous subissiez une **baisse du nombre de profils activés** dans vos flux de données à [!DNL Microsoft Bing].
>
> Cette baisse est due à l’introduction de l’exigence de mappage **ECID** pour toutes les activations sur cette plateforme de destination. Pour plus d’informations, consultez la section [mappage obligatoire](#mandatory-mappings) de cette page.
>
>**Changements :**
>
>* Le mappage ECID (Experience Cloud ID) est désormais **obligatoire** pour toutes les activations de profil.
>* Les profils sans mappage ECID seront **supprimés** des flux de données d’activation existants.
>
>**Ce que vous devez faire**
>
>* Vérifiez les données de votre audience pour vous assurer que les profils possèdent des valeurs ECID valides.
>* Surveillez vos mesures d’activation pour vérifier le nombre de profils attendu.

Utilisez la destination [!DNL Microsoft Bing] pour envoyer des données de profil à l’ensemble du [!DNL Microsoft Advertising Network], y compris [!DNL Display Advertising], [!DNL Search] et [!DNL Native].

La destination [!DNL Microsoft Bing] crée des *[!DNL Custom Audiences]* dans Microsoft. Ils sont disponibles dans les [!DNL Microsoft Search Network] et [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]), comme indiqué dans la documentation Microsoft Advertising [&#128279;](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Pour envoyer des données de profil à [!DNL Microsoft Bing], vous devez d’abord vous connecter à la destination .

## Cas d’utilisation {#use-cases}

En tant que spécialiste marketing, je souhaite pouvoir utiliser des audiences créées à partir de [!DNL Microsoft Advertising IDs] pour cibler les utilisateurs et utilisatrices par le biais de publicités display ou search sur plusieurs canaux [!DNL Microsoft Advertising].

## Identités prises en charge {#supported-identities}

[!DNL Microsoft Bing] prend en charge l’activation des audiences en fonction des identités présentées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité | Description |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud ID. Cette identité est obligatoire pour que l’intégration fonctionne correctement, mais elle n’est pas utilisée pour l’activation de l’audience. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

**[!DNL Audience Export]** - vous exportez tous les membres d’une audience vers la destination [!DNL Microsoft Bing].

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience vers la destination [!DNL Microsoft Bing]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Microsoft Bing] sans jamais avoir activé la fonctionnalité de synchronisation des identifiants [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service Experience Cloud ID par le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations [!DNL Microsoft Bing] dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Experience Platform.

Lors de la configuration de la destination, vous devez fournir les informations suivantes :

* [!UICONTROL Account ID] : il s’agit de votre [!DNL Bing Ads CID], au format entier.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Renseigner les détails de la destination {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Account ID]** : votre [!DNL Bing Ads Customer ID] (CID). Votre CID est un entier qui se trouve dans l’URL lorsque vous vous connectez à [!DNL Microsoft Advertising].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Identifiant de mappage"
>abstract="Saisissez l’identifiant numérique de l’audience Bing auquel vous souhaitez mapper le segment sélectionné. Si le [!UICONTROL Mapping ID] fourni ne correspond pas à un ID d&#39;audience dans la destination Bing, vous ne verrez pas les données d&#39;audience attendues dans votre compte Bing."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Jeux de mappages préconfigurés"
>abstract="Nous avons préconfiguré ces deux jeux de mappages pour vous. Lorsque vous activez des données vers Microsoft Bing, les profils qualifiés pour les audiences activées doivent avoir au moins une identité ECID associée à leur profil, afin de pouvoir être exportés vers la destination."

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans l’étape [Planning des audiences](../../ui/activate-segment-streaming-destinations.md#scheduling), vous devez mapper manuellement le nom de l’audience dans le champ [!UICONTROL Mapping ID]. Cela permet de s’assurer que les métadonnées d’audience sont correctement transmises à [!DNL Bing].

![Image de l’interface utilisateur affichant l’écran du planning d’audience avec un exemple de la manière de mapper le nom de l’audience à l’identifiant de mappage Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Mappages obligatoires {#mandatory-mappings}

Toutes les identités cibles décrites dans la section [identités prises en charge](#supported-identities) sont obligatoires et doivent être mappées pendant le processus d’activation de l’audience. Cela inclut :

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

L’échec du mappage de toutes les identités requises vous empêche de terminer le workflow d’activation. Chaque identité remplit un rôle spécifique dans l’intégration et toutes sont nécessaires au bon fonctionnement de la destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Microsoft Bing], vérifiez votre compte [!DNL Microsoft Bing Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
