---
keywords: Experience Platform;accueil;IAB;IAB 2.0;consentement;Consentement
solution: Experience Platform
title: Prise en charge de l’IAB TCF 2.0 dans Experience Platform
description: Découvrez comment configurer vos opérations et schémas de données pour transmettre les choix de consentement des clients lors de l’activation de segments vers des destinations dans Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 1%

---

# Prise en charge de l’IAB TCF 2.0 dans Experience Platform

Le [!DNL Transparency & Consent Framework] (TCF), tel que défini par le [!DNL Interactive Advertising Bureau] (IAB), est un cadre technique standard ouvert destiné à permettre aux organisations d&#39;obtenir, d&#39;enregistrer et de mettre à jour le consentement des consommateurs pour le traitement de leurs données personnelles, conformément au [!DNL General Data Protection Regulation] de l&#39;Union européenne (RGPD). La deuxième itération du cadre, le FCT 2.0, offre plus de souplesse quant à la façon dont les consommateurs peuvent donner ou refuser leur consentement, y compris la question de savoir si et comment les fournisseurs peuvent utiliser certaines fonctionnalités du traitement des données, comme la géolocalisation précise.

>[!NOTE]
>
>Vous trouverez plus d&#39;informations sur le TCF 2.0 sur le site web [IAB Europe](https://iabeurope.eu/), y compris les supports et les spécifications techniques.

Adobe Experience Platform fait partie de la liste de fournisseurs [IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf/) enregistrée sous l’ID **565**. Conformément aux exigences de TCF 2.0, Experience Platform vous permet de collecter les données de consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si les profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

>[!IMPORTANT]
>
>Experience Platform peut uniquement se conformer à la version 2.0 du TCF (ou ultérieure). Les versions précédentes du TCF ne sont pas prises en charge.

Ce document présente un aperçu de la configuration de vos opérations de données et de vos schémas de profil pour accepter les données de consentement client générées par votre plateforme de gestion du consentement (CMP). Elle explique également comment Experience Platform transmet les choix de consentement des utilisateurs et utilisatrices lors de l’exportation de segments.

## Conditions préalables

Pour suivre ce guide, vous devez utiliser un CMP, commercial ou personnel, qui est intégré et conforme au FCT de l’IAB. Voir la [liste des CMP conformes](https://iabeurope.eu/cmp-list/) pour plus d’informations.

>[!IMPORTANT]
>
>Si l’identifiant de votre CMP n’est pas valide, Experience Platform continue à traiter vos données en l’état. Pour appliquer le TCF 2.0, vous devez confirmer que votre CMP possède un ID valide qui a été enregistré auprès de l’IAB TCF 2.0 avant d’envoyer des données à Experience Platform.

Ce guide nécessite également une compréhension pratique des services Experience Platform suivants :

* [Modèle de données d’expérience (XDM)](/help/xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Adobe Experience Platform Identity Service ](/help/identity-service/home.md) : résout le problème fondamental de la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [Real-Time Customer Profile](/help/profile/home.md) : utilise des [!DNL Identity Service] pour créer des profils clients détaillés à partir de vos jeux de données en temps réel. [!DNL Real-Time Customer Profile] extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) : bibliothèque JavaScript côté client qui vous permet d’intégrer divers services Experience Platform à votre site web destiné aux clients.
   * [Commandes de consentement SDK ](/help/collection/js/commands/setconsent.md) : présentation du cas d’utilisation des commandes SDK liées au consentement présentées dans ce guide.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md) : permet de diviser les données [!DNL Real-Time Customer Profile] en groupes d’individus qui partagent des caractéristiques similaires et qui réagissent de la même manière aux stratégies marketing.

Outre les services Experience Platform répertoriés ci-dessus, vous devez également connaître [destinations](/help/data-governance/home.md) ainsi que leur rôle dans l’écosystème Experience Platform.

## Résumé du flux de consentement du client {#summary}

Les sections suivantes décrivent la manière dont les données de consentement sont collectées et appliquées une fois le système correctement configuré.

### Collecte de données de consentement

Experience Platform vous permet de collecter les données de consentement des clients par le biais du processus suivant :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site web.
1. Votre CMP détecte le changement de préférence de consentement et génère les données de consentement TCF en conséquence.
1. À l’aide du SDK Web d’Experience Platform, les données de consentement générées (renvoyées par le CMP) sont envoyées à Adobe Experience Platform.
1. Les données de consentement collectées sont ingérées dans un jeu de données compatible avec le [!DNL Profile] dont le schéma contient des champs de consentement TCF.

Outre les commandes SDK déclenchées par les hooks de changement de consentement CMP, les données de consentement peuvent également être transmises à Experience Platform par le biais de données XDM générées par le client ou la cliente et chargées directement dans un jeu de données compatible avec les [!DNL Profile].

