---
title: Connexion CRM The Trade Desk
description: Activez les profils sur votre compte Trade Desk pour le ciblage et la suppression d'audiences en fonction des données CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 8%

---

# La connexion [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Il existe deux destinations The Trade Desk - CRM dans le [catalogue de destinations](/help/destinations/catalog/overview.md).
>
>* Si vos données proviennent de l’UE, utilisez la destination **[!DNL The Trade Desk - CRM (EU)]**.
>* Si vos données proviennent des régions APAC ou NAMER, utilisez la destination **[!DNL The Trade Desk - CRM (NAMER & APAC)]** .
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *[!DNL Trade Desk]*. Pour toute demande ou information, veuillez contacter votre représentant [!DNL Trade Desk].

## Vue d’ensemble {#overview}

Découvrez comment activer des profils sur votre compte [!DNL Trade Desk] pour le ciblage et la suppression d’audiences en fonction des données CRM.

Ce connecteur envoie des données à [!DNL The Trade Desk] pour l’activation des données propriétaires. [!DNL The Trade Desk] stocker vos e-mails et numéros de téléphone bruts (non hachés).

>[!TIP]
>
>Utilisez [!DNL The Trade Desk - CRM] destination pour envoyer des données CRM (telles que des e-mails et des numéros de téléphone) et d’autres identifiants de données propriétaires tels que des cookies et des identifiants d’appareil. Vous pouvez continuer à utiliser la destination [Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) dans le catalogue Experience Platform pour les cookies et les mappages d’ID d’appareil.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Avant de pouvoir activer des audiences dans The Trade Desk, vous devez contacter votre gestionnaire de compte [!DNL Trade Desk] pour activer la fonctionnalité. Si vous envoyez des e-mails, des numéros de téléphone et un UID2/EUID, vous devez partager le contrat UID2/EUID signé avec [!DNL The Trade Desk].

## Exigences de correspondance des identifiants {#id-matching-requirements}

Selon le type d’identifiants ingérés dans Adobe Experience Platform, vous devez respecter les exigences correspondantes. Pour plus d’informations, consultez la [présentation de l’espace de noms d’identité](/help/identity-service/features/namespaces.md).

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Les adresses e-mail et numéros de téléphone non hachés et hachés sont pris en charge par Adobe Experience Platform. Suivez les instructions de la section Exigences de correspondance des identifiants et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement.

| Identité cible | Description |
|---|---|
| E-mail | Adresses e-mail (texte clair) |
| Email_LC_SHA256 | Les adresses e-mail doivent être hachées à l’aide de SHA256 et en minuscules. Vous ne pourrez pas modifier ce paramètre ultérieurement. |
| Téléphone (E.164) | Numéros de téléphone à normaliser au format E.164. Le format E.164 comprend un signe plus (+), un indicatif national international, un indicatif régional et un numéro de téléphone. Par exemple : (+)(indicatif du pays)(indicatif régional)(numéro de téléphone). Cet identifiant n&#39;est pas disponible pour The Trade Desk - Données propriétaires (UE). |
| Téléphone (SHA256_E.164) | Numéros de téléphone qui ont déjà été normalisés au format E.164, puis hachés à l’aide de SHA-256, avec le hachage résultant codé en Base64. Cet identifiant n&#39;est pas disponible pour The Trade Desk - Données propriétaires (UE). |
| TDID | ID de cookie dans The Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Identifiant Apple pour les annonceurs |
| UID2 | Valeur brute d’UID2 |
| Jeton UID2Token | Jeton UID2 chiffré, également appelé jeton publicitaire. |
| EUID | Valeur brute de l’identifiant de l’Union européenne |
| EUIDoken | Jeton EUID chiffré, également appelé jeton publicitaire. |
| RampID | RampID de 49 ou 70 caractères (précédemment appelé IdentityLink ou IDL). Il doit s&#39;agir d&#39;un RampID de LiveRamp mappé spécifiquement pour The Trade Desk. |
| netID | netID de l’utilisateur sous la forme d’une chaîne codée en base64 de 70 caractères. Cet identifiant est pris en charge uniquement en Europe. |
| FirstID | First-id de l’utilisateur, un cookie propriétaire généralement défini par les éditeurs en France. Cet identifiant est pris en charge uniquement en Europe. |

