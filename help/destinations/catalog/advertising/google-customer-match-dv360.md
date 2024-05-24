---
title: Correspondance client Google + connexion Display & Video 360
description: Avec le connecteur de destination Correspondance client Google + Display & Video 360 , vous pouvez utiliser vos données en ligne et hors ligne d’Experience Platform pour atteindre et réengager vos clients dans les propriétés Google détenues et exploitées, telles que la recherche, le shopping, Gmail et YouTube.
badgeBeta: label="Version bêta" type="Informative"
source-git-commit: 7a9312a3722e205de3d11e17f6f079709b20237c
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 18%

---


# Connexion [!DNL Google Customer Match + Display & Video 360]

Utilisez cette destination pour activer vos PII propriétaires. [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) répertorie directement les [!DNL Google Display & Video 360] les propriétés telles que [!DNL Search], [!DNL YouTube], [!DNL Gmail], et la variable [!DNL Google Display Network].

Certains tiers intégrés à Google, tels qu’Adobe Real-Time CDP, peuvent utiliser la variable [!DNL Google Audience Partner API] pour créer [!DNL Customer Match] audiences directement dans les clients [!DNL Display & Video 360] compte .

Grâce à la nouvelle fonctionnalité d’ [!DNL Customer Matched] audiences à travers [!DNL Display & Video 360], vous pouvez désormais cibler des audiences sur un grand nombre de sources d’inventaire.

>[!IMPORTANT]
>
>Ce connecteur de destination est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès, contactez votre représentant Adobe.

