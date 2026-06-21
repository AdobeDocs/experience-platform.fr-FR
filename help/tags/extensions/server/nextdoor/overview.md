---
title: Extension de l’API de conversion Nextdoor
description: Découvrez comment utiliser l’extension d’API de conversion Nextdoor pour envoyer des événements de conversion afin de suivre les performances de vos campagnes publicitaires.
last-substantial-update: 2025-12-18T00:00:00Z
exl-id: fbab477d-a865-4a35-94ba-6e887d7d28db
source-git-commit: 2d7ba15f918c314fe219212df82aec6d7ac1fc77
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 8%

---

# Extension de l’API de conversion [!DNL Nextdoor] - Guide de l’utilisateur

## Vue d’ensemble

[!DNL Nextdoor] est un service de réseautage social pour les quartiers qui relie les gens à leurs communautés locales. Il s&#39;agit d&#39;une plateforme où les voisins peuvent communiquer, partager de l&#39;information, se tenir au courant des événements et des nouvelles locales, et acheter et vendre des articles avec d&#39;autres personnes de leur région.

Utilisez l’extension [[!DNL Nextdoor] API de conversion](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) pour envoyer directement des événements de conversion à [!DNL Nextdoor's]’API de conversion. Cette extension vous permet de suivre et de mesurer les performances de vos campagnes publicitaires [!DNL Nextdoor] en envoyant des données de conversion côté serveur.

Ce guide vous explique comment installer, configurer et utiliser l’extension d’API de conversion [!DNL Nextdoor] dans vos [règles](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) de transfert d’événement.

## Conditions préalables {#prerequisites}

Vous avez besoin d’un compte [!DNL Nextdoor] Ads Manager valide pour utiliser cette extension. Si vous n’en avez pas encore, rendez-vous sur la [[!DNL Nextdoor Ads] page d’inscription](https://ads.nextdoor.com/v2/signup) pour vous inscrire et créer votre compte.

### Collecter les détails de configuration requis {#configuration-details}

Pour connecter Experience Platform à [!DNL Nextdoor], vous aurez besoin des informations suivantes :

| Informations d’identification | Description | Notes de sécurité |
| --- | --- | --- |
| ID de source de données | Identifiant de source de données unique de [!DNL Nextdoor], que vous pouvez trouver dans votre compte [!DNL Nextdoor Ads Manager] en accédant à la page Assets > Pixels et en générant un pixel Nextdoor. | Partagez-le en toute sécurité au sein de votre organisation. |
| Jeton d’accès | Votre jeton d’accès d’authentification API pour une communication sécurisée. Vous pouvez générer ce jeton en vous connectant à votre compte [!DNL Nextdoor Ads Manager] et en accédant aux paramètres de l’API. | Gardez ce jeton sécurisé, car il permet d’accéder à votre compte . |

## Installation et configuration de l’extension [!DNL Nextdoor] {#install}

Pour installer l’extension, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]**, sélectionnez l’**[!UICONTROL Extension de l’API de conversion Nextdoor]** puis sélectionnez **[!UICONTROL Installer]**.

![Catalogue d’extensions affichant la carte d’extension [!DNL Nextdoor] mettant en surbrillance install.](../../../images/extensions/server/nextdoor/install-extension.png)

Dans l’écran suivant, saisissez les valeurs de configuration que vous avez générées à partir de votre [!DNL Nextdoor Ads Manager] :

* **[!UICONTROL ID de Source de données]**
* **[!UICONTROL Jeton d’accès]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![[!DNL Nextdoor] écran de configuration de l’extension de l’API de conversion [!DNL Nextdoor].](../../../images/extensions/server/nextdoor/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez créer des règles de transfert d’événement qui déterminent quand et comment vos événements sont envoyés à [!DNL Nextdoor].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Extension de l’API de conversion Nextdoor]**. Pour envoyer des événements Edge Network à [!DNL Nextdoor], définissez le **[!UICONTROL Type d’action]** sur **[!UICONTROL Signaler les conversions web]**.

![Type d’action [!UICONTROL Report Web Conversions] sélectionné pour une règle de [!DNL Nextdoor] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/nextdoor/select-action.png)

Après avoir effectué cette sélection, des commandes supplémentaires s’affichent pour vous permettre de configurer davantage l’événement, comme indiqué ci-dessous. Une fois l’opération terminée, sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer la règle.

**Paramètres du corps principal**

Ces paramètres principaux définissent votre événement de conversion :

| Paramètre | Description | Type de données | Obligatoire | Options/Format | Exemple |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Nom de l’événement] | Indique le type d’événement de conversion suivi. | Chaîne (liste déroulante) | Obligatoire | <ul><li>Achat</li><li>Lead</li><li>S’inscrire</li><li>Ajouter au panier</li><li>Lancer le passage en caisse</li><li>Page vue</li><li>Recherche</li><li>Afficher le contenu</li><li>Ajouter à la liste de souhaits</li><li>S’abonner</li><li>Valeur personnalisée</li></li>Conversion 1-10</li></ul> | `Purchase` |
| [!UICONTROL Identifiant de l’événement] | Identifiant unique pour éviter les rapports d’événements en double. Cette valeur sera générée automatiquement si elle est vide. | Chaîne | Facultatif | Identifiant de chaîne unique | `order_12345` |
| [!UICONTROL Heure de l’événement (Unix Epoch)] | Date et heure auxquelles l’événement de conversion s’est produit. La valeur par défaut est l’heure actuelle si rien n’est indiqué. | Entier | Facultatif | Date et heure Unix en secondes | `1703980800` (30 décembre 2023) |
| [!UICONTROL Action Source] | Canal ou plateforme sur lequel la conversion a eu lieu. | Chaîne (liste déroulante) | Obligatoire | <ul><li>site internet</li><li>E-mail</li><li>appli</li><li>phone_call</li><li>bavarder</li><li>physical_store</li><li>system_generated</li><li>autres frais</li></ul> | `website` |
| [!UICONTROL ID de Source de données] | Remplacer l’identifiant global de source de données pour des événements spécifiques. Hérite de la configuration si rien n’est indiqué. | Chaîne | Facultatif | Chaîne alphanumérique | `12345` |
| [!UICONTROL URL Source de l’action] | URL spécifique où la conversion a eu lieu. | Chaîne | Facultatif | URL complète avec protocole | https://example.com/checkout/success |

