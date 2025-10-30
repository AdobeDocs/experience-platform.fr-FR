---
keywords: extension de transfert d’événement;pinterest;extension de transfert d’événement pinterest
title: Extension de transfert d’événement Pinterest
description: Cette extension de transfert d’événement Adobe Experience Platform vous permet d’ingérer des événements dans Pinterest en fonction des besoins de votre entreprise.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 5%

---

# Extension de transfert d’événement [!DNL Pinterest]

[!DNL Pinterest] est un moteur de découverte visuelle permettant de trouver des idées telles que des recettes, un décor de maison, une inspiration de style, etc. Il y a des milliards d&#39;épingles sur [!DNL Pinterest], qui peuvent également être partagées avec d&#39;autres sur [!DNL Pinterest]. Vous pouvez assembler les événements d’interaction utilisateur et tirer parti des [!DNL Pinterest Analytics] pour comprendre le comportement des utilisateurs et exécuter des publicités ciblées.

L’extension [[!DNL Pinterest] Conversions](https://developers.pinterest.com/docs/conversions/conversion-management/) API [transfert d’événement](../../../ui/event-forwarding/overview.md) vous permet d’exploiter les données capturées dans l’Edge Network Adobe Experience Platform et de les envoyer à [!DNL Pinterest]. Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités dans vos [règles](../../../ui/managing-resources/rules.md) de transfert d’événement.

Les jetons d’accès de conversion sont la méthode d’authentification utilisée par [!DNL Pinterest] lors de l’interaction avec l’API [!DNL Pinterest].

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données d’Edge Network en [!DNL Pinterest] pour tirer parti de ses fonctionnalités d’analyse des clients.

Prenons l’exemple d’une équipe marketing au sein d’une organisation. L’équipe capture les données d’événement d’interaction utilisateur de son site web et les charge dans [!DNL Pinterest] à l’aide de cette extension de transfert d’événement.

Les équipes de marketing et d’analyse peuvent ensuite exploiter les fonctionnalités d’[!DNL Pinterest] Analytics pour comprendre les interactions et les comportements clés des utilisateurs, ce qui vous permet de mieux comprendre les utilisateurs et de les cibler pour des campagnes publicitaires ciblées.

Pour plus d’informations sur les cas d’utilisation spécifiques à [!DNL Pinterest], consultez la documentation [[!DNL Pinterest] cas d’utilisation](https://business.pinterest.com/en/success-stories).

## Conditions préalables de [!DNL Pinterest] {#prerequisites}

Vous devez disposer d’un [!DNL Pinterest] [compte professionnel](https://help.pinterest.com/en/business/article/get-a-business-account) valide pour utiliser cette extension. Accédez à la [[!DNL Pinterest] page d’enregistrement](https://www.pinterest.com/business/create/) pour vous enregistrer et créer un compte si vous n’en avez pas déjà un.

Vous aurez également besoin d’un compte de développeur [!DNL Pinterest], qui devra être associé à votre compte professionnel [!DNL Pinterest]. Pour associer votre compte de développeur à votre compte d’entreprise, reportez-vous à la section [[!DNL Pinterest &#x200B;] Compte de développeur](https://developers.pinterest.com/account-setup/).

### Collecter les détails de configuration requis {#configuration-details}

Pour connecter Experience Platform à [!DNL Pinterest], les entrées suivantes sont requises :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| ID de compte publicitaire | Identifiant De Votre Compte [!DNL Pinterest] Ads. Reportez-vous à la documentation de [[!DNL Pinterest] &#x200B;](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) pour obtenir des conseils. | 123456789012 |
| Jeton d’accès de conversion | Votre Jeton D’Accès À La Conversion [!DNL Pinterest]. Reportez-vous au document [[!DNL Pinterest] API de conversion](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) pour obtenir des conseils. <br> **Vous ne devrez effectuer cette opération qu’une seule fois, car ce jeton n’expire pas.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installation et configuration de l’extension [!DNL Pinterest] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez plutôt une propriété existante à modifier.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionnez **[!UICONTROL Install]** sur la carte de l’extension [!DNL Pinterest] dans l’onglet **[!UICONTROL Catalog]** .

![Catalogue affichant l’extension de [!DNL Pinterest] avec [!UICONTROL Install] mise en surbrillance.](../../../images/extensions/server/pinterest/install.png)

### Configuration de l’extension [!DNL Pinterest]

>[!IMPORTANT]
>
>Selon vos besoins d’implémentation, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionnez **[!UICONTROL Configure]** sur la carte de l’extension [!DNL Pinterest] dans l’onglet [!UICONTROL Installed]** .

![[!DNL Pinterest] extension affichée dans l’onglet [!UICONTROL Install] avec le [!UICONTROL Configure] en surbrillance.](../../../images/extensions/server/pinterest/configure.png)

Dans l’écran suivant, saisissez les [!UICONTROL Ads Account Id] et [!UICONTROL Conversion Access Token] que vous avez précédemment rassemblés dans la section [détails de la configuration](#configuration-details). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]**.

![Écran [!DNL Pinterest] [!UICONTROL Configure] mettant en surbrillance les champs de saisie [!UICONTROL Ads Account Id] et [!UICONTROL Conversion Access Token].](../../../images/extensions/server/pinterest/input.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Pinterest].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Pinterest]**. Pour envoyer des événements Edge Network à [!DNL Pinterest], définissez la **[!UICONTROL Action Type]** sur **[!UICONTROL Send Event].**

![Création de la règle de [!DNL Pinterest] [!UICONTROL Send Event].](../../../images/extensions/server/pinterest/rule.png)

Après la sélection, des commandes supplémentaires apparaissent pour configurer plus en détail l’événement. Vous devez mapper les propriétés d’événement [!DNL Pinterest] aux éléments de données que vous avez précédemment créés.

### [!UICONTROL Event Data]

Les données d’événement suivantes seront nécessaires pour créer la règle :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL Event Name] | Type de l’événement utilisateur. Cependant, il peut s’agir de n’importe quel type d’événement. Pour tirer parti de [!DNL Pinterest Analytics], il est recommandé d’utiliser des [[!DNL Pinterest] codes d’événement](https://help.pinterest.com/en/business/article/add-event-codes) | &ast; checkout <br> &ast; add_to_cart <br> &ast; page_visit <br> &ast; signup <br> &ast; [événement défini par l’utilisateur] |
| [!UICONTROL Action Source] | Source indiquant où l’événement de conversion s’est produit. | &ast; app_android <br> &ast; app_ios <br> &ast; <br> web &ast; hors ligne |
| [!UICONTROL Event Time] | Fait référence à l’heure de l’événement. Le format d’heure par défaut utilisé est UNIX, au format `<seconds>.<miliseconds>` en fonction du fuseau horaire local. Pour plus d’informations, consultez la section [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255,500 indique 1433188255 secondes et 500 millisecondes après l’époque Unix, ou lundi 1er juin 2015 à 19:50:55 GMT. |
| [!UICONTROL Event ID] | Chaîne d’identifiant unique qui identifie cet événement et qui peut être utilisée pour dédupliquer les événements ingérés à la fois par l’intermédiaire de l’API de conversion et du suivi Pinterest. Sans cela, les données de l&#39;événement seront probablement comptées deux fois et signaleront l&#39;inflation métrique. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Un objet JSON contenant les propriétés personnalisées de l’événement. Faites votre choix entre fournir du code JSON brut ou utiliser un ensemble simplifié d’entrées clé-valeur. | { « event_source_url »: « http://site.com » } |

![La [!DNL Pinterest] [!UICONTROL Event Data] mise en surbrillance dans l’action de règle.](../../../images/extensions/server/pinterest/event-data.png)

Les propriétés d’événement suivantes peuvent être configurées :

| Nom du champ | Description |
| --- | --- |
| URL de Source de l’événement | URL de l’événement de conversion web. |
| ID de magasin d’applications | L’identifiant de l’application App Store. |
| Nom de l’application | Nom de l’application. |
| Application Version | Version de l’application. |
| Marque de l’appareil | Marque de l’appareil utilisé par l’utilisateur. |
| Support d&#39;appareil | Opérateur mobile de l’utilisateur pour son appareil. |
| Modèle d’appareil | Modèle de l’appareil de l’utilisateur. |
| Type d’appareil | Type d’appareil utilisé par l’utilisateur. |
| Version du système d’exploitation | Version du système d’exploitation de l’appareil. |
| Langue de l&#39;utilisateur | Code de langue ISO-639-1 à deux caractères indiquant la langue de l’utilisateur. |

### [!UICONTROL User Data]

Les données utilisateur suivantes peuvent être saisies par : ne sont pas des champs obligatoires :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL Email] | Adresse e-mail de l’utilisateur ou hachage SHA256 de l’adresse e-mail de l’utilisateur. | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | Hachages Sha256 des « ID Google Advertising » (GAID) ou « Identifiant Apple pour les annonceurs » (IDFA) de l’utilisateur | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | L’adresse IP de l’utilisateur, qui peut être au format IPv4 ou IPv6. Utilisé pour la correspondance. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | Chaîne de l’agent utilisateur du navigateur web de l’utilisateur. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Un objet JSON contenant d’autres informations sur le client. Faites votre choix entre fournir du code JSON brut ou utiliser un ensemble simplifié d’entrées clé-valeur. | { « ph »: « 122333445 » } |

![La [!DNL Pinterest] [!UICONTROL User Data] mise en surbrillance dans l’action de règle.](../../../images/extensions/server/pinterest/user-data.png)

Les propriétés d’informations client configurables sont les suivantes :

| Nom du champ | Description |
| --- | --- |
| Téléphone | Numéro de contact de l’utilisateur. Seuls les chiffres sont acceptés et doivent être entrés avec l&#39;indicatif du pays, l&#39;indicatif régional et le numéro. |
| Genre | Le genre peut être saisi sous la forme « f » pour le féminin, « m » pour le masculin ou « n » pour le non binaire. |
| Date de naissance | Date de naissance, saisie sous la forme année, mois et jour. |
| Nom | Nom de l’utilisateur. |
| Prénom | Prénom de l’utilisateur. |
| Ville | Ville de résidence de l’utilisateur. Il est principalement utilisé à des fins de facturation. |
| État | État de l’utilisateur, fourni sous la forme d’un code à deux lettres en minuscules. |
| Code postal | Code postal de l’utilisateur, qui est principalement utilisé à des fins de facturation. |
| Pays | Code pays ISO-3166 à deux caractères indiquant le pays de l’utilisateur. |
| Identifiant externe | ID unique de l’annonceur qui identifie un utilisateur dans son espace. Par exemple, l’identifiant utilisateur, l’identifiant de fidélité, etc. |
| Clic sur l’ID | Identifiant unique stocké dans le cookie _epik sur votre domaine ou paramètre de requête &amp;epik= dans l’URL. |

>[!IMPORTANT]
>
>Avant d’envoyer les données au point d’entrée de l’API [!DNL Pinterest], l’extension hache et normalise les valeurs des champs suivants : e-mail, numéro de téléphone, prénom, nom, genre, date de naissance, ville, État, code postal, pays et ID externe. L’extension ne hache pas la valeur de ces champs si une chaîne SHA256 est déjà présente.

### [!UICONTROL Custom Data]

Les données personnalisées suivantes peuvent être saisies pour la règle :

| Nom du champ | Description |
| --- | --- |
| Devise | Code de devise ISO-4217. Si ce n’est pas le cas, [!DNL Pinterest] utilisera par défaut la devise de l’annonceur définie lors de la création du compte. |
| Valeur | Valeur totale de l’événement. Acceptée en tant que chaîne dans la requête. Elle sera analysée en un nombre à deux chiffres. |
| Chaîne de recherche | Chaîne de recherche liée à l’événement de conversion de l’utilisateur. |
| ID de commande | Identifiant de commande. L’envoi de `order_id` permet [!DNL Pinterest] dédupliquer les événements si nécessaire. |
| Nombre de produits | Nombre total de produits de l&#39;événement. Par exemple, le nombre total d’articles achetés dans un événement de passage en caisse. |
| ID de contenu | Liste (tableau) des ID de produits. |
| Contenus | Liste (tableau) d’objets contenant des informations sur les produits, telles que le prix et la quantité. |

![La [!DNL Pinterest] [!UICONTROL Custom Data] mise en surbrillance dans l’action de règle.](../../../images/extensions/server/pinterest/custom-data.png)

## Valider les données dans [!DNL Pinterest]

Une fois la règle de transfert d’événement créée et exécutée, vérifiez si l’événement envoyé à l’API [!DNL Pinterest] s’affiche comme prévu dans l’interface utilisateur de [!DNL Pinterest].

Si la collecte d’événements et l’intégration des [!DNL Experience Platform] ont été effectuées avec succès, des événements s’afficheront dans l’interface utilisateur de [!DNL Pinterest].

![Gestionnaire d’événements [!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history.png)

Vous pouvez effectuer une analyse plus approfondie et afficher la distribution des données d’événement [!DNL Pinterest].

![La répartition [!DNL Pinterest] données](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Étapes suivantes

Ce guide explique comment installer et configurer l’extension de transfert d’événement [!DNL Pinterest] dans l’interface utilisateur. Pour plus d’informations, consultez la documentation officielle :

* [[!DNL Pinterest]  API &#x200B;](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Présentation de l’API de conversion](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
