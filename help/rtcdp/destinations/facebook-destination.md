---
title: Destination Facebook
seo-title: Destination Facebook
description: Activez des profils pour vos campagnes Facebook pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.
seo-description: Activez des profils pour vos campagnes Facebook pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.
translation-type: tm+mt
source-git-commit: 522014f8e5f3de0f553a69763d3a37482953b7c4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---


# Destination Facebook

## Aperçu {#overview}

Activez des profils pour vos campagnes Facebook pour le ciblage, la personnalisation et la suppression des audiences en fonction des courriers électroniques hachés.

![Destination Facebook dans l’interface utilisateur CDP en temps réel](/help/rtcdp/destinations/assets/facebook-destination.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination Facebook, voici deux exemples d’utilisation que les clients de la plateforme de données clientes Adobe en temps réel peuvent résoudre à l’aide de cette fonctionnalité.


### Cas d’utilisation 1


Un détaillant en ligne souhaite atteindre les clients existants par le biais de plateformes sociales et leur montrer des offres personnalisées en fonction de leurs commandes précédentes. Le détaillant en ligne peut assimiler des adresses électroniques de son propre service de gestion de la relation client au CDP Adobe en temps réel, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à la plateforme sociale Facebook afin d’optimiser ses dépenses publicitaires.


### Cas d’utilisation no 2


Une compagnie aérienne a différents niveaux de clients (Bronze, Argent et Or) et veut fournir à chacun des niveaux des offres personnalisées via des plateformes sociales. Cependant, tous les clients n’utilisent pas l’application mobile de la compagnie aérienne et certains d’entre eux ne se sont pas connectés au site Web de la société. Les seuls identifiants dont dispose la société à propos de ces clients sont les identifiants d’adhésion et les adresses électroniques.
Pour les cible sur les réseaux sociaux, ils peuvent intégrer les données client de leur gestion de la relation client dans le CDP en temps réel d’Adobe, en utilisant les adresses électroniques hachées comme identifiants.
Ensuite, ils peuvent combiner leurs données hors ligne avec leurs données d’activité en ligne existantes, afin de créer de nouveaux segments d’audience qu’ils peuvent cible via la destination Facebook.

## Spécifications de destination {#destination-specs}

### Gouvernance des données pour les destinations Facebook {#data-governance}

>[!IMPORTANT]
>
>Les données envoyées à Facebook ne doivent pas inclure d’identités cousues. Vous êtes responsable du respect de cette obligation et pouvez le faire en vous assurant que les segments sélectionnés pour l’activation n’utilisent pas d’option de raccordement dans leur stratégie de fusion. En savoir plus sur les stratégies [de](/help/profile/ui/merge-policies.md)fusion.

### Type d&#39;Activation {#activation-type}

**Exportation** de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone, etc.) utilisé dans la destination Facebook.

### Conditions préalables du compte Facebook {#facebook-account-prerequisites}

Avant d’envoyer vos segments d’audience à [!DNL Facebook], assurez-vous de respecter les exigences suivantes :

1. L’ [!DNL Facebook] autorisation doit être activée pour votre compte **[!DNL Manage campaigns]** utilisateur pour le compte publicitaire que vous prévoyez d’utiliser.
2. Ajouter le compte **Adobe Experience Cloud** en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]entreprise. Utilisez `business ID=206617933627973`. Pour plus d’informations, reportez-vous à la documentation [Ajouter Partenaires de votre gestionnaire](https://www.facebook.com/business/help/1717412048538897) d’entreprise dans la documentation Facebook.
   >[!IMPORTANT]
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer les campagnes** . Cela est nécessaire pour l&#39; [!DNL Adobe Real-time CDP] intégration.
3. Lisez et signez les [!DNL Facebook Custom Audiences] conditions d’utilisation. Pour ce faire, allez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].

### Conditions requises pour le hachage des courriels {#email-hashing-requirements}

Facebook exige qu&#39;aucune information d&#39;identification personnelle (PII) ne soit envoyée de manière claire. Par conséquent, les audiences activées sur Facebook doivent être masquées par des adresses électroniques *hachées* . Vous pouvez choisir de hacher des adresses électroniques avant de les importer dans Adobe Experience Platform ou de les utiliser avec des adresses électroniques clairement définies dans Experience Platform et de les faire hacher par l’algorithme sur activation.

Pour en savoir plus sur l’assimilation d’adresses électroniques dans Experience Platform, consultez la présentation [de l’assimilation par](/help/ingestion/batch-ingestion/overview.md) lot et la présentation [de l’assimilation par](/help/ingestion/streaming-ingestion/overview.md)flux continu.

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Rogner tous les espaces de début et de fin de la chaîne de courriel ; exemple : `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Lors du hachage des chaînes de courrier électronique, veillez à mettre la chaîne en minuscules en hachage ;
   * Exemple : `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assurez-vous que la chaîne hachée est en minuscules.
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Ne salez pas la chaîne.


>[!IMPORTANT]
>
>Si vous choisissez de ne pas hacher les adresses électroniques, le CDP en temps réel d’Adobe le fera pour vous lorsque vous activerez des segments sur Facebook. Dans le processus [d’](/help/rtcdp/destinations/activate-destinations.md#activate-data) activation (voir étape 5), sélectionnez l’ `Email` option comme illustré ci-dessous pour les adresses *de courriel* brutes et `Email_LC_SHA256` *pour les adresses de courriel hachées.*


![Hachage sur l’activation](/help/rtcdp/destinations/assets/identity-mapping.png)

## Se connecter à la destination {#connect-destination}

Pour vous connecter à la destination Facebook, voir Processus [d’authentification des destinations de réseau](/help/rtcdp/destinations/social-network-destinations-workflow.md)Social.


## Activer les segments sur Facebook {#activate-segments}

For instructions on how to activate segments to Facebook, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).