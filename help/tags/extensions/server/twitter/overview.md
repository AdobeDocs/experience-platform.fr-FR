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

[[!DNL Twitter]](https://twitter.com/i/flow/login) est un service de réseaux sociaux en ligne, sur lequel les utilisateurs publient et interagissent avec des messages de 280 caractères, appelés tweets. Les utilisateurs peuvent interagir avec Twitter à l’aide d’un navigateur, d’un logiciel frontal mobile ou par programmation via ses [API](https://developer.twitter.com/en/docs/twitter-api)

L’extension [!DNL Twitter] Web Conversions API [ de transfert d’événement](../../../ui/event-forwarding/overview.md) vous permet d’exploiter les données capturées dans l’Edge Network Adobe Experience Platform et de les envoyer à [!DNL Twitter]. Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités dans le transfert d’événement [rules](../../../ui/managing-resources/rules.md).

[!DNL Twitter] nécessite [ OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) pour l&#39;authentification avec l&#39;API [!DNL Twitter] [!DNL Web Conversions].

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données de l’Edge Network dans [!DNL Twitter] pour tirer parti de ses fonctionnalités d’analyse et de ciblage des clients.

Prenons l’exemple d’une équipe marketing au sein d’une organisation. L’équipe capture les données d’événement d’interaction de l’utilisateur de son site web en tant que données d’événement de son site web et les charge dans [!DNL Twitter] à l’aide de cette extension de transfert d’événement.

Les équipes de marketing et d’analyse peuvent ensuite exploiter les fonctionnalités [!DNL Twitter's] pour effectuer une analyse supplémentaire et cibler ces utilisateurs pour les campagnes de publicité ciblées.

Pour plus d&#39;informations sur les cas d&#39;utilisation spécifiques à [!DNL Twitter], consultez la documentation [[!DNL Twitter] Cas d&#39;utilisation](https://developer.twitter.com/en/use-cases/build-for-businesses) .

## [!DNL Twitter] conditions préalables et barrières de sécurité {#prerequisites}

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Twitter] valide. Accédez à la [[!DNL Twitter] page d&#39;inscription](https://help.twitter.com/en/using-twitter/create-twitter-account) pour vous enregistrer et créer un compte si vous n&#39;en avez pas déjà un.

Vous devez configurer votre compte en tant que compte de développeur [!DNL Twitter]. Pour savoir comment vous inscrire en tant que développeur, reportez-vous au [[!DNL Twitter] compte développeur](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### Protections des API {#guardrails}

L’API de conversion web [!DNL Twitter] a une limite de taux de 60 000 demandes par intervalle de 15 minutes, où chaque demande autorise 500 événements.

### Collecte des détails de configuration requis {#configuration-details}

Pour connecter l’Experience Platform à [!DNL Twitter], les entrées suivantes sont requises :

| Type de clé | Description |
| --- | --- |
| Clé client | &#x200B; Clé API de l’application pour accéder à l’API [!DNL Twitter]. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Twitter] sur les [clés et secrets d&#39;api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) . | |
| Secret du client | Le secret API permet à votre application d’accéder à l’API [!DNL Twitter]. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Twitter] sur les [clés et secrets d&#39;api](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) . |
| Secret du jeton | Secret de jeton non expirant de votre application, utilisé pour l’authentification à l’API [!DNL Twitter] via OAuth. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Twitter] sur l&#39; [obtention des jetons d&#39;accès à l&#39;utilisation](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) . |
| Jeton d’accès | Jeton d’accès non expirant de votre application, utilisé pour l’authentification à l’API [!DNL Twitter] via OAuth. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Twitter] sur l&#39; [obtention des jetons d&#39;accès à l&#39;utilisation](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) . |
| Pixel Id | Le pixel [!DNL Twitter] est une balise de site web qui est implémentée sur votre site web pour suivre les actions ou les conversions du site. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Twitter] sur le [suivi de conversion pour les sites web](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) . |

## Installation et configuration de l’extension [!DNL Twitter] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier à la place.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]** , sélectionnez **[!UICONTROL Installer]** sur la carte de l’extension [!DNL Twitter].

