---
keywords: correspondance client Google;correspondance client Google;correspondance client Google
title: Connexion à Google Customer Match
description: La correspondance client Google vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et interagir avec eux dans les propriétés détenues et exploitées de Google, telles que la recherche, le shopping, Gmail et YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 19%

---

# Connexion [!DNL Google Customer Match]

## Présentation {#overview}

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées de Google, telles que : [!DNL Search], [!DNL Shopping], [!DNL Gmail], et [!DNL YouTube].

![Destination de correspondance du client Google dans l’interface utilisateur de Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL Google Customer Match] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Une marque de vêtements d’athlétisme souhaite atteindre ses clients existants par l’intermédiaire de [!DNL Google Search] et [!DNL Google Shopping] pour personnaliser les offres et les articles en fonction de leurs achats précédents et de leur historique de navigation. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers l’Experience Platform et créer des audiences à partir de ses propres données hors ligne. Ensuite, ils peuvent envoyer ces audiences à [!DNL Google Customer Match] à utiliser dans [!DNL Search] et [!DNL Shopping], optimisant leurs dépenses publicitaires.

### Cas d’utilisation #2

Une importante entreprise technologique a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à faire connaitre les nouvelles fonctionnalités du téléphone aux clients qui possèdent des modèles précédents de leurs téléphones.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données CRM dans Experience Platform, en utilisant les adresses électroniques comme identifiants. Les audiences sont créées en fonction des clients qui possèdent des modèles de téléphone plus anciens. Ensuite, les audiences sont envoyées à [!DNL Google Customer Match], afin que l’entreprise puisse cibler les clients actuels, les clients qui possèdent des modèles de téléphone anciens et des clients similaires sur [!DNL YouTube].

## Gouvernance des données pour [!DNL Google Customer Match] destinations {#data-governance}

Certaines destinations en Experience Platform ont certaines règles et obligations pour les données envoyées ou reçues de la plateforme de destination. Il vous incombe de comprendre les limites et les obligations de vos données, ainsi que la manière dont vous utilisez ces données dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations en matière d’utilisation des données. [En savoir plus](../../../data-governance/labels/overview.md) à propos des outils et des politiques de gouvernance des données.

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Google Advertising ID | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| phone_sha256_e.164 | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| user_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit toutes les audiences que vous pouvez exporter vers cette destination.

Toutes les destinations prennent en charge l’activation des audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md).

En outre, cette destination prend également en charge l’activation des audiences décrites dans le tableau ci-dessous.

| Type d’audience | Description |
---------|----------|
| Chargements personnalisés | Audiences ingérées dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation de l’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone, etc.) utilisés dans la variable [!DNL Google Customer Match] destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu&#39;un profil est mis à jour en Experience Platform en fonction de l&#39;évaluation de l&#39;audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] conditions préalables du compte {#google-account-prerequisites}

Avant de configurer une [!DNL Google Customer Match] destination dans Experience Platform, veillez à lire et à respecter la politique de Google pour l’utilisation de [!DNL Customer Match], comme indiqué dans la section [Documentation de prise en charge de Google](https://support.google.com/google-ads/answer/6299717).

Ensuite, assurez-vous que la variable [!DNL Google] compte configuré pour un [!DNL Standard] ou niveau d’autorisation supérieur. Voir [Documentation sur Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) pour plus d’informations.

### Liste autorisée {#allowlist}

Avant de créer la variable [!DNL Google Customer Match] dans Experience Platform, assurez-vous que la variable [!DNL Google Ads] est conforme au [[!DNL Google Customer Match] policy](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Les clients disposant de comptes conformes sont automatiquement autorisés à être répertoriés par Google.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Google] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL Google Customer Match] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

### Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match]:

* **Ingestion de numéros de téléphone bruts**: vous pouvez ingérer des numéros de téléphone bruts dans la variable [!DNL E.164] format dans [!DNL Platform]et sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans la variable `Phone_E.164` espace de noms.
* **Ingestion de numéros de téléphone hachés**: vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans la variable `PHONE_SHA256_E.164` espace de noms.

>[!NOTE]
>
>Numéros de téléphone ingérés dans la variable `Phone` L’espace de noms ne peut pas être activé dans [!DNL Google Customer Match].

### Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et disposer des [!DNL Platform] hachez-les lors de l’activation.

