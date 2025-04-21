---
title: Extension de l’API Conversions d’Adobe Amazon
description: Cette API d’événements web Adobe Experience Platform vous permet de partager des interactions de site web directement avec Amazon.
last-substantial-update: 2025-04-17T00:00:00Z
source-git-commit: 65a3eb20dc3de62319f73be49197dacb8fc1778b
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 2%

---

# Présentation de l’extension d’API d’événements web [!DNL Amazon]

L’extension [!DNL Amazon] Conversions API crée une connexion directe entre les données marketing du serveur d’un annonceur et [!DNL Amazon]. Cela permet aux annonceurs d’évaluer l’efficacité des campagnes indépendamment de l’emplacement de conversion et d’optimiser les campagnes en conséquence. L’extension permet une attribution plus complète, une fiabilité des données améliorée et une diffusion mieux optimisée.

## Conditions préalables de [!DNL Amazon] {#prerequisites}

Avant d’installer et de configurer l’extension d’API [!DNL Amazon] Conversions, vous devez effectuer plusieurs étapes préalables pour garantir une authentification et un accès aux données corrects.

### Créer un secret et un élément de données {#secret}

L’authentification avec [!DNL Amazon] nécessite un jeton sécurisé qui doit être correctement stocké et référencé :

1. Créez un secret de transfert d’événement [!DNL Amazon] avec un nom unique pour l’authentification.
2. Créez un élément de données à l’aide de l’extension **Core** avec un type d’élément de données **Secret** pour référencer votre secret [!DNL Amazon].

Ce processus garantit que vos informations d’authentification restent sécurisées tout en restant accessible à l’extension si nécessaire.

## Installation et configuration de l’extension [!DNL Amazon]

L’installation de l’extension nécessite l’accès à votre propriété de transfert d’événement dans Experience Platform :

- Créez ou modifiez une propriété de transfert d’événement.
- Sélectionnez **Extensions** dans le volet de navigation de gauche, puis sélectionnez [!DNL Amazon] extension dans l’onglet Catalogue.
- Sélectionnez **Installer**.

![[!DNL Amazon]’extension sélectionnée dans le catalogue d’extensions avec le bouton d’installation.](../../../images/extensions/server/amazon/amazon-extension.png)

- Configurez avec :

- **Jeton d’accès** : secret de l’élément de données contenant le jeton OAuth 2

![Paramètres individuels pour saisir le secret de l’élément de données mis en surbrillance.](../../../images/extensions/server/amazon/2.png)

- **Identifiant d’entité** : votre identifiant d’entité (figurant dans l’URL du portail Campaign Manager avec le préfixe « entity »)

![Le portail du gestionnaire de campagnes dans le volet de navigation de gauche.](../../../images/extensions/server/amazon/3.png)

- Sélectionnez **Enregistrer**.

Ces valeurs de configuration établissent la connexion entre Platform et votre compte [!DNL Amazon].

### [!DNL Amazon] OAuth 2 {#oauth}

Pour créer un secret OAuth 2 [!DNL Amazon] :

- Sélectionnez [!DNL Amazon] OAuth 2 dans la liste déroulante **Type** et sélectionnez **Créer un secret**.

![Amazon OAuth 2 dans le menu déroulant.](../../../images/extensions/server/amazon/Oauth.png)

- Sélectionnez **Créer et autoriser un secret avec Amazon** dans la fenêtre contextuelle pour autoriser manuellement le secret et continuer.

![Créer et autoriser un secret avec Amazon sélectionné.](../../../images/extensions/server/amazon/Oauth.1.png)

- Saisissez vos informations d’identification [!DNL Amazon] dans la boîte de dialogue qui s’affiche. Suivez les invites pour accorder l’accès au transfert d’événement à vos données.

Une fois l’opération terminée, votre secret avec son statut et sa date d’expiration s’affiche dans l’onglet **Secrets**.

![Secret créé dans l’onglet Secrets.](../../../images/extensions/server/amazon/Oauth.2.png)

## Configurer une règle de transfert d’événement {#config-rule}

Une fois tous vos éléments de données configurés, vous pouvez créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à Amazon.

- Accédez à **Règles** et créez une règle de transfert d’événement.
- Sous **Actions**, sélectionnez **Extension de l’API Conversions Amazon**.
- Définissez le **Type d’action** sur **Importer les événements de conversion**.

![Les options de configuration d’action sont mises en surbrillance.](../../../images/extensions/server/amazon/4.png)

- Configurez les propriétés d’événement comme indiqué ci-dessous :

| Entrée | Description |
| --- | --- |
| **Nom de l’événement** | Nom de l’événement de conversion. |
| **Event Type** (Type d’événement) | Définit le type d’événement suivi (par exemple, achats, ajouts au panier). |
| **Horodatage** | Heure de l’événement au format ISO. |
| **ID de déduplication client** | Identifiant unique pour la déduplication. |
| **Clés de correspondance** | Identifiants utilisateur et appareil pour l’attribution. |
| **Valeur** | Valeur monétaire de l’événement. |
| **Code de devise** | Devise au format ISO-4217. |
| **Unités vendues** | Quantité d&#39;articles achetés. |
| **Code Pays** | Pays où l’événement s’est produit. |
| **Options de traitement des données** | Indicateurs pour une utilisation limitée des données. |
| **Consentement** | Indique le consentement de l’utilisateur pour l’utilisation des données publicitaires. |

- Sélectionnez **Conserver les modifications** pour enregistrer la règle.

![Paramètres d’événement dans la configuration d’action mis en surbrillance avec le bouton Conserver les modifications.](../../../images/extensions/server/amazon/5.png)

![Paramètres d’événement supplémentaires dans la configuration d’action mis en surbrillance avec le bouton Conserver les modifications.](../../../images/extensions/server/amazon/6.png)

## Déduplication des événements {#deduplication}

Si vous utilisez [!DNL Amazon] balise Advertising (AAT) et l’extension de l’API [!DNL Amazon] Conversions pour les mêmes événements, la configuration de la déduplication est requise. Incluez des `clientDedupeId` dans chaque événement partagé pour garantir une déduplication adéquate.
La déduplication n’est pas nécessaire si les événements client et serveur ne se chevauchent pas.

Une déduplication appropriée évite les nombres de conversions exagérés et garantit que les données d’optimisation restent précises.

Pour plus d’informations](https://advertising.amazon.com/) consultez le [Guide de déduplication des événements d’Amazon .

## Étapes suivantes

Ce guide explique comment configurer et envoyer des événements de conversion à [!DNL Amazon] à l’aide de l’extension d’API [!DNL Amazon] Conversions. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans [!DNL Adobe Experience Platform], consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md)

Pour plus d’informations sur le débogage de votre implémentation à l’aide du débogueur Experience Platform et de l’outil de surveillance du transfert d’événement, lisez la [présentation d’Adobe Experience Platform Debugger](https://experienceleague.adobe.com/en/docs/experience-platform/debugger/home) et [activités de surveillance](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring) dans le transfert d’événement.