---
keywords: Experience Platform;accueil;IAB;IAB 2.0;consentement;consentement
solution: Experience Platform
title: Prise en charge du TCF 2.0 de l’IAB en Experience Platform
description: Découvrez comment configurer vos opérations de données et vos schémas pour transmettre les choix de consentement des clients lors de l’activation de segments vers des destinations dans Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 1%

---

# Prise en charge du TCF 2.0 de l’IAB dans Experience Platform

La variable [!DNL Transparency & Consent Framework] (TCF), comme indiqué par [!DNL Interactive Advertising Bureau] (IAB) est un cadre technique standard destiné à permettre aux organisations d’obtenir, d’enregistrer et de mettre à jour le consentement des consommateurs pour le traitement de leurs données personnelles, conformément aux directives de l’Union européenne. [!DNL General Data Protection Regulation] (RGPD). La deuxième itération de la structure, TCF 2.0, offre davantage de flexibilité quant à la manière dont les consommateurs peuvent fournir ou refuser le consentement, y compris si et comment les fournisseurs peuvent utiliser certaines fonctionnalités du traitement des données, telles que la géolocalisation précise.

>[!NOTE]
>
>Vous trouverez plus d’informations sur TCF 2.0 sur la page [Site de l’IAB Europe](https://iabeurope.eu/), y compris les documents d’assistance et les spécifications techniques.

Adobe Experience Platform fait partie de la [Liste des fournisseurs IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf/), sous l’ID **565**. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter des données de consentement des clients et de les intégrer à vos profils client stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si les profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

>[!IMPORTANT]
>
>Platform ne peut se conformer qu’à la version 2.0 du TCF (ou supérieure). Les versions précédentes de TCF ne sont pas prises en charge.

Ce document fournit un aperçu de la configuration de vos opérations de données et de vos schémas de profil pour accepter les données de consentement du client générées par votre plateforme de gestion du consentement (CMP). Elle couvre également la manière dont Platform transmet les choix de consentement de l’utilisateur lors de l’exportation de segments.

## Conditions préalables

Pour suivre ce guide, vous devez utiliser une CMP, commerciale ou personnelle, intégrée et conforme au TCF de l’IAB. Voir [liste des CMP conformes](https://iabeurope.eu/cmp-list/) pour plus d’informations.

>[!IMPORTANT]
>
>Si l’ID de votre CMP n’est pas valide, Platform continue à traiter vos données en l’état. Pour appliquer TCF 2.0, vous devez confirmer que votre CMP dispose d’un ID valide qui a été enregistré auprès de IAB TCF 2.0 avant d’envoyer des données à Platform.

Ce guide nécessite également une compréhension pratique des services Platform suivants :

* [Modèle de données d’expérience (XDM)](/help/xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données d’expérience client.
* [Service Adobe Experience Platform Identity](/help/identity-service/home.md): résout le problème fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les appareils et les systèmes.
* [Profil client en temps réel](/help/profile/home.md): Utilisations [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-Time Customer Profile] extrait les données du lac de données et conserve les profils client dans sa propre banque de données distincte.
* [SDK Web Adobe Experience Platform](/help/web-sdk/home.md): une bibliothèque JavaScript côté client qui vous permet d’intégrer divers services Platform à votre site web destiné aux clients.
   * [Commandes de consentement du SDK](../../../../web-sdk/commands/setconsent.md): présentation du cas d’utilisation des commandes du SDK liées au consentement présentée dans ce guide.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md): permet de diviser [!DNL Real-Time Customer Profile] données regroupées en groupes d’individus qui partagent des caractéristiques similaires et réagissent de la même manière aux stratégies marketing.

Outre les services Platform répertoriés ci-dessus, vous devez également connaître les [destinations](/help/data-governance/home.md) et leur rôle dans l’écosystème de Platform.

## Synthèse du flux de consentement du client {#summary}

Les sections suivantes décrivent la manière dont les données de consentement sont collectées et appliquées une fois le système correctement configuré.

### Collecte de données de consentement

Platform vous permet de collecter les données de consentement des clients par le biais du processus suivant :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site web.
1. Votre CMP détecte le changement de préférence de consentement et génère les données de consentement TCF en conséquence.
1. À l’aide du SDK Web Platform, les données de consentement générées (renvoyées par la CMP) sont envoyées à Adobe Experience Platform.
1. Les données de consentement collectées sont ingérées dans une [!DNL Profile]Jeu de données activé dont le schéma contient des champs de consentement TCF.

Outre les commandes du SDK déclenchées par les hooks de modification du consentement de la CMP, les données de consentement peuvent également être transmises à l’Experience Platform par le biais de toutes les données XDM générées par le client qui sont directement transférées vers un [!DNL Profile]Jeu de données activé.

Tout segment partagé avec Platform par Adobe Audience Manager (via [!DNL Audience Manager] connecteur source ou autre) peut également contenir des données de consentement si les champs appropriés ont été appliqués à ces segments via [!DNL Experience Cloud Identity Service]. Pour plus d’informations sur la collecte de données de consentement dans [!DNL Audience Manager], reportez-vous au document sur la page [Module externe Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=fr).

### Application du consentement en aval

Une fois que les données de consentement TCF ont été correctement ingérées, les processus suivants ont lieu dans les services Platform en aval :

1. [!DNL Real-Time Customer Profile] met à jour les données de consentement stockées pour le profil de ce client.
1. Platform traite les ID de client uniquement si l’autorisation du fournisseur pour Platform (565) est fournie pour chaque ID d’une grappe.
1. Lors de l’exportation de segments vers des destinations appartenant à la liste des fournisseurs TCF 2.0, Platform n’inclut les profils que si les autorisations de fournisseur pour les deux plateformes (565) *et* les destinations individuelles sont fournies pour chaque ID d’une grappe.

Les autres sections de ce document fournissent des conseils sur la configuration de Platform et de vos opérations de données pour répondre aux exigences de collecte et d’application décrites ci-dessus.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Chaque système de CMP étant unique, vous devez déterminer la meilleure manière de permettre à vos clients de fournir un consentement lorsqu’ils interagissent avec votre service. Une boîte de dialogue de consentement de cookie est un moyen courant d’obtenir le consentement du client. Vous trouverez ci-dessous un exemple de boîte de dialogue de CMP.

![Exemple de boîte de dialogue Plateforme de gestion du consentement .](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Cette boîte de dialogue doit permettre au client de s’abonner ou de se désabonner des éléments suivants :

| Option de consentement | Description |
| --- | --- |
| **Objectif** | Les objectifs définissent les objectifs technologiques des publicités pour lesquels une marque peut utiliser les données d’un client. Les objectifs suivants doivent être inscrits dans pour que Platform puisse traiter les ID de client : <ul><li>**Objectif 1**: stockage et/ou accès aux informations sur un appareil</li><li>**Objectif 10**: développez et améliorez des produits.</li></ul> |
| **Autorisations du fournisseur** | Outre les technologies publicitaires, la boîte de dialogue doit également permettre au client d’activer ou de désactiver l’utilisation de ses données par des fournisseurs spécifiques, y compris Adobe Experience Platform (565). |

### Chaînes de consentement {#consent-strings}

Quelle que soit la méthode que vous utilisez pour collecter les données, l’objectif est de générer une valeur de chaîne en fonction des options de consentement choisies par le client, appelée chaîne de consentement.

Dans la spécification TCF, les chaînes de consentement sont utilisées pour coder les détails pertinents sur les paramètres de consentement d’un client, en termes d’objectifs marketing spécifiques, tels que définis par les stratégies et les fournisseurs. Platform utilise ces chaînes pour stocker les paramètres de consentement de chaque client. Par conséquent, une nouvelle chaîne de consentement doit être générée chaque fois que ces paramètres changent.

Les chaînes de consentement ne peuvent être créées que par une CMP enregistrée auprès du TCF de l’IAB. Pour plus d’informations sur la génération de chaînes de consentement à l’aide de votre CMP spécifique, reportez-vous à la section [guide de formatage des chaînes de consentement](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) dans le référentiel GitHub du TCF de l’IAB.

## Création de jeux de données avec des champs de consentement TCF {#datasets}

Les données de consentement du client doivent être envoyées aux jeux de données dont les schémas contiennent des champs de consentement TCF. Consultez le tutoriel sur [création de jeux de données pour capturer le consentement TCF 2.0](./dataset.md) pour savoir comment créer le jeu de données de profil requis (et un jeu de données d’événement d’expérience facultatif) avant de poursuivre avec ce guide.

## Mettre à jour [!DNL Profile] stratégies de fusion pour inclure des données de consentement {#merge-policies}

Une fois que vous avez créé une [!DNL Profile]Jeu de données activé pour la collecte de données de consentement, vous devez vous assurer que vos stratégies de fusion ont été configurées pour toujours inclure des champs de consentement TCF dans vos profils client. Cela implique de définir la priorité du jeu de données afin que votre jeu de données de consentement soit hiérarchisé par rapport à d’autres jeux de données potentiellement conflictuels.

Pour plus d’informations sur l’utilisation des stratégies de fusion, reportez-vous au [présentation des stratégies de fusion](/help/profile/merge-policies/overview.md). Lors de la configuration de vos stratégies de fusion, vous devez vous assurer que vos segments incluent tous les attributs de consentement requis fournis par la variable [Groupe de champs de schéma de confidentialité XDM](./dataset.md#privacy-field-group), comme indiqué dans le guide sur la préparation des jeux de données.

## Intégrer le SDK Web Experience Platform pour collecter les données de consentement des clients {#sdk}

>[!NOTE]
>
>L’utilisation du SDK Web Experience Platform est requise pour traiter les données de consentement directement dans Adobe Experience Platform. [!DNL Experience Cloud Identity Service] n’est pas prise en charge.
>
>[!DNL Experience Cloud Identity Service] est toujours pris en charge pour le traitement du consentement dans Adobe Audience Manager, mais la conformité avec TCF 2.0 nécessite uniquement que la bibliothèque soit mise à jour vers [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Une fois que vous avez configuré votre CMP pour générer des chaînes de consentement, vous devez intégrer le SDK Web Experience Platform pour collecter ces chaînes et les envoyer à Platform. Le SDK Platform fournit deux commandes qui peuvent être utilisées pour envoyer des données de consentement du TCF à Platform (comme expliqué dans les sous-sections ci-dessous). Ces commandes doivent être utilisées lorsqu’un client fournit des informations de consentement pour la première fois et chaque fois que ce consentement change par la suite.

**Le SDK n’interface pas avec les CMP prêtes à l’emploi.**. C’est à vous de déterminer comment intégrer le SDK à votre site web, écouter les modifications apportées au consentement dans la CMP et appeler la commande appropriée.

### Création dʼun flux de données

Pour que le SDK envoie des données à l’Experience Platform, vous devez d’abord créer un flux de données pour Platform. Vous trouverez des étapes spécifiques pour créer un flux de données dans la section [Documentation du SDK](/help/datastreams/overview.md).

Après avoir fourni un nom unique pour la banque de données, cliquez sur le bouton de basculement en regard de **[!UICONTROL Adobe Experience Platform]**. Utilisez ensuite les valeurs suivantes pour compléter le reste du formulaire :

| Champ de flux de données | Valeur |
| --- | --- |
| [!UICONTROL Sandbox] | Nom de la plateforme [sandbox](/help/sandboxes/home.md) qui contient la connexion en continu et les jeux de données requis pour configurer le flux de données. |
| [!UICONTROL Inlet de diffusion en continu] | Une connexion en continu valide pour l’Experience Platform. Voir le tutoriel sur [création d’une connexion en continu](/help/ingestion/tutorials/create-streaming-connection-ui.md) si vous n’avez pas d’inlet de diffusion en continu existant. |
| [!UICONTROL Jeu de données d’événement] | Sélectionnez la variable [!DNL XDM ExperienceEvent] jeu de données créé dans [étape précédente](#datasets). Si vous avez inclus la variable [[!UICONTROL Consentement IAB TCF 2.0] groupe de champs](/help/xdm/field-groups/event/iab.md) dans le schéma de ce jeu de données, vous pouvez effectuer le suivi des événements de modification du consentement au fil du temps à l’aide de la variable [`sendEvent`](#sendEvent) , en stockant ces données dans ce jeu de données. Gardez à l’esprit que les valeurs de consentement stockées dans ce jeu de données sont **not** utilisé dans les workflows d’application automatique. |
| [!UICONTROL Jeu de données de profil] | Sélectionnez la variable [!DNL XDM Individual Profile] jeu de données créé dans [étape précédente](#datasets). Lorsque vous répondez aux hooks de modification du consentement de la CMP à l’aide de la variable [`setConsent`](#setConsent) , les données collectées sont stockées dans ce jeu de données. Comme ce jeu de données est activé pour Profile, les valeurs de consentement stockées dans ce jeu de données sont honorées pendant les workflows d’application automatique. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** en bas de l’écran et continuez à suivre les autres invites pour terminer la configuration.

### Exécution de commandes de changement de consentement

Une fois que vous avez créé le flux de données décrit dans la section précédente, vous pouvez commencer à utiliser les commandes du SDK pour envoyer des données de consentement à Platform. Les sections ci-dessous fournissent des exemples d’utilisation de chaque commande du SDK dans différents scénarios.

#### Utilisation des hooks de modification du consentement de la CMP {#setConsent}

De nombreuses CMP fournissent des hooks prêts à l’emploi qui écoutent les événements de modification du consentement. Lorsque ces événements se produisent, vous pouvez utiliser la variable [`setConsent`](/help/web-sdk/commands/setconsent.md) pour mettre à jour les données de consentement de ce client.

La variable `setConsent` La commande attend deux arguments :

1. Chaîne indiquant le type de commande (ici, &quot;setConsent&quot;).
1. Une payload contenant un `consent` tableau. Le tableau doit contenir au moins un objet qui fournit les champs de consentement requis.

La variable `setConsent` s’affiche ci-dessous :

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

| Propriété Payload | Description |
| --- | --- |
| `standard` | La norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `version` | Le numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `value` | Chaîne de consentement codée en base 64 générée par la CMP. |
| `gdprApplies` | Une valeur booléenne qui indique si le RGPD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué pour ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

La variable `setConsent` doit être utilisée dans le cadre d’un crochet CMP qui détecte les modifications apportées aux paramètres de consentement. Le code JavaScript suivant illustre la manière dont la variable `setConsent` peut être utilisée pour la fonction `OnConsentChanged` hook :

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

#### Utilisation des événements {#sendEvent}

Vous pouvez également collecter des données de consentement TCF 2.0 sur chaque événement déclenché dans Platform en utilisant la variable `sendEvent` .

>[!NOTE]
>
>Pour utiliser cette méthode, vous devez avoir ajouté le groupe de champs Confidentialité des événements d’expérience à votre [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schéma. Voir la section sur [mise à jour du schéma ExperienceEvent](./dataset.md#event-schema) dans le guide de préparation des jeux de données pour connaître les étapes de configuration.

La variable `sendEvent` doit être utilisée comme rappel dans les écouteurs d’événements appropriés de votre site web. La commande attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, `sendEvent`), et (2) un payload contenant une variable `xdm` qui fournit les champs de consentement requis au format JSON :

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

| Propriété Payload | Description |
| --- | --- |
| `xdm.consentStrings` | Tableau qui doit contenir au moins un objet qui fournit les champs de consentement requis. |
| `consentStandard` | La norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `consentStandardVersion` | Le numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `consentStringValue` | Chaîne de consentement codée en base 64 générée par la CMP. |
| `gdprApplies` | Une valeur booléenne qui indique si le RGPD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué pour ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

### Gestion des réponses du SDK

De nombreuses commandes du SDK Web renvoient des promesses indiquant si l’appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage des messages de confirmation au client. Voir [Réponses de commande](/help/web-sdk/commands/command-responses.md) pour plus d’informations.

## Exportation de segments {#export}

>[!NOTE]
>
>Avant de commencer l’exportation de segments, vous devez vous assurer que vos segments incluent tous les champs de consentement requis. Voir la section sur [configuration des stratégies de fusion](#merge-policies) pour plus d’informations.

Une fois que vous avez collecté les données de consentement du client et créé des segments d’audience contenant les attributs de consentement requis, vous pouvez ensuite appliquer la conformité TCF 2.0 lors de l’exportation de ces segments vers des destinations en aval.

Si le paramètre de consentement `gdprApplies` est défini sur `true` pour un ensemble de profils client, toutes les données de ces profils qui sont exportées vers des destinations en aval sont filtrées en fonction des préférences de consentement TCF pour chaque profil. Tout profil qui ne respecte pas les préférences de consentement requises est ignoré pendant le processus d’exportation.

Les clients doivent consentir aux finalités suivantes (comme indiqué par [Stratégies TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) pour que leurs profils soient inclus dans les segments qui sont exportés vers les destinations :

* **Objectif 1**: stockage et/ou accès aux informations sur un appareil
* **Objectif 10**: développez et améliorez des produits.

TCF 2.0 exige également que la source de données vérifie l’autorisation du fournisseur de la destination avant d’envoyer des données vers cette destination. Par conséquent, Platform vérifie si l’autorisation du fournisseur de la destination est activée sur pour tous les identifiants de la grappe avant d’inclure des données liées à cette destination.

>[!NOTE]
>
>Tous les segments partagés avec Adobe Audience Manager contiennent les mêmes valeurs de consentement TCF 2.0 que leurs homologues Platform. Depuis [!DNL Audience Manager] partage le même ID de fournisseur que Platform (565), les mêmes fins et les mêmes autorisations de fournisseur sont requises. Consultez le document sur la page [Module externe Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=fr) pour plus d’informations.

## Tester votre mise en oeuvre {#test-implementation}

Une fois que vous avez configuré votre mise en oeuvre TCF 2.0 et que vous avez exporté des segments vers des destinations, les données qui ne respectent pas les exigences de consentement ne seront pas exportées. Pour vérifier si les profils client corrects ont été filtrés pendant l’exportation, vous devez vérifier manuellement les entrepôts de données sur vos destinations pour vérifier si le consentement a été correctement appliqué.

>[!IMPORTANT]
>
>Si plusieurs identifiants constituent une grappe et que TCF 2.0 s’applique, l’ensemble de la grappe est exclu si même un seul identifiant ne contient pas les finalités correctes et les autorisations de fournisseur.

## Étapes suivantes

Ce document couvrait le processus de configuration de vos opérations de données Platform pour répondre à vos obligations commerciales, comme indiqué par le TCF 2.0. Consultez la présentation sur [gouvernance, confidentialité et sécurité](../../overview.md) pour plus d’informations sur les fonctionnalités liées à la confidentialité de Platform.