![Catalogue présentant l’installation de mise en surbrillance de l’extension [!DNL Twitter].](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>En fonction des besoins de mise en oeuvre, vous devrez peut-être créer un schéma, des éléments de données et un jeu de données avant de configurer l’extension. Avant de commencer, consultez toutes les étapes de configuration afin de déterminer les entités à configurer pour votre cas d’utilisation.

Sur l’écran suivant, saisissez les [valeurs de configuration](#configuration-details) suivantes que vous avez précédemment collectées à partir de [!DNL Twitter] :

* **[!UICONTROL Id Pixel]**
* **[!UICONTROL Clé client]**
* **[!UICONTROL Secret du client]**
* **[!UICONTROL Jeton]**
* **[!UICONTROL Jeton Secret]**

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

Écran de configuration ![[!DNL Twitter] pour l’extension [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Twitter].

Créez une [règle](../../../ui/managing-resources/rules.md) dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Twitter]**. Pour envoyer des événements Edge Network à [!DNL Twitter], définissez le **[!UICONTROL Type d’action]** sur **[!UICONTROL Envoyer la conversion web].**

Une fois la sélection effectuée, d’autres commandes s’affichent pour configurer davantage l’événement. Vous devez mapper les propriétés d’événement [!DNL Twitter] aux éléments de données que vous avez précédemment créés. Pour plus d’informations, reportez-vous à l’ [[!DNL Twitter]  API de conversion web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![ [!DNL Twitter] créant une règle d’événement de conversion.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Identification de l’utilisateur]**

| Nom du champ | Description | Exemple | Obligatoire |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] ID de clic] | [!DNL Twitter] ID de clic tel qu’analysé à partir de l’URL de clic publicitaire. | 26l6412g5p4iyj65a2oic2ayg2 | Obligatoire si aucun autre identifiant n’est ajouté. |
| [!UICONTROL E-mail.] | Adresse électronique hachée avec SHA256. Le texte doit être en minuscules et les espaces à la fin ou au début doivent être supprimés avant le hachage. | eventforwarding@example.com | Obligatoire si aucun autre identifiant n’est ajouté. |
| [!UICONTROL Phone] | Phone sert d’identifiant pour correspondre à l’événement de conversion. Le numéro de téléphone doit être au format E164 [+][code pays][code zone][local phone number] avant le hachage. | +911234567875 | Obligatoire si aucun autre identifiant n’est ajouté. |

**[!UICONTROL Données de conversion]**

| Nom du champ | Description | Exemple | Obligatoire |
| --- | --- | --- | --- |
| [!UICONTROL Temps de conversion] | Date-time sous la forme d’une chaîne au format ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Oui |
| [!UICONTROL  {Event Id] | ID de base 36 d’un événement spécifique. Cet identifiant doit correspondre à un événement préconfiguré contenu dans votre compte publicitaire [!DNL Twitter]. Il s’agit de l’identifiant de l’événement correspondant dans le Gestionnaire d’événements. | o87ne ou tw-o8z6j-o87ne (tw-pixel_id-event-id) | Oui |
| [!UICONTROL Nombre d’éléments] | Nombre d’éléments achetés dans l’événement. Il doit s’agir d’un nombre positif supérieur à 0. | 4 | Non |
| [!UICONTROL Devise] | Devise des éléments achetés dans l’événement. Elle est exprimée dans la norme ISO-4217 et, si elle n’est pas fournie, la valeur par défaut est USD. | USD | Non |
| [!UICONTROL Valeur] | Valeur du prix des articles achetés dans l’événement. | 100,00 | Non |
| [!UICONTROL ID de conversion] | Identifiant d’un événement de conversion pouvant être utilisé pour la déduplication entre les conversions de l’API de conversion et de pixel web dans la même balise d’événement. | 23294827 | Non |
| [!UICONTROL Description] | Description contenant des informations supplémentaires sur les conversions. | Test de la conversion | Non |

## Validation des données dans [!DNL Twitter]

Une fois la règle de transfert d’événement créée et exécutée, vérifiez si l’événement envoyé à l’API [!DNL Twitter] s’affiche comme prévu dans l’interface utilisateur de [!DNL Twitter].

Si la collecte d’événements et l’intégration de [!DNL Experience Platform] ont réussi, vous verrez des événements dans le [!DNL Twitter] [!UICONTROL gestionnaire d’événements].

![Le [!DNL Twitter] gestionnaire d’événements](../../../images/extensions/server/twitter/event-manager.png)

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion vers [!DNL Twitter] à l’aide du transfert d’événement. Pour plus d&#39;informations sur ces technologies sous-jacentes, consultez la documentation officielle :

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API de conversion web](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Jeton d’accès utilisateur](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [ID de pixel et suivi de conversion](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
