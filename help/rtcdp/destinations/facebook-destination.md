---
keywords: facebook extensions;facebook extension;facebook destinations;facebook
title: Destination Facebook
seo-title: Destination Facebook
description: Activez les profils de vos campagnes Facebook pour un ciblage, une personnalisation et une suppression de l’audience basés sur des e-mails hachés.
seo-description: Activez les profils de vos campagnes Facebook pour un ciblage, une personnalisation et une suppression de l’audience basés sur des e-mails hachés.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 19%

---


# [!DNL Facebook] Destination

## Présentation {#overview}

Activate profiles for your [!DNL Facebook] campaigns for audience targeting, personalization and suppression based on hashed emails.

![Destination Facebook dans l’interface utilisateur CDP en temps réel](/help/rtcdp/destinations/assets/facebook-destination.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la [!DNL Facebook] destination, voici deux exemples d’utilisation que les clients de la plate-forme de données client en temps réel Adobe peuvent résoudre à l’aide de cette fonctionnalité.


### Cas d’utilisation 1


Un détaillant en ligne souhaite atteindre les clients existants par le biais de plateformes sociales et leur montrer des offres personnalisées en fonction de leurs commandes précédentes. Le détaillant en ligne peut assimiler des adresses électroniques de sa propre gestion de la relation client à un CDP en temps réel Adobe, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à la plateforme [!DNL Facebook] sociale, optimisant ainsi ses dépenses publicitaires.


### Cas d’utilisation no 2


Une compagnie aérienne a différents niveaux de clients (Bronze, Argent et Or) et veut fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n’utilisent pas l’application mobile de la compagnie aérienne et certains d’entre eux ne se sont pas connectés au site Web de la société. Les seuls identifiants dont dispose la société à propos de ces clients sont les identifiants d’adhésion et les adresses électroniques.

Pour les cible sur les réseaux sociaux, ils peuvent intégrer les données client de leur gestion de la relation client dans un CDP en temps réel Adobe, en utilisant les adresses électroniques comme identifiants.

Ensuite, ils peuvent utiliser leurs données hors ligne, y compris les ID d’adhésion et les niveaux de clients associés, pour créer de nouveaux segments d’audience qu’ils peuvent cible à travers la [!DNL Facebook] destination.

## Spécifications de destination {#destination-specs}

### Gouvernance des données pour les [!DNL Facebook] destinations {#data-governance}

>[!IMPORTANT]
>
>Les données envoyées à [!DNL Facebook] ne doivent pas inclure d’identités assemblées. Vous êtes responsable du respect de cette obligation et pouvez le faire en vous assurant que les segments sélectionnés pour l’activation n’utilisent pas d’option de raccordement dans leur stratégie de fusion. En savoir plus sur les stratégies [de](/help/profile/ui/merge-policies.md)fusion.

### Type d’activation {#activation-type}

**Exportation** de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone, etc.) utilisé dans la destination Facebook.

### Conditions préalables du compte Facebook {#facebook-account-prerequisites}

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

1. Your [!DNL Facebook] user account must have the **[!DNL Manage campaigns]** permission enabled for the Ad account that you plan to use.
2. Ajoutez le compte commercial **Adobe Experience Cloud** comme partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Pour plus d’informations, reportez-vous à la documentation [Ajouter des partenaires à votre gestionnaire](https://www.facebook.com/business/help/1717412048538897) d’entreprise dans la documentation Facebook.
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Real-time CDP].
3. Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].

### Conditions requises pour le hachage des courriels {#email-hashing-requirements}

[!DNL Facebook] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Facebook] doivent être masquées des adresses électroniques *hachées* . Vous pouvez choisir de hacher les adresses électroniques avant de les importer dans Adobe Experience Platform, ou vous pouvez choisir de travailler avec les adresses électroniques en clair dans l&#39;Experience Platform et de faire en sorte que notre algorithme les hache sur l&#39;activation.

Pour en savoir plus sur l&#39;assimilation d&#39;adresses électroniques dans l&#39;Experience Platform, consultez la présentation [de l&#39;assimilation par](/help/ingestion/batch-ingestion/overview.md) lot et la présentation [de l&#39;assimilation par](/help/ingestion/streaming-ingestion/overview.md)flux continu.

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Rogner tous les espaces de début et de fin de la chaîne de courriel ; exemple : `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Lors du hachage des chaînes de courrier électronique, veillez à mettre la chaîne en minuscules en hachage ;
   * Exemple : `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assurez-vous que la chaîne hachée est en minuscules.
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Ne salez pas la chaîne.


>[!IMPORTANT]
>
>Si vous choisissez de ne pas hacher les adresses électroniques, le CDP en temps réel Adobe le fera pour vous lorsque vous activerez les segments vers [!DNL Facebook]. Dans le processus [d’](/help/rtcdp/destinations/activate-destinations.md#activate-data) activation (voir étape 5), sélectionnez l’ `Email` option comme illustré ci-dessous pour les adresses *de courriel* brutes et `Email_LC_SHA256` *pour les adresses de courriel hachées.*


![Hachage sur l’activation](/help/rtcdp/destinations/assets/identity-mapping.png)

## Se connecter à la destination {#connect-destination}

To connect to the [!DNL Facebook] destination, see [Social network destinations authentication workflow](/help/rtcdp/destinations/social-network-destinations-workflow.md).


## Activate segments to [!DNL Facebook] {#activate-segments}

For instructions on how to activate segments to [!DNL Facebook], see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).

## Données exportées {#exported-data}

For [!DNL Facebook], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L&#39;intégration entre le CDP en temps réel de l&#39;Adobe et la prise en charge [!DNL Facebook] des renvois d&#39;audiences historiques. Toutes les qualifications des segments historiques sont envoyées [!DNL Facebook] lorsque vous activez les segments vers la destination.