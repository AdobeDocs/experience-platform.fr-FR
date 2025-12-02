---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Traitement du consentement dans Adobe Experience Platform
description: Découvrez comment traiter les signaux de consentement des clients dans Adobe Experience Platform à l’aide de la norme Adobe 2.0.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 1%

---

# Traitement du consentement dans Adobe Experience Platform

Adobe Experience Platform vous permet de traiter les données de consentement que vous avez collectées auprès de vos clients et de les intégrer dans vos profils clients stockés. Ces données peuvent ensuite être utilisées par des processus en aval pour déterminer si la collecte de données a lieu pour un client spécifique ou si leurs profils sont utilisés à des fins spécifiques. Par exemple, les données de consentement pour un profil particulier peuvent déterminer si elles peuvent être incluses dans un segment d’audience exporté ou si elles peuvent participer à des canaux marketing spécifiques tels que les e-mails, les SMS ou les notifications push.

Ce document présente un aperçu de la configuration de vos opérations de données Experience Platform pour ingérer les données de consentement client générées par une plateforme de gestion du consentement (CMP) et intégrer ces données dans les profils client pour les cas d’utilisation en aval.

>[!NOTE]
>
>Ce document se concentre sur le traitement des données de consentement à l’aide de la norme Adobe. Si vous traitez les données de consentement conformément au Transparency and Consent Framework (TCF) 2.0 de l’IAB, consultez le guide sur la prise en charge du [TCF 2.0 dans Adobe Real-Time Customer Data Platform](../iab/overview.md).

## Conditions préalables

Ce guide nécessite une compréhension pratique des différents services Experience Platform impliqués dans le traitement des données de consentement :