**Paramètres de confidentialité et de conformité**

Utilisez ces paramètres pour garantir la conformité en matière de confidentialité :

| Paramètre | Description | Type de données | Obligatoire | Valeurs/Format | Exemple |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Utilisation restreinte des données] | Indicateur pour limiter l’utilisation des données pour la conformité en matière de confidentialité. | Entier | Facultatif | <ul><li>0 = Aucune restriction</li><li>1 = Restreindre</li></ul> | `0` |
| [!UICONTROL Utilisation restreinte des données (pays)] | Restrictions de traitement des données spécifiques à un pays. | Entier | Facultatif | 1 = USA (d&#39;autres codes peuvent être pris en charge) | `1` |
| [!UICONTROL Utilisation restreinte des données (état)] | Restrictions spécifiques à l’État pour les utilisateurs américains. | Entier | Facultatif | 1 000 = CA, 1 001 = CO, etc. | `1000` |
| [!UICONTROL Événement de test] | Marque l’événement en tant que test pour le développement/débogage. | Chaîne | Facultatif | Toute chaîne non vide | `test` |

**Paramètres des informations sur le client**

>[!IMPORTANT]
>
>Vous devez fournir au moins un paramètre d’informations client pour une attribution et une correspondance d’événement appropriées.

| Paramètre | Description | Type de données | Obligatoire | Format | Exemple |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL E-mail] | Adresse e-mail du client pour la correspondance d’identité. | Chaîne | Au moins un champ client obligatoire | Texte brut ou hachage SHA-256 | `user@example.com` |
| [!UICONTROL Numéro de téléphone] | Numéro de téléphone du client pour la correspondance d’identité. | Chaîne | Au moins un champ client obligatoire | Format E.164 (haché avec SHA-256) | `+15551234567` |
| [!UICONTROL Prénom] | Prénom du client pour une correspondance améliorée. | Chaîne | Au moins un champ client obligatoire | Texte brut ou hachage SHA-256 | `John` |
| [!UICONTROL Nom] | Nom du client pour une correspondance améliorée. | Chaîne | Au moins un champ client obligatoire | Texte brut ou hachage SHA-256 | `Smith` |
| [!UICONTROL &#x200B; Date de naissance &#x200B;] | Date de naissance du client pour l’appariement démographique. | Chaîne | Facultatif | AAAAMMJJ (SHA-256 haché) | `19900115` |
| [!UICONTROL Genre] | Sexe du client pour le ciblage démographique. | Chaîne | Facultatif | M/F/O (SHA-256 haché) | `M` |
| [!UICONTROL ID externe] | Votre identifiant client interne. | Chaîne | Facultatif | Toute chaîne unique | `customer_12345` |
| [!UICONTROL Adresse postale] | Adresse postale du client. | Chaîne | Facultatif | SHA-256 haché | `123 Main Street` (haché) |
| [!UICONTROL Ville] | Ville du client. | Chaîne | Facultatif | SHA-256 haché | `San Francisco` (haché) |
| [!UICONTROL État] | Département/province du client. | Chaîne | Facultatif | Code à deux lettres (SHA-256 haché) | `CA` (haché) |
| [!UICONTROL &#x200B; Code postal &#x200B;] | Code postal du client. | Chaîne | Facultatif | 5 premiers chiffres (États-Unis) (SHA-256 haché) | `94102` (haché) |
| [!UICONTROL Pays] | Pays du client. | Chaîne | Facultatif | ISO-3166-1 alpha-2 (SHA-256 haché) | `US` (haché) |
| [!UICONTROL Cliquez sur ID] | Identifiant de clic suivant pour l’attribution. | Chaîne | Facultatif | Capturé à partir `ndclid` paramètre d’URL | `nd_click_12345abcdef` |
| [!UICONTROL Adresse IP du client] | Adresse IP de l’appareil de l’utilisateur. | Chaîne | Facultatif | Adresse IPv4 ou IPv6 | `192.168.1.1` |
| [!UICONTROL Agent utilisateur client] | Chaîne de l’agent utilisateur du navigateur. | Chaîne | Facultatif | Chaîne user-agent brute du navigateur | `Mozilla/5.0 (Windows...)` |

**Paramètres personnalisés**

Ces paramètres fournissent un contexte supplémentaire sur votre événement de conversion :

| Paramètre | Description | Type de données | Obligatoire | Format | Exemple |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Valeur de commande] | Valeur totale de la transaction d’achat. | Chaîne | **OBLIGATOIRE pour les événements d’achat** | ISO 4217 Devise + Montant (pas d’espace) | `USD123.45` |
| [!UICONTROL ID de commande] | Identifiant de transaction ou de commande unique. | Chaîne | Facultatif | Toute chaîne unique | `order_12345` |
| [!UICONTROL Catégorie de diffusion] | Méthode de livraison du produit/service. | Chaîne | Facultatif | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Informations détaillées sur les produits achetés. | Chaîne (tableau JSON) | Facultatif | Tableau JSON d’objets de produit | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Paramètres de l’application mobile**

Vous devez inclure ces paramètres lors de l’`Action Source = 'APP'` :

| Paramètre | Description | Type de données | Obligatoire | Format | Exemple |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL ID de l’application*] | Identifiant de l&#39;application mobile. | Chaîne | **REQUIS pour les événements d’application** | <ul><li>Identifiant du bundle (iOS)</li><li>Nom du package (Android)</li></ul> | `com.company.app` |
| [!UICONTROL Suivi des applications activé] | Statut de consentement de la transparence du suivi des applications iOS. | Chaîne | **REQUIS pour les événements d’application** | Chaîne booléenne | `true` |
| [!UICONTROL Plateforme] | Système d’exploitation mobile. | Chaîne | **REQUIS pour les événements d’application** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL Version de l’application] | Version de l’application mobile. | Chaîne | **REQUIS pour les événements d’application** | Chaîne de version telle que définie par votre application | `2.0.0-beta` |

