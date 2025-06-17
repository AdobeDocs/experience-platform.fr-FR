---
keywords: connexion facebook;connexion facebook;destinations facebook;facebook;instagram;messenger;facebook messenger
title: Connexion Facebook
description: Activez les profils dans vos campagnes Facebook pour cibler votre audience et effectuer des personnalisat ions ou encore des suppressions reposant sur les e-mails hachés.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: dd725b4d383bbcd93e68c81d4fe5182d6086e9be
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 22%

---

# Connexion [!DNL Facebook]

## Présentation {#overview}

Activez les profils de vos campagnes [!DNL Facebook] pour le ciblage, la personnalisation et la suppression des audiences en fonction des e-mails hachés.

Vous pouvez utiliser cette destination pour le ciblage d’audience dans [!DNL Facebook's] famille d’applications prises en charge par [!DNL Custom Audiences], notamment [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l’application sur laquelle vous souhaitez exécuter la campagne est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

![Destination Facebook dans l’interface utilisateur de Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Cas d’utilisation

Pour mieux comprendre quand et comment utiliser la destination [!DNL Facebook], consultez les deux exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1

Un retailer en ligne souhaite atteindre les clients existants par le biais de plateformes sociales et leur présenter des offres personnalisées en fonction de leurs commandes précédentes. Le retailer en ligne peut ingérer des adresses e-mail de son propre CRM vers Adobe Experience Platform, créer des audiences à partir de ses propres données hors ligne et envoyer ces audiences à la plateforme sociale [!DNL Facebook], ce qui optimise ses dépenses publicitaires.

### Cas d’utilisation #2

Une compagnie aérienne a différents niveaux de clients (bronze, argent et or) et souhaite fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n&#39;utilisent pas l&#39;application mobile de la compagnie aérienne et certains d&#39;entre eux ne se sont pas connectés au site Web de la compagnie. Les seuls identifiants dont dispose l’entreprise à propos de ces clients sont les identifiants d’abonnement et les adresses e-mail.

Pour les cibler sur les médias sociaux, ils peuvent intégrer les données client de leur CRM dans Adobe Experience Platform, en utilisant les adresses e-mail comme identifiants.

Ensuite, ils peuvent utiliser leurs données hors ligne, y compris les identifiants d’abonnement associés et les niveaux de client, pour créer de nouvelles audiences qu’ils peuvent cibler via la destination [!DNL Facebook].

## Identités prises en charge {#supported-identities}

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| `IDFA` | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| `phone_sha256` | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les numéros de téléphone hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `email_lc_sha256` | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour les adresses électroniques en texte brut et hachées, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| `extern_id` | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |
| `gender` | Genre | Valeurs acceptées : <ul><li>`m`pour les hommes</li><li>`f`pour les femmes</li></ul> Experience Platform **hache automatiquement** cette valeur avant de l’envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `date_of_birth` | Date of birth | Format accepté : `yyyy-MM-DD`. <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `last_name` | Nom | Format accepté : minuscules, `a-z` caractères uniquement, pas de ponctuation. Utilisez le codage UTF-8 pour les caractères spéciaux.  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `first_name` | Prénom | Format accepté : minuscules, `a-z` caractères uniquement, pas de ponctuation, pas d’espaces. Utilisez le codage UTF-8 pour les caractères spéciaux.  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `first_name_initial` | Initiale du prénom | Format accepté : minuscules, `a-z` caractères uniquement. Utilisez le codage UTF-8 pour les caractères spéciaux.  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `state` | État | Utilisez le code d’abréviation ANSI [2 caractères](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code) en minuscules. Pour les états non-US, utilisez des caractères minuscules, sans ponctuation, sans caractères spéciaux et sans espaces.  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `city` | Ville | Format accepté : minuscules, caractères `a-z` uniquement, pas de ponctuation, pas de caractères spéciaux, pas d’espaces.  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `zip` | Code postal | Format accepté : minuscules, pas d’espaces. Pour les codes postaux américains, utilisez uniquement les 5 premiers chiffres. Pour le Royaume-Uni, utilisez le format `Area/District/Sector` .  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |
| `country` | Pays | Format accepté : codes de pays à 2 lettres, en minuscules, au format [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2).  <br>Experience Platform **hache automatiquement** cette valeur avant de l&#39;envoyer à Facebook. Ce hachage automatique est nécessaire pour respecter les exigences de sécurité et de confidentialité de Facebook. Ne fournissez **de valeurs préhachées pour ce champ** car cela entraînerait l’échec du processus de correspondance. |

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
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination Facebook. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables relatives au compte Facebook {#facebook-account-prerequisites}

Avant d’envoyer vos audiences à [!DNL Facebook], veillez à respecter les exigences suivantes :

* Votre compte utilisateur [!DNL Facebook] doit disposer d’un accès complet au [!DNL Facebook Business Account] propriétaire du compte publicitaire que vous utilisez.
* L’autorisation **[!DNL Manage campaigns]** doit être activée pour votre compte utilisateur [!DNL Facebook] pour le compte publicitaire que vous prévoyez d’utiliser.
* Le compte professionnel **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Voir [Ajouter des partenaires à votre Business Manager](https://www.facebook.com/business/help/1717412048538897) dans la documentation Facebook pour plus d’informations.

  >[!IMPORTANT]
  >
  > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. L’autorisation est requise pour l’intégration [!DNL Adobe Experience Platform].

* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, rendez-vous sur `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`, où `accountID` est votre [!DNL Facebook Ad Account ID]. Assurez-vous que la section `business_id=206617933627973` est présente dans l’URL lorsque vous signez les Conditions d’utilisation.

  >[!IMPORTANT]
  >
  >Lors de la signature des Conditions d’utilisation de [!DNL Facebook Custom Audiences], veillez à utiliser le même compte utilisateur que celui utilisé pour vous authentifier dans l’API Facebook.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL Facebook] nécessite qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Facebook] peuvent être masquées à partir d’identifiants *hachés* tels que des adresses e-mail ou des numéros de téléphone.

Selon le type d’identifiants ingérés dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Maximiser les taux de correspondance d’audience {#match-rates}

Pour obtenir les taux de correspondance d’audience les plus élevés dans [!DNL Facebook], il est vivement recommandé d’utiliser les identités cible `phone_sha256` et `email_lc_sha256`.

Ces identifiants sont les principaux utilisés par les [!DNL Facebook] pour faire correspondre les audiences sur leurs plateformes. Assurez-vous que vos données sources sont correctement mappées à ces identités cibles et respectent les exigences de hachage [!DNL Facebook's].

## Exigences de hachage des numéros de téléphone {#phone-number-hashing-requirements}

Il existe deux méthodes pour activer les numéros de téléphone dans [!DNL Facebook] :

* **Ingestion de numéros de téléphone bruts** : vous pouvez ingérer des numéros de téléphone bruts au format [!DNL E.164] dans [!DNL Experience Platform]. Ils sont automatiquement hachés lors de l’activation. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone bruts dans l’espace de noms `Phone_E.164`.
* **Ingestion de numéros de téléphone hachés** : vous pouvez préhacher vos numéros de téléphone avant l’ingestion dans [!DNL Experience Platform]. Si vous choisissez cette option, veillez à toujours ingérer vos numéros de téléphone hachés dans l’espace de noms `Phone_SHA256`.

>[!NOTE]
>
>Les numéros de téléphone ingérés dans l’espace de noms `Phone` ne peuvent pas être activés dans [!DNL Facebook].

## Exigences en matière de hachage des e-mails {#email-hashing-requirements}

Vous pouvez hacher les adresses e-mail avant de les ingérer dans Adobe Experience Platform ou les utiliser en clair dans Experience Platform et demander à [!DNL Experience Platform] de les hacher lors de l’activation.

Pour en savoir plus sur l’ingestion d’adresses e-mail dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher les adresses e-mail vous-même, veillez à respecter les exigences suivantes :

* Supprimez tous les espaces de début et de fin de la chaîne d’e-mail ; par exemple : `johndoe@example.com`, pas `<space>johndoe@example.com<space>` ;
* Lors du hachage des chaînes de l’e-mail, veillez à hacher la chaîne en minuscules ;
   * Exemple : `example@email.com`, pas `EXAMPLE@EMAIL.COM` ;
* Vérifiez que la chaîne hachée est en minuscules
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, pas `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` ;
* Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Experience Platform] lors de l’activation.
>> Les données source des attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation.
>> L’option **[!UICONTROL Appliquer la transformation]** ne s’affiche que lorsque vous sélectionnez des attributs comme champs source. Elle ne s’affiche pas lorsque vous choisissez des espaces de noms.

![Appliquez le contrôle de transformation mis en surbrillance dans l’étape de mappage.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilisation d’espaces de noms personnalisés {#custom-namespaces}

Avant de pouvoir utiliser l’espace de noms `Extern_ID` pour envoyer des données à [!DNL Facebook], veillez à synchroniser vos propres identifiants à l’aide de [!DNL Facebook Pixel]. Voir la [documentation officielle de Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) pour plus d’informations.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

La vidéo ci-dessous montre également les étapes à suivre pour configurer une destination [!DNL Facebook] et activer des audiences.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous au tutoriel [configuration de destination](../../ui/connect-destination.md).

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination Facebook dans le catalogue de destinations et sélectionnez **[!UICONTROL Configurer]**.
2. Sélectionnez **[!UICONTROL Se connecter à la destination]**.
   ![Étape S’authentifier sur Facebook affichée dans le workflow d’activation.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Saisissez vos identifiants Facebook et sélectionnez **Connexion**.

### Actualiser les informations d’identification d’authentification {#refresh-authentication-credentials}

Les jetons d’authentification Facebook expirent tous les 60 jours. Une fois le jeton expiré, les exportations de données vers la destination cessent de fonctionner.

Vous pouvez surveiller les dates d’expiration de votre jeton à partir de la colonne **[!UICONTROL Date d’expiration du compte]** dans les onglets **[!UICONTROL Comptes]** ou **[!UICONTROL Parcourir]**.

![Colonne de date d’expiration du jeton de compte Facebook dans l’onglet Parcourir ](../../assets/catalog/social/facebook/account-expiration-browse.png)

![Colonne de date d’expiration du jeton de compte Facebook dans l’onglet Comptes ](../../assets/catalog/social/facebook/account-expiration-accounts.png)

Pour éviter que l’expiration du jeton ne provoque des interruptions dans vos flux de données d’activation, réauthentifiez-vous en procédant comme suit :

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]**
2. (Facultatif) Utilisez les filtres disponibles sur la page pour afficher uniquement les comptes Facebook.
   ![Filtrer pour afficher uniquement les comptes Facebook](/help/destinations/assets/catalog/social/facebook/refresh-oauth-filters.png)
3. Sélectionnez le compte à actualiser, puis les points de suspension et sélectionnez **[!UICONTROL Modifier les détails]**.
   ![Sélectionnez Modifier les détails](/help/destinations/assets/catalog/social/facebook/refresh-oauth-edit-details.png)
4. Dans la fenêtre modale, sélectionnez **[!UICONTROL Reconnecter OAuth]** et réauthentifiez-vous à l’aide de vos informations d’identification Facebook.
   ![Fenêtre modale avec l’option Reconnecter OAuth ](/help/destinations/assets/catalog/social/facebook/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Vos informations d’authentification sont actualisées et leur délai d’expiration est réinitialisé à 60 jours.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de votre compte publicitaire Facebook. Vous trouverez cet identifiant dans le Gestionnaire de publicités de votre compte Facebook. Lors de la saisie de cet identifiant, faites-le toujours précéder de `act_`."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]** : votre [!DNL Facebook Ad Account ID]. Cet identifiant se trouve dans votre compte [!DNL Facebook Ads Manager]. Lors de la saisie de cet identifiant, faites-le toujours précéder de `act_`.

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
>title="Origine de l’audience"
>abstract="Les annonceurs ont collecté des données directement auprès des clients."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origine de l’audience"
>abstract="Les annonceurs ont collecté des données directement auprès de leurs partenaires."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origine de l’audience"
>abstract="Les annonceurs ont collecté des données directement auprès de leurs clients et partenaires."

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Dans l’étape **[!UICONTROL Planning des segments]** vous devez indiquer l’[!UICONTROL origine de l’audience] lors de l’envoi d’audiences à [!DNL Facebook Custom Audiences].

![Liste déroulante Origine de l’audience affichée à l’étape d’activation Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Exemple de mappage : activation des données d’audience dans [!DNL Facebook Custom Audience] {#example-facebook}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation des données d’audience dans [!DNL Facebook Custom Audience].

Sélection des champs sources :

* Sélectionnez l’espace de noms `Email` comme identité source si les adresses e-mail que vous utilisez ne sont pas hachées.
* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité source si vous avez haché les adresses e-mail des clients lors de l’ingestion des données dans [!DNL Experience Platform], conformément [!DNL Facebook] [exigences de hachage des e-mails](#email-hashing-requirements).
* Sélectionnez l’espace de noms `PHONE_E.164` comme identité source si vos données sont composées de numéros de téléphone non hachés. [!DNL Experience Platform] hachera les numéros de téléphone pour se conformer aux exigences [!DNL Facebook].
* Sélectionnez l’espace de noms `Phone_SHA256` comme identité source si vous hachez des numéros de téléphone lors de l’ingestion de données dans [!DNL Experience Platform], conformément [!DNL Facebook] [exigences de hachage des numéros de téléphone](#phone-number-hashing-requirements).
* Sélectionnez l’espace de noms `IDFA` comme identité source si vos données sont composées d’identifiants d’appareil [!DNL Apple].
* Sélectionnez l’espace de noms `GAID` comme identité source si vos données sont composées d’identifiants d’appareil [!DNL Android].
* Sélectionnez l’espace de noms `Custom` comme identité source si vos données sont composées d’autres types d’identifiants.

Sélection des champs cibles :

* Sélectionnez l’espace de noms `Email_LC_SHA256` comme identité cible lorsque vos espaces de noms sources sont `Email` ou `Email_LC_SHA256`.
* Sélectionnez l’espace de noms `Phone_SHA256` comme identité cible lorsque vos espaces de noms sources sont `PHONE_E.164` ou `Phone_SHA256`.
* Sélectionnez les espaces de noms `IDFA` ou `GAID` comme identité cible lorsque vos espaces de noms sources sont `IDFA` ou `GAID`.
* Sélectionnez l’espace de noms `Extern_ID` comme identité cible lorsque l’espace de noms source est personnalisé.

>[!IMPORTANT]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Experience Platform] lors de l’activation.
> 
>Les données source des attributs ne sont pas automatiquement hachées. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation.

![Appliquez le contrôle de transformation mis en surbrillance dans l’étape de mappage.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Données exportées {#exported-data}

Par [!DNL Facebook], une activation réussie signifie qu’une audience personnalisée [!DNL Facebook] serait créée par programmation dans [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’appartenance à une audience serait ajoutée et supprimée au fur et à mesure que les utilisateurs sont qualifiés ou disqualifiés pour les audiences activées.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL Facebook] prend en charge les renvois d’audience historiques. Toutes les qualifications d’audience historiques sont envoyées à [!DNL Facebook] lorsque vous activez les audiences vers la destination.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les clients utilisent des comptes nouvellement créés et que les autorisations [!DNL Facebook] ne sont pas encore actives.

>[!IMPORTANT]
>
>Veillez à accepter le [!DNL Facebook Custom Audience Terms of Service] sous `business ID 206617933627973`, comme illustré dans le modèle d’URL de la section [Conditions préalables du compte](#facebook-account-prerequisites).

Si vous recevez le message d’erreur `400 Bad Request` après avoir suivi les étapes de la section [Conditions préalables du compte Facebook](#facebook-account-prerequisites), patientez quelques jours pour que les autorisations [!DNL Facebook] prennent effet.


