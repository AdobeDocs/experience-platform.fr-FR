---
title: Acxiom Real ID&trade ; Audience Connection
description: Utilisez la destination  [!DNL Acxiom Real ID&trade; Audience Connection]  pour améliorer et activer les audiences sur les plateformes telles que  [!DNL Altice],  [!DNL Ampersand] et  [!DNL Comcast].
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 15%

---


# Destination [!DNL Acxiom Real ID™ Audience Connection]

Utilisez la destination [!DNL Acxiom Real ID Audience Connection] pour améliorer les audiences avec la technologie [Real ID™](https://www.acxiom.com/real-id/real-id/) de [!DNL Acxiom]. Activez ensuite ces audiences sur plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

>[!NOTE]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Acxiom]. Pour toute demande ou information, contactez [!DNL Acxiom] directement à l’adresse [acxiom-adobe-help@acxiom.com](mailto:acxiom-adobe-help@acxiom.com).

Pour créer un connecteur de destination [!DNL Acxiom Real ID Audience Connection] à l’aide de l’interface utilisateur [!DNL Adobe Experience Platform], procédez comme suit. Utilisez ce connecteur pour créer et distribuer des audiences vers des destinations sélectionnées.

## Cas d’utilisation {#use-cases}

Utilisez cette destination si les [!DNL Real ID] de [!DNL Acxiom] sont chargées dans [!DNL Real-Time CDP] en tant qu’identifiant. Les cas d’utilisation suivants montrent comment utiliser la destination [!DNL Acxiom Real ID Audience Connection].

### Envoi d’audiences de [!DNL Experience Platform] vers votre compte [!DNL Acxiom] {#send-audiences}

Utilisez ce connecteur de destination pour envoyer des audiences de [!DNL Experience Platform] vers votre compte [!DNL Acxiom] pour l’acquisition cross-canal.

Par exemple, le service des opérations marketing d’une marque mondiale de services financiers s’intéresse à l’acquisition de clients cross-canal par le biais de plusieurs plateformes publicitaires. Ils peuvent utiliser le connecteur de destination [!DNL Acxiom Real ID Audience Connection] pour envoyer des audiences de [!DNL Experience Platform] à [!DNL Acxiom], améliorer les audiences avec la technologie [!DNL Real ID] de [!DNL Acxiom] et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

## Conditions préalables {#prerequisites}

Avant de configurer la destination [!DNL Acxiom Real ID Audience Connection], remplissez les conditions préalables suivantes.

