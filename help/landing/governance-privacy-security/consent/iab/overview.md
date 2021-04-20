---
keywords: Experience Platform ; accueil ; IAB ; IAB 2.0 ; consentement ; consentement
solution: Experience Platform
title: Prise en charge d’IAB TCF 2.0 dans l’Experience Platform
topic: privacy events
description: Découvrez comment configurer vos opérations de données et vos schémas pour transmettre les choix de consentement des clients lors de l’activation de segments vers des destinations dans Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a845ade0fc1e6e18c36b5f837fe7673a976f01c7
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 1%

---


# Prise en charge d’IAB TCF 2.0 dans l’Experience Platform

Le [!DNL Transparency & Consent Framework] (TCF), tel qu&#39;il est décrit par le [!DNL Interactive Advertising Bureau] (IAB), est un cadre technique ouvert visant à permettre aux organisations d&#39;obtenir, d&#39;enregistrer et de mettre à jour le consentement des consommateurs pour le traitement de leurs données personnelles, conformément à l&#39;Union européenne [!DNL General Data Protection Regulation] (GDPR). La deuxième version du cadre, TCF 2.0, offre une plus grande flexibilité quant à la manière dont les consommateurs peuvent fournir ou refuser le consentement, y compris quant à savoir si et comment les fournisseurs peuvent utiliser certaines caractéristiques du traitement des données, telles que la géolocalisation précise.

