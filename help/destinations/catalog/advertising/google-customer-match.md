---
keywords: correspondance client google;correspondance client Google;correspondance client Google
title: Connexion à Google Customer Match
description: Le ciblage par correspondance des clients de Google vous permet d’utiliser vos données en ligne et hors ligne pour contacter et réengager vos clients dans les propriétés détenues et exploitées par Google, telles que Search, Shopping et Gmail.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 4541e812ac1f44b5374b81685c1e41cb7f00993f
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 22%

---

# Connexion [!DNL Google Customer Match]

>[!IMPORTANT]
>
> Google publie des modifications de l’API [Google Ads](https://developers.google.com/google-ads/api/docs/start), de l’API [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) et de l’API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies dans le [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) de l’Union européenne ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’application de ces modifications aux exigences en matière de consentement est effective à compter du 6 mars 2024.
> &#x200B;><br/>
> &#x200B;>Pour se conformer à la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audience pour les utilisateurs dans l’Espace économique européen (EEE), les annonceurs et les partenaires doivent s’assurer de transmettre le consentement de l’utilisateur final lors du téléchargement des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.
> &#x200B;><br/>
> &#x200B;>Les clients qui ont acheté Adobe Privacy &amp; Security Shield et configuré une [politique de consentement](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non consentis n’ont aucune action à effectuer.
> &#x200B;><br/>
> &#x200B;>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser les fonctionnalités [définition de segment](../../../segmentation/home.md#segment-definitions) du [créateur de segments](../../../segmentation/ui/segment-builder.md) pour filtrer les profils non consentis afin de continuer à utiliser les destinations Real-Time CDP Google existantes sans interruption.

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) vous permet d’utiliser vos données en ligne et hors ligne pour contacter et réengager vos clients dans les propriétés détenues et exploitées par Google, telles que : [!DNL Search], [!DNL Shopping] et [!DNL Gmail].

>[!TIP]
>
>Pour atteindre les clients figurant dans [!DNL YouTube] inventaire, utilisez la destination [Correspondance client Google + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) , qui utilise l’API Google Audience Partner.

Destination ![Google Customer Match dans l’interface utilisateur de Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Google Customer Match], consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1

Une marque de vêtements de sport souhaite atteindre les clients existants par le biais de [!DNL Google Search] et de [!DNL Google Shopping] afin de personnaliser les offres et les articles en fonction de leurs achats précédents et de leur historique de navigation. La marque de vêtements peut ingérer des adresses e-mail de son propre CRM vers Experience Platform et créer des audiences à partir de ses propres données hors ligne. Ensuite, elles peuvent envoyer ces audiences à [!DNL Google Customer Match] pour qu’elles soient utilisées dans les [!DNL Search] et les [!DNL Shopping], optimisant ainsi leurs dépenses publicitaires.

### Cas d’utilisation #2

>[!TIP]
>
>Pour exécuter ce cas d’utilisation sur [!DNL YouTube] inventaire, utilisez la nouvelle destination [Correspondance client Google + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), qui utilise l’API Google Audience Partner.

Une importante société de technologie a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à faire connaître les nouvelles fonctionnalités du téléphone aux clients qui possèdent des modèles précédents de leurs téléphones.

Pour promouvoir la version, ils chargent les adresses e-mail de leur base de données CRM dans Experience Platform, en utilisant les adresses e-mail comme identifiants. Les audiences sont créées en fonction des clients qui possèdent d’anciens modèles de téléphone. Ensuite, les audiences sont envoyées à [!DNL Google Customer Match], afin que l’entreprise puisse cibler les clients actuels, les clients qui possèdent des modèles de téléphone plus anciens et des clients similaires sur [!DNL YouTube].

## Gouvernance des données pour les destinations [!DNL Google Customer Match] {#data-governance}