![Destination Google Customer Match + DV360 dans l’interface utilisateur de Adobe Experience Platform.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Avis important concernant les modifications apportées aux destinations Google liées aux exigences de consentement mises à jour dans l’Union européenne

>[!IMPORTANT]
>
> Google publie des modifications apportées à la variable [API Google Ads](https://developers.google.com/google-ads/api/docs/start), [Correspondance client](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), et la variable [API Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies sous la rubrique [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) dans l’Union européenne ([Stratégie de consentement de l’utilisateur de l’UE](https://www.google.com/about/company/user-consent-policy/)). L’application de ces modifications aux exigences de consentement est en ligne depuis le 6 mars 2024.
><br/>
>Pour respecter la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audiences pour les utilisateurs de l’Espace économique européen (EEE), les publicitaires et les partenaires doivent s’assurer qu’ils transmettent le consentement de l’utilisateur final lors du transfert des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.
><br/>
>Clients ayant acheté Adobe Privacy &amp; Security Shield et ayant configuré une [stratégie de consentement](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non autorisés, il n’est pas nécessaire d’effectuer une action.
><br/>
>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser la variable [définition de segment](../../../segmentation/home.md#segment-definitions) fonctionnalités dans [Créateur de segments](../../../segmentation/ui/segment-builder.md) pour filtrer les profils non autorisés afin de continuer à utiliser sans interruption les destinations Google Real-Time CDP existantes.

## Quand utiliser cette destination ?

Plusieurs intégrations avec Google sont disponibles dans le catalogue des destinations et il peut être difficile de comprendre quand utiliser chacune des destinations Google disponibles. Tenez compte des différents cas pratiques en lisant les informations dans le tableau ci-dessous :

| [Correspondance client Google](/help/destinations/catalog/advertising/google-customer-match.md) | [Google Display &amp; Video 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (ce connecteur) |
|---------|----------|---------|
| Exportez vos audiences basées sur les informations d’identification personnelles et accédez-les selon l’inventaire disponible dans [!DNL Google Customer Match]. | Atteindre les audiences basées sur des cookies dans l’inventaire disponible via [!DNL Google Display & Video 360], sur les propriétés détenues et exploitées par Google telles que YouTube et [!DNL Search], et au-delà. | Création d’audiences basées sur les PII dans [!DNL Google Customer Match] et les atteindre dans l’inventaire disponible dans [!DNL Google Display & Video 360], sur les propriétés détenues et exploitées par Google uniquement. |

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser cette destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Une marque de vêtements d’athlétisme souhaite atteindre ses clients existants par l’intermédiaire de [!DNL Google Search] et [!DNL Google Shopping] pour personnaliser les offres et les articles en fonction de leurs achats précédents et de leur historique de navigation. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers l’Experience Platform et créer des audiences à partir de ses propres données hors ligne. Ensuite, ils peuvent envoyer ces audiences à l’événement [!DNL Google Customer Match + Display & Video 360] destination à utiliser dans [!DNL Google Display & Video 360] les propriétés telles que [!DNL Search], [!DNL YouTube], [!DNL Gmail], et la variable [!DNL Google Display Network].

### Cas d’utilisation #2

Une importante société technologique a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à faire connaitre les nouvelles fonctionnalités du téléphone aux clients qui possèdent des modèles précédents de leurs téléphones.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données CRM dans Experience Platform, en utilisant les adresses électroniques comme identifiants. Les audiences sont créées en fonction des clients qui possèdent des modèles de téléphone plus anciens. Ensuite, les audiences sont envoyées à [!DNL Google Customer Match], afin que l’entreprise puisse cibler les clients actuels, les clients qui possèdent des modèles de téléphone anciens et des clients similaires sur [!DNL Google Display & Video 360] les propriétés telles que [!DNL Search], [!DNL YouTube], [!DNL Gmail], et la variable [!DNL Google Display Network].

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| phone_sha256_e.164 | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

<!-- not supported in beta

|GAID|Google Advertising ID|Select this target identity when your source identity is a GAID namespace.|
|IDFA|Apple ID for Advertisers|Select this target identity when your source identity is an IDFA namespace.|
|user_id|Custom user IDs|Select this target identity when your source identity is a custom namespace.| 

-->

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone, etc.) utilisés dans la variable [!DNL Google Customer Match] destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] conditions préalables du compte {#google-account-prerequisites}

Avant de configurer une [!DNL Google Customer Match] destination dans Experience Platform, veillez à lire et à respecter la politique de Google pour l’utilisation de [!DNL Customer Match], comme indiqué dans la section [Documentation de prise en charge de Google](https://support.google.com/google-ads/answer/6299717).

Ensuite, assurez-vous que la variable [!DNL Google] est configuré pour un compte [!DNL Standard] ou niveau d’autorisation supérieur. Voir [Documentation sur Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) pour plus d’informations.

### Liste autorisée {#allowlist}

Avant de créer la variable [!DNL Google Customer Match] dans Experience Platform, assurez-vous que la variable [!DNL Google Ads] est conforme au [[!DNL Google Customer Match] policy](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Les clients disposant de comptes conformes sont automatiquement placés sur la liste autorisée par Google.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Google] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL Google Customer Match] doit être désactivé *haché* identifiants, tels que des adresses électroniques hachées ou des numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

### Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match]:

* **Ingestion de numéros de téléphone bruts**: vous pouvez ingérer des numéros de téléphone bruts dans la variable [!DNL E.164] format dans [!DNL Platform]et sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans la variable `Phone_E.164` espace de noms.
* **Ingestion de numéros de téléphone hachés**: vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans la variable `PHONE_SHA256_E.164` espace de noms.

>[!NOTE]
>
>Numéros de téléphone ingérés dans la variable `Phone` L’espace de noms ne peut pas être activé dans la variable [!DNL Google Customer Match + DV360] destination.

### Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et disposer des [!DNL Platform] hachez-les lors de l’activation.

Pour plus d’informations sur les exigences de hachage de Google et d’autres restrictions sur l’activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou identifiant utilisateur](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] avec le numéro de téléphone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] avec des identifiants d’appareil mobile](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, voir [Présentation de l’ingestion par lots](../../../ingestion/batch-ingestion/overview.md) et la variable [présentation de l’ingestion par flux](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: indiquez un nom pour cette connexion de destination.
* **[!UICONTROL Description]**: fournissez une description pour cette connexion de destination.
* **[!UICONTROL Identifiant de compte]**: votre [Identifiant client Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). Le format de l’ID est xxx-xxx-xxxx. Si vous utilisez la variable [!DNL Google Ads Manager Account (My Client Center)], n’utilisez pas votre ID de compte de gestionnaire. Utilisez la variable [Identifiant client Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en) au lieu de .
* **[!UICONTROL Type de compte]**: type de compte Google. Sélectionnez une option en fonction du type de compte publicitaire avec Google :
   * **[!UICONTROL Afficher le partenaire vidéo]**
   * **[!UICONTROL Afficher le publicitaire vidéo]**

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités* vers les destinations, vous avez besoin de la variable **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Exemple de mappage : activation des données d’audience dans [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Il s’agit d’un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Google Customer Match + Display & Video 360].

Sélection des champs sources :

* Sélectionnez la variable `Email` espace de noms comme identité source si les adresses électroniques que vous utilisez ne sont pas hachées.
* Sélectionnez la variable `Email_LC_SHA256` espace de noms comme identité source si vous avez haché des adresses électroniques client lors de l’ingestion de données dans [!DNL Platform], selon [!DNL Google Customer Match] [exigences de hachage des emails](#hashing-requirements).
* Sélectionnez la variable `PHONE_E.164` espace de noms en tant qu’identité source si vos données se composent de numéros de téléphone non hachés. [!DNL Platform] hachera les numéros de téléphone pour qu’ils soient conformes. [!DNL Google Customer Match] conditions requises.
* Sélectionnez la variable `Phone_SHA256_E.164` espace de noms comme identité source si vous avez haché des numéros de téléphone lors de l’ingestion des données dans [!DNL Platform], selon [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).

Sélection des champs cibles :

* Sélectionnez la variable `Email_LC_SHA256` l’espace de noms comme identité cible lorsque vos espaces de noms sources `Email` ou `Email_LC_SHA256`.
* Sélectionnez la variable `Phone_SHA256_E.164` l’espace de noms comme identité cible lorsque vos espaces de noms sources `PHONE_E.164` ou `Phone_SHA256_E.164`.

![Mappage des identités entre les champs source et cible affiché à l’étape Mappage du workflow d’activation.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.

Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance à l&#39;étape Mappage du workflow d&#39;activation.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Vérification de la réussite de l’activation de l’audience {#verify-activation}

Une fois le flux d’activation terminé, passez à la **[!UICONTROL Publicités Google]** compte . Les audiences activées s’affichent dans votre compte Google sous forme de listes de clients. Selon la taille de l’audience, certaines audiences ne sont pas renseignées, à moins qu’il y ait plus de 1 000 utilisateurs actifs à diffuser. Pour plus d’informations, voir [Documentation du partenaire d’audience Google](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Notez que vous devez demander à Google l’accès à la documentation dans le lien.

## Gouvernance des données

Certaines destinations en Experience Platform ont certaines règles et obligations pour les données envoyées ou reçues de la plateforme de destination. Il vous incombe de comprendre les limites et les obligations de vos données, ainsi que la manière dont vous utilisez ces données dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations en matière d’utilisation des données. [En savoir plus](../../../data-governance/labels/overview.md) à propos des outils et des politiques de gouvernance des données.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes clients ne sont pas conformes aux [conditions préalables](#google-account-prerequisites). Pour résoudre ce problème, contactez Google et assurez-vous que votre compte est sur liste autorisée et est configuré pour une [!DNL Standard] ou niveau d’autorisation supérieur. Voir [Documentation sur Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) pour plus d’informations.