* [Modèle de données d’expérience (XDM)](/help/xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Adobe Experience Platform Identity Service &#x200B;](/help/identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [Real-Time Customer Profile](/help/profile/home.md) : utilise des fonctionnalités [!DNL Identity Service] pour créer des profils clients détaillés à partir de vos jeux de données en temps réel. Le profil client en temps réel extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) : bibliothèque JavaScript côté client qui vous permet d’intégrer divers services Experience Platform à votre site web destiné aux clients.
   * [Commandes de consentement SDK &#x200B;](/help/collection/js/commands/setconsent.md) : présentation du cas d’utilisation des commandes SDK liées au consentement présentées dans ce guide.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md) : permet de diviser les données du profil client en temps réel en groupes d’individus qui partagent des caractéristiques similaires et qui réagissent de la même manière aux stratégies marketing.

## Résumé du flux de traitement du consentement {#summary}

La section suivante décrit le traitement des données de consentement une fois le système correctement configuré :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site web.
1. À chaque chargement de page (ou lorsque votre CMP détecte un changement dans les préférences de consentement), un script personnalisé sur votre site mappe les préférences actives à un objet XDM standard. Cet objet est ensuite transmis à la commande `setConsent` d’Experience Platform Web SDK.
1. Lorsqu’`setConsent` est appelé, Experience Platform Web SDK vérifie si les valeurs de consentement sont différentes de celles qu’il a reçues en dernier. Si les valeurs sont différentes (ou s’il n’existe aucune valeur précédente), les données structurées de consentement/préférence sont envoyées à Adobe Experience Platform.
1. Les données de consentement/préférence sont ingérées dans un jeu de données activé pour [!DNL Profile] dont le schéma contient des champs de consentement/préférence.

Outre les commandes SDK déclenchées par les hooks de changement de consentement CMP, les données de consentement peuvent également être transmises à Experience Platform par le biais de données XDM générées par le client ou la cliente et chargées directement dans un jeu de données compatible avec les [!DNL Profile].

### Application du consentement

Dans la version actuelle de la prise en charge du traitement du consentement dans Experience Platform, seule l’autorisation de collecte de données (`collect.val`) est automatiquement appliquée par Experience Platform Web SDK. Bien qu’il soit possible de collecter et de conserver des consentements et des préférences plus granulaires dans les profils client, ces signaux supplémentaires doivent être appliqués manuellement dans vos propres processus en aval.

>[!NOTE]
>
>Pour plus d’informations sur la structure des champs de consentement XDM mentionnés ci-dessus, reportez-vous au guide sur le type de données [[!UICONTROL Consents and Preferences] &#x200B;](/help/xdm/data-types/consents.md) .

Une fois le système configuré, Experience Platform Web SDK interprète la valeur de consentement de la collecte de données pour l’utilisateur actuel afin de déterminer si les données doivent être envoyées à Adobe Experience Platform Edge Network, supprimées du client ou conservées jusqu’à ce que l’autorisation de collecte de données soit définie sur oui ou non.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Comme chaque système de CMP est unique, vous devez déterminer la meilleure façon de permettre à vos clients de donner leur consentement lorsqu’ils interagissent avec votre service. Pour ce faire, une méthode courante consiste à utiliser une boîte de dialogue de consentement des cookies, similaire à l’exemple suivant :

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Cette boîte de dialogue doit permettre au client ou à la cliente de s’exclure ou de s’exclure des cas d’utilisation spécifiques de marketing et de personnalisation pour ses données. Ces consentements et préférences doivent être conformes au modèle de données que vous définissez pour le jeu de données activé pour [!DNL Profile] à l’étape suivante.

## Ajouter des champs de consentement normalisés à un jeu de données compatible avec les [!DNL Profile] {#dataset}

Les données de consentement du client doivent être envoyées à un jeu de données compatible avec les [!DNL Profile] dont le schéma contient des champs de consentement. Ces champs doivent être inclus dans le même schéma et le même jeu de données que ceux que vous utilisez pour capturer les informations d’attribut sur les clients individuels.

Reportez-vous au tutoriel sur [configuration d’un jeu de données pour capturer des données de consentement](./dataset.md) pour obtenir des instructions détaillées sur la manière d’ajouter ces champs obligatoires à un jeu de données activé pour [!DNL Profile] avant de poursuivre avec ce guide.

## Mettre à jour [!DNL Profile] politiques de fusion pour inclure les données de consentement {#merge-policies}

Une fois que vous avez créé un jeu de données compatible avec [!DNL Profile] pour le traitement des données de consentement, vous devez vous assurer que vos politiques de fusion ont été configurées pour toujours inclure des champs de consentement dans chaque profil client. Cela implique de définir la priorité du jeu de données afin que votre jeu de données de consentement soit prioritaire sur les autres jeux de données potentiellement conflictuels.

>[!NOTE]
>
>Si vous ne disposez d’aucun jeu de données en conflit, vous devez définir la priorité d’horodatage pour votre politique de fusion à la place. Cela permet de s’assurer que le dernier consentement spécifié par un client correspond au paramètre de consentement utilisé.

Pour plus d’informations sur l’utilisation des politiques de fusion, commencez par lire la [présentation des politiques de fusion](../../../../profile/merge-policies/overview.md). Lors de la configuration de vos politiques de fusion, vous devez vous assurer que vos profils incluent tous les attributs de consentement requis fournis par le groupe de champs de schéma [!UICONTROL Consents and Preferences], comme indiqué dans le guide sur la [préparation des jeux de données](./dataset.md).

## Importation de données de consentement dans Experience Platform

Une fois que vous disposez de vos jeux de données et politiques de fusion pour représenter les champs de consentement requis dans vos profils clients, l’étape suivante consiste à importer les données de consentement elles-mêmes dans Experience Platform.

Avant toute chose, vous devez utiliser Adobe Experience Platform Web SDK pour envoyer des données de consentement à Experience Platform chaque fois que des événements de changement de consentement sont détectés par votre CMP. Si vous collectez des données de consentement sur une plateforme mobile, vous devez utiliser le SDK mobile Adobe Experience Platform. Vous pouvez également choisir d’ingérer directement vos données de consentement collectées en les mappant au schéma XDM de votre jeu de données de consentement et en les envoyant à Experience Platform par ingestion par lots.

Vous trouverez des détails sur chacune de ces méthodes dans les sous-sections ci-dessous.

### Configurer Experience Platform Web SDK pour traiter les données de consentement {#web-sdk}

Une fois que vous avez configuré votre CMP pour écouter les événements de changement de consentement sur votre site web, vous pouvez intégrer Experience Platform Web SDK pour recevoir les paramètres de consentement mis à jour et les envoyer à Experience Platform à chaque chargement de page et chaque fois que des événements de changement de consentement se produisent. Pour plus d’informations, consultez le guide sur la [configuration de Web SDK pour traiter les données de consentement client](../sdk.md).

### Configuration d’Experience Platform Mobile SDK pour traiter les données de consentement {#mobile-sdk}

Si les préférences de consentement des clients sont requises dans votre application mobile, vous pouvez intégrer Experience Platform Mobile SDK pour récupérer et mettre à jour les paramètres de consentement, en les envoyant à Experience Platform chaque fois que l&#39;API de consentement est appelée.

Consultez la documentation de Mobile SDK pour [configurer l’extension mobile de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) et [utiliser l’API de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Pour plus d’informations sur la gestion des problèmes de confidentialité à l’aide de Mobile SDK, reportez-vous à la section [Confidentialité et RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Ingérer directement des données de consentement conformes à XDM {#batch}

Vous pouvez ingérer des données de consentement conformes à XDM à partir d’un fichier CSV à l’aide de l’ingestion par lots. Cela peut s’avérer utile si vous disposez d’une liste d’attente de données de consentement précédemment collectées qui n’ont pas encore été intégrées à vos profils clients.

Suivez le tutoriel sur [le mappage d’un fichier CSV à XDM](../../../../ingestion/tutorials/map-csv/overview.md) pour savoir comment convertir vos champs de données en XDM et les ingérer dans Experience Platform. Lors de la sélection du [!UICONTROL Destination] pour le mappage, veillez à sélectionner l’option **[!UICONTROL Use existing dataset]** et à choisir le jeu de données de consentement activé pour le [!DNL Profile] que vous avez créé précédemment.

## Tester votre implémentation {#test-implementation}

Une fois que vous avez ingéré des données de consentement client dans votre jeu de données activé pour [!DNL Profile], vous pouvez vérifier vos profils mis à jour pour voir s’ils contiennent des attributs de consentement.

>[!IMPORTANT]
>
>Pour afficher les attributs d’un profil existant dans l’interface utilisateur, vous devez connaître au moins une valeur d’identité (et son espace de noms correspondant) associée à ce profil.
>
>Si vous n’avez pas accès à ces informations, vous pouvez choisir d’ingérer vos propres données de consentement de test et de les associer à une valeur d’identité/un espace de noms que vous connaissez à la place.

Consultez la section sur la [navigation dans les profils par identité](../../../../profile/ui/user-guide.md#browse) dans le guide de l’interface utilisateur [!DNL Profile] pour obtenir des instructions spécifiques sur la recherche des détails d’un profil.

Par défaut, les nouveaux attributs de consentement n’apparaissent pas dans le tableau de bord d’un profil. Par conséquent, vous devez accéder à l’onglet **[!UICONTROL Attributes]** dans la page de détails d’un profil afin de confirmer qu’ils ont été ingérés comme prévu. Consultez le guide sur le [tableau de bord des profils](../../../../profile/ui/profile-dashboard.md) pour savoir comment personnaliser le tableau de bord en fonction de vos besoins.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Experience Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Experience Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Experience Platform and the appropriate profile attributes are updated accordingly.
-->

## Étapes suivantes

Ce guide explique comment configurer vos opérations Experience Platform pour traiter les données de consentement des clients à l’aide de la norme Adobe et faire en sorte que ces attributs soient représentés dans les profils clients. Vous pouvez désormais intégrer les préférences de consentement des clients en tant que facteur déterminant dans la qualification de segment et dans d’autres cas d’utilisation en aval.

Pour plus d’informations sur les fonctionnalités Experience Platform relatives à la confidentialité, consultez la présentation de la [&#x200B; gouvernance, confidentialité et sécurité dans Experience Platform](../../overview.md).