Certaines destinations dans Experience Platform ont certaines règles et obligations pour les données envoyées à, ou reçues de la plateforme de destination. La compréhension des limites et des obligations engendrées par vos données, ainsi que l’usage que vous faites de ces données dans Adobe Experience Platform et sur la plateforme de destination relèvent de votre responsabilité. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations d’utilisation des données. [En savoir plus](../../../data-governance/labels/overview.md) sur les outils et les politiques de gouvernance des données.

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| `IDFA` | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| `phone_sha256_e.164` | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `email_lc_sha256` | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour les adresses électroniques en texte brut et hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `user_id` | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |
| `address_info_first_name` | Prénom de l’utilisateur | Cette identité cible est destinée à être utilisée avec `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`, lorsque vous souhaitez envoyer des données d’adresse postale à votre destination. <br><br>Pour que Google assure la correspondance de l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’il n’existe pas de données de champs manquantes dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google n’assure pas la correspondance de l’adresse. |
| `address_info_last_name` | Nom de famille de l&#39;utilisateur | Cette identité cible est destinée à être utilisée avec `address_info_first_name`, `address_info_country_code` et `address_info_postal_code`, lorsque vous souhaitez envoyer des données d’adresse postale à votre destination. <br><br>Pour que Google assure la correspondance de l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’il n’existe pas de données de champs manquantes dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google n’assure pas la correspondance de l’adresse. |
| `address_info_country_code` | Code pays de l’adresse de l’utilisateur | Cette identité cible est destinée à être utilisée avec `address_info_first_name`, `address_info_last_name` et `address_info_postal_code`, lorsque vous souhaitez envoyer des données d’adresse postale à votre destination. <br><br>Pour que Google assure la correspondance de l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’il n’existe pas de données de champs manquantes dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google ne correspond pas à l’adresse. <br><br>Format accepté : codes pays à 2 lettres, en minuscules, au format [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| `address_info_postal_code` | Code postal de l’adresse de l’utilisateur | Cette identité cible est destinée à être utilisée avec `address_info_first_name`, `address_info_last_name` et `address_info_country_code`, lorsque vous souhaitez envoyer des données d’adresse postale à votre destination. <br><br>Pour que Google assure la correspondance de l’adresse, vous devez mapper les quatre champs d’adresse (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`) et vous assurer qu’il n’existe pas de données de champs manquantes dans les profils exportés. <br> Si un champ n’est pas mappé ou contient des données manquantes, Google n’assure pas la correspondance de l’adresse. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la destination [!DNL Google Customer Match]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables relatives au compte [!DNL Google Customer Match] {#google-account-prerequisites}

Avant de configurer une destination [!DNL Google Customer Match] dans Experience Platform, assurez-vous de lire et de respecter la politique de Google relative à l’utilisation de [!DNL Customer Match], décrite dans la [documentation d’assistance Google](https://support.google.com/google-ads/answer/6299717).

Ensuite, assurez-vous que votre compte [!DNL Google] est configuré pour un niveau d’autorisation [!DNL Standard] ou supérieur. Pour plus d’informations[ consultez la documentation sur les Google Ads ](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1).

### Liste autorisée {#allowlist}

Avant de créer la destination [!DNL Google Customer Match] dans Experience Platform, assurez-vous que votre compte [!DNL Google Ads] est conforme à la [[!DNL Google Customer Match]  politique ](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Les clients disposant de comptes conformes sont automatiquement placés sur la liste autorisée par Google.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Google] nécessite qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Google Customer Match] peuvent être masquées à partir d’identifiants *hachés* tels que des adresses e-mail ou des numéros de téléphone.

Selon le type d’identifiants ingérés dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

### Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match] :

* **Ingestion de numéros de téléphone bruts** : vous pouvez ingérer des numéros de téléphone bruts au format [!DNL E.164] dans [!DNL Experience Platform], et ils sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans l’espace de noms `Phone_E.164`.
* **Ingestion de numéros de téléphone hachés** : vous pouvez préhacher vos numéros de téléphone avant l’ingestion dans [!DNL Experience Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans l’espace de noms `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Les numéros de téléphone ingérés dans l’espace de noms `Phone` ne peuvent pas être activés dans [!DNL Google Customer Match].

### Exigences en matière de hachage des e-mails {#hashing-requirements}

Vous pouvez hacher les adresses e-mail avant de les ingérer dans Adobe Experience Platform ou les utiliser en clair dans Experience Platform et demander à [!DNL Experience Platform] de les hacher lors de l’activation.

Pour plus d’informations sur les exigences de hachage de Google et d’autres restrictions sur l’activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse e-mail, adresse ou ID utilisateur](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] avec numéro de téléphone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] avec ID d’appareil mobile](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’ingestion d’adresses e-mail dans Experience Platform, consultez la [présentation de l’ingestion par lots](../../../ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher les adresses e-mail vous-même, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

### Exigences en matière de hachage des champs d’adresse {#address-field-hashing}

Lors du mappage des champs liés aux adresses à des [!DNL Google Customer Match], Experience Platform **hache automatiquement** les valeurs `address_info_first_name` et `address_info_last_name` avant de les envoyer à Google. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Google.

Ne fournissez **pas** de valeurs préhachées pour `address_info_first_name` ou `address_info_last_name`. Si vous fournissez des valeurs déjà hachées, le processus de correspondance échoue.

### Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l’espace de noms `User_ID` pour envoyer des données à Google, veillez à synchroniser vos propres identifiants à l’aide de [!DNL gTag]. Consultez la documentation officielle de [Google](https://support.google.com/google-ads/answer/9199250) pour plus d&#39;informations.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Vue d’ensemble des vidéos {#video-overview}

Regardez la vidéo ci-dessous pour une explication des avantages et de la manière d’activer les données dans le ciblage par correspondance client Google.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : attribuez un nom à cette connexion de destination
* **[!UICONTROL Description]** : fournissez une description de cette connexion de destination
* **[!UICONTROL ID de compte]** : votre [ID de client Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). Le format de l’ID est xxx-xxx-xxxx. Si vous utilisez le [!DNL Google Ads Manager Account (My Client Center)], n’utilisez pas l’ID de compte Manager. Utilisez plutôt l’ID de client [Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en).

>[!NOTE]
>
>Pendant le processus de connexion OAuth2, il se peut que « Test Marketo » s’affiche comme nom du projet OAuth Google. Il s’agit d’un comportement normal, car Adobe utilise ce nom de projet pour l’intégration de la correspondance client Google. Cela n’affecte pas la configuration de la destination.

>[!IMPORTANT]
>
> * L’action marketing **[!UICONTROL Combiner avec des PII]** est sélectionnée par défaut pour la destination [!DNL Google Customer Match] et ne peut pas être supprimée.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités* vers les destinations, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans l’étape **[!UICONTROL Planning des segments]**, vous devez fournir l’identifiant [!UICONTROL App] lors de l’envoi d’audiences [!DNL IDFA] ou [!DNL GAID] à des [!DNL Google Customer Match].

![Le champ ID de l’application de correspondance client Google est mis en surbrillance à l’étape Planification des segments du workflow d’activation.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Pour plus d’informations sur la recherche du [!DNL App ID], consultez la documentation officielle de [Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) ou demandez à votre représentant Google.

### Exemple de mappage : activation des données d’audience dans [!DNL Google Customer Match] {#example-gcm}

Il s’agit d’un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Google Customer Match].

Sélection des champs sources :

* Sélectionnez l’espace de noms `Email` comme identité source si les adresses e-mail que vous utilisez ne sont pas hachées.
* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité source si vous avez haché les adresses e-mail des clients lors de l’ingestion des données dans [!DNL Experience Platform], conformément [!DNL Google Customer Match] [exigences de hachage des e-mails](#hashing-requirements).
* Sélectionnez l’espace de noms `PHONE_E.164` comme identité source si vos données sont composées de numéros de téléphone non hachés. [!DNL Experience Platform] hachera les numéros de téléphone pour se conformer aux exigences [!DNL Google Customer Match].
* Sélectionnez l’espace de noms `Phone_SHA256_E.164` comme identité source si vous hachez des numéros de téléphone lors de l’ingestion de données dans [!DNL Experience Platform], conformément [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez l’espace de noms `IDFA` comme identité source si vos données sont composées d’identifiants d’appareil [!DNL Apple].
* Sélectionnez l’espace de noms `GAID` comme identité source si vos données sont composées d’identifiants d’appareil [!DNL Android].
* Sélectionnez l’espace de noms `Custom` comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité cible lorsque vos espaces de noms sources sont `Email` ou `Email_LC_SHA256`.
* Sélectionnez l’espace de noms `Phone_SHA256_E.164` comme identité cible lorsque vos espaces de noms sources sont `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Sélectionnez les espaces de noms `IDFA` ou `GAID` comme identité cible lorsque vos espaces de noms sources sont `IDFA` ou `GAID`.
* Sélectionnez l’espace de noms `User_ID` comme identité cible lorsque l’espace de noms source est personnalisé.

![Mappage d’identité entre les champs source et cible affiché à l’étape Mappage du workflow d’activation.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Experience Platform] lors de l’activation.

Les données source des attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance dans l’étape Mappage du workflow d’activation.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Surveiller la destination {#monitor-destination}

Après vous être connecté à la destination et avoir établi un flux de données de destination, vous pouvez utiliser la [fonctionnalité de surveillance](/help/dataflows/ui/monitor-destinations.md) de Real-Time CDP pour obtenir des informations détaillées sur les enregistrements de profil activés vers la destination dans chaque exécution du flux de données.

>[!IMPORTANT]
>
>Lorsque vous mappez les quatre identités cibles liées aux adresses (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` et `address_info_postal_code`), elles sont comptabilisées comme des identités individuelles distinctes pour chaque profil dans la page de surveillance des flux de données.

## Vérifiez que l’activation de l’audience a réussi. {#verify-activation}

Une fois le flux d’activation terminé, basculez vers votre compte **[!UICONTROL Google Ads]**. Les audiences activées s’affichent dans votre compte Google sous forme de listes de clients. Selon la taille de votre audience, certaines audiences ne sont pas renseignées, sauf s’il y a plus de 100 utilisateurs actifs à servir.

Lors du mappage d’une audience à des ID mobiles [!DNL IDFA] et [!DNL GAID], [!DNL Google Customer Match] crée une audience distincte pour chaque mappage d’ID. Votre compte [!DNL Google Ads] affiche deux segments différents, l’un pour le [!DNL IDFA] et l’autre pour le mappage [!DNL GAID].

## Dépannage {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes client ne respectent pas les [ conditions préalables ](#google-account-prerequisites). Pour résoudre ce problème, contactez Google et assurez-vous que votre compte est sur liste autorisée et configuré pour un niveau d’autorisation [!DNL Standard] ou supérieur. Pour plus d’informations[ consultez la documentation sur les Google Ads ](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1).