---
title: Notes de mise à jour relatives aux balises et au transfert d’événements
description: Dernières notes de mise à jour concernant les balises et le transfert d’événement dans Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 2b11fb87523c777d5c2d855e97a4af78a8483abe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 100%

---

# Notes de mise à jour relatives aux balises et au transfert d’événements

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