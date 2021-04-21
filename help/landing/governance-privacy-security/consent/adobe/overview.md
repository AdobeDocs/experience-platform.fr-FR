---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Traitement du consentement dans Adobe Experience Platform
topic-legacy: getting started
description: Découvrez comment traiter les signaux de consentement des clients à Adobe Experience Platform en utilisant la norme Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# Traitement du consentement dans Adobe Experience Platform

Adobe Experience Platform vous permet de traiter les données de consentement que vous avez collectées auprès de vos clients et de les intégrer à vos profils clients stockés. Ces données peuvent ensuite être utilisées par les processus en aval pour déterminer si la collecte de données a lieu pour un client spécifique ou si leurs profils sont utilisés à des fins spécifiques. Par exemple, les données de consentement d’un profil donné peuvent déterminer s’il peut être inclus dans un segment d’audience exporté ou s’il peut participer à des canaux marketing spécifiques tels que des courriers électroniques, des messages texte ou des notifications Push.

Ce document fournit un aperçu de la manière de configurer les opérations de données de votre plateforme pour intégrer les données de consentement des clients générées par une plateforme de gestion du consentement (CMP) et intégrer ces données dans les profils des clients en vue d&#39;une utilisation en aval.

>[!NOTE]
>
>Ce document se concentre sur le traitement des données de consentement en utilisant la norme Adobe. Si vous traitez les données de consentement conformément à la norme IAB Transparency and Consent Framework (TCF) 2.0, consultez le guide sur la [prise en charge de TCF 2.0 dans la plate-forme de données client en temps réel](../iab/overview.md).

## Conditions préalables

Ce guide exige une compréhension pratique des divers services Experience Platform impliqués dans le traitement des données de consentement :

