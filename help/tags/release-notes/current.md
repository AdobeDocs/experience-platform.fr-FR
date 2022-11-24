---
title: Notes de mise à jour relatives aux balises et au transfert d’événements
description: Dernières notes de mise à jour concernant les balises et le transfert d’événement dans Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 30%

---

# Notes de mise à jour relatives aux balises et au transfert d’événement

## 26 octobre 2022

* **Gestion des données sensibles pour les flux de données**: Les flux de données exploitent désormais plusieurs technologies Platform pour gérer de manière appropriée les données sensibles telles qu’elles sont mises en oeuvre par des réglementations telles que la Loi sur la transférabilité et la responsabilité de l’assurance-maladie (HIPAA). Consultez la section relative à la [gestion des données sensibles dans les flux de données](../../edge/datastreams/overview.md#sensitive) pour plus d’informations.
* Extension **[!DNL Splunk]pour le transfert d’événement**: Vous pouvez désormais envoyer des données à [!DNL Splunk] à l’aide d’une [transfert d’événement](../ui/event-forwarding/overview.md) extension . Pour plus d’informations, consultez la présentation de l’extension [[!DNL Splunk] ](../extensions/server/splunk/overview.md).
* Extension **[!DNL Zendesk]pour le transfert d’événement**: Vous pouvez désormais envoyer des données à [!DNL Zendesk] à l’aide d’une [transfert d’événement](../ui/event-forwarding/overview.md) extension . Pour plus d’informations, consultez la présentation de l’extension [[!DNL Zendesk] ](../extensions/server/zendesk/overview.md).

## 28 septembre 2022

* **Intégration de la navigation de gauche Adobe Experience Platform**: Toutes les fonctionnalités qui étaient auparavant exclusives à l’interface utilisateur de collecte de données (y compris les balises et le transfert d’événement) sont désormais également disponibles via la navigation de gauche dans l’interface utilisateur de l’Experience Platform, sous la catégorie . **[!UICONTROL Collecte de données]**. Il n’est donc pas nécessaire de basculer entre les interfaces utilisateur lors de l’utilisation des fonctionnalités de collecte de données dans Platform.
* **Attribution utilisateur dans les balises et le transfert d’événement**: Lors de la mise en liste des propriétés disponibles dans les balises et le transfert d’événement, chaque propriété répertoriée indique désormais à quel moment elle a été mise à jour pour la dernière fois et par qui.
* **[[!DNL Snap Conversions API] extension](https://exchange.adobe.com/apps/ec/108550) pour le transfert d’événement**: Vous pouvez désormais envoyer des données à la variable [!DNL Snapchat Conversions API] à l’aide d’une [transfert d’événement](../../tags/ui/event-forwarding/overview.md) extension . Pour plus d’informations sur la configuration et l’utilisation de l’API, voir la [[!DNL Snapchat Marketing API] documentation dédiée](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juillet 2022

* L’accès aux balises et aux fonctionnalités de transfert d’événement est désormais géré via Adobe Admin Console sous la carte pour la collecte de données Adobe Experience Platform. Pour en savoir plus, consultez le guide des [autorisations relatives à la collecte de données](../../collection/permissions.md).
* Prise en charge d’Internet Explorer 10 et 11 [obsolète](../ie-deprecation.md).

## 22 juin 2022

De nouvelles extensions ont été publiées :

* [Extension de balise de la couche de données Google](../extensions/client/google-data-layer/overview.md): Permet d’utiliser une couche de données Google dans l’implémentation de vos balises.
* [Extension de transfert d’événement Conversions améliorées de Google Ads](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Permet d’améliorer les conversions Google Ads en temps réel.
* [Extension de transfert d’événement Mailchimp](../extensions/server/mailchimp/overview.md): Envoie des événements à l’API marketing Mailchimp qui peuvent déclencher des courriers électroniques pour des campagnes, des parcours ou des transactions marketing Mailchimp.