Pour plus d’informations sur les exigences de hachage de Google et d’autres restrictions sur l’activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou identifiant utilisateur](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] avec numéro de téléphone](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] avec des identifiants d’appareil mobile](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, voir [Présentation de l’ingestion par lots](../../../ingestion/batch-ingestion/overview.md) et le [présentation de l’ingestion par flux](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

### Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant d’utiliser la variable `User_ID` espace de noms pour envoyer des données à Google, veillez à synchroniser vos propres identifiants à l’aide de [!DNL gTag]. Reportez-vous à la section [Documentation officielle de Google](https://support.google.com/google-ads/answer/9199250) pour plus d’informations.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: fournir un nom pour cette connexion de destination ;
* **[!UICONTROL Description]**: fournir une description pour cette connexion de destination ;
* **[!UICONTROL Identifiant de compte]**: your [Identifiant client Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). Le format de l’ID est xxx-xxx-xxxx. Si vous utilisez la variable [!DNL Google Ads Manager Account (My Client Center)], n’utilisez pas votre ID de compte de gestionnaire. Utilisez la variable [Identifiant client Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en) au lieu de .

>[!IMPORTANT]
>
> * Le **[!UICONTROL Combiner avec les PII]** l’action marketing est sélectionnée par défaut pour la variable [!DNL Google Customer Match] destination et ne peuvent pas être supprimés.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer les audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation d’audience par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

Dans le **[!UICONTROL Planification du segment]** , vous devez fournir la variable [!UICONTROL ID de l’application] lors de l’envoi [!DNL IDFA] ou [!DNL GAID] audiences vers [!DNL Google Customer Match].

![ID de l’application de correspondance client Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Pour plus d’informations sur la manière de trouver le [!DNL App ID], reportez-vous à la section [Documentation officielle de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Exemple de mappage : activation des données d’audience dans [!DNL Google Customer Match] {#example-gcm}

Il s’agit d’un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Google Customer Match].

Sélection des champs sources :

* Sélectionnez la `Email` espace de noms comme identité source si les adresses électroniques que vous utilisez ne sont pas hachées.
* Sélectionnez la `Email_LC_SHA256` espace de noms comme identité source si vous avez haché des adresses électroniques client lors de l’ingestion de données dans [!DNL Platform], en fonction de [!DNL Google Customer Match] [exigences de hachage des emails](#hashing-requirements).
* Sélectionnez la `PHONE_E.164` espace de noms en tant qu’identité source si vos données se composent de numéros de téléphone non hachés. [!DNL Platform] hachera les numéros de téléphone pour les [!DNL Google Customer Match] conditions requises.
* Sélectionnez la `Phone_SHA256_E.164` espace de noms comme identité source si vous avez haché des numéros de téléphone lors de l’ingestion des données dans [!DNL Platform], en fonction de [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez la `IDFA` espace de noms comme identité source si vos données sont composées [!DNL Apple] ID d’appareil.
* Sélectionnez la `GAID` espace de noms comme identité source si vos données sont composées [!DNL Android] ID d’appareil.
* Sélectionnez la `Custom` espace de noms comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez la `Email_LC_SHA256` espace de noms comme identité cible lorsque vos espaces de noms sources `Email` ou `Email_LC_SHA256`.
* Sélectionnez la `Phone_SHA256_E.164` espace de noms comme identité cible lorsque vos espaces de noms sources `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Sélectionnez la `IDFA` ou `GAID` les espaces de noms comme identité cible lorsque vos espaces de noms sources `IDFA` ou `GAID`.
* Sélectionnez la `User_ID` espace de noms comme identité cible lorsque votre espace de noms source est personnalisé.

![Mappage des identités](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.

Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation.

![Transformation du mapping des identités](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Vérification de la réussite de l’activation de l’audience {#verify-activation}

Une fois le flux d’activation terminé, passez à la **[!UICONTROL Publicités Google]** compte . Les audiences activées s’affichent dans votre compte Google sous forme de listes de clients. En fonction de la taille de votre audience, certaines audiences ne sont pas renseignées, sauf s’il y a plus de 100 principaux utilisateurs à diffuser.

Lors du mappage d’une audience à la fois [!DNL IDFA] et [!DNL GAID] les identifiants mobiles, [!DNL Google Customer Match] crée une audience distincte pour chaque mappage d’ID. Votre [!DNL Google Ads] Le compte affiche deux segments différents, l’un pour la variable [!DNL IDFA], et un pour le [!DNL GAID] mappage.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Bad Request {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes clients ne sont pas conformes aux [conditions préalables](#google-account-prerequisites). Pour résoudre ce problème, contactez Google et assurez-vous que votre compte est placé sur la liste autorisée et configuré pour une [!DNL Standard] ou niveau d’autorisation supérieur. Voir [Documentation sur Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) pour plus d’informations.

## Ressources supplémentaires {#additional-resources}

* [Intégrer [!DNL Google Customer Match] - Tutoriel vidéo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html?lang=fr)

