---
title: Notes de mise à jour relatives aux balises et au transfert d’événements
description: Dernières notes de mise à jour concernant les balises et le transfert d’événement dans Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7f09da40d2ea84de6f21669bdda16c0175a63c1
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 86%

---

# Notes de mise à jour relatives aux balises et au transfert d’événements

## 26 avril 2023

* **Secret JWT OAuth**: Le [Secret JWT OAuth](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) permet aux clients d’utiliser des jetons Adobe et Google Service pour prendre en charge les interactions serveur à serveur dans le transfert d’événements.

La nouvelle extension suivante a été publiée :

* **[!DNL Pinterest Conversions API]extension**: Le [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) l’extension de transfert d’événement vous permet d’exploiter les données capturées dans Adobe Experience Platform Edge Network et de les envoyer à [!DNL Pinterest] sous la forme d’événements côté serveur à l’aide de la variable [!DNL Pinterest Conversions API].

## 29 mars 2023

**Workflows de démarrage rapide (Beta)**

Accédez aux nouveaux workflows de démarrage rapide sous « Prise en main » à partir de l’écran d’accueil Collecte de données. Les workflows suivants sont désormais disponibles pour les clientes et clients sous la forme d’une version Beta publique.
* **[API Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=fr#quick-start)** : les clientes et clients utilisant le transfert d’événement peuvent collecter et transférer rapidement des données d’événement côté serveur vers les métadonnées pour les conversions publicitaires en quelques étapes simples.
* **[SDK mobile](https://developer.adobe.com/client-sdks/documentation/)** : les clientes et clients peuvent rapidement implémenter le SDK mobile et valider les événements mobiles de base en quelques étapes simples.

De nouvelles extensions ont été publiées :

* Extension de transfert d’événement **[!DNL Braze]** : l’extension de transfert d’événement [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=fr) vous permet d’exploiter les données capturées sur le réseau Edge d’Adobe Experience Platform et de les envoyer à [!DNL Braze] sous la forme d’événements côté serveur à l’aide des API de suivi des utilisateurs [!DNL Braze].
* **[API des événements Epsilon] extension de transfert d’événement**: Le [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=fr) l’extension vous permet d’exploiter le transfert d’événement pour capturer des informations d’événement dans Adobe Experience Platform Edge Network et les envoyer à [!DNL Epsilon] en utilisant la variable [!DNL Epsilon] API d’événement.
* Extension de transfert d’événement **[!DNL Mixpanel]** : l’extension [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=fr)[!DNL Mixpanel] vous permet d’exploiter le transfert d’événement pour capturer des informations d’événement sur le réseau Edge d’Adobe Experience Platform et les envoyer à à l’aide de l’API de suivi des événements.

## 25 janvier 2023

* **Nouvel écran d’accueil** : la page d’accueil de l’interface utilisateur de collecte de données a été mise à jour afin d’inclure des informations d’intégration et des liens utiles pour optimiser la productivité. Cela inclut :
   1. Documentation et workflows recommandés pour commencer
   1. Propriétés, règles et éléments de données récents
   1. Extensions populaires
   1. Nouvelles mises à jour des extensions avec une fonction d’installation rapide
* **Envoi de données à [!DNL Google Ads] à l’aide du transfert d’événement** : vous pouvez désormais utiliser l’[[!DNL Google Ads Enhanced Conversions] extension d’API](../extensions/server/google-ads-enhanced-conversions/overview.md) pour le transfert d’événement, combiné avec les [secrets Google Oauth 2](../ui/event-forwarding/secrets.md#google-oauth2), pour envoyer en toute sécurité des données côté serveur à [!DNL Google Ads] en temps réel.

## 23 novembre 2022

* Extension **[!DNL AWS] pour le transfert d’événement** : vous pouvez désormais envoyer des données à [!DNL Amazon Web Services] ([!DNL AWS]) à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la [[!DNL AWS] présentation de l’extension](../../tags/extensions/server/aws/overview.md).
* Extension **[!DNL Google Ads Enhanced Conversions] pour le transfert d’événement** : vous pouvez désormais envoyer des données de conversion à [!DNL Google Ads] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la [[!DNL Google Ads Enhanced Conversions] présentation de l’extension](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md).
* Extension **[!DNL Microsoft Azure] pour le transfert d’événement** : vous pouvez désormais envoyer des données à [!DNL Microsoft Azure] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la [[!DNL Microsoft Azure] présentation de l’extension](../../tags/extensions/server/azure/overview.md).

## 26 octobre 2022

* **Gestion des données sensibles pour les flux de données** : les flux de données exploitent désormais plusieurs technologies Platform pour gérer de manière appropriée les données sensibles selon les applications des réglementations telles que le Health Insurance Portability and Accountability Act (HIPAA). Consultez la section relative à la [gestion des données sensibles dans les flux de données](../../edge/datastreams/overview.md#sensitive) pour plus d’informations.
* Extension **[!DNL Splunk] pour le transfert d’événement** : vous pouvez désormais envoyer des données à [!DNL Splunk] à l’aide d’une extension de [transfert d’événement](../ui/event-forwarding/overview.md). Pour plus d’informations, consultez la [[!DNL Splunk] présentation de l’extension](../extensions/server/splunk/overview.md).
* Extension **[!DNL Zendesk] pour le transfert d’événement** : vous pouvez désormais envoyer des données à [!DNL Zendesk] à l’aide d’une extension de [transfert d’événement](../ui/event-forwarding/overview.md). Pour plus d’informations, consultez la [[!DNL Zendesk] présentation de l’extension](../extensions/server/zendesk/overview.md).

## 28 septembre 2022

* **Intégration à la navigation de gauche d’Adobe Experience Platform** : toutes les fonctionnalités qui étaient auparavant exclusives à l’interface utilisateur de collecte de données (y compris les balises et le transfert d’événement) sont désormais également disponibles via la navigation de gauche dans l’interface utilisateur d’Experience Platform, sous la catégorie **[!UICONTROL Collecte de données]**. Il n’est donc pas nécessaire de basculer entre les interfaces utilisateur lors de l’utilisation des fonctionnalités de collecte de données dans Platform.
* **Attribution utilisateur dans les balises et le transfert d’événement** : lors de l’énumération des propriétés disponibles dans les balises et le transfert d’événement, chaque propriété répertoriée indique désormais la date de sa dernière mise à jour et la personne qui l’a effectuée.
* Extension **[[!DNL Snap Conversions API] ](https://exchange.adobe.com/apps/ec/108550) pour le transfert d’événement** : vous pouvez désormais envoyer des données à l’[!DNL Snapchat Conversions API] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations sur la configuration et l’utilisation de l’API, voir la [[!DNL Snapchat Marketing API] documentation dédiée](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juillet 2022

* L’accès aux fonctionnalités de balises et de transfert d’événement est désormais géré via Adobe Admin Console, sous la vignette correspondant à la collecte de données d’Adobe Experience Platform. Pour en savoir plus, consultez le guide des [autorisations relatives à la collecte de données](../../collection/permissions.md).
* La prise en charge d’Internet Explorer 10 et 11 est [obsolète](../ie-deprecation.md).

## 22 juin 2022

De nouvelles extensions ont été publiées :

* [Extension de balise de la couche de données Google](../extensions/client/google-data-layer/overview.md) : elle vous permet d’utiliser une couche de données Google lorsque vous implémentez des balises.
* [Extension de transfert d’événement Google Ads Enhanced Conversions](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html) : elle permet d’améliorer vos conversions Google Ads en temps réel.
* [Extension de transfert d’événement Mailchimp](../extensions/server/mailchimp/overview.md) : elle envoie des événements à l’API marketing Mailchimp qui peut déclencher des e-mails pour les campagnes marketing, les parcours ou les transactions Mailchimp.