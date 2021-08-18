---
keywords: Connexion facebook;connexion facebook;destinations facebook;facebook;instagram;messenger;facebook messenger
title: Connexion facebook
description: Activez les profils de vos campagnes Facebook pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 183aff5a3b6bcc1635ae7b4b0e503a9d4b6d4d31
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 6%

---

# [!DNL Facebook] connection

## Présentation {#overview}

Activez les profils de vos campagnes [!DNL Facebook] pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.

Vous pouvez utiliser cette destination pour le ciblage des audiences dans la famille [!DNL Facebook’s] d’applications prises en charge par [!DNL Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l’application sur laquelle vous souhaitez exécuter la campagne est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

![Destination facebook dans l’interface utilisateur de Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Cas d&#39;utilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Facebook], voici deux exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Un détaillant en ligne souhaite atteindre des clients existants par le biais de plateformes sociales et leur présenter des offres personnalisées basées sur leurs commandes précédentes. Le détaillant en ligne peut ingérer des adresses électroniques de son propre CRM vers Adobe Experience Platform, créer des segments à partir de ses propres données hors ligne et envoyer ces segments vers la plateforme sociale [!DNL Facebook], afin d’optimiser ses dépenses publicitaires.

### Cas d’utilisation #2

Une compagnie aérienne possède différents niveaux de clients (Bronze, Argent et Or) et souhaite fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n’utilisent pas l’application mobile de la compagnie aérienne et certains d’entre eux ne se sont pas connectés au site web de la société. Les seuls identifiants de membre et d’adresse électronique de l’entreprise concernant ces clients sont les identifiants de membre et les adresses électroniques.

Pour les cibler sur les réseaux sociaux, ils peuvent intégrer les données client de leur CRM dans Adobe Experience Platform, en utilisant les adresses email comme identifiants.

Ensuite, ils peuvent utiliser leurs données hors ligne, y compris les identifiants d’adhésion et les niveaux de client associés, pour créer de nouveaux segments d’audience qu’ils peuvent cibler via la destination [!DNL Facebook].

## Identités prises en charge {#supported-identities}

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance des ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Facebook.

## Conditions préalables au compte facebook {#facebook-account-prerequisites}

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* L’autorisation [!DNL Facebook] doit être activée pour votre compte utilisateur **[!DNL Manage campaigns]** pour le compte publicitaire que vous prévoyez d’utiliser.
* Le compte commercial **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Pour plus d’informations, voir [Ajout de partenaires à votre compte Business Manager](https://www.facebook.com/business/help/1717412048538897) dans la documentation Facebook.
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. L’autorisation est requise pour l’intégration [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` correspond à votre [!DNL Facebook Ad Account ID].

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Facebook] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences activées vers [!DNL Facebook] peuvent être masquées à partir des identifiants *hachés*, tels que les adresses électroniques ou les numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Facebook] :

* **Ingestion de numéros** de téléphone bruts : vous pouvez ingérer des numéros de téléphone bruts au  [!DNL E.164] format  [!DNL Platform]. Ils se sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans l’espace de noms `Phone_E.164`.
* **Ingestion de numéros** de téléphone hachés : vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans  [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans l’espace de noms `Phone_SHA256`.

>[!NOTE]
>
>Les numéros de téléphone ingérés dans l’espace de noms `Phone` ne peuvent pas être activés dans [!DNL Facebook].


## Exigences en matière de hachage des emails {#email-hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et les [!DNL Platform] hacher lors de l’activation.

Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Rogner tous les espaces de début et de fin de la chaîne de courrier électronique ; exemple : `johndoe@example.com` et non `<space>johndoe@example.com<space>`;
* Lors du hachage des chaînes d’email, veillez à mettre la chaîne en minuscules par hachage.
   * Exemple : `example@email.com` et non `EXAMPLE@EMAIL.COM`;
* Assurez-vous que la chaîne hachée est entièrement en minuscules.
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149` et non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.
> Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation.
> L’option **[!UICONTROL Appliquer la transformation]** ne s’affiche que lorsque vous sélectionnez des attributs comme champs source. Il ne s’affiche pas lorsque vous choisissez des espaces de noms.

![Transformation du mapping des identités](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l’espace de noms `Extern_ID` pour envoyer des données à [!DNL Facebook], veillez à synchroniser vos propres identifiants à l’aide de [!DNL Facebook Pixel]. Consultez la [documentation officielle de Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) pour plus d’informations.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

La vidéo ci-dessous présente également les étapes de configuration d’une destination [!DNL Facebook] et d’activation de segments.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interface utilisateur de l’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous au [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** du compte : votre  [!DNL Facebook Ad Account ID]. Vous pouvez trouver cet ID dans votre compte [!DNL Facebook Ads Manager]. Lors de la saisie de cet ID, ajoutez toujours un préfixe `act_`.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

À l’étape **[!UICONTROL Planification du segment]** , vous devez indiquer [!UICONTROL Origine de l’audience] lors de l’envoi de segments à [!DNL Facebook Custom Audiences].

![Origine facebook de l’audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Exemple de mappage : activation des données d’audience dans [!DNL Facebook Custom Audience] {#example-facebook}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Facebook Custom Audience].

Sélection des champs sources :

* Sélectionnez l’espace de noms `Email` comme identité source si les adresses électroniques que vous utilisez ne sont pas hachées.
* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité source si vous avez haché les adresses électroniques du client lors de l’ingestion des données dans [!DNL Platform], conformément aux [!DNL Facebook] [exigences de hachage des emails](#email-hashing-requirements).
* Sélectionnez l’espace de noms `PHONE_E.164` comme identité source si vos données se composent de numéros de téléphone non hachés. [!DNL Platform] hachera les numéros de téléphone pour se conformer aux  [!DNL Facebook] exigences.
* Sélectionnez l’espace de noms `Phone_SHA256` comme identité source si vous avez haché des numéros de téléphone lors de l’ingestion de données dans [!DNL Platform], conformément aux [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez l’espace de noms `IDFA` comme identité source si vos données se composent d’identifiants d’appareil [!DNL Apple].
* Sélectionnez l’espace de noms `GAID` comme identité source si vos données se composent d’identifiants d’appareil [!DNL Android].
* Sélectionnez l’espace de noms `Custom` comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité cible lorsque vos espaces de noms source sont `Email` ou `Email_LC_SHA256`.
* Sélectionnez l’espace de noms `Phone_SHA256` comme identité cible lorsque vos espaces de noms source sont `PHONE_E.164` ou `Phone_SHA256`.
* Sélectionnez les espaces de noms `IDFA` ou `GAID` comme identité cible lorsque vos espaces de noms source sont `IDFA` ou `GAID`.
* Sélectionnez l’espace de noms `Extern_ID` comme identité cible lorsque l’espace de noms source est personnalisé.

>[!IMPORTANT]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.
> 
>Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation.

![Mappage des identités](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Données exportées {#exported-data}

Pour [!DNL Facebook], une activation réussie signifie qu’une audience personnalisée [!DNL Facebook] serait créée par programmation dans [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL Facebook] prend en charge les renvoi d’audience historiques. Toutes les qualifications de segments historiques sont envoyées à [!DNL Facebook] lorsque vous activez les segments vers la destination.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Bad Request {#bad-request}

Lors de l’activation de segments vers [!DNL Facebook], vous pouvez recevoir l’erreur suivante :

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les clients utilisent des comptes nouvellement créés et que les autorisations [!DNL Facebook] ne sont pas encore principales.

Si vous recevez le message d’erreur `400 Bad Request` après avoir suivi les étapes de la section [Conditions préalables du compte Facebook](#facebook-account-prerequisites), attendez quelques jours pour que les autorisations [!DNL Facebook] entrent en vigueur.