* [Modèle de données d’expérience (XDM)](../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [Service](../../../../identity-service/home.md) d&#39;identité Adobe Experience Platform : Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [Profil](../../../../profile/home.md) client en temps réel : Utilise  [!DNL Identity Service] les fonctionnalités pour créer des profils client détaillés à partir de vos jeux de données en temps réel. Le Profil client en temps réel extrait les données de Data Lake et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md) : Bibliothèque JavaScript côté client qui vous permet d’intégrer divers services de plate-forme à votre site Web destiné aux clients.
   * [Commandes](../../../../edge/consent/supporting-consent.md) de consentement SDK : Présentation des cas d’utilisation des commandes du SDK liées au consentement, présentée dans ce guide.
* [Service](../../../../segmentation/home.md) de segmentation Adobe Experience Platform : Vous permet de diviser les données du Profil client en temps réel en groupes de personnes qui partagent des caractéristiques similaires et qui réagissent de la même manière aux stratégies marketing.

## Récapitulatif du flux de traitement de consentement {#summary}

La section suivante décrit comment les données de consentement sont traitées une fois que le système a été correctement configuré :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site Web.
1. Lors de chaque chargement de page (ou lorsque votre CMP détecte un changement des préférences de consentement), un script personnalisé de votre site mappe les préférences actuelles à un objet XDM standard. Cet objet est ensuite transmis à la commande Platform Web SDK `setConsent`.
1. Lorsque `setConsent` est appelé, le SDK Web de la plate-forme vérifie si les valeurs de consentement sont différentes de celles qu&#39;il a reçues la dernière fois. Si les valeurs sont différentes (ou qu’il n’existe aucune valeur précédente), les données de consentement/préférence structurées sont envoyées à Adobe Experience Platform.
1. Les données de consentement/préférence sont assimilées à un jeu de données [!DNL Profile] dont le schéma contient des champs de consentement/préférence.

Outre les commandes SDK déclenchées par les crochets de modification du consentement de CMP, les données de consentement peuvent également être transférées dans l&#39;Experience Platform par le biais de toute donnée XDM générée par le client et directement téléchargée dans un jeu de données [!DNL Profile] activé.

### Application du consentement

Dans la version actuelle de la prise en charge du traitement du consentement dans Platform, seule l&#39;autorisation de collecte de données (`collect.val`) est automatiquement appliquée par le Platform Web SDK. Bien qu&#39;il soit possible de collecter et de conserver des préférences plus granulaires dans les profils clients, ces signaux supplémentaires doivent être appliqués manuellement dans vos propres processus en aval.

>[!NOTE]
>
>Pour plus d&#39;informations sur la structure des champs de consentement XDM mentionnés ci-dessus, consultez le guide sur le [type de données Contenus et préférences](../../../../xdm/data-types/consents.md).

Une fois que le système a été configuré, le SDK Web de la plate-forme interprète la valeur de consentement de collecte de données de l&#39;utilisateur actuel afin de déterminer si les données doivent être envoyées au réseau Edge de Adobe Experience Platform, abandonnées par le client ou conservées jusqu&#39;à ce que l&#39;autorisation de collecte de données soit définie sur oui ou non.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Chaque système CMP étant unique, vous devez déterminer la meilleure façon de permettre à vos clients de donner leur consentement lorsqu&#39;ils interagissent avec votre service. Pour ce faire, il est courant d’utiliser une boîte de dialogue de consentement de cookie, comme dans l’exemple suivant :

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Cette boîte de dialogue doit permettre au client d’opt-in ou de sortir des cas d’utilisation spécifiques du marketing et de la personnalisation pour ses données. Ces consentements et préférences doivent être conformes au modèle de données que vous définissez pour le jeu de données [!DNL Profile] activé à l’étape suivante.

## Ajouter des champs de consentement normalisés à un jeu de données [!DNL Profile] compatible {#dataset}

Les données de consentement du client doivent être envoyées à un jeu de données compatible [!DNL Profile] dont le schéma contient des champs de consentement. Ces champs doivent être inclus dans le même schéma et jeu de données que celui que vous utilisez pour capturer des informations d’attribut sur des clients individuels.

Reportez-vous au didacticiel sur la [configuration d&#39;un jeu de données pour la capture de données de consentement](./dataset.md) pour obtenir des instructions détaillées sur la façon d&#39;ajouter ces champs obligatoires à un jeu de données compatible [!DNL Profile] avant de poursuivre avec ce guide.

## Mettre à jour les stratégies de fusion [!DNL Profile] pour inclure les données de consentement {#merge-policies}

Une fois que vous avez créé un jeu de données [!DNL Profile] activé pour le traitement des données de consentement, vous devez vous assurer que vos stratégies de fusion ont été configurées pour inclure systématiquement les champs de consentement dans chaque profil client. Cela implique de définir la priorité des jeux de données afin que votre jeu de données de consentement soit hiérarchisé par rapport à d&#39;autres jeux de données potentiellement conflictuels.

>[!NOTE]
>
>Si vous n’avez pas de jeux de données conflictuels, vous devez définir la priorité de l’horodatage pour votre stratégie de fusion. Cela permet de s’assurer que le dernier consentement spécifié par un client correspond au paramètre de consentement utilisé.

Pour plus d&#39;informations sur la façon d&#39;utiliser les stratégies de fusion, consultez le [guide de l&#39;utilisateur des stratégies de fusion](../../../../profile/ui/merge-policies.md). Lors de la configuration de vos stratégies de fusion, vous devez vous assurer que vos profils incluent tous les attributs de consentement requis fournis par le mixin Contenus et Préférences, comme indiqué dans le guide sur la préparation des jeux de données [](./dataset.md).

## Intégration des données de consentement dans la plate-forme

Une fois que vous disposez de vos jeux de données et que vous fusionnez des stratégies pour représenter les champs de consentement requis dans vos profils clients, l’étape suivante consiste à importer les données de consentement elles-mêmes dans Plateforme.

En premier lieu, vous devez utiliser le Adobe Experience Platform Web SDK pour envoyer des données de consentement à la plateforme chaque fois que des événements de changement de consentement sont détectés par votre CMP. Si vous collectez des données de consentement sur une plateforme mobile, vous devez utiliser le Adobe Experience Platform Mobile SDK. Vous pouvez également choisir d&#39;assimiler directement vos données de consentement collectées en les mappant au schéma XDM de votre jeu de données de consentement et en les envoyant à Plateforme par assimilation par lot.

Les détails de chacune de ces méthodes sont présentés dans les sous-sections ci-dessous.

### Configurez le SDK Web Experience Platform pour traiter les données de consentement {#web-sdk}

Une fois que vous avez configuré votre CMP pour qu’elle écoute les événements de changement de consentement sur votre site Web, vous pouvez intégrer le SDK Web Experience Platform pour recevoir les paramètres de consentement mis à jour et les envoyer à la plateforme à chaque chargement de page et chaque fois que des événements de changement de consentement se produisent. Pour plus d&#39;informations, consultez le guide [Configuration du SDK Web pour traiter les données de consentement des clients](./sdk.md).

### Configurez le SDK mobile Experience Platform pour traiter les données de consentement {#mobile-sdk}

Si des préférences de consentement client sont requises dans votre application mobile, vous pouvez intégrer le SDK mobile Experience Platform pour récupérer et mettre à jour les paramètres de consentement, en les envoyant à la plate-forme chaque fois que l’API de consentement est appelée.

Consultez la documentation du kit SDK Mobile pour [configurer l’extension mobile Consent](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent) et [à l’aide de l’API Consent](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge-consent/edge-consent-api-reference). Pour plus d&#39;informations sur la façon de gérer les problèmes de confidentialité à l&#39;aide du kit SDK Mobile, consultez la section [Confidentialité et RMPD](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/resources/privacy-and-gdpr).

### Envoi direct des données de consentement conformes à XDM {#batch}

Vous pouvez ingérer des données de consentement conformes XDM à partir d’un fichier CSV en utilisant l’assimilation par lot. Cela peut s’avérer utile si vous disposez d’un arriéré de données de consentement collectées précédemment qui n’ont pas encore été intégrées dans vos profils clients.

Suivez le didacticiel sur le [mappage d’un fichier CSV à XDM](../../../../ingestion/tutorials/map-a-csv-file.md) pour savoir comment convertir vos champs de données en XDM et les assimiler à Platform. Lorsque vous sélectionnez [!UICONTROL Destination] pour le mappage, veillez à sélectionner l&#39;option **[!UICONTROL Utiliser le jeu de données existant]** et à choisir le jeu de données de consentement [!DNL Profile] activé que vous avez créé précédemment.

## Testez votre implémentation {#test-implementation}

Une fois que vous avez assimilé des données de consentement client dans votre jeu de données [!DNL Profile] activé, vous pouvez vérifier vos profils mis à jour afin de déterminer s’ils contiennent des attributs de consentement.

>[!IMPORTANT]
>
>Pour vue les attributs d’un profil existant dans l’interface utilisateur, vous devez connaître au moins une valeur d’identité (et son espace de nommage correspondant) associée à ce profil.
>
>Si vous n&#39;avez pas accès à ces informations, vous pouvez choisir d&#39;assimiler vos propres données de consentement au test et de les associer à une valeur ou un espace de nommage d&#39;identité que vous connaissez à la place.

Consultez la section [profils de navigation par identité](../../../../profile/ui/user-guide.md#browse) du guide de l&#39;interface utilisateur [!DNL Profile] pour connaître les étapes spécifiques à suivre pour rechercher les détails d&#39;un profil.

Par défaut, les nouveaux attributs de consentement n’apparaissent pas sur un tableau de bord de profil. Par conséquent, vous devez accéder à l&#39;onglet **[!UICONTROL Attributs]** de la page de détails d&#39;un profil pour confirmer qu&#39;ils ont été ingérés comme prévu. Consultez le guide sur le [tableau de bord de profil](../../../../profile/ui/profile-dashboard.md) pour savoir comment personnaliser le tableau de bord en fonction de vos besoins.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Étapes suivantes

Ce guide explique comment configurer les opérations de votre plateforme pour traiter les données de consentement des clients à l’aide de la norme Adobe et pour que ces attributs soient représentés dans les profils client. Vous pouvez désormais intégrer les préférences de consentement des clients en tant que facteur déterminant dans la qualification des segments et d’autres cas d’utilisation en aval.

Pour plus d&#39;informations sur les fonctionnalités de confidentialité des Experience Platform, consultez la présentation de [gouvernance, confidentialité et sécurité dans Platform](../../overview.md).
