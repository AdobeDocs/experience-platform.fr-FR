---
keywords: extension de transfert d’événement;twitter;extension de transfert d’événement de twitter
title: Extension de transfert d’événement de twitter
description: Cette extension de transfert d’événement Adobe Experience Platform vous permet d’ingérer des événements en Twitter pour répondre aux besoins de votre entreprise.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 7%

---

# Extension de transfert d’événement [!DNL Twitter]

[[!DNL Twitter]](https://twitter.com/i/flow/login) est un service en ligne de médias sociaux et de réseaux sociaux, sur lequel les utilisateurs publient et interagissent avec des messages de 280 caractères, appelés tweets. Les utilisateurs peuvent interagir avec Twitter à l’aide d’un navigateur, d’un logiciel frontal mobile ou par programmation via son [API](https://developer.twitter.com/en/docs/twitter-api)

La variable [!DNL Twitter] API de conversion web [transfert d’événement](../../../ui/event-forwarding/overview.md) l’extension vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL Twitter]. Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités à votre transfert d’événement. [rules](../../../ui/managing-resources/rules.md).

[!DNL Twitter] require [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) pour l’authentification avec le [!DNL Twitter] [!DNL Web Conversions] API.

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données du réseau Edge dans [!DNL Twitter] pour tirer parti de ses capacités de ciblage et d’analyse client.

Prenons l’exemple d’une équipe marketing au sein d’une organisation. L’équipe capture les données d’événement d’interaction utilisateur de son site web en tant que données d’événement de son site web et les charge dans [!DNL Twitter] en utilisant cette extension de transfert d’événement.

