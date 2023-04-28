---
keywords: extension de transfert d’événement;pinterest;extension de transfert d’événement pinterest
title: Extension de transfert d’événement pinterest
description: Cette extension de transfert d’événement Adobe Experience Platform vous permet d’ingérer des événements dans Pinterest en fonction de vos besoins.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 7%

---

# Extension de transfert d’événement [!DNL Pinterest]

[!DNL Pinterest] est un moteur de découverte visuelle qui permet de trouver des idées telles que des recettes, des décors maison, des modèles inspirés, etc. Il y a des milliards de pin&#39;s sur [!DNL Pinterest], qui peut également être partagé avec d’autres utilisateurs de [!DNL Pinterest]. Vous pouvez rassembler les événements d’interaction de l’utilisateur et exploiter les [!DNL Pinterest Analytics] pour comprendre le comportement des utilisateurs et exécuter des publicités ciblées.

Le [[!DNL Pinterest] Conversions](https://developers.pinterest.com/docs/conversions/conversion-management/) API [transfert d’événement](../../../ui/event-forwarding/overview.md) l’extension vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL Pinterest]. Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités à votre transfert d’événement. [rules](../../../ui/managing-resources/rules.md).

Les jetons d’accès aux conversions sont la méthode d’authentification utilisée par [!DNL Pinterest] lors de l’interaction avec la variable [!DNL Pinterest] API.

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données du réseau Edge dans [!DNL Pinterest] pour tirer parti de ses fonctionnalités d’analyse client.

Prenons l’exemple d’une équipe marketing au sein d’une organisation. L’équipe capture les données d’événement d’interaction utilisateur de son site web et les charge dans [!DNL Pinterest] en utilisant cette extension de transfert d’événement.

Les équipes marketing et d’analyse peuvent alors tirer parti des [!DNL Pinterest] Fonctionnalités d’Analytics permettant de comprendre les principales interactions et le comportement des utilisateurs, ce qui vous permet de mieux comprendre les utilisateurs et de les cibler pour des campagnes publicitaires ciblées.

Pour plus d’informations sur les cas d’utilisation spécifiques à [!DNL Pinterest], reportez-vous à la section [[!DNL Pinterest] cas d’utilisation](https://business.pinterest.com/en/success-stories) documentation.

## Conditions préalables de [!DNL Pinterest] {#prerequisites}

Vous devez disposer d’un [!DNL Pinterest] [compte commercial](https://help.pinterest.com/en/business/article/get-a-business-account) afin d’utiliser cette extension. Accédez au [[!DNL Pinterest] page d’enregistrement](https://www.pinterest.com/business/create/) pour enregistrer et créer un compte si vous n’en avez pas déjà un.

Vous aurez également besoin d’une [!DNL Pinterest] , qui doit être associé à votre [!DNL Pinterest] compte professionnel. Pour associer votre compte de développeur à votre compte d’entreprise, reportez-vous à la section [[!DNL Pinterest ] compte développeur](https://developers.pinterest.com/account-setup/).

### Collecte des détails de configuration requis {#configuration-details}

Pour connecter l’Experience Platform à [!DNL Pinterest], les entrées suivantes sont requises :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant de compte Ads | Votre [!DNL Pinterest] Identifiant De Compte Ads. Reportez-vous à la documentation de [[!DNL Pinterest] ](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) pour obtenir des conseils. | 123456789012 |
| Jeton d’accès à la conversion | Votre [!DNL Pinterest] Jeton d’accès à la conversion. Reportez-vous à la section [[!DNL Pinterest] API de conversion](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) document à titre indicatif. <br> **Vous n’aurez besoin de le faire qu’une seule fois, car ce jeton n’expire pas.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installez et configurez le [!DNL Pinterest] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionner **[!UICONTROL Installer]** sur la carte de la variable [!DNL Pinterest] dans l’extension **[!UICONTROL Catalogue]** .

![Catalogue affichant le [!DNL Pinterest] extension avec [!UICONTROL Installer] surlignée.](../../../images/extensions/server/pinterest/install.png)

### Configuration de l’extension [!DNL Pinterest]

>[!IMPORTANT]
>
>En fonction des besoins de mise en oeuvre, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Extensions]**. Sélectionner **[!UICONTROL Configurer]** sur la carte de la variable [!DNL Pinterest] dans l’extension [!UICONTROL Installé]Onglet **.

![[!DNL Pinterest] l’extension affichée dans la [!UICONTROL Installer] avec [!UICONTROL Configurer] surlignée.](../../../images/extensions/server/pinterest/configure.png)

Dans l’écran suivant, saisissez la variable [!UICONTROL Identifiant de compte Ads] et [!UICONTROL Jeton d’accès à la conversion] que vous avez précédemment rassemblé dans la variable [détails de configuration](#configuration-details) . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Le [!DNL Pinterest] [!UICONTROL Configurer] mise en surbrillance de l’écran [!UICONTROL Identifiant de compte Ads] et [!UICONTROL Jeton d’accès à la conversion] champs de saisie.](../../../images/extensions/server/pinterest/input.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Pinterest].

Créer [règle](../../../ui/managing-resources/rules.md) dans la propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Pinterest]**. Pour envoyer des événements Adobe Experience Edge Network à [!DNL Pinterest], définissez la variable **[!UICONTROL Type d’action]** to **[!UICONTROL Envoyer un événement].**

![Le [!DNL Pinterest] [!UICONTROL Envoyer un événement] création de règles.](../../../images/extensions/server/pinterest/rule.png)

Une fois la sélection effectuée, d’autres commandes s’affichent pour configurer davantage l’événement. Vous devez mapper la variable [!DNL Pinterest] propriétés d’événement aux éléments de données que vous avez précédemment créés.

### [!UICONTROL Données d’événement]

Les données d’événement suivantes seront nécessaires pour créer la règle :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL Nom de l’événement] | Type de l’événement utilisateur. Il peut toutefois s’agir de n’importe quel type d’événement pour tirer parti de [!DNL Pinterest Analytics] il est recommandé d’utiliser [[!DNL Pinterest] codes d’événement](https://help.pinterest.com/en/business/article/add-event-codes) | * paiement <br> * add_to_cart <br> * page_visit <br> * inscription <br> * [Événement défini par l’utilisateur] |
| [!UICONTROL Action Source] | Source indiquant où l’événement de conversion s’est produit. | * app_android <br> * app_ios <br> * web <br> * hors ligne |
| [!UICONTROL Heure de l’événement] | Cela fait référence à l’heure de l’événement. Le format d’heure par défaut utilisé est UNIX, au format `<seconds>.<miliseconds>` selon votre fuseau horaire local. Pour plus d’informations, reportez-vous à la section [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | La version 1433188255.500 indique 1433188255 secondes et 500 millisecondes après l’époque, ou le lundi 1er juin 2015, à 7:50:17 h GMT. |
| [!UICONTROL Identifiant d’événement] | Chaîne d’identifiant unique qui identifie cet événement et peut être utilisée pour dédupliquer les événements ingérés à la fois via l’API de conversion et le suivi Pinterest. Sans cela, les données de l’événement seront probablement comptabilisées deux fois et signaleront le gonflement des mesures. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propriétés de l’événement] | Objet JSON contenant des propriétés personnalisées de l’événement. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![Le [!DNL Pinterest] [!UICONTROL Données d’événement] surligné dans l’action de règle.](../../../images/extensions/server/pinterest/event-data.png)

Les propriétés d’événement suivantes peuvent être configurées :

| Nom du champ | Description |
| --- | --- |
| URL source de l’événement | URL de l’événement de conversion web. |
| ID de magasin d’applications | Identifiant de l’application de la boutique d’applications. |
| Nom de l’application | Nom de l’application  |
| Application Version | Version de l’application. |
| Marque du périphérique | Marque de l’appareil utilisé par l’utilisateur. |
| Opérateur de périphérique | Opérateur de téléphonie mobile de l’utilisateur pour son appareil. |
| Modèle de périphérique | Modèle de l’appareil de l’utilisateur. |
| Device Type | Type de périphérique utilisé par l’utilisateur. |
| Version du système d’exploitation | Version du système d’exploitation du périphérique. |
| Langue de l’utilisateur | Code de langue ISO-639-1 à deux caractères indiquant la langue de l’utilisateur. |

### [!UICONTROL Données utilisateur]

Les données utilisateur suivantes peuvent être saisies à l’aide de ne sont pas des champs obligatoires :

| Nom du champ | Description | Exemple |
| --- | --- | --- | 
| [!UICONTROL E-mail.] | Adresse électronique de l’utilisateur ou hachage SHA256 de l’adresse électronique de l’utilisateur. | ebd543592..f2b7e1 |
| [!UICONTROL Identifiants de publicité mobile] | hachages Sha256 des &quot;identifiants de publicité Google&quot; (GAID) ou &quot;identifiant Apple pour les annonceurs&quot; (IDFA) de l’utilisateur ; | ebd543592..f2b7e1 |
| [!UICONTROL Adresse IP du client] | Adresse IP de l’utilisateur, qui peut être au format IPv4 ou IPv6. Utilisé pour la correspondance. | 192.168.0.1 |
| [!UICONTROL Agent utilisateur client] | Chaîne de l’agent utilisateur du navigateur web de l’utilisateur. | Mozilla/5.0 (plateforme); rv:geckoversion) Gecko/geckotrail Firefox/firefox/firefoxversion |
| [!UICONTROL Données sur les clients] | Objet JSON contenant d’autres informations sur le client. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | { &quot;ph&quot;: &quot;122333445&quot; } |

![Le [!DNL Pinterest] [!UICONTROL Données utilisateur] surligné dans l’action de règle.](../../../images/extensions/server/pinterest/user-data.png)

Les propriétés d’informations sur les clients qui peuvent être configurées sont les suivantes :

| Nom du champ | Description |
| --- | --- |
| Téléphone | Numéro de contact de l&#39;utilisateur. Seuls les chiffres sont acceptés et doivent être renseignés avec l&#39;indicatif du pays, l&#39;indicatif régional et le numéro. |
| Genre | Le genre peut être renseigné en tant que &quot;f&quot; pour féminin, &quot;m&quot; pour masculin ou &quot;n&quot; pour non-binaire. |
| Date de naissance | Date de naissance, saisie sous forme d’année, de mois et de jour. |
| Nom | Nom de l’utilisateur. |
| Prénom | Prénom de l’utilisateur. |
| Ville | Ville de résidence de l’utilisateur. Il est principalement utilisé à des fins de facturation. |
| State (État) | État de l’utilisateur, fourni en minuscules sous forme de code à deux lettres. |
| Code postal | Code postal de l’utilisateur, principalement utilisé à des fins de facturation. |
| Pays | Code de pays ISO-3166 à deux caractères indiquant le pays de l’utilisateur. |
| Identifiant externe | Identifiant unique de l’annonceur qui identifie un utilisateur dans son espace. Par exemple, identifiant utilisateur, identifiant de fidélité, etc. |
| ID de clic | Identifiant unique stocké dans le cookie _epik sur votre domaine ou le paramètre de requête &amp;epik= dans l’URL. |

>[!IMPORTANT]
>
>Avant d’envoyer les données à la variable [!DNL Pinterest] Point d’entrée de l’API, l’extension hachera et normalisera les valeurs des champs suivants : E-mail, numéro de téléphone, prénom, nom, genre, date de naissance, ville, état, code postal, pays et ID externe. L’extension ne hachera pas la valeur de ces champs si une chaîne SHA256 est déjà présente.

### [!UICONTROL Données personnalisées]

Les données personnalisées suivantes peuvent être saisies pour la règle :

| Nom du champ | Description |
| --- | --- |
| Devise | Code de devise ISO-4217. Si elle n’est pas fournie, [!DNL Pinterest] est définie par défaut sur la devise de l’annonceur définie lors de la création du compte. |
| Valeur | Valeur totale de l’événement. Acceptée comme chaîne dans la requête. Ce chiffre sera analysé dans un double chiffre. |
| Chaîne de recherche | Chaîne de recherche associée à l’événement de conversion de l’utilisateur. |
| ID de commande | ID de commande. Envoi `order_id` help [!DNL Pinterest] dédupliquez les événements si nécessaire. |
| Nombre de produits | Nombre total de produits de l’événement. Par exemple, le nombre total d’articles achetés dans un événement de passage en caisse. |
| ID de contenu | Liste (tableau) des ID de produits. |
| Contenu | Liste (tableau) d’objets contenant des informations sur les produits, telles que le prix et la quantité. |

![Le [!DNL Pinterest] [!UICONTROL Données personnalisées] surligné dans l’action de règle.](../../../images/extensions/server/pinterest/custom-data.png)

## Validation des données dans [!DNL Pinterest]

Une fois la règle de transfert d’événement créée et exécutée, vérifiez si l’événement envoyé à la variable [!DNL Pinterest] L’API s’affiche comme prévu dans la variable [!DNL Pinterest] Interface utilisateur.

Si la collecte d’événements et [!DNL Experience Platform] l’intégration a réussi, vous verrez des événements dans la variable [!DNL Pinterest] Interface utilisateur.

![Le [!DNL Pinterest] gestionnaire d&#39;événements](../../../images/extensions/server/pinterest/event-history.png)

Vous pouvez approfondir l’analyse et afficher les [!DNL Pinterest] distribution des données d’événement.

![Le [!DNL Pinterest] répartition des données](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Étapes suivantes

Ce guide explique comment installer et configurer le [!DNL Pinterest] extension de transfert d’événement dans l’interface utilisateur. Pour plus d&#39;informations, consultez la documentation officielle :

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Présentation de l’API de conversion](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