Tous les segments partagés avec Experience Platform par Adobe Audience Manager (par le biais du connecteur source [!DNL Audience Manager] ou autre) peuvent également contenir des données de consentement si les champs appropriés ont été appliqués à ces segments par le biais de [!DNL Experience Cloud Identity Service]. Pour plus d’informations sur la collecte de données de consentement dans [!DNL Audience Manager], consultez le document sur le plug-in [Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=fr).

### Application du consentement en aval

Une fois les données de consentement TCF ingérées avec succès, les processus suivants ont lieu dans les services Experience Platform en aval :

1. [!DNL Real-Time Customer Profile] met à jour les données de consentement stockées pour le profil de ce client.
1. Experience Platform traite les ID client uniquement si l’autorisation du fournisseur pour Experience Platform (565) est fournie pour chaque ID d’un cluster.
1. Lors de l’exportation de segments vers des destinations appartenant aux membres de la liste des fournisseurs TCF 2.0, Experience Platform n’inclut que les profils si les autorisations de fournisseur pour Experience Platform (565) *et* la destination individuelle sont fournies pour chaque identifiant d’un cluster.

Le reste des sections de ce document fournit des conseils sur la configuration d’Experience Platform et de vos opérations de données pour répondre aux exigences de collecte et d’application décrites ci-dessus.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Comme chaque système de CMP est unique, vous devez déterminer la meilleure façon de permettre à vos clients de donner leur consentement lorsqu’ils interagissent avec votre service. Une boîte de dialogue de consentement des cookies est un moyen courant d’obtenir le consentement du client. Un exemple de boîte de dialogue CMP est illustré ci-dessous.

