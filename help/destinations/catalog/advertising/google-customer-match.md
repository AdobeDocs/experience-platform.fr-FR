---
keywords: correspondance client Google;correspondance client Google;correspondance client Google
title: Connexion à la correspondance client Google
description: Google Customer Match vous permet d’utiliser vos données en ligne et hors ligne pour atteindre vos clients et les réengager dans les propriétés détenues et exploitées par Google, telles que Search, Shopping, Gmail et YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 1%

---

# [!DNL Google Customer Match] connection

## Présentation {#overview}

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets vous permet d’utiliser vos données en ligne et hors ligne pour atteindre et réengager vos clients dans les propriétés détenues et exploitées de Google, comme :  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail] et  [!DNL YouTube].

![Destination de correspondance client Google dans l’interface utilisateur de Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Cas d&#39;utilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Google Customer Match], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Une marque de vêtements de sport souhaite atteindre ses clients existants par [!DNL Google Search] et [!DNL Google Shopping] afin de personnaliser les offres et les articles en fonction de leurs achats passés et de leur historique de navigation. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers l’Experience Platform et créer des segments à partir de ses propres données hors ligne. Ensuite, ils peuvent envoyer ces segments à [!DNL Google Customer Match] afin qu’ils soient utilisés dans [!DNL Search] et [!DNL Shopping], optimisant ainsi leurs dépenses publicitaires.

### Cas d’utilisation #2

Une importante entreprise technologique a lancé un nouveau téléphone. Pour promouvoir ce nouveau modèle de téléphone, ils cherchent à faire connaitre les nouvelles fonctionnalités du téléphone aux clients qui possèdent des modèles précédents de leurs téléphones.

Pour promouvoir cette version, ils téléchargent les adresses électroniques de leur base de données CRM dans Experience Platform, en utilisant les adresses électroniques comme identifiants. Les segments sont créés en fonction des clients qui possèdent des modèles de téléphone plus anciens. Ensuite, les segments sont envoyés à [!DNL Google Customer Match] afin que l’entreprise puisse cibler les clients actuels, les clients qui possèdent des modèles de téléphone anciens et des clients similaires sur [!DNL YouTube].

## Gouvernance des données pour les destinations [!DNL Google Customer Match] {#data-governance}

Certaines destinations en Experience Platform ont certaines règles et obligations pour les données envoyées ou reçues de la plateforme de destination. Il vous incombe de comprendre les limites et les obligations de vos données, ainsi que la manière dont vous utilisez ces données dans Adobe Experience Platform et la plateforme de destination. Adobe Experience Platform fournit des outils de gouvernance des données pour vous aider à gérer certaines de ces obligations en matière d’utilisation des données. [En savoir ](../../../data-governance/labels/overview.md) plus sur les outils et les politiques de gouvernance des données.

## Identités prises en charge {#supported-identities}

[!DNL Google Customer Match] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| phone_sha256_e.164 | Numéros de téléphone au format E164, hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| user_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la  [!DNL Google Customer Match] destination.

## [!DNL Google Customer Match] conditions préalables du compte {#google-account-prerequisites}

Avant de configurer une destination [!DNL Google Customer Match] en Experience Platform, veillez à lire et à respecter la politique d’utilisation de [!DNL Customer Match] de Google, décrite dans la [documentation du support Google](https://support.google.com/google-ads/answer/6299717).

Ensuite, assurez-vous que votre compte [!DNL Google] est configuré pour un niveau d’autorisation [!DNL Standard] ou supérieur. Pour plus d’informations, voir la [documentation Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .

### Liste autorisée {#allowlist}

Avant de créer la destination [!DNL Google Customer Match] en Experience Platform, assurez-vous que votre compte [!DNL Google Ads] est conforme à la [politique de correspondance client de Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Les clients disposant de comptes conformes sont automatiquement autorisés par Google.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Google] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences activées vers [!DNL Google Customer Match] peuvent être masquées à partir des identifiants *hachés*, tels que les adresses électroniques ou les numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Google Customer Match] :

* **Ingestion de numéros** de téléphone bruts : vous pouvez ingérer des numéros de téléphone bruts au  [!DNL E.164] format  [!DNL Platform], qui sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans l’espace de noms `Phone_E.164`.
* **Ingestion de numéros** de téléphone hachés : vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans  [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans l’espace de noms `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Les numéros de téléphone ingérés dans l’espace de noms `Phone` ne peuvent pas être activés dans [!DNL Google Customer Match].

## Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et les [!DNL Platform] hacher lors de l’activation.

Pour plus d’informations sur les exigences de hachage de Google et d’autres restrictions sur l’activation, consultez les sections suivantes de la documentation de Google :

* [[!DNL Customer Match] avec adresse électronique, adresse ou identifiant utilisateur](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considérations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Correspondance client avec numéro de téléphone](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Correspondance client avec les identifiants d’appareil mobile](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, consultez la [présentation de l’ingestion par lots](../../../ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](../../../ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences de Google, décrites dans les liens ci-dessus.

## Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l’espace de noms `User_ID` pour envoyer des données à Google, veillez à synchroniser vos propres identifiants à l’aide de [!DNL gTag]. Consultez la [documentation officielle de Google](https://support.google.com/google-ads/answer/9199250) pour plus d’informations.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : fournir un nom pour cette connexion de destination ;
* **[!UICONTROL Description]** : fournir une description pour cette connexion de destination ;
* **[!UICONTROL ID]** du compte : votre ID client Google. Le format de l’ID est xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * L’action marketing **[!UICONTROL Combiner avec les PII]** est sélectionnée par défaut pour la destination [!DNL Google Customer Match] et ne peut pas être supprimée.


## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

À l’étape **[!UICONTROL Planification du segment]** , vous devez fournir l’ [!UICONTROL ID d’application] lors de l’envoi de segments [!DNL IDFA] ou [!DNL GAID] à [!DNL Google Customer Match].

![ID de l’application de correspondance client Google](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Pour plus d&#39;informations sur la façon de trouver la [!DNL App ID], consultez la [documentation officielle de Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Exemple de mappage : activation des données d’audience dans [!DNL Google Customer Match] {#example-gcm}

Il s’agit d’un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Google Customer Match].

Sélection des champs sources :

* Sélectionnez l’espace de noms `Email` comme identité source si les adresses électroniques que vous utilisez ne sont pas hachées.
* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité source si vous avez haché les adresses électroniques du client lors de l’ingestion des données dans [!DNL Platform], conformément aux [!DNL Google Customer Match] [exigences de hachage des emails](#hashing-requirements).
* Sélectionnez l’espace de noms `PHONE_E.164` comme identité source si vos données se composent de numéros de téléphone non hachés. [!DNL Platform] hachera les numéros de téléphone pour se conformer aux  [!DNL Google Customer Match] exigences.
* Sélectionnez l’espace de noms `Phone_SHA256_E.164` comme identité source si vous avez haché des numéros de téléphone lors de l’ingestion de données dans [!DNL Platform], conformément aux [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez l’espace de noms `IDFA` comme identité source si vos données se composent d’identifiants d’appareil [!DNL Apple].
* Sélectionnez l’espace de noms `GAID` comme identité source si vos données se composent d’identifiants d’appareil [!DNL Android].
* Sélectionnez l’espace de noms `Custom` comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité cible lorsque vos espaces de noms source sont `Email` ou `Email_LC_SHA256`.
* Sélectionnez l’espace de noms `Phone_SHA256_E.164` comme identité cible lorsque vos espaces de noms source sont `PHONE_E.164` ou `Phone_SHA256_E.164`.
* Sélectionnez les espaces de noms `IDFA` ou `GAID` comme identité cible lorsque vos espaces de noms source sont `IDFA` ou `GAID`.
* Sélectionnez l’espace de noms `User_ID` comme identité cible lorsque l’espace de noms source est personnalisé.

![Mappage des identités](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.

Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation.

![Transformation du mapping des identités](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Vérification de la réussite de l’activation du segment {#verify-activation}

Une fois le flux d’activation terminé, basculez vers votre compte **[!UICONTROL Google Ads]**. Les segments activés s’affichent dans votre compte Google sous forme de listes de clients. En fonction de la taille du segment, certaines audiences ne sont pas renseignées, sauf s’il y a plus de 100 principaux utilisateurs à diffuser.

Lors du mappage d’un segment sur les [!DNL IDFA] et [!DNL GAID] identifiants mobiles, [!DNL Google Customer Match] crée un segment distinct pour chaque mappage d’identifiant. Votre compte [!DNL Google Ads] affiche deux segments différents, l’un pour [!DNL IDFA] et l’autre pour le mappage [!DNL GAID].

## Dépannage {#troubleshooting}

### Message d’erreur 400 Bad Request {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes clients ne respectent pas les [conditions préalables](#google-account-prerequisites). Pour résoudre ce problème, contactez Google et assurez-vous que votre compte est placé sur la liste autorisée et configuré pour un niveau d’autorisation [!DNL Standard] ou supérieur. Pour plus d’informations, voir la [documentation Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .

## Ressources supplémentaires {#additional-resources}

* [Intégration de la correspondance client Google - Tutoriel vidéo](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

