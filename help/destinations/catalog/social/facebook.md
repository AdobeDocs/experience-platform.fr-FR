---
keywords: Connexion facebook;connexion facebook;destinations facebook;facebook;instagram;messenger;facebook messenger
title: Connexion Facebook
description: Activez les profils dans vos campagnes Facebook pour cibler votre audience et effectuer des personnalisat ions ou encore des suppressions reposant sur les e-mails hachés.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 31%

---

# Connexion [!DNL Facebook]

## Présentation {#overview}

Activez les profils pour votre [!DNL Facebook] des campagnes pour le ciblage, la personnalisation et la suppression des audiences en fonction d’emails hachés.

Vous pouvez utiliser cette destination pour le ciblage des audiences sur l’ensemble des [!DNL Facebook's] famille d’applications prises en charge par [!DNL Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], et [!DNL Messenger]. La sélection de l’application sur laquelle vous souhaitez exécuter la campagne est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

![Destination facebook dans l’interface utilisateur de Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Cas d’utilisation

Pour mieux comprendre comment et à quel moment utiliser la variable [!DNL Facebook] destination, voici deux exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

### Cas d’utilisation #1

Un détaillant en ligne souhaite atteindre des clients existants par le biais de plateformes sociales et leur présenter des offres personnalisées basées sur leurs commandes précédentes. Le détaillant en ligne peut ingérer des adresses électroniques de son propre CRM vers Adobe Experience Platform, créer des audiences à partir de ses propres données hors ligne et envoyer ces audiences au [!DNL Facebook] plateforme sociale, optimisant leurs dépenses publicitaires.

### Cas d’utilisation #2

Une compagnie aérienne possède différents niveaux de clients (Bronze, Argent et Or) et souhaite fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n’utilisent pas l’application mobile de la compagnie aérienne et certains d’entre eux ne se sont pas connectés au site web de la société. Les seuls identifiants dont dispose la société concernant ces clients sont les identifiants d’adhésion et les adresses électroniques.

Pour les cibler sur les réseaux sociaux, ils peuvent intégrer les données client de leur CRM dans Adobe Experience Platform, en utilisant les adresses email comme identifiants.

Ensuite, ils peuvent utiliser leurs données hors ligne, y compris les identifiants d’adhésion associés et les niveaux de client, pour créer de nouvelles audiences qu’ils peuvent cibler par le biais de la variable [!DNL Facebook] destination.

## Identités prises en charge {#supported-identities}

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

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
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Facebook. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables au compte facebook {#facebook-account-prerequisites}

Avant d’envoyer vos audiences à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* Votre [!DNL Facebook] le compte utilisateur doit disposer d’un accès complet à la variable [!DNL Facebook Business Account] qui détient le compte publicitaire que vous utilisez.
* Votre [!DNL Facebook] Le compte utilisateur doit avoir la variable **[!DNL Manage campaigns]** autorisation activée pour le compte publicitaire que vous prévoyez d’utiliser.
* La variable **Adobe Experience Cloud** votre compte professionnel doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Voir [Ajout de partenaires à votre compte Business Manager](https://www.facebook.com/business/help/1717412048538897) pour plus d’informations, voir la documentation de Facebook .
  >[!IMPORTANT]
  >
  > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. L’autorisation est requise pour la variable [!DNL Adobe Experience Platform] intégration.
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >Lors de la signature de la [!DNL Facebook Custom Audiences] Conditions d’utilisation, veillez à utiliser le même compte utilisateur que celui que vous utilisiez pour vous authentifier dans l’API Facebook.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Facebook] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL Facebook] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Facebook]:

* **Ingestion de numéros de téléphone bruts**: vous pouvez ingérer des numéros de téléphone bruts dans la variable [!DNL E.164] format dans [!DNL Platform]. Ils se sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans la variable `Phone_E.164` espace de noms.
* **Ingestion de numéros de téléphone hachés**: vous pouvez pré-hacher vos numéros de téléphone avant l’ingestion dans [!DNL Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans la variable `Phone_SHA256` espace de noms.

>[!NOTE]
>
>Numéros de téléphone ingérés dans la variable `Phone` L’espace de noms ne peut pas être activé dans [!DNL Facebook].

## Exigences en matière de hachage des emails {#email-hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et disposer des [!DNL Platform] hachez-les lors de l’activation.

Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, voir [Présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md) et la variable [présentation de l’ingestion par flux](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Rogner tous les espaces de début et de fin de la chaîne d’email ; par exemple : `johndoe@example.com`, not `<space>johndoe@example.com<space>`;
* Lors du hachage des chaînes d’email, veillez à mettre la chaîne en minuscules par hachage.
   * Exemple : `example@email.com`, not `EXAMPLE@EMAIL.COM`;
* Assurez-vous que la chaîne hachée est entièrement en minuscules.
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.
> Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation.
> La variable **[!UICONTROL Appliquer la transformation]** ne s’affiche que lorsque vous sélectionnez des attributs comme champs source. Il ne s’affiche pas lorsque vous choisissez des espaces de noms.

![Appliquez le contrôle de transformation mis en surbrillance à l’étape de mappage.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant d’utiliser la variable `Extern_ID` Espace de noms pour envoyer des données à [!DNL Facebook], veillez à synchroniser vos propres identifiants à l’aide de [!DNL Facebook Pixel]. Voir [Documentation officielle de facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) pour plus d’informations.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

La vidéo ci-dessous présente également les étapes de configuration d’une [!DNL Facebook] destination et activation des audiences.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous au [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination Facebook dans le catalogue des destinations et sélectionnez **[!UICONTROL Configuration]**.
2. Sélectionner **[!UICONTROL Se connecter à la destination]**.
   ![L’étape Authentification à Facebook s’affiche dans le workflow d’activation.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Saisissez vos informations d’identification Facebook et sélectionnez **Connexion**.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de votre compte publicitaire Facebook. Vous trouverez cet identifiant dans le Gestionnaire de publicités de votre compte Facebook. Lors de la saisie de cet identifiant, faites-le toujours précéder de `act_`."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]**: votre [!DNL Facebook Ad Account ID]. Vous pouvez trouver cet identifiant dans votre [!DNL Facebook Ads Manager] compte . Lors de la saisie de cet identifiant, faites-le toujours précéder de `act_`.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origine de l’audience"
>abstract="Choisissez la manière dont les données client de l’audience ont été collectées à l’origine. Les données s’affichent dans Facebook lorsqu’un utilisateur ou une utilisatrice est ciblé par le segment."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Origine de l&#39;audience"
>abstract="Les annonceurs ont collecté des données directement auprès des clients."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origine de l&#39;audience"
>abstract="Les annonceurs ont collecté des données directement auprès de leurs partenaires."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origine de l&#39;audience"
>abstract="Les annonceurs ont collecté des données directement auprès de leurs clients et partenaires."

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans le **[!UICONTROL Planification du segment]** , vous devez fournir la variable [!UICONTROL Origine de l’audience] lors de l’envoi d’audiences à [!DNL Facebook Custom Audiences].

![Liste déroulante Origine de l’audience affichée à l’étape d’activation de Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Exemple de mappage : activation des données d’audience dans [!DNL Facebook Custom Audience] {#example-facebook}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Facebook Custom Audience].

Sélection des champs sources :

* Sélectionnez la variable `Email` espace de noms comme identité source si les adresses électroniques que vous utilisez ne sont pas hachées.
* Sélectionnez la variable `Email_LC_SHA256` espace de noms comme identité source si vous avez haché des adresses électroniques client lors de l’ingestion de données dans [!DNL Platform], selon [!DNL Facebook] [exigences de hachage des emails](#email-hashing-requirements).
* Sélectionnez la variable `PHONE_E.164` espace de noms en tant qu’identité source si vos données se composent de numéros de téléphone non hachés. [!DNL Platform] hachera les numéros de téléphone pour qu’ils soient conformes. [!DNL Facebook] conditions requises.
* Sélectionnez la variable `Phone_SHA256` espace de noms comme identité source si vous avez haché des numéros de téléphone lors de l’ingestion des données dans [!DNL Platform], selon [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez la variable `IDFA` espace de noms comme identité source si vos données sont composées [!DNL Apple] ID d’appareil.
* Sélectionnez la variable `GAID` espace de noms comme identité source si vos données sont composées [!DNL Android] ID d’appareil.
* Sélectionnez la variable `Custom` espace de noms comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez la variable `Email_LC_SHA256` l’espace de noms comme identité cible lorsque vos espaces de noms sources `Email` ou `Email_LC_SHA256`.
* Sélectionnez la variable `Phone_SHA256` l’espace de noms comme identité cible lorsque vos espaces de noms sources `PHONE_E.164` ou `Phone_SHA256`.
* Sélectionnez la variable `IDFA` ou `GAID` les espaces de noms comme identité cible lorsque vos espaces de noms sources `IDFA` ou `GAID`.
* Sélectionnez la variable `Extern_ID` espace de noms comme identité cible lorsque votre espace de noms source est personnalisé.

>[!IMPORTANT]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.
> 
>Les données de la source d’attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance à l’étape de mappage.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Données exportées {#exported-data}

Pour [!DNL Facebook], une activation réussie signifie qu’une [!DNL Facebook] une audience personnalisée serait créée par programmation dans [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’appartenance à une audience serait ajoutée et supprimée lorsque les utilisateurs sont qualifiés ou disqualifiés pour les audiences activées.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL Facebook] prend en charge les renvois d’audience historique. Toutes les qualifications d’audience historique sont envoyées à [!DNL Facebook] lorsque vous activez les audiences vers la destination.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les clients utilisent des comptes nouvellement créés et que la variable [!DNL Facebook] les autorisations ne sont pas encore actives.

Si vous recevez la variable `400 Bad Request` message d’erreur après avoir suivi les étapes de la section [Conditions préalables au compte facebook](#facebook-account-prerequisites), prévoyez quelques jours pour la variable [!DNL Facebook] les autorisations pour qu’elles entrent en vigueur.