![Exemple de boîte de dialogue Plateforme de gestion du consentement.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Cette boîte de dialogue doit permettre au client de s’inscrire ou de se désinscrire des éléments suivants :

| Option de consentement | Description |
| --- | --- |
| **Objectifs** | Les objectifs définissent à quelles fins publicitaires une marque peut utiliser les données d’un client. Les objectifs suivants doivent être acceptés pour qu’Experience Platform traite les ID de client : <ul><li>**Objectif 1** : Stocker et/ou accéder à des informations sur un appareil</li><li>**Objectif 10** : Développer et améliorer les produits</li></ul> |
| **Autorisations des fournisseurs** | Outre les objectifs techniques de la publicité, la boîte de dialogue doit également permettre au client de choisir d’utiliser ou non ses données par des fournisseurs spécifiques, y compris Adobe Experience Platform (565). |

### Chaînes de consentement {#consent-strings}

Quelle que soit la méthode que vous utilisez pour collecter les données, l’objectif est de générer une valeur de chaîne basée sur les options de consentement sélectionnées par le client ou la cliente, appelée chaîne de consentement.

Dans la spécification TCF, les chaînes de consentement sont utilisées pour coder les détails pertinents sur les paramètres de consentement d’un client ou d’une cliente, à des fins marketing spécifiques telles que définies par les politiques et les fournisseurs. Experience Platform utilise ces chaînes pour stocker les paramètres de consentement de chaque client. Par conséquent, une nouvelle chaîne de consentement doit être générée chaque fois que ces paramètres changent.

Les chaînes de consentement ne peuvent être créées que par un CMP enregistré auprès du IAB TCF. Pour plus d’informations sur la manière de générer des chaînes de consentement à l’aide de votre CMP spécifique, reportez-vous au [guide de formatage des chaînes de consentement](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) dans le référentiel GitHub IAB TCF.

## Créer des jeux de données avec des champs de consentement TCF {#datasets}

Les données de consentement du client doivent être envoyées aux jeux de données dont les schémas contiennent des champs de consentement TCF. Reportez-vous au tutoriel sur la [création de jeux de données pour capturer le consentement TCF 2.0](./dataset.md) pour savoir comment créer le jeu de données de profil requis (et un jeu de données d’événement d’expérience facultatif) avant de poursuivre avec ce guide.

## Mettre à jour [!DNL Profile] politiques de fusion pour inclure les données de consentement {#merge-policies}

Une fois que vous avez créé un jeu de données compatible avec [!DNL Profile] pour la collecte des données de consentement, vous devez vous assurer que vos politiques de fusion ont été configurées pour toujours inclure les champs de consentement TCF dans vos profils de clients. Cela implique de définir la priorité du jeu de données afin que votre jeu de données de consentement soit prioritaire sur les autres jeux de données potentiellement conflictuels.

Pour plus d’informations sur l’utilisation des politiques de fusion, reportez-vous à la [ présentation des politiques de fusion ](/help/profile/merge-policies/overview.md). Lors de la configuration de vos politiques de fusion, vous devez vous assurer que vos segments incluent tous les attributs de consentement requis fournis par le [groupe de champs de schéma de confidentialité XDM](./dataset.md#privacy-field-group), comme indiqué dans le guide sur la préparation des jeux de données.

## Intégrer Experience Platform Web SDK pour collecter les données de consentement des clients {#sdk}

>[!NOTE]
>
>L’utilisation d’Experience Platform Web SDK est nécessaire pour traiter les données de consentement directement dans Adobe Experience Platform. [!DNL Experience Cloud Identity Service] n’est pas pris en charge.
>
>Cependant, [!DNL Experience Cloud Identity Service] est toujours pris en charge pour le traitement du consentement dans Adobe Audience Manager et la conformité à TCF 2.0 nécessite uniquement que la bibliothèque soit mise à jour vers [ version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Une fois que vous avez configuré votre CMP pour générer des chaînes de consentement, vous devez intégrer Experience Platform Web SDK pour collecter ces chaînes et les envoyer à Experience Platform. Experience Platform SDK fournit deux commandes qui peuvent être utilisées pour envoyer des données de consentement TCF à Experience Platform (expliquées dans les sous-sections ci-dessous). Ces commandes doivent être utilisées lorsqu’un client ou une cliente fournit des informations de consentement pour la première fois, et chaque fois que le consentement change par la suite.

**Le SDK n’est pas compatible avec les CMP prêts à l’emploi**. C’est à vous de déterminer comment intégrer SDK à votre site web, d’être attentif aux modifications apportées au consentement dans la CMP et d’appeler la commande appropriée.

### Création dʼun flux de données

Pour que le SDK envoie des données à Experience Platform, vous devez d’abord créer un flux de données pour Experience Platform. Les étapes spécifiques de création d’un flux de données sont fournies dans la documentation de [SDK](/help/datastreams/overview.md).

Après avoir fourni un nom unique pour le flux de données, sélectionnez le bouton de basculement en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs suivantes pour compléter le reste du formulaire :

| Champ du flux de données | Valeur |
| --- | --- |
| [!UICONTROL Sandbox] | Nom de l’Experience Platform [sandbox](/help/sandboxes/home.md) qui contient la connexion en continu requise et les jeux de données pour configurer le flux de données. |
| [!UICONTROL Streaming Inlet] | Une connexion en continu valide pour Experience Platform. Consultez le tutoriel sur la [création d’une connexion en continu](/help/ingestion/tutorials/create-streaming-connection-ui.md) si vous ne disposez pas d’une entrée de flux en continu existante. |
| [!UICONTROL Event Dataset] | Sélectionnez le jeu de données [!DNL XDM ExperienceEvent] créé à l’[étape précédente](#datasets). Si vous avez inclus le groupe de champs [[!UICONTROL IAB TCF 2.0 Consent]](/help/xdm/field-groups/event/iab.md) dans le schéma de ce jeu de données, vous pouvez suivre les événements de changement de consentement au fil du temps à l’aide de la commande [`sendEvent`](#sendEvent) et stocker ces données dans ce jeu de données. Gardez à l’esprit que les valeurs de consentement stockées dans ce jeu de données ne sont **pas** utilisées dans les workflows d’application automatiques. |
| [!UICONTROL Profile Dataset] | Sélectionnez le jeu de données [!DNL XDM Individual Profile] créé à l’[étape précédente](#datasets). Lors de la réponse aux hooks de changement de consentement CMP à l’aide de la commande [`setConsent`](#setConsent), les données collectées sont stockées dans ce jeu de données. Comme ce jeu de données est activé pour Profil, les valeurs de consentement stockées dans ce jeu de données sont respectées lors des workflows d’application automatiques. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** en bas de l’écran et continuez à suivre les invites supplémentaires pour terminer la configuration.

### Exécution de commandes de modification du consentement

Une fois que vous avez créé le flux de données décrit dans la section précédente, vous pouvez commencer à utiliser les commandes SDK pour envoyer des données de consentement à Experience Platform. Les sections ci-dessous fournissent des exemples d’utilisation de chaque commande SDK dans différents scénarios.

#### Utilisation de hooks de modification du consentement CMP {#setConsent}

De nombreuses CMP fournissent des hooks prêts à l’emploi qui écoutent les événements de changement de consentement. Lorsque ces événements se produisent, vous pouvez utiliser la commande [`setConsent`](/help/collection/js/commands/setconsent.md) pour mettre à jour les données de consentement de ce client.

La commande `setConsent` attend deux arguments :

1. Chaîne qui indique le type de commande (dans ce cas, « setConsent »).
1. Payload contenant un tableau `consent`. Le tableau doit contenir au moins un objet qui fournit les champs de consentement requis.

La commande `setConsent` s’affiche ci-dessous :

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Propriété de payload | Description |
| --- | --- |
| `standard` | Norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `value` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGPD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué pour ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

La commande `setConsent` doit être utilisée dans le cadre d’un hook CMP qui détecte les modifications des paramètres de consentement. Le JavaScript suivant fournit un exemple de la manière dont la commande `setConsent` peut être utilisée pour le hook `OnConsentChanged` de OneTrust :

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Utilisation d’événements {#sendEvent}

Vous pouvez également collecter des données de consentement TCF 2.0 sur chaque événement déclenché dans Experience Platform à l’aide de la commande `sendEvent`.

>[!NOTE]
>
>Pour utiliser cette méthode, vous devez avoir ajouté le groupe de champs Confidentialité des événements d’expérience à votre schéma de [!DNL Profile] activé pour [!DNL XDM ExperienceEvent]. Voir la section [mise à jour du schéma ExperienceEvent](./dataset.md#event-schema) dans le guide de préparation des jeux de données pour savoir comment configurer cela.

La commande `sendEvent` doit être utilisée comme rappel dans les écouteurs d’événement appropriés sur votre site web. La commande attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, `sendEvent`), et (2) une payload contenant un objet `xdm` qui fournit les champs de consentement requis au format JSON :

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Propriété de payload | Description |
| --- | --- |
| `xdm.consentStrings` | Un tableau qui doit contenir au moins un objet qui fournit les champs de consentement requis. |
| `consentStandard` | Norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `consentStandardVersion` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `consentStringValue` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGPD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué pour ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

### Gestion des réponses SDK

De nombreuses commandes Web SDK renvoient des promesses indiquant si l’appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage de messages de confirmation au client. Voir [Réponses des commandes](/help/collection/js/commands/command-responses.md) pour plus d’informations.

## Exporter les segments {#export}

>[!NOTE]
>
>Avant de commencer à exporter des segments, vous devez vous assurer que vos segments incluent tous les champs de consentement obligatoires. Pour plus d’informations, consultez la section sur la [configuration des politiques de fusion](#merge-policies).

Une fois que vous avez collecté les données de consentement des clients et que vous avez créé des segments d’audience contenant les attributs de consentement requis, vous pouvez appliquer la conformité TCF 2.0 lors de l’exportation de ces segments vers des destinations en aval.

Si le `gdprApplies` de paramètre de consentement est défini sur `true` pour un ensemble de profils client, toutes les données de ces profils exportées vers des destinations en aval sont filtrées en fonction des préférences de consentement TCF pour chaque profil. Tout profil qui ne répond pas aux préférences de consentement requises est ignoré pendant le processus d’exportation.

Les clients doivent consentir aux fins suivantes (comme indiqué par les [politiques TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) pour que leurs profils soient inclus dans les segments qui sont exportés vers les destinations :

* **Objectif 1** : Stocker et/ou accéder à des informations sur un appareil
* **Objectif 10** : Développer et améliorer les produits

TCF 2.0 exige également que la source de données vérifie l’autorisation du fournisseur de la destination avant d’envoyer des données à cette destination. Ainsi, Experience Platform vérifie si l’autorisation du fournisseur de la destination est acceptée pour tous les identifiants du cluster avant d’inclure les données liées à cette destination.

>[!NOTE]
>
>Tous les segments partagés avec Adobe Audience Manager contiennent les mêmes valeurs de consentement TCF 2.0 que leurs homologues Experience Platform. Comme [!DNL Audience Manager] partage le même ID de fournisseur qu’Experience Platform (565), les mêmes objectifs et autorisations de fournisseur sont requis. Pour plus d’informations, consultez le document sur le plug-in [Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=fr).

## Tester votre implémentation {#test-implementation}

Une fois que vous avez configuré votre implémentation TCF 2.0 et que vous avez exporté des segments vers les destinations, toutes les données qui ne répondent pas aux exigences de consentement ne sont pas exportées. Pour vérifier si les profils client corrects ont été filtrés pendant l’exportation, vous devez vérifier manuellement les magasins de données sur vos destinations pour voir si le consentement a été correctement appliqué.

>[!IMPORTANT]
>
>Si plusieurs identifiants constituent un cluster et que TCF 2.0 s’applique, l’ensemble du cluster est exclu si même un seul identifiant ne contient pas les objectifs corrects et les autorisations du fournisseur.

## Étapes suivantes

Ce document couvrait le processus de configuration des opérations de données d’Experience Platform pour répondre aux obligations de votre entreprise telles qu’elles sont décrites dans le TCF 2.0. Consultez la présentation de la [gouvernance, confidentialité et sécurité](../../overview.md) pour plus d’informations sur les fonctionnalités d’Experience Platform relatives à la confidentialité.
