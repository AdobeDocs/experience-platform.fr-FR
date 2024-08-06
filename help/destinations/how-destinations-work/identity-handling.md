---
title: Gestion des identités dans le workflow d’activation des destinations
description: Découvrez comment l’exportation d’identités est gérée dans le workflow d’activation, en fonction du type de destination.
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: 322510055bd8b8803292a2b4af9df9e1dbee7ffb
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 99%

---

# Gestion des identités dans le workflow d’activation des destinations

Cette page décrit les particularités de l’exportation d’identités vers différents types de destination et vous explique comment trouver les identités disponibles à l’exportation en fonction de la destination.

>[!TIP]
>
> Pour obtenir des informations détaillées sur les identités, les espaces de noms d’identités et les définitions de termes liés aux identités, consultez la [présentation du Service d’identités](/help/identity-service/home.md).

Chaque destination du [catalogue](/help/destinations/catalog/overview.md) est légèrement différente. Il n’existe donc pas de configuration unique pour toutes les destinations. Cependant, certains modèles guident la configuration des destinations et leurs exigences en matière d’identité, comme décrit dans les sections ci-dessous.

## Destinations basées sur des fichiers {#file-based}

Pour les [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based) (par exemple, [!DNL Amazon S3], SFTP, la plupart des destinations de marketing par e-mail, telles que [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), la configuration de l’identité dans la plupart de ces destinations est ouverte, ce qui signifie que vous n’êtes pas tenu de sélectionner une identité à l’étape [Sélectionner des attributs](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) du workflow d’activation par lots.

Si vous choisissez d’ajouter des identités à vos exportations de fichiers, notez qu’une seule identité de l’[espace de noms d’identité](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer) peut être sélectionné dans une exportation. Lorsque vous sélectionnez une identité à exporter, elle est automatiquement sélectionnée en tant qu’[attribut obligatoire](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) et [clé de déduplication](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Une identité sélectionnée comme attribut obligatoire et clé de déduplication.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Pour pallier ce problème, vous pouvez ajouter d’autres identités à l’exportation si elles ont été ingérées en tant qu’attributs dans Experience Platform. Consultez l’exemple ci-dessous dans lequel l’adresse e-mail d’attribut XDM a été sélectionnée pour l’exportation, en plus de l’espace de noms d’identité `Phone_E.164`.

![Exemple d’attribut d’adresse e-mail sélectionné pour l’exportation.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exporter une identité depuis un mappage d’identités et exporter une identité en tant qu’attribut XDM - les différences {#identity-map-or-attribute}

Le nombre d’enregistrements exportés peut varier, selon votre choix d’exporter des identités à partir du mappage d’identités ou des identités qui ont été ingérées en tant qu’attributs dans Experience Platform. Les [politiques de fusion](/help/profile/merge-policies/overview.md) jouent également un rôle important dans le nombre d’enregistrements qui sont exportés lorsque vous sélectionnez des identités à partir d’un mappage d’identités.

Supposons que vous disposiez de deux jeux de données différents. Les fragments de profil suivants seront fusionnés en un seul profil client :

**Fragment de profil 1**

| Mappage d’identités | Prénom | Nom | Attribut d’e-mail |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | email 1 |


**Fragment de profil 2**

| Mappage d’identités | Prénom | Nom | Attribut d’e-mail |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | email 2 |

Le profil fusionné se présente comme suit :

| Mappage d’identités | Prénom | Nom | Attribut d’e-mail |
|---------|----------|---------|--------|
| email 1, email 2, Loyalty ID1 | John | Doe | email 2 |

Le comportement de l’exportation diffère selon que vous sélectionnez `IdentityMap: Email` ou `xdm: personalEmail.address` pour l’exportation.

Si un client ou une cliente active `IdentityMap: Email`, il y aura deux enregistrements dans le fichier exporté, un pour email1 et un autre pour email2.

Cependant, si un client ou une cliente active `xdm: personalEmail.address`, seul email2 sera présent dans l’enregistrement, puisque le champ d’attribut d’e-mail inclut uniquement email2. Ces situations peuvent répondre à différents cas d’utilisation où vous pouvez souhaiter activer toutes les adresses e-mail que vous avez dans un fichier pour un client ou une cliente, ou simplement l’adresse e-mail la plus récente que vous avez dans un fichier pour le client ou la cliente.

N’oubliez pas que le nombre d’enregistrements que vous exportez dépend de vos politiques de fusion et de votre choix de sélection des identités ou des attributs dans l’exportation.

## Destinations de streaming basées sur les API {#streaming-destinations}

Les [destinations de streaming basées sur les API](/help/destinations/destination-types.md#streaming-destination) créées avec [Destination SDK](/help/destinations/destination-sdk/overview.md) (par exemple, [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze], etc.) ne prennent en charge que des identifiants spécifiques pour l’exportation. Pour plus d’informations sur les identités spécifiques qui peuvent être exportées vers chaque destination, reportez-vous à la section *identités prises en charge* dans chaque page de documentation de destination (voir par exemple la [section des identités prises en charge](/help/destinations/catalog/advertising/pinterest.md) dans la page de destination [!DNL Pinterest]).

Notez toutefois que vous avez la possibilité d’utiliser les données de [graphiques privés](/help/profile/merge-policies/overview.md#id-stitching) ou d’attributs en tant qu’identités. Cela signifie que vous pouvez mapper les attributs XDM au champ d’identité requis par la destination. Vous trouverez ci-dessous un exemple pour la destination [!DNL Pinterest], où l’attribut XDM `personalEmail.address` est mappé sur l’identité [!DNL Pinterest] `pinterest_audience` requise.

>[!TIP]
>
>Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour qu’Experience Platform hache automatiquement les données lors de l’activation. En savoir plus sur l’option **[!UICONTROL Appliquer la transformation]** dans le [tutoriel sur l’activation des destinations de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exemple d’attribut d’adresse e-mail mappé à un champ d’identité pour la destination Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinations publicitaires reposant sur des intégrations de cookies tiers {#third-party-cookie-destinations}

Les clientes et clients n’ont pas besoin de sélectionner des identifiants dans le workflow d’activation pour les destinations publicitaires reposant sur des cookies tiers (par exemple : [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]). Pour ces destinations, lors de la configuration d’un workflow d’activation, Experience Platform recherche automatiquement la table de correspondance d’identité créée par [[!UICONTROL Experience Cloud ID service]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et exporte toutes les identités disponibles pour un profil et prises en charge par la destination

Ces destinations nécessitent qu’une synchronisation des identifiants se produise via [!UICONTROL Experience Cloud ID Service] ou [!UICONTROL Experience Platform Web SDK].

Si vous utilisez le [!UICONTROL SDK Web Experience Platform] et que l’ancien [!UICONTROL Experience Cloud ID Service] n’est pas implémenté sur la page, vous devez vous assurer que le flux de données du site web en question est activé pour permettre la synchronisation des identifiants tiers, comme indiqué dans la [documentation sur la configuration des trains de données](/help/datastreams/configure.md#create).

Lors de la configuration d’un train de données comme décrit dans la documentation ci-dessus, vous devez vous assurer que le curseur **[!UICONTROL Synchronisation des identifiants tiers]** est activé. La plupart des clientes et clients laissent le champ `container_id` vide (0 par défaut). Vous ne devez modifier cette valeur que si l’ancienne implémentation de votre Audience Manager utilisait un ID de conteneur spécifique (notez toutefois qu’il s’agit de la vaste minorité de clientes et clients).

>[!NOTE]
>
>La plupart de ces destinations publicitaires sont prises en charge dans Audience Manager (ces types de destinations sont connus dans Audience Manager en tant que destinations basées sur des appareils. Voir une [liste de toutes les destinations basées sur des appareils prises en charge dans Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)). Seules quelques-unes sont répertoriées dans Experience Platform. Pour plus d’informations sur le partage de données entre Experience Platform et Audience Manager, consultez la section sur l’[activation du partage de données entre Experience Platform et Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data). Actuellement, il n’est pas prévu de prendre en charge d’autres destinations de cookie tiers.

## Destinations d’entreprise {#enterprise-destinations}

[Destinations d’entreprise](/help/destinations/destination-types.md#advanced-enterprise-destinations) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) ne nécessitent pas d’identifiants spécifiques dans l’exportation des données, car ils sont conçus pour les cas d’utilisation de l’intégration d’entreprise. Cependant, vous pouvez exporter des identités en tant qu’attributs XDM ou à partir du mappage d’identité, si vous le souhaitez. Affichez un [exemple de données exportées vers la destination HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), qui inclut l’attribut XDM `personalEmail.address` et les identités `ECID` et `email_lc_sha256` (adresse électronique hachée) à partir du mappge d’identité.

## Destinations de personnalisation {#personalization-destinations}

Les [Destinations de personnalisation (ou Edge)](/help/destinations/destination-types.md#edge-personalization-destinations) (par exemple : Adobe Target, [!DNL Custom Personalization]) ne nécessitent aucune sélection d’identité dans le workflow d’activation, car l’intégration est une recherche de profil. Le client ou la cliente ([!DNL Target], [!DNL Web SDK], ou d’autres) interroge [[!UICONTROL Edge]](/help/collection/home.md#edge) et extrait les informations de profil nécessaires pour la personnalisation sur site.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment déterminer les identités prises en charge ou requises pour des destinations individuelles. Vous savez également comment fonctionne la sélection d’identité pour chaque type de destination.

Ensuite, vous pouvez en savoir plus sur les [paramètres d’exportation](/help/destinations/how-destinations-work/destinations-configurations.md) pour les destinations sont communs parmi les types de destination, ceux qui peuvent être configurés au niveau d’une destination individuelle par les développeurs et développeuses, et sur les paramètres qui peuvent être modifiés par les utilisateurs et utilisatrices dans le processus d’activation.

Vous pouvez également consulter toutes les destinations disponibles dans le [catalogue](/help/destinations/catalog/overview.md).