>[!NOTE]
>
>Vous trouverez de plus amples informations sur le TCF 2.0 sur le [site Web d&#39;IAB Europe](https://iabeurope.eu/tcf-2-0/), y compris des documents d&#39;appui et des spécifications techniques.

Adobe Experience Platform fait partie de la liste [fournisseur IAB TCF 2.0 ](https://iabeurope.eu/vendor-list-tcf-v2-0/) enregistrée, sous l&#39;ID **565**. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter les données de consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si les profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

>[!IMPORTANT]
>
>Plateforme est seulement capable de se conformer à la version 2.0 du TCF (ou supérieur). Les versions précédentes de TCF ne sont pas prises en charge.

Ce document fournit une vue d’ensemble de la configuration de vos opérations de données et de vos schémas de profil pour accepter les données de consentement des clients générées par votre CMP, ainsi que de la manière dont Plateforme transmet les choix de consentement des utilisateurs lors de l’exportation de segments.

## Conditions préalables

Afin de suivre ce guide, vous devez utiliser une plateforme de gestion du consentement (CMP), commerciale ou la vôtre, qui est intégrée et conforme au TCF de l&#39;IAB. Pour plus d&#39;informations, consultez la [liste des CMP conformes](https://iabeurope.eu/cmp-list/).

>[!IMPORTANT]
>
>Si l&#39;ID de votre CMP n&#39;est pas valide, la plate-forme continuera à traiter vos données en l&#39;état. Pour appliquer TCF 2.0, vous devez confirmer que votre CMP possède un ID valide qui a été enregistré auprès d’IAB TCF 2.0 avant d’envoyer les données à la plate-forme.

Ce guide nécessite également une compréhension pratique des services de plate-forme suivants :

* [Modèle de données d’expérience (XDM)](../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
* [Service](../../../../identity-service/home.md) d&#39;identité Adobe Experience Platform : Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [Profil](../../../../profile/home.md) client en temps réel : Exploite  [!DNL Identity Service] pour créer des profils client détaillés à partir de vos jeux de données en temps réel. [!DNL Real-time Customer Profile] Profile extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md) : Bibliothèque JavaScript côté client qui vous permet d’intégrer divers services de plate-forme à votre site Web destiné aux clients.
   * [Commandes](../../../../edge/consent/supporting-consent.md) de consentement SDK : Présentation des cas d’utilisation des commandes du SDK liées au consentement, présentée dans ce guide.
* [Service](../../../../segmentation/home.md) de segmentation Adobe Experience Platform : Permet de diviser  [!DNL Real-time Customer Profile] les données en groupes d’individus partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.

Outre les services de la Plateforme énumérés ci-dessus, vous devez également connaître [destinations](../../../../data-governance/home.md) et leur rôle dans l&#39;écosystème de la Plateforme.

## Récapitulatif du flux de consentement du client {#summary}

Les sections suivantes décrivent comment les données de consentement sont collectées et appliquées une fois que le système a été correctement configuré.

### Collecte de données de consentement

La plate-forme vous permet de collecter les données de consentement des clients par le biais du processus suivant :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site Web.
1. Votre CMP détecte le changement de préférence de consentement et génère les données de consentement du FCT en conséquence.
1. À l’aide du SDK Web de la plate-forme, les données de consentement générées (renvoyées par le CMP) sont envoyées à Adobe Experience Platform.
1. Les données de consentement collectées sont ingérées dans un jeu de données [!DNL Profile] activé dont le schéma contient des champs de consentement TCF.

Outre les commandes SDK déclenchées par les crochets de modification du consentement de CMP, les données de consentement peuvent également être transférées dans l&#39;Experience Platform par le biais de toute donnée XDM générée par le client et directement téléchargée dans un jeu de données [!DNL Profile] activé.

Tout segment partagé avec la plateforme par Adobe Audience Manager (par l&#39;intermédiaire du [!DNL Audience Manager] connecteur source ou autre) peut également contenir des données de consentement, à condition que les champs appropriés aient été appliqués à ces segments par l&#39;intermédiaire de [!DNL Experience Cloud Identity Service]. Pour plus d&#39;informations sur la collecte de données de consentement dans [!DNL Audience Manager], consultez le document du module externe [Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Application du consentement en aval

Une fois que les données de consentement TCF ont été correctement ingérées, les processus suivants ont lieu dans les services Plateforme en aval :

1. [!DNL Real-time Customer Profile] met à jour les données de consentement stockées pour le profil de ce client.
1. La plate-forme traite les ID de client uniquement si l’autorisation du fournisseur pour la plate-forme (565) est fournie pour chaque ID d’une grappe.
1. Lors de l’exportation de segments vers des destinations appartenant à des membres de la liste fournisseur TCF 2.0, la plate-forme inclut uniquement des profils si les autorisations du fournisseur pour la plate-forme (565) *et* la destination individuelle sont fournies pour chaque ID d’une grappe.

Le reste des sections de ce document explique comment configurer la plateforme et vos opérations de données pour répondre aux exigences de collecte et d&#39;application décrites ci-dessus.

## Déterminer comment générer des données de consentement client dans votre CMP {#consent-data}

Chaque système CMP étant unique, vous devez déterminer la meilleure façon de permettre à vos clients de donner leur consentement lorsqu&#39;ils interagissent avec votre service. Pour ce faire, il est courant d’utiliser une boîte de dialogue de consentement des cookies, semblable à l’exemple suivant :

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Cette boîte de dialogue doit permettre au client d&#39;opt-in ou de sortir des éléments suivants :

| Option de consentement | Description |
| --- | --- |
| **Objectifs** | Les fins permettent de définir les objectifs technologiques publicitaires pour lesquels une marque peut utiliser les données d’un client. Pour que Platform puisse traiter les ID de client, les objectifs suivants doivent être choisis : <ul><li>**Objectif 1** : Stocker et/ou accéder aux informations sur un périphérique</li><li>**But 10** : Développer et améliorer les produits</li></ul> |
| **Autorisations du fournisseur** | Outre les technologies publicitaires, la boîte de dialogue doit également permettre au client de opt-in ou de ne pas utiliser ses données par des fournisseurs spécifiques, y compris Adobe Experience Platform (565). |

### Chaînes de consentement {#consent-strings}

Quelle que soit la méthode utilisée pour collecter les données, l’objectif est de générer une valeur de chaîne basée sur les options de consentement choisies par le client, appelée chaîne de consentement.

Dans la spécification TCF, les chaînes de consentement sont utilisées pour coder les détails pertinents sur les paramètres de consentement d&#39;un client, en termes d&#39;objectifs marketing spécifiques définis par les stratégies et les fournisseurs. La plate-forme utilise ces chaînes pour stocker les paramètres de consentement de chaque client. Par conséquent, une nouvelle chaîne de consentement doit être générée chaque fois que ces paramètres changent.

Les chaînes de consentement ne peuvent être créées que par un CMP enregistré auprès du CCI TCF. Pour plus d&#39;informations sur la façon de générer des chaînes de consentement à l&#39;aide de votre CMP spécifique, consultez le [guide de formatage de la chaîne de consentement](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) dans le référentiel GitHub TCF de l&#39;IAB.

## Créer des jeux de données avec des champs de consentement TCF {#datasets}

Les données de consentement du client doivent être envoyées à des jeux de données dont les schémas contiennent des champs de consentement TCF. Reportez-vous au didacticiel sur la [création de jeux de données pour la capture du consentement TCF 2.0](./dataset.md) pour savoir comment créer les deux jeux de données requis avant de poursuivre avec ce guide.

## Mettre à jour les stratégies de fusion [!DNL Profile] pour inclure les données de consentement {#merge-policies}

Une fois que vous avez créé un jeu de données [!DNL Profile] activé pour collecter les données de consentement, vous devez vous assurer que vos stratégies de fusion ont été configurées pour inclure systématiquement les champs de consentement TCF dans vos profils clients. Cela implique de définir la priorité des jeux de données afin que votre jeu de données de consentement soit hiérarchisé par rapport à d&#39;autres jeux de données potentiellement conflictuels.

Pour plus d&#39;informations sur la façon d&#39;utiliser les stratégies de fusion, consultez le [guide de l&#39;utilisateur des stratégies de fusion](../../../../profile/ui/merge-policies.md). Lors de la configuration de vos stratégies de fusion, vous devez vous assurer que vos segments incluent tous les attributs de consentement requis fournis par le [mixin de confidentialité XDM](./dataset.md#privacy-mixin), comme indiqué dans le guide de préparation des jeux de données.

## Intégrer le SDK Web Experience Platform pour collecter les données de consentement des clients {#sdk}

>[!NOTE]
>
>L&#39;utilisation du SDK Web Experience Platform est nécessaire pour traiter directement les données de consentement dans Adobe Experience Platform. [!DNL Experience Cloud Identity Service] n’est actuellement pas prise en charge.
>
>[!DNL Experience Cloud Identity Service] est toujours pris en charge pour le traitement du consentement à Adobe Audience Manager, et la conformité à TCF 2.0 nécessite uniquement que la bibliothèque soit mise à jour vers la  [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Une fois que vous avez configuré votre CMP pour générer des chaînes de consentement, vous devez intégrer le SDK Web Experience Platform pour collecter ces chaînes et les envoyer à la plate-forme. Le SDK de plate-forme fournit deux commandes qui peuvent être utilisées pour envoyer des données de consentement TCF à Platform (expliquées dans les sous-sections ci-dessous), et qui doivent être utilisées lorsqu’un client fournit des informations de consentement pour la première fois, et chaque fois que ce consentement change par la suite.

**Le SDK n’interface pas avec les CMP prêtes à l’emploi**. Il vous appartient de déterminer comment intégrer le SDK à votre site Web, d’écouter les modifications apportées au consentement dans le CMP et d’appeler la commande appropriée.

### Créer une configuration de bord

Pour que le SDK envoie des données à l&#39;Experience Platform, vous devez d&#39;abord créer une nouvelle configuration de périphérie pour Platform dans [!DNL Adobe Experience Platform Launch]. Des étapes spécifiques pour créer une nouvelle configuration sont fournies dans la [documentation du SDK](../../../../edge/fundamentals/edge-configuration.md).

Après avoir fourni un nom unique pour la configuration, sélectionnez le bouton bascule en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs suivantes pour compléter le reste du formulaire :

| Champ de configuration Edge | Valeur |
| --- | --- |
| [!UICONTROL Environnement de test] | Nom de la plate-forme [sandbox](../../../../sandboxes/home.md) qui contient la connexion de flux continu et les jeux de données nécessaires pour configurer la configuration du bord. |
| [!UICONTROL Entrée de diffusion en continu] | Connexion de flux continu valide pour l’Experience Platform. Consultez le didacticiel sur [la création d&#39;une connexion de diffusion](../../../../ingestion/tutorials/create-streaming-connection-ui.md) si vous n&#39;avez pas d&#39;entrée de diffusion existante. |
| [!UICONTROL Jeu de données événement] | Sélectionnez le jeu de données [!DNL XDM ExperienceEvent] créé à l&#39;étape [précédente](#datasets). |
| [!UICONTROL Jeu de données profil] | Sélectionnez le jeu de données [!DNL XDM Individual Profile] créé à l&#39;étape [précédente](#datasets). |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** en bas de l’écran et continuez à suivre les invites supplémentaires pour terminer la configuration.

### Commandes de modification du consentement

Une fois que vous avez créé la configuration de bord décrite dans la section précédente, vous pouvez début à l’aide des commandes SDK pour envoyer des données de consentement à Platform. Les sections ci-dessous fournissent des exemples d’utilisation de chaque commande SDK dans différents scénarios.

>[!NOTE]
>
>Pour une introduction à la syntaxe commune pour toutes les commandes du SDK de plate-forme, voir le document sur [l&#39;exécution des commandes](../../../../edge/fundamentals/executing-commands.md).

#### Utilisation de crochets de modification du consentement CMP

De nombreux CPM fournissent des crochets prêts à l&#39;emploi qui écoutent les événements de changement de consentement. Lorsque ces événements se produisent, vous pouvez utiliser la commande `setConsent` pour mettre à jour les données de consentement de ce client.

La commande `setConsent` attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, &quot;setConsent&quot;) et (2) une charge utile qui contient un tableau `consent`, qui doit contenir au moins un objet qui fournit les champs de consentement requis, comme indiqué ci-dessous :

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
| `standard` | Norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `value` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué à ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

La commande `setConsent` doit être utilisée dans le cadre d&#39;un hook CMP qui détecte les modifications des paramètres de consentement. Le code JavaScript suivant fournit un exemple d&#39;utilisation de la commande `setConsent` pour le hook `OnConsentChanged` de OneTrust :

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

#### Utilisation de événements

Vous pouvez également collecter des données de consentement TCF 2.0 sur chaque événement déclenché dans Platform à l&#39;aide de la commande `sendEvent`.

>[!NOTE]
>
>Pour utiliser cette méthode, vous devez avoir ajouté [!DNL Experience Event Privacy mixin] à votre schéma [!DNL Profile] [!DNL XDM ExperienceEvent] activé. Consultez la section [mise à jour du schéma ExperienceEvent](./dataset.md#event-schema) dans le guide de préparation des jeux de données pour connaître les étapes de configuration de ce paramètre.

La commande `sendEvent` doit être utilisée comme rappel dans les écouteurs de événement appropriés de votre site Web. La commande attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, `sendEvent`) et (2) une charge utile contenant un objet `xdm` qui fournit les champs de consentement requis sous la forme JSON :

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
| `xdm.consentStrings` | Tableau qui doit contenir au moins un objet fournissant les champs de consentement requis. |
| `consentStandard` | Norme de consentement utilisée. Cette valeur doit être définie sur `IAB` pour le traitement du consentement TCF 2.0. |
| `consentStandardVersion` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur `2.0` pour le traitement du consentement TCF 2.0. |
| `consentStringValue` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué à ce client, la valeur doit être définie sur `true`. La valeur par défaut est `true` si elle n’est pas définie. |

### Gestion des réponses au SDK

Toutes les commandes [!DNL Platform SDK] renvoient des promesses indiquant si l&#39;appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage de messages de confirmation à l’intention du client. Pour obtenir des exemples spécifiques, reportez-vous à la section [gestion des réussites ou des échecs](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) du guide sur l’exécution des commandes du SDK.

## Exporter des segments {#export}

>[!NOTE]
>
>Avant d’exporter des segments, vous devez vous assurer que vos segments incluent tous les champs de consentement obligatoires. Pour plus d&#39;informations, consultez la section [Configuration des stratégies de fusion](#merge-policies).

Une fois que vous avez collecté les données de consentement des clients et créé des segments d’audience contenant les attributs de consentement requis, vous pouvez ensuite appliquer la conformité TCF 2.0 lors de l’exportation de ces segments vers des destinations en aval.

Pour autant que le paramètre de consentement `gdprApplies` soit défini sur `true` pour un ensemble de profils client, toutes les données des profils exportés vers les destinations en aval sont filtrées en fonction des préférences de consentement TCF pour chaque profil. Tout profil qui ne respecte pas les préférences de consentement requises est ignoré pendant le processus d’exportation.

Les clients doivent consentir aux objectifs suivants (décrits par les [stratégies TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) afin que leurs profils soient inclus dans les segments qui sont exportés vers les destinations :

* **Objectif 1** : Stocker et/ou accéder aux informations sur un périphérique
* **But 10** : Développer et améliorer les produits

TCF 2.0 exige également que la source de données vérifie l&#39;autorisation du fournisseur de la destination avant d&#39;envoyer les données vers cette destination. Par conséquent, la plate-forme vérifie si l’autorisation du fournisseur de la destination est sélectionnée pour tous les ID de la grappe avant d’inclure les données liées à cette destination.

>[!NOTE]
>
>Tous les segments partagés avec Adobe Audience Manager contiendront les mêmes valeurs de consentement TCF 2.0 que leurs homologues de Plateforme. Puisque [!DNL Audience Manager] partage le même ID de fournisseur que Platform (565), les mêmes fins et les mêmes autorisations de fournisseur sont requises. Pour plus d’informations, voir le document du [module externe Adobe Audience Manager pour IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

## Testez votre implémentation {#test-implementation}

Une fois que vous avez configuré votre implémentation TCF 2.0 et que vous avez exporté des segments vers des destinations, les données qui ne respectent pas les conditions de consentement ne seront pas exportées. Toutefois, pour déterminer si les profils clients appropriés ont été filtrés lors de l’exportation, vous devez vérifier manuellement les entrepôts de données sur vos destinations afin de vérifier si le consentement a été correctement appliqué.

Il est important de noter que si plusieurs identifiants composent un cluster et que TCF 2.0 s’applique, l’ensemble du cluster sera exclu si même un seul identifiant ne contient pas les fins appropriées et les autorisations du fournisseur.

## Étapes suivantes

Ce document portait sur le processus de configuration de vos opérations de données de plateforme pour répondre à vos obligations commerciales, comme l&#39;indique le TCF 2.0. Pour plus d&#39;informations, consultez la présentation de [gouvernance, confidentialité et sécurité](../../overview.md).