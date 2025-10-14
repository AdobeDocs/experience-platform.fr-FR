---
keywords: extension de transfert d’événement;pinterest;extension de transfert d’événement pinterest
title: Extension de transfert d’événement Pinterest
description: Cette extension de transfert d’événement Adobe Experience Platform vous permet d’ingérer des événements dans Pinterest en fonction de vos besoins.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 6%

---

# Extension de transfert d’événement [!DNL Pinterest]

[!DNL Pinterest] est un moteur de découverte visuelle qui permet de trouver des idées telles que des recettes, un décor, une inspiration de style, etc. Il existe des milliards de pin&#39;s sur [!DNL Pinterest], qui peuvent également être partagés avec d&#39;autres sur [!DNL Pinterest]. Vous pouvez rassembler les événements d’interaction de l’utilisateur et exploiter [!DNL Pinterest Analytics] pour comprendre le comportement de l’utilisateur et exécuter des publicités ciblées.

L’extension [[!DNL Pinterest] Conversions](https://developers.pinterest.com/docs/conversions/conversion-management/) API [&#x200B; de transfert d’événement](../../../ui/event-forwarding/overview.md) vous permet d’exploiter les données capturées dans l’Edge Network Adobe Experience Platform et de les envoyer à [!DNL Pinterest]. Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités dans le transfert d’événement [rules](../../../ui/managing-resources/rules.md).

Les jetons d’accès aux conversions sont la méthode d’authentification utilisée par [!DNL Pinterest] lors de l’interaction avec l’API [!DNL Pinterest].

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données de l’Edge Network dans [!DNL Pinterest] pour tirer parti de ses fonctionnalités d’analyse client.

Prenons l’exemple d’une équipe marketing au sein d’une organisation. L’équipe capture les données d’événement d’interaction de l’utilisateur à partir de son site web et les charge dans [!DNL Pinterest] à l’aide de cette extension de transfert d’événement.

Les équipes de marketing et d’analyse peuvent ensuite exploiter les fonctionnalités [!DNL Pinterest] d’Analytics pour comprendre les interactions et le comportement des utilisateurs clés, ce qui vous permet de mieux comprendre les utilisateurs et de les cibler pour les campagnes publicitaires ciblées.

Pour plus d&#39;informations sur les cas d&#39;utilisation spécifiques à [!DNL Pinterest], consultez la documentation [[!DNL Pinterest] Cas d&#39;utilisation](https://business.pinterest.com/en/success-stories) .

## Conditions préalables de [!DNL Pinterest] {#prerequisites}

Pour utiliser cette extension, vous devez disposer d&#39;un [!DNL Pinterest] [compte d&#39;entreprise](https://help.pinterest.com/en/business/article/get-a-business-account) valide. Accédez à la [[!DNL Pinterest] page d&#39;inscription](https://www.pinterest.com/business/create/) pour vous enregistrer et créer un compte si vous n&#39;en avez pas déjà un.

Vous aurez également besoin d’un compte de développeur [!DNL Pinterest], qui devra être associé à votre compte d’entreprise [!DNL Pinterest]. Pour associer votre compte de développeur à votre compte d&#39;entreprise, reportez-vous au [[!DNL Pinterest &#x200B;] compte de développeur](https://developers.pinterest.com/account-setup/).

### Collecte des détails de configuration requis {#configuration-details}

Pour connecter l’Experience Platform à [!DNL Pinterest], les entrées suivantes sont requises :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant de compte Ads | Votre Identifiant De Compte Ads [!DNL Pinterest]. Reportez-vous à la documentation de [[!DNL Pinterest] &#x200B;](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) pour obtenir des conseils. | 123456789012 |
| Jeton d’accès à la conversion | Votre Jeton d’accès à la conversion [!DNL Pinterest]. Consultez le document [[!DNL Pinterest] API de conversion](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) pour obtenir des conseils. <br> **Vous n’aurez besoin de le faire qu’une seule fois, car ce jeton n’expire pas.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installation et configuration de l’extension [!DNL Pinterest] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier à la place.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionnez **[!UICONTROL Install]** sur la carte de l’extension [!DNL Pinterest] dans l’onglet **[!UICONTROL Catalog]**.

![Catalogue affichant l’extension [!DNL Pinterest] avec [!UICONTROL Install] en surbrillance.](../../../images/extensions/server/pinterest/install.png)

### Configuration de l’extension [!DNL Pinterest]

>[!IMPORTANT]
>
>En fonction des besoins de mise en oeuvre, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionnez **[!UICONTROL Configurer]** sur la carte de l’extension [!DNL Pinterest] dans l’onglet [!UICONTROL Installé]**.

Extension ![[!DNL Pinterest] affichée dans l&#39;onglet [!UICONTROL Installer] avec [!UICONTROL Configurer] en surbrillance.](../../../images/extensions/server/pinterest/configure.png)

Sur l’écran suivant, saisissez les [!UICONTROL Ads Account Id] et [!UICONTROL Conversion Access Token] que vous avez précédemment rassemblés dans la section [configuration details](#configuration-details) . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![&#x200B; L’écran [!DNL Pinterest] [!UICONTROL &#x200B; de configuration &#x200B;] surlignant les champs d’entrée [!UICONTROL Ads Account Id] et [!UICONTROL Conversion Access Token].](../../../images/extensions/server/pinterest/input.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Pinterest].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Pinterest]**. Pour envoyer des événements Edge Network à [!DNL Pinterest], définissez le **[!UICONTROL Type d’action]** sur **[!UICONTROL Envoyer l’événement].**

![Création de la règle [!DNL Pinterest] [!UICONTROL Envoyer l’événement].](../../../images/extensions/server/pinterest/rule.png)

Une fois la sélection effectuée, d’autres commandes s’affichent pour configurer davantage l’événement. Vous devez mapper les propriétés d’événement [!DNL Pinterest] aux éléments de données que vous avez précédemment créés.

### [!UICONTROL &#x200B; Event Data]

Les données d’événement suivantes seront nécessaires pour créer la règle :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL Nom de l’événement] | Type de l’événement utilisateur. Il peut toutefois s&#39;agir de n&#39;importe quel type d&#39;événement. Pour utiliser [!DNL Pinterest Analytics], il est recommandé d&#39;utiliser [[!DNL Pinterest] code d&#39;événement](https://help.pinterest.com/en/business/article/add-event-codes) | * passage en caisse <br> * add_to_cart <br> * page_visit <br> * inscription <br> * [Événement défini par l’utilisateur] |
| [!UICONTROL Action Source] | Source indiquant où l’événement de conversion s’est produit. | * app_android <br> * app_ios <br> * web <br> * hors ligne |
| [!UICONTROL Heure de l’événement] | Cela fait référence à l’heure de l’événement. Le format d’heure par défaut utilisé est UNIX, au format `<seconds>.<miliseconds>` selon votre fuseau horaire local. Pour plus d’informations, reportez-vous à l’ [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | La version 1433188255.500 indique 1433188255 secondes et 500 millisecondes après l’époque, ou le lundi 1er juin 2015, à 7:50:55 PM GMT. |
| [!UICONTROL ID d’événement] | Chaîne d’identifiant unique qui identifie cet événement et peut être utilisée pour dédupliquer les événements ingérés à la fois via l’API de conversion et le suivi Pinterest. Sans cela, les données de l’événement seront probablement comptabilisées deux fois et signaleront le gonflement des mesures. | ba7816bf8f01cfea414140de5dae223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propriétés de l’événement] | Objet JSON contenant des propriétés personnalisées de l’événement. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![&#x200B; [!DNL Pinterest] [!UICONTROL Données de l’événement] surlignées dans l’action de règle.](../../../images/extensions/server/pinterest/event-data.png)

Les propriétés d’événement suivantes peuvent être configurées :

| Nom du champ | Description |
| --- | --- |
| URL Source d’événement | URL de l’événement de conversion web. |
| ID de magasin d’applications | Identifiant de l’application de la boutique d’applications. |
| Nom de l’application | Nom de l’application. |
| Application Version | Version de l’application. |
| Marque du périphérique | Marque du périphérique utilisé par l’utilisateur. |
| Opérateur de périphérique | Opérateur de téléphonie mobile de l’utilisateur pour son appareil. |
| Modèle de périphérique | Modèle du périphérique de l’utilisateur. |
| Type d’appareil | Type de périphérique utilisé par l’utilisateur. |
| Version du système d’exploitation | Version du système d’exploitation du périphérique. |
| Langue de l’utilisateur | Code de langue ISO-639-1 à deux caractères indiquant la langue de l’utilisateur. |

### [!UICONTROL Données utilisateur]

Les données utilisateur suivantes peuvent être saisies à l’aide de ne sont pas des champs obligatoires :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL E-mail.] | Adresse électronique de l’utilisateur ou hachage SHA256 de l’adresse électronique de l’utilisateur. | ebd543592...f2b7e1 |
| [!UICONTROL Identifiants de publicité mobile] | hachages Sha256 des &quot;Google Advertising IDs&quot; (GAID) ou &quot;Apple Identifier pour les annonceurs&quot; (IDFA) de l’utilisateur ; | ebd543592...f2b7e1 |
| [!UICONTROL Adresse IP du client] | Adresse IP de l’utilisateur, qui peut être au format IPv4 ou IPv6. Utilisé pour la correspondance. | 192.168.0.1 |
| [!UICONTROL Agent utilisateur client] | Chaîne de l’agent utilisateur du navigateur web de l’utilisateur. | Mozilla/5.0 (plate-forme ; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Données d’informations sur le client] | Objet JSON contenant d’autres informations sur le client. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | { &quot;ph&quot;: &quot;122333445&quot; } |

![&#x200B; [!DNL Pinterest] [!UICONTROL Données utilisateur] surlignées dans l’action de règle.](../../../images/extensions/server/pinterest/user-data.png)

Les propriétés d’informations sur les clients qui peuvent être configurées sont les suivantes :

| Nom du champ | Description |
| --- | --- |
| Téléphone | Numéro de contact de l&#39;utilisateur. Seuls les chiffres sont acceptés et doivent être renseignés avec l&#39;indicatif du pays, l&#39;indicatif régional et le numéro. |
| Genre | Le genre peut être renseigné en tant que &quot;f&quot; pour féminin, &quot;m&quot; pour masculin ou &quot;n&quot; pour non-binaire. |
| Date de naissance | Date de naissance, saisie sous forme d’année, de mois et de jour. |
| Nom | Nom de l’utilisateur. |
| Prénom | Prénom de l’utilisateur. |
| Ville | Ville de résidence de l’utilisateur. Il est principalement utilisé à des fins de facturation. |
| État | État de l’utilisateur, fourni en minuscules sous forme de code à deux lettres. |
| Code postal | Code postal de l’utilisateur, principalement utilisé à des fins de facturation. |
| Pays | Code de pays ISO-3166 à deux caractères indiquant le pays de l’utilisateur. |
| Identifiant externe | Identifiant unique de l’annonceur qui identifie un utilisateur dans son espace. Par exemple, identifiant utilisateur, identifiant de fidélité, etc. |
| ID de clic | Identifiant unique stocké dans le cookie _epik sur votre domaine ou le paramètre de requête &amp;epik= dans l’URL. |

>[!IMPORTANT]
>
>Avant d’envoyer les données au point de terminaison de l’API [!DNL Pinterest], l’extension hachera et normalisera les valeurs des champs suivants : Email, Numéro de téléphone, Prénom, Nom, Genre, Date de naissance, Ville, État, Code postal, Pays et Identifiant externe. L’extension ne hachera pas la valeur de ces champs si une chaîne SHA256 est déjà présente.

### [!UICONTROL Données personnalisées]

Les données personnalisées suivantes peuvent être saisies pour la règle :

| Nom du champ | Description |
| --- | --- |
| Devise | Code de devise ISO-4217. Si cette valeur n’est pas fournie, [!DNL Pinterest] sera défini par défaut sur la devise de l’annonceur définie lors de la création du compte. |
| Valeur | Valeur totale de l’événement. Acceptée comme chaîne dans la requête. Ce chiffre sera analysé dans un double chiffre. |
| Chaîne de recherche | Chaîne de recherche associée à l’événement de conversion de l’utilisateur. |
| ID de commande | ID de commande. L&#39;envoi de `order_id` aidera [!DNL Pinterest] à dédupliquer les événements si nécessaire. |
| Nombre de produits | Nombre total de produits de l’événement. Par exemple, le nombre total d’articles achetés dans un événement de passage en caisse. |
| ID de contenu | Liste (tableau) des ID de produits. |
| Contenu | Liste (tableau) d’objets contenant des informations sur les produits, telles que le prix et la quantité. |

![&#x200B; [!DNL Pinterest] [!UICONTROL Données personnalisées] surlignées dans l’action de règle.](../../../images/extensions/server/pinterest/custom-data.png)

## Validation des données dans [!DNL Pinterest]

Une fois la règle de transfert d’événement créée et exécutée, vérifiez si l’événement envoyé à l’API [!DNL Pinterest] s’affiche comme prévu dans l’interface utilisateur de [!DNL Pinterest].

Si la collecte d’événements et l’intégration de [!DNL Experience Platform] ont réussi, des événements s’affichent dans l’interface utilisateur de [!DNL Pinterest].

![Le [!DNL Pinterest] gestionnaire d’événements](../../../images/extensions/server/pinterest/event-history.png)

Vous pouvez approfondir l’analyse et afficher la distribution des données d’événement [!DNL Pinterest].

![La [!DNL Pinterest] distribution de données](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Étapes suivantes

Ce guide explique comment installer et configurer l’extension de transfert d’événement [!DNL Pinterest] dans l’interface utilisateur. Pour plus d&#39;informations, consultez la documentation officielle :

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Présentation de l’API de conversion](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