## Types d’événements {#event-types}

Les types d’événements suivants sont pris en charge pour différents scénarios de conversion :

| Nom de l’événement | Type d’événement | Description | Exemple d’utilisation | Champs obligatoires | Remarques |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Achat] | Standard | Transaction d&#39;achat terminée. | Conversions e-commerce | <ul><li>Nom de l’événement</li><li>Valeur d’ordre</li><li>Informations sur le client</li></ul> | Le plus important pour l’optimisation du retour sur dépenses publicitaires |
| [!UICONTROL Lead] | Standard | Génération de leads ou recherche. | Envois de formulaires, demandes de contact | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Conversion de grande valeur pour B2B |
| [!UICONTROL S’inscrire] | Standard | Enregistrement des utilisateurs ou création de comptes. | Inscription à la newsletter, enregistrement au compte | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Suivi des conversions Top-funnel |
| [!UICONTROL Ajouter au panier] | Standard | Produit ajouté au panier. | Suivi des funnel e-commerce | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Signal d’engagement Mid-funnel |
| [!UICONTROL Lancer le passage en caisse] | Standard | Processus de passage en caisse démarré. | Suivi des intentions d’achat | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Indicateur d’intention d’achat fort |
| [!UICONTROL &#x200B; Page vue &#x200B;] | Standard | Page importante visitée. | Engagement du contenu, pages de destination | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Utiliser uniquement pour les pages à valeur élevée |
| [!UICONTROL Rechercher] | Standard | Recherche effectuée sur le site. | Découverte de produits/contenus | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Indique l’interaction client active. |
| [!UICONTROL Afficher le contenu] | Standard | Contenu ou produit consulté. | Pages vues du produit, engagement du contenu | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Utile pour les audiences de remarketing |
| [!UICONTROL Ajouter à la liste de souhaits] | Standard | Produit ajouté à la liste de souhaits. | Intention d’achat future | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Indique un fort intérêt pour le produit |
| [!UICONTROL S&#39;abonner] | Standard | Abonnement à un service ou à une newsletter. | Chiffre d’affaires récurrent, engagement | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Indicateur de valeur de durée de vie élevée |
| [!UICONTROL Conversion personnalisée 1 - 10] | Valeur personnalisée | Événement de conversion spécifique à l’entreprise. | Définition de votre propre type de conversion | <ul><li>Nom de l’événement</li><li>Informations sur le client</li></ul> | Personnaliser pour des actions commerciales uniques |

## Intégration des éléments de données {#data-element}

Tous les champs prennent en charge les éléments de données de transfert d’événement Adobe. Sélectionnez l’icône d’élément de données ![éléments de données](../../../images/extensions/server/nextdoor/data-element-icon.png) en regard d’un champ pour :

* **Sélectionner des éléments de données existants** : permet de sélectionner des éléments de données déjà créés.
* **Ajouter de nouveaux éléments de données** : créez et définissez de nouveaux éléments de données selon vos besoins.
* **Appliquer des valeurs dynamiques** : renseignez les champs avec du contenu dynamique provenant de votre site web.

## Bonnes pratiques {#best-practices}

Suivez ces bonnes pratiques pour garantir un suivi des conversions précis, améliorer la qualité des données et respecter les réglementations de confidentialité. Ces recommandations vous aideront à optimiser l’efficacité de votre intégration de l’API de conversion [!DNL Nextdoor] et à optimiser vos performances publicitaires.

### Qualité des données et conformité en matière de confidentialité

Une gestion appropriée des données est essentielle pour optimiser la précision de l’attribution de conversion tout en préservant la confidentialité des utilisateurs et la conformité réglementaire. Ces pratiques permettent de s’assurer que les données de vos clients sont correctement formatées, traitées en toute sécurité et traitées conformément aux réglementations de confidentialité.

* **Utiliser une mise en forme de données cohérente** : mettez en forme de manière cohérente les e-mails, les numéros de téléphone et d’autres données :

   * **Normalisation des e-mails** : convertissez les e-mails en minuscules, supprimez les espaces et les points des adresses [!DNL Gmail].
   * **Normalisation des numéros de téléphone** : utilisez le format E.164 (+1234567890) pour assurer la compatibilité internationale.
   * **Normalisation des adresses** : Normalisez les abréviations des rues (St., Ave., Rd.) et supprimez les espaces supplémentaires.
   * **Formatage des noms** : convertissez les noms en minuscules, supprimez les espaces supplémentaires et gérez les caractères spéciaux de manière cohérente.

* **Hacher les données sensibles** : envisagez de hacher les données client sensibles avant de les envoyer. Normalisez toujours vos données avant le hachage pour garantir des valeurs de hachage cohérentes :

   * Utilisez le hachage SHA-256 pour les numéros de téléphone, les adresses et d’autres informations d’identification personnelles.
   * L’extension hache automatiquement les e-mails en texte brut - vous pouvez envoyer les deux formats.
   * Hachage cohérent des données sur toutes vos implémentations de suivi.
      * **Exemple** : normalisez « John@Example.COM » → « john@example.com » avant de procéder au hachage.

* **Fournir des informations complètes** : incluez autant d’informations client que possible pour une meilleure correspondance :

   * Incluez plusieurs identifiants (e-mail + téléphone ou e-mail + nom + adresse), le cas échéant.
   * Utilisez des ID de client externes pour lier les événements de conversion à vos données CRM.
   * Fournir des données démographiques (âge, sexe) lorsqu&#39;elles sont disponibles et conformes aux lois sur la protection des renseignements personnels.

* **Gestion du consentement** : vérifiez que vous disposez du consentement approprié pour la collecte de données :

   * Implémentez des mécanismes de consentement appropriés avant de collecter les données client.
   * Respectez les préférences de désinscription des utilisateurs et les demandes de suppression de données.
   * Utilisez les paramètres d’utilisation des données restreintes pour les utilisateurs qui se sont désinscrits.
   * **Ressources** :
      * [Guide de conformité au RGPD](https://gdpr.eu/compliance/)
      * [Exigences de confidentialité du CCPA](https://oag.ca.gov/privacy/ccpa)

* **Minimisation des données** : envoyez uniquement les données nécessaires au suivi des conversions :

   * Ne collectez et n’envoyez que les données essentielles à l’attribution et à l’optimisation.
   * Examinez et auditez régulièrement les champs de données que vous envoyez.
   * Supprimez les informations client inutiles pour réduire les risques liés à la confidentialité.

* **Utiliser des horodatages précis** : assurez-vous que les horodatages des événements sont précis pour une attribution correcte.
   * Utilisez l’heure réelle à laquelle la conversion a eu lieu, et non le moment où vous avez traité les données.
   * Vérifiez que les dates et heures sont au format Unix epoch (secondes depuis le 1er janvier 1970).
   * Tenez compte des différences de fuseau horaire dans vos calculs d’horodatage.

### Déduplication des événements

Empêchez les événements de conversion en double pour garantir une mesure de campagne précise et éviter les mesures de performances exagérées. Implémentez une déduplication appropriée afin que chaque conversion ne soit comptabilisée qu’une seule fois, ce qui fournit des données fiables pour vos décisions d’optimisation.

* **Fournir des identifiants d’événement uniques** : utilisez toujours des identifiants d’événement uniques pour éviter les conversions en double.
* **Utiliser des noms cohérents** : appliquez des noms d’événement cohérents dans votre implémentation.

### Limitation de débit

L’API de conversion [!DNL Nextdoor] est soumise à une limitation de débit. La limite tarifaire actuelle est de **100 requêtes/minute** par annonceur. Si vous dépassez la limite de débit, l’API renvoie un code d’erreur `HTTP 429 Too Many Requests`.

## Conclusion {#conclusion}

L’extension [!DNL Nextdoor] Conversion API offre un moyen puissant de suivre les conversions et de mesurer l’efficacité de vos campagnes publicitaires [!DNL Nextdoor]. En suivant ce guide et en implémentant les bonnes pratiques, vous pouvez assurer un suivi de conversion précis et optimiser vos performances publicitaires.

Pour obtenir les informations les plus récentes et des ressources supplémentaires, consultez [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Étapes suivantes {#next-steps}

Ce guide vous a montré comment envoyer des données d’événement côté serveur à [!DNL Nextdoor] à l’aide de l’extension de l’API de conversion [!DNL Nextdoor]. Pour en savoir plus sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