* **Confirmer les conditions d’utilisation :** lisez et signez les conditions d’utilisation de [!DNL Acxiom]. Vous recevez le lien vers le contrat une fois la commande client exécutée terminée. Tant que vous n’avez pas signé le contrat, la carte de destination [!DNL Acxiom Real ID Audience Connection] n’apparaît pas dans le catalogue des destinations [!DNL Experience Platform]. Une fois que vous avez accepté et signé le contrat, [!DNL Adobe] terminez la configuration et la carte de destination [!DNL Acxiom Real ID Audience Connection] devient visible.
* **Connaître votre ID d’organisation [!DNL Adobe] :** votre ID d’organisation [!DNL Adobe] est nécessaire pour remplir vos conditions d’utilisation. Voir la rubrique *Organisations dans Experience Cloud* de [!DNL Adobe] pour plus d’informations sur la manière d’[afficher votre ID d’organisation](https://experienceleague.adobe.com/fr/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Obtention d’une licence pour le produit [!DNL Real ID] d’[!DNL Acxiom] :** une fois que vous avez obtenu une licence, rendez les [!DNL Real ID] d’[!DNL Acxiom] disponibles dans [!DNL Real-Time CDP]. Voir [Acxiom Data Enhancement](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md) pour plus d’informations.

## Identités prises en charge {#supported-identities}

La destination [!DNL Real ID] Audience Connection de [!DNL Acxiom] prend en charge les activations d’identité suivantes. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | Mappez un champ source à cette identité cible. Votre champ source peut être un [!DNL Real ID] [!DNL Acxiom] ou un identifiant personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | Oui | Audiences générées via le [!DNL Experience Platform] [Segmentation Service](/help/segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li>audiences de chargement personnalisées [importées](/help/segmentation/ui/audience-portal.md#import-audience) dans [!DNL Experience Platform] à partir de fichiers CSV,</li><li>les audiences semblables,</li><li>les audiences fédérées,</li><li>les audiences générées dans d’autres applications [!DNL Experience Platform] telles que [!DNL Adobe Journey Optimizer],</li><li>et plus encore.</li></ul> |

{style="table-layout:auto"}

### Audiences prises en charge par type de données {#supported-audiences-data-type}

Le tableau suivant décrit les types de données d’audience que vous pouvez exporter vers cette destination.

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
| -------------------- | --------- | ----------- | --------- |
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client. Utilisez-les pour cibler des groupes spécifiques de personnes dans le cadre de campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Le tableau suivant décrit le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| ---- | ---- | ----- |
| Type d’exportation | **[!UICONTROL Audience export]** | Exporte tous les membres d’une audience avec les identifiants utilisés dans la destination [!DNL Acxiom Real ID Audience Connection]. |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Destinations prises en charge {#supported-destinations}

Activez les audiences vers les plateformes suivantes via la destination [!DNL Acxiom Real ID Audience Connection].

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## Se connecter à la destination {#connect}

[!DNL Experience Platform] gère automatiquement l’authentification pour la destination [!DNL Acxiom Real ID Audience Connection].

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

## Paramètres spécifiques à la destination {#destination-settings}

Certaines destinations [!DNL Acxiom Real ID Audience Connection] nécessitent des informations supplémentaires. Les sections suivantes fournissent des instructions détaillées sur la configuration de ces options.

### [!DNL Amazon] {#amazon}

Pour configurer les détails de la destination, renseignez les champs suivants.

* **[!UICONTROL Publisher Account ID]** : saisissez l’ID du compte d’éditeur associé à cette destination.

  ![Copie d’écran du panneau des détails de la destination [!DNL Amazon] affichant le champ ID du compte d’éditeur.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Pour configurer les détails de la destination, renseignez les champs suivants.

* **[!UICONTROL Destination Account ID]** : saisissez l’identifiant du compte de destination pour cette destination.

  ![Copie d’écran du panneau des détails de la destination [!DNL Facebook] affichant le champ Identifiant du compte de destination.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Pour configurer les détails de la destination, renseignez les champs suivants.

* **[!UICONTROL Segment Category]** : catégorie cible ou verticale de votre segment. Exemple : services financiers, automobile ou santé.

  ![Copie d’écran du panneau Détails de la destination [!DNL LG Ads] affichant le champ Catégorie de segments.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Pour configurer les détails de la destination, renseignez les champs suivants.

* **[!UICONTROL Destination Account ID]** : saisissez l’identifiant du compte de destination pour cette destination.

  ![Copie d’écran du panneau des détails de la destination [!DNL Pinterest] affichant le champ Identifiant du compte de destination.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Pour configurer les détails de la destination, renseignez les champs suivants.

* **[!UICONTROL Advertiser Name]** : saisissez le nom de l’annonceur pour cette destination.

  ![Copie d’écran du panneau des détails de la destination [!DNL Vizio] affichant le champ Nom de l’annonceur.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## Activer des audiences vers cette destination {#activate}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès [**[!UICONTROL View Identity Graph]**](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>La destination [!DNL Acxiom Real ID Audience Connection] ne prend en charge que les exportations de fichiers complets.

### Mapper les attributs et les identités {#map}

Pour que la destination [!DNL Acxiom Real ID Audience Connection] reçoive correctement les données d’audience, mappez le champ source de [!DNL Experience Platform] au champ cible [!DNL Acxiom Real ID Audience Connection] correct.

Le champ cible **[!UICONTROL Real ID]** est prérempli automatiquement à l’étape de mappage. Mappez-y votre champ source : un espace de noms d’identifiant personnalisé ou un [!DNL Acxiom] réel [!DNL Real ID] stocké dans votre schéma de profil.

| Nom du champ | Description | Obligatoire |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | Un [!DNL Real ID] est un identifiant alphanumérique unique de 36 octets provenant du graphique de résolution d’identité propriétaire de [!DNL Acxiom]. Il s’agit d’un identifiant qui représente une personne, un foyer ou une adresse. | Oui |

{style="table-layout:auto"}

Dans la colonne **[!UICONTROL Source Field]** , saisissez le nom de l’attribut source à mapper au champ cible **[!UICONTROL Real ID]**. Ou sélectionnez **[!UICONTROL Select source field]** pour parcourir les champs sources disponibles. Sélectionnez ensuite **[!UICONTROL Next]**.

![Capture d’écran de l’écran de mappage affichant la colonne [!UICONTROL Source Field] et le panneau [!UICONTROL Select source field].](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

Si vous n’utilisez pas le schéma standard de [!DNL Adobe], consultez le guide de l’interface utilisateur de [Query Service](/help/query-service/ui/overview.md) pour renseigner le schéma standard de [!DNL Adobe] avec vos noms de champ.

### Vérifier la destination {#review}

Une fois toutes les étapes effectuées, vérifiez le statut de la connexion de destination et les détails de l’audience avant de l’activer. Les audiences que vous avez sélectionnées apparaissent dans une liste. Chaque audience est un appel distinct à l’API [!DNL Acxiom Real ID Audience Connection].

Lorsque les résultats semblent corrects, sélectionnez **[!UICONTROL Finish]** pour activer la destination.

![Copie d’écran de l’écran Vérifier affichant le statut de connexion de destination et les audiences sélectionnées avant l’activation.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

## Résolution des problèmes {#troubleshooting}

Si votre représentant de destination ne parvient pas à localiser votre audience, contactez votre représentant de [!DNL Adobe] pour obtenir de l’aide.

Fournissez les informations suivantes à votre représentant [!DNL Adobe] :

* Nom de l’audience
* Nom de la destination
* Date d’activation de l’audience
* Nom du fichier exporté

## Étapes suivantes {#next-steps}

Vous avez activé une audience sur la plateforme de destination sélectionnée. Ensuite, contactez le représentant de votre plateforme de destination pour commencer à configurer votre campagne.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