Les équipes marketing et d’analyse peuvent alors tirer parti des [!DNL Twitter's] fonctionnalités permettant d’effectuer une analyse supplémentaire et de cibler ces utilisateurs pour des campagnes publicitaires ciblées.

Pour plus d’informations sur les cas d’utilisation spécifiques à [!DNL Twitter], reportez-vous au [[!DNL Twitter] cas d’utilisation](https://developer.twitter.com/en/use-cases/build-for-businesses) la documentation.

## [!DNL Twitter] conditions préalables et barrières de sécurité {#prerequisites}

Vous devez disposer d’un [!DNL Twitter] afin d’utiliser cette extension. Accédez au [[!DNL Twitter] page d’enregistrement](https://help.twitter.com/en/using-twitter/create-twitter-account) pour enregistrer et créer un compte si vous n’en avez pas déjà un.

Vous devez configurer votre compte en tant que [!DNL Twitter] compte développeur. Pour savoir comment vous inscrire en tant que développeur, reportez-vous à la section [[!DNL Twitter] compte développeur](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Protections des API {#guardrails}

La variable [!DNL Twitter] L’API de conversion web est limitée à 60 000 requêtes par intervalle de 15 minutes, où chaque requête autorise 500 événements.

### Collecte des détails de configuration requis {#configuration-details}

Pour connecter l’Experience Platform à [!DNL Twitter], les entrées suivantes sont requises :

| Type de clé | Description |
| --- | --- |
| Clé client | &#x200B; Clé API de l’application permettant d’accéder au [!DNL Twitter] API. Voir [!DNL Twitter] documentation sur [clés et secrets d’api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) pour obtenir des conseils. | |
| Secret du client | Le secret d’API permet à votre application d’accéder à [!DNL Twitter] API. Voir [!DNL Twitter] documentation sur [clés et secrets d’api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) pour obtenir des conseils. |
| Secret du jeton | Le secret du jeton non expirant de votre application, qui est utilisé pour l’authentification au [!DNL Twitter] API via OAuth. Voir [!DNL Twitter] documentation sur [obtention des jetons d’accès d’utilisation](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) pour obtenir des conseils. |
| Jeton d’accès | Jeton d’accès non expirant de votre application, utilisé pour l’authentification au [!DNL Twitter] API via OAuth. Voir [!DNL Twitter] documentation sur [obtention des jetons d’accès d’utilisation](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) pour obtenir des conseils. |
| Pixel Id | La variable [!DNL Twitter] Pixel est une balise de site web qui est implémentée sur votre site web pour effectuer le suivi des actions ou des conversions du site. Voir [!DNL Twitter] documentation sur [suivi des conversions pour les sites web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) pour obtenir des conseils. |

## Installez et configurez le [!DNL Twitter] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** onglet, sélectionnez **[!UICONTROL Installer]** sur la carte de la variable [!DNL Twitter] extension .

![Catalogue affichant le [!DNL Twitter] installation de mise en surbrillance de l’extension.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>En fonction des besoins de mise en oeuvre, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Dans l’écran suivant, saisissez ce qui suit : [valeurs de configuration](#configuration-details) que vous avez précédemment rassemblé à partir de [!DNL Twitter]:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Clé client]**
* **[!UICONTROL Secret du client]**
* **[!UICONTROL Jeton]**
* **[!UICONTROL Secret du jeton]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![[!DNL Twitter] écran de configuration pour la [!DNL Twitter] extension .](../../../images/extensions/server/twitter/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Twitter].

Créer [règle](../../../ui/managing-resources/rules.md) dans la propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Twitter]**. Pour envoyer des événements Edge Network à [!DNL Twitter], définissez la variable **[!UICONTROL Type d’action]** to **[!UICONTROL Envoyer la conversion web].**

Une fois la sélection effectuée, d’autres commandes s’affichent pour configurer davantage l’événement. Vous devez mapper la variable [!DNL Twitter] propriétés d’événement aux éléments de données que vous avez précédemment créés. Pour plus d’informations, voir la section [[!DNL Twitter] API de conversion web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![La variable [!DNL Twitter] création d’une règle d’événement de conversion.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identification de l’utilisateur]**

| Nom du champ | Description | Exemple | Obligatoire |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID de clic] | [!DNL Twitter] Cliquez sur ID tel qu’analysé dans l’URL du clic publicitaire. | 26l6412g5p4iyj65a2oic2ayg2 | Obligatoire si aucun autre identifiant n’est ajouté. |
| [!UICONTROL E-mail.] | Adresse électronique hachée avec SHA256. Le texte doit être en minuscules et les espaces à la fin ou au début doivent être supprimés avant le hachage. | eventforwarding@example.com | Obligatoire si aucun autre identifiant n’est ajouté. |
| [!UICONTROL Phone] | Phone sert d’identifiant pour correspondre à l’événement de conversion. Le numéro de téléphone doit être au format E164 [+][code pays][code zone][local phone number] avant le hachage. | +911234567875 | Obligatoire si aucun autre identifiant n’est ajouté. |

**[!UICONTROL Données de conversion]**

| Nom du champ | Description | Exemple | Obligatoire |
| --- | --- | --- | --- |
| [!UICONTROL Temps de conversion] | Date-time sous forme de chaîne dans ISO 8601 ou dans `yyyy-MM-dd'T'HH:mm:ss:SSSZ` format. | 2022-02-18T01:14:00.603Z | Oui |
| [!UICONTROL Identifiant d’événement] | ID de base 36 d’un événement spécifique. Cet identifiant doit correspondre à un événement préconfiguré contenu dans votre [!DNL Twitter] compte publicitaire. Il s’agit de l’identifiant de l’événement correspondant dans le Gestionnaire d’événements. | o87ne ou tw-o8z6j-o87ne (tw-pixel_id-event-id) | Oui |
| [!UICONTROL Nombre d’éléments] | Nombre d’éléments achetés dans l’événement. Il doit s’agir d’un nombre positif supérieur à 0. | 4 | Non |
| [!UICONTROL Devise] | Devise des éléments achetés dans l’événement. Elle est exprimée dans la norme ISO-4217 et, si elle n’est pas fournie, la valeur par défaut est USD. | USD | Non |
| [!UICONTROL Valeur] | Valeur du prix des articles achetés dans l’événement. | 100,00 | Non |
| [!UICONTROL ID de conversion] | Identifiant d’un événement de conversion pouvant être utilisé pour la déduplication entre les conversions de l’API de conversion et de pixel web dans la même balise d’événement. | 23294827 | Non |
| [!UICONTROL Description] | Description contenant des informations supplémentaires sur les conversions. | Test de la conversion | Non |

## Validation des données dans [!DNL Twitter]

Une fois la règle de transfert d’événement créée et exécutée, vérifiez si l’événement envoyé à la variable [!DNL Twitter] L’API s’affiche comme prévu dans [!DNL Twitter] Interface utilisateur.

Si la collecte d’événements et [!DNL Experience Platform] l’intégration a réussi, vous verrez des événements dans la variable [!DNL Twitter] [!UICONTROL Gestionnaire d’événements].

![La variable [!DNL Twitter] gestionnaire d&#39;événements](../../../images/extensions/server/twitter/event-manager.png)

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Twitter] à l’aide du transfert d’événement. Pour plus d&#39;informations sur ces technologies sous-jacentes, consultez la documentation officielle :

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversion Web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Jeton d’accès utilisateur](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel ID et suivi de conversion](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
