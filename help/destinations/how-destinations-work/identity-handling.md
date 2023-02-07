---
title: Gestion des identités dans le workflow d’activation des destinations
description: Découvrez comment l’exportation d’identité est gérée dans le workflow d’activation, en fonction du type de destination.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 3%

---

# Gestion des identités dans le workflow d’activation des destinations

Cette page décrit les particularités de la manière dont les identités sont exportées vers différents types de destination et vous explique comment trouver les identités disponibles à l’exportation en fonction de la destination.

>[!TIP]
>
> Pour obtenir des informations détaillées sur les identités, les espaces de noms d’identité et les définitions de termes liés à l’identité, consultez la rubrique [présentation d’identity service](/help/identity-service/home.md).

Chaque destination du [catalogue](/help/destinations/catalog/overview.md) est légèrement différent. Il n’existe donc pas de configuration unique pour toutes les destinations. Cependant, certains modèles guident la configuration des destinations et leurs exigences d’identité, comme décrit dans les sections ci-dessous.

## Destinations basées sur des fichiers {#file-based}

Pour [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based) (par exemple, [!DNL Amazon S3], SFTP, la plupart des destinations de marketing par e-mail, telles que [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), la configuration de l’identité dans la plupart de ces destinations est ouverte, ce qui signifie que vous n’êtes pas tenu de sélectionner une identité dans la variable [Sélectionner des attributs](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) étape du workflow d’activation par lots.

Si vous choisissez d’ajouter des identités à vos exportations de fichiers, notez qu’une seule identité de la variable [namespace d’identité](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) peut être sélectionné dans un export. Lorsque vous sélectionnez une identité à exporter, elle est automatiquement sélectionnée en tant que [attribut obligatoire](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) et [clé de déduplication](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Une identité sélectionnée comme attribut obligatoire et clé de déduplication.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Pour pallier ce problème, vous pouvez ajouter d’autres identités à l’exportation si elles ont été ingérées en tant qu’attributs dans Experience Platform. Voir ci-dessous un exemple dans lequel l’adresse électronique d’attribut XDM a été sélectionnée pour l’exportation, en plus de l’espace de noms d’identité. `Phone_E.164`.

![Exemple d&#39;attribut d&#39;adresse email sélectionné pour l&#39;export.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Exporter une identité depuis une carte d’identité plutôt que d’exporter une identité en tant qu’attribut XDM - les différences {#identity-map-or-attribute}

Le nombre d’enregistrements exportés peut varier, selon que vous sélectionnez pour exporter des identités à partir de la carte d’identité ou des identités qui ont été ingérées en tant qu’attributs dans Experience Platform. [Stratégies de fusion](/help/profile/merge-policies/overview.md) joue également un rôle important dans le nombre d’enregistrements qui sont exportés lorsque vous sélectionnez des identités dans identity map.

Supposons, par exemple, que vous disposiez de deux jeux de données différents les fragments de profil suivants qui seront fusionnés en un seul profil client :

**Fragment de profil 1**

| Mappage d’identités | Prénom | Nom | Email attribute |
|---------|----------|---------|--------|
| email1, Loyalty ID1 | John | Doe | email 1 |


**Fragment de profil 2**

| Mappage d’identités | Prénom | Nom | Email attribute |
|---------|----------|---------|--------|
| email2, Loyalty ID1 | John | Doe | email 2 |

Le profil fusionné se présente comme suit :

| Mappage d’identités | Prénom | Nom | Email attribute |
|---------|----------|---------|--------|
| email 1, email 2, Loyalty ID1 | John | Doe | email 2 |

Le comportement de l’exportation diffère selon que vous sélectionnez ou non `IdentityMap: Email` ou `xdm: personalEmail.address` pour l’exportation.

Si un client s’active `IdentityMap: Email`, il y aura deux enregistrements dans le fichier exporté, un pour email1 et un autre pour email2.

Cependant, si un client s’active `xdm: personalEmail.address`, seul email2 sera présent dans l’enregistrement, puisque le champ attribut email inclut uniquement email2. Ces situations peuvent résoudre différents cas d’utilisation où vous pouvez souhaiter activer toutes les adresses électroniques que vous avez dans un fichier pour un client, ou simplement l’adresse électronique la plus récente que vous avez dans un fichier pour le client.

Il est à retenir que le nombre d’enregistrements que vous exportez dépend des stratégies de fusion de votre choix et de la sélection des identités ou des attributs dans l’exportation.

## Destinations de diffusion en continu basées sur les API {#streaming-destinations}

[Destinations de diffusion en continu basées sur les API](/help/destinations/destination-types.md#streaming-destination) créé avec [Destination SDK](/help/destinations/destination-sdk/overview.md) (par exemple, [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze], etc.) ne prennent en charge que des identifiants spécifiques pour l’exportation. Pour plus d’informations sur les identités spécifiques qui peuvent être exportées vers chaque destination, reportez-vous à la section *identités prises en charge* dans chaque page de documentation de destination (voir par exemple [section identités prises en charge](/help/destinations/catalog/advertising/pinterest.md) dans le [!DNL Pinterest] page de destination).

Notez toutefois que vous avez la possibilité d’utiliser les données de l’une ou l’autre des manières suivantes : [graphiques privés](/help/profile/merge-policies/overview.md#id-stitching) ou des attributs en tant qu’identités. Cela signifie que vous pouvez mapper les attributs XDM au champ d’identité requis par la destination. Voir ci-dessous un exemple pour la [!DNL Pinterest] destination, où l’attribut XDM `personalEmail.address` est mappé à la propriété [!DNL Pinterest] identité `pinterest_audience`.

>[!TIP]
>
>Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** pour que l’Experience Platform hache automatiquement les données lors de l’activation. En savoir plus sur les **[!UICONTROL Appliquer la transformation]** dans le [tutoriel sur l’activation des destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Exemple d’attribut d’adresse électronique mappé à un champ d’identité pour la destination Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinations publicitaires reposant sur des intégrations de cookies tiers {#third-party-cookie-destinations}

Destinations publicitaires reposant sur des cookies tiers (par exemple : [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) n’exigent pas que les clients sélectionnent des identifiants dans le workflow d’activation. Pour ces destinations, lors de la configuration d’un workflow d’activation, Experience Platform recherche automatiquement la table de correspondance d’identité créée par la variable [[!UICONTROL Service d’ID Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et exporte toutes les identités disponibles pour un profil et prises en charge par la destination.

Ces destinations nécessitent une synchronisation des identifiants pour se produire via l’une des destinations suivantes : [!UICONTROL Service d’ID Experience Cloud] ou [!UICONTROL SDK Web Experience Platform].

Si vous utilisez [!UICONTROL SDK Web Experience Platform] et l’héritage [!UICONTROL Service d’ID Experience Cloud] n’est pas implémenté sur la page, vous devez vous assurer que le flux de données du site web en question est activé pour permettre la synchronisation des identifiants tiers, comme indiqué dans la section [configuration de la documentation du flux de données](/help/edge/datastreams/configure.md#create).

Lors de la configuration d’un flux de données comme décrit dans la documentation ci-dessus, vous devez vous assurer que la variable **[!UICONTROL Synchronisation des identifiants tiers]** est activé. La plupart des clients quitteraient la variable `container_id` vide (0 par défaut). Vous ne devez modifier cette valeur que si l’implémentation de votre Audience Manager héritée utilisait un ID de conteneur spécifique (notez toutefois qu’il s’agit de la grande minorité de clients).

>[!NOTE]
>
>La plupart de ces destinations publicitaires sont prises en charge dans Audience Manager (ces types de destinations sont connus dans Audience Manager en tant que destinations basées sur des appareils. Voir [liste de toutes les destinations basées sur des appareils prises en charge dans l’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Seuls quelques-uns sont répertoriés dans Experience Platform. Pour plus d’informations sur le partage de données entre l’Experience Platform et l’Audience Manager, consultez la section sur [activation du partage de données entre Experience Platform et Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). Actuellement, il n’est pas prévu de prendre en charge d’autres destinations de cookie tiers.

## Destinations d’entreprise {#enterprise-destinations}

[Destinations d’entreprise](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) ne nécessitent pas d’identifiants spécifiques dans l’exportation des données, car ils sont conçus pour les cas d’utilisation de l’intégration d’entreprise. Cependant, vous pouvez exporter des identités en tant qu’attributs XDM ou à partir de la carte d’identité, si vous le souhaitez. Afficher un [exemple de données exportées vers la destination HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), qui inclut les `personalEmail.address` Attribut XDM et identités `ECID` et `email_lc_sha256` (adresse électronique hachée) à partir de la carte d’identité.

## Destinations de personnalisation {#personalization-destinations}

[Destinations de personnalisation (ou de périphérie)](/help/destinations/destination-types.md#edge-personalization-destinations) (par exemple : Adobe Target, [!DNL Custom Personalization]) ne nécessitent aucune sélection d’identité dans le workflow d’activation, car l’intégration est une recherche de profil. Le client ([!DNL Target], [!DNL Web SDK], ou d’autres) interroge la variable [[!UICONTROL Edge]](/help/collection/home.md#edge) et extrait les informations de profil dont il a besoin pour la personnalisation sur site.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment déterminer les identités prises en charge ou requises pour des destinations individuelles. Vous savez également comment fonctionne la sélection d’identité pour chaque type de destination.

Ensuite, vous pouvez savoir à propos de [paramètres d’exportation](/help/destinations/how-destinations-work/destinations-configurations.md) les destinations sont communes aux types de destination, qui peuvent être configurés par les développeurs au niveau d’une destination individuelle et quels paramètres peuvent être modifiés par les utilisateurs dans le processus d’activation.

Vous pouvez également extraire toutes les destinations disponibles dans le [catalogue](/help/destinations/catalog/overview.md).