{style="table-layout:auto"}

## Exigences en matière de hachage des e-mails {#email-hashing}

Vous pouvez hacher les adresses e-mail avant de les ingérer dans Adobe Experience Platform ou utiliser des adresses e-mail brutes.

Pour en savoir plus sur l’ingestion d’adresses e-mail dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md).

Si vous choisissez de hacher les adresses e-mail vous-même, veillez à respecter les exigences suivantes :

* Supprimez les espaces de début et de fin.
* Convertissez tous les caractères ASCII en minuscules.
* Dans `gmail.com` adresses e-mail, supprimez les caractères suivants de la partie nom d’utilisateur de l’adresse e-mail :

      * La période («. ») caractère (code ASCII 46). Par exemple, normalisez « jane.doe@gmail.com » en « janedoe@gmail.com ».
     * Le signe plus (`+`) (code ASCII 43) et tous les caractères suivants. Par exemple, normalisez « janedoe+home@gmail.com » en « janedoe@gmail.com ».
  
## Normalisation des numéros de téléphone et exigences de hachage {#phone-hashing}

Voici ce que vous devez savoir sur le téléchargement de numéros de téléphone :

* Vous devez normaliser les numéros de téléphone avant de les envoyer dans une requête, que vous les envoyiez hachés ou non dans une requête.
* Pour charger des données normalisées, hachées et codées, vous devez envoyer les numéros de téléphone sous la forme de hachages SHA-256 codés en Base64 des numéros de téléphone normalisés.

Si vous souhaitez charger des numéros de téléphone bruts ou hachés, vous devez les normaliser.

>[!IMPORTANT]
>
>La normalisation avant hachage garantit que la valeur d’identifiant générée sera toujours la même et que les données peuvent être associées avec précision.

Voici ce que vous devez savoir sur les exigences de normalisation des numéros de téléphone :

* L’opérateur UID2 accepte les numéros de téléphone au format E.164, qui est le format de numéro de téléphone international qui garantit l’unicité mondiale.
* Les numéros de téléphone E.164 peuvent contenir au maximum 15 chiffres.
* Les numéros de téléphone normalisés E.164 utilisent la syntaxe suivante : `[+][country code][subscriber number including area code]` sans espaces, tirets, parenthèses ou autres caractères spéciaux. Voici quelques exemples :

      * US : 1 (234) 567-8901 est normalisé à +12345678901.
     * Singapour : 65 1243 5678 est normalisé à +6512345678.
     * Australie : le numéro de téléphone portable 0491 570 006 est normalisé pour ajouter le code du pays et déposer le zéro en début de page : +61491570006.
     * UK : le numéro de téléphone mobile 07812 345678 est normalisé pour ajouter le code du pays et déposer le zéro en début de liste : +447812345678.
  
Assurez-vous que le numéro de téléphone normalisé est UTF-8, et non un autre système d’encodage tel que UTF-16.

Un hachage de numéro de téléphone est un hachage SHA-256 codé en Base64 d’un numéro de téléphone normalisé. Le numéro de téléphone est d’abord normalisé, puis haché à l’aide de l’algorithme de hachage SHA-256, puis les octets résultants de la valeur de hachage sont codés à l’aide du codage Base64. Notez que le codage Base64 est appliqué aux octets de la valeur de hachage, et non à la représentation sous forme de chaîne codée en hexadécimal.
Le tableau suivant illustre un exemple de numéro de téléphone d’entrée simple, et le résultat obtenu à chaque étape est appliqué pour obtenir une valeur sécurisée et opaque.

| Type | Exemple | Commentaires et utilisation |
|---|---|---|
| Numéro de téléphone brut | 1 (234) 567-8901 | C&#39;est le point de départ. |
| Numéro de téléphone normalisé | +12345678901 | La normalisation est toujours la première étape. |
| Hachage SHA-256 du numéro de téléphone normalisé | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Cette chaîne de 64 caractères est une représentation codée en hexadécimal du SHA-256 de 32 octets. |
| Encodage Hex à Base64 SHA-256 d’un numéro de téléphone normalisé et haché | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | Cette chaîne de 44 caractères est une représentation codée en Base64 du SHA-256 de 32 octets. Le hachage SHA-256 est une valeur hexadécimale. Vous devez utiliser un encodeur Base64 qui prend une valeur hexadécimale en entrée. Utilisez ce codage pour les valeurs phone_hash envoyées dans le corps de la requête. |

>[!IMPORTANT]
>
>Lors de l’application du codage Base64, veillez à utiliser une fonction qui prend une valeur hexadécimale en entrée. Si vous utilisez une fonction qui prend du texte comme entrée, le résultat est une chaîne plus longue qui n’est pas valide aux fins d’UID2.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail ou e-mail haché) utilisés dans la destination Trade Desk. |
| Fréquence des exportations | **[!UICONTROL Daily Batch]** | Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le profil (les identités) est mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur les [ exportations par lots ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

### Authentification à la destination {#authenticate}

[!DNL The Trade Desk] destination CRM est un chargement quotidien de fichiers par lots qui ne nécessite pas d’authentification de l’utilisateur.

### Renseigner les détails de la destination {#fill-in-details}

Avant de pouvoir envoyer ou activer des données d’audience vers une destination, vous devez configurer une connexion à votre propre plateforme de destination. Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Account Type]** : Merci de choisir l&#39;option **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Advertiser ID]** : votre [!DNL Trade Desk Advertiser ID], qui peut être partagée par votre gestionnaire de compte [!DNL Trade Desk] ou qui se trouve sous [!DNL Advertiser Preferences] dans l’interface utilisateur de [!DNL Trade Desk].

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant comment remplir les détails de destination.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Lors de la connexion à la destination , la définition d’une politique de gouvernance des données est complètement facultative. Veuillez consulter la présentation de la gouvernance des données [Experience Platform](/help/data-governance/policies/overview.md) pour plus d’informations.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers une destination.

Dans la page **[!UICONTROL Scheduling]** , vous pouvez configurer le planning et les noms des fichiers pour chaque audience que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Toutes les audiences activées vers [!DNL The Trade Desk] destination CRM sont automatiquement définies sur une fréquence quotidienne et une exportation de fichiers complets.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Dans la page **[!UICONTROL Mapping]**, vous devez sélectionner des attributs ou des espaces de noms d’identité dans la colonne source et les mapper à la colonne cible.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour mapper l’activation des audiences.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation d’audiences vers [!DNL The Trade Desk] destination CRM.

Sélection des champs source et cible :

| Champ source | Champ cible |
|---|---|
| E-mail | e-mail |
| Email_LC_SHA256 | hashed_email |
| Téléphone (E.164) | phone |
| Téléphone (SHA256_E.164) | hashed_phone |
| TDID | tridé |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| Jeton UID2Token | uid2_token |
| EUID | euid |
| EUIDoken | euid_token |
| RampID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Valider l’exportation des données {#validate}

Pour vérifier que les données sont correctement exportées depuis Experience Platform et vers [!DNL The Trade Desk], recherchez les audiences sous l’onglet Adobe 1PD dans [!DNL The Trade Desk] bibliothèque « Données et identité de l’annonceur ». Pour trouver l’identifiant correspondant dans l’interface utilisateur de [!DNL Trade Desk], procédez comme suit :

1. Sélectionnez tout d’abord l’onglet **[!UICONTROL Libraries]** , puis passez en revue la section **[!UICONTROL Advertiser data and identity]** .
2. Cliquez sur le **[!UICONTROL Adobe 1PD]** pour répertorier toutes les audiences activées à [!DNL The Trade Desk].
3. Le nom de segment ou l’identifiant de segment d’Experience Platform s’affiche en tant que nom de segment dans l’interface utilisateur de [!DNL Trade Desk].

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
