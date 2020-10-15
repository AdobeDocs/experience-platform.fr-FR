---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: Prise en charge d’IAB TCF 2.0 dans la plate-forme de données client en temps réel
topic: privacy events
translation-type: tm+mt
source-git-commit: b24c624df188be3cbe7f71dcdf8a23d2478c287c
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 3%

---


# Prise en charge d’IAB TCF 2.0 dans [!DNL Real-time Customer Data Platform]

Le [!DNL Transparency & Consent Framework] (TCF), tel qu&#39;il est décrit par le [!DNL Interactive Advertising Bureau] (IAB), est un cadre technique ouvert visant à permettre aux organisations d&#39;obtenir, d&#39;enregistrer et de mettre à jour le consentement des consommateurs pour le traitement de leurs données personnelles, conformément à l&#39;Union européenne [!DNL General Data Protection Regulation] (GDPR). La deuxième version du cadre, TCF 2.0, offre une plus grande flexibilité quant à la manière dont les consommateurs peuvent fournir ou refuser le consentement, y compris quant à savoir si et comment les fournisseurs peuvent utiliser certaines caractéristiques du traitement des données, telles que la géolocalisation précise.

>[!NOTE]
>
>Pour plus d&#39;informations sur le TCF 2.0, consultez le site Web [de l&#39;](https://iabeurope.eu/tcf-2-0/)IAB Europe, y compris des documents d&#39;appui et des spécifications techniques.

[!DNL Real-time Customer Data Platform (Real-time CDP)] fait partie de la liste [du fournisseur](https://iabeurope.eu/vendor-list-tcf-v2-0/)IAB TCF 2.0 enregistrée, sous l’ID **565**. Conformément aux exigences de TCF 2.0, [!DNL Real-time CDP] vous permet de collecter les données de consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si les profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] est uniquement capable de se conformer à la version 2.0 du TCF (ou supérieure). Les versions précédentes de TCF ne sont pas prises en charge.

Ce document fournit une vue d’ensemble de la configuration de vos opérations de données et de vos schémas de profil pour accepter les données de consentement des clients générées par votre CMP, ainsi que de la manière dont [!DNL Real-time CDP] les choix de consentement des utilisateurs sont transmis lors de l’exportation de segments.

## Conditions préalables 

Afin de suivre ce guide, vous devez utiliser une plateforme de gestion du consentement (CMP), commerciale ou la vôtre, qui est intégrée et conforme au TCF de l&#39;IAB. Pour plus d&#39;informations, consultez la [liste des CMP](https://iabeurope.eu/cmp-list/) conformes.

>[!IMPORTANT]
>
>Si l&#39;ID de votre CMP n&#39;est pas valide, [!DNL Real-time CDP] continuera à traiter vos données en l&#39;état. Pour appliquer TCF 2.0, vous devez confirmer que votre CMP possède un ID valide qui a été enregistré auprès d’IAB TCF 2.0 avant d’envoyer des données à [!DNL Experience Platform].

Ce guide nécessite également une compréhension pratique des services Adobe Experience Platform suivants :

* [Modèle de données d’expérience (XDM)](../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel Experience organise les données d’expérience client.
* [Service](../../../identity-service/home.md)d&#39;identité Adobe Experience Platform : Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.
* [Real-time Customer Profile](../../../profile/home.md)[!DNL Identity Service] : exploite pour créer en temps réel des profils clients détaillés à partir de vos jeux de données. [!DNL Real-time Customer Profile] Profile extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Bibliothèque JavaScript côté client qui vous permet d’intégrer divers [!DNL Platform] services à votre site Web destiné aux clients.
   * [Commandes](../../../edge/consent/supporting-consent.md)de consentement SDK : Présentation des cas d’utilisation des commandes du SDK liées au consentement, présentée dans ce guide.
* [Service](../../../segmentation/home.md)de segmentation Adobe Experience Platform : Permet de diviser [!DNL Real-time Customer Profile] les données en groupes d’individus partageant des caractéristiques similaires et réagissant de la même manière aux stratégies marketing.

En plus des [!DNL Platform] services énumérés ci-dessus, vous devez également connaître les [destinations](../../destinations/destinations-overview.md) et leur utilisation dans [!DNL Real-time CDP]les.

## Récapitulatif du flux de consentement du client {#summary}

Les sections suivantes décrivent comment les données de consentement sont collectées et appliquées une fois que le système a été correctement configuré.

### Collecte de données de consentement

[!DNL Real-time CDP] vous permet de collecter les données de consentement des clients par le biais du processus suivant :

1. Un client fournit ses préférences de consentement pour la collecte de données par le biais d’une boîte de dialogue sur votre site Web.
1. Votre CMP détecte le changement de préférence de consentement et génère les données de consentement IAB en conséquence.
1. À l&#39;aide de [!DNL Experience Platform Web SDK]cette méthode, les données de consentement générées (renvoyées par le CMP) sont envoyées à Adobe Experience Platform.
1. Les données de consentement collectées sont ingérées dans un jeu de données [!DNL Profile]activé dont le schéma contient des champs de consentement IAB.

Outre les commandes du SDK déclenchées par les hooks de modification du consentement de CMP, les données de consentement peuvent également être transférées [!DNL Experience Platform] par le biais de toute donnée XDM générée par le client et directement transférées vers un jeu de données [!DNL Profile]activé.

Tout segment partagé avec [!DNL Platform] Adobe Audience Manager (par le biais du connecteur [!DNL Audience Manager] source ou autre) peut également contenir des données de consentement, à condition que les champs appropriés aient été appliqués à ces segments par [!DNL Experience Cloud Identity Service]. Pour plus d’informations sur la collecte des données de consentement dans [!DNL Audience Manager], voir le document du module externe [Adobe Audience Manager pour IAB TCF](https://docs.adobe.com/help/fr-FR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Application du consentement en aval

Une fois que les données de consentement IAB ont été correctement ingérées, les processus suivants ont lieu dans les [!DNL Real-time CDP] services en aval :

1. [!DNL Real-time Customer Profile] met à jour les données de consentement stockées pour le profil de ce client.
1. [!DNL Real-time CDP] traite les ID de client uniquement si l’autorisation fournisseur pour [!DNL Real-time CDP] (565) est fournie pour chaque ID d’une grappe.
1. Lors de l’exportation de segments vers des destinations appartenant à des membres de la liste fournisseur TCF 2.0, [!DNL Real-time CDP] inclut uniquement des profils si les autorisations du fournisseur pour [!DNL Real-time CDP] (565) ** et la destination sont fournies pour chaque ID d’une grappe.

Le reste des sections de ce document fournit des instructions sur la configuration [!DNL Real-time CDP] et les opérations de données pour répondre aux exigences de collecte et de mise en application décrites ci-dessus.

## Déterminer comment générer les données de consentement des clients dans votre CMP {#consent-data}

Chaque système CMP étant unique, vous devez déterminer la meilleure façon de permettre à vos clients de donner leur consentement lorsqu&#39;ils interagissent avec votre service. Pour ce faire, il est courant d’utiliser une boîte de dialogue de consentement des cookies, semblable à l’exemple suivant :

![](../assets/iab/cmp-dialog.png)

Cette boîte de dialogue doit permettre au client d&#39;opt-in ou de sortir des éléments suivants :

| Option de consentement | Description |
| --- | --- |
| **Objectifs** | Les fins permettent de définir les objectifs technologiques publicitaires pour lesquels une marque peut utiliser les données d’un client. Pour [!DNL Real-time CDP] traiter les ID de client, vous devez opter pour les objectifs suivants : <ul><li>**Objectif 1**: Stocker et/ou accéder aux informations sur un périphérique</li><li>**But 10**: Développer et améliorer les produits</li></ul> |
| **Autorisations du fournisseur** | Outre les technologies publicitaires, la boîte de dialogue doit également permettre au client de opt-in ou de ne pas utiliser ses données par des fournisseurs spécifiques, y compris [!DNL  Real-time CDP] (565). |

### Chaînes de consentement {#consent-strings}

Quelle que soit la méthode utilisée pour collecter les données, l’objectif est de générer une valeur de chaîne basée sur les options de consentement choisies par le client, appelée chaîne de consentement.

Dans la spécification TCF, les chaînes de consentement sont utilisées pour coder les détails pertinents sur les paramètres de consentement d&#39;un client, en termes d&#39;objectifs marketing spécifiques définis par les stratégies et les fournisseurs. [!DNL Real-time CDP] utilise ces chaînes pour stocker les paramètres de consentement de chaque client. Par conséquent, une nouvelle chaîne de consentement doit être générée chaque fois que ces paramètres changent.

Les chaînes de consentement ne peuvent être créées que par un CMP enregistré auprès du CCI TCF. Pour plus d&#39;informations sur la façon de générer des chaînes de consentement à l&#39;aide de votre CMP spécifique, consultez le guide [de formatage de la chaîne de](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) consentement dans la référence GitHub TCF de l&#39;IAB.

## Création de jeux de données avec des champs de consentement IAB {#datasets}

Les données de consentement du client doivent être envoyées à des jeux de données dont le schéma contient des champs de consentement IAB. Consultez le didacticiel sur la [création de jeux de données pour capturer le consentement](./dataset-preparation.md) TCF 2.0 pour savoir comment créer les deux jeux de données requis avant de continuer avec ce guide.

## Mettre à jour [!DNL Profile] les stratégies de fusion pour inclure les données de consentement {#merge-policies}

Une fois que vous avez créé un jeu de données [!DNL Profile]activé pour collecter les données de consentement, vous devez vous assurer que vos stratégies de fusion ont été configurées pour inclure systématiquement les champs de consentement IAB dans vos profils clients. Cela implique de définir la priorité des jeux de données afin que votre jeu de données de consentement soit hiérarchisé par rapport à d&#39;autres jeux de données potentiellement conflictuels.

Pour plus d’informations sur l’utilisation des stratégies de fusion, consultez le guide [d’utilisation des stratégies de](../../../profile/ui/merge-policies.md)fusion. Lors de la configuration de vos stratégies de fusion, vous devez vous assurer que vos segments incluent tous les attributs de consentement requis fournis par le mélange [de confidentialité](./dataset-preparation.md#privacy-mixin)XDM, comme indiqué dans le guide de préparation des jeux de données.

## Intégration du SDK [!DNL Experience Platform] Web pour collecter les données de consentement des clients {#sdk}

>[!NOTE]
>
>L&#39;utilisation du SDK [!DNL Experience Platform] Web est nécessaire pour traiter directement les données de consentement à Adobe Experience Platform. [!DNL Experience Cloud Identity Service] n’est actuellement pas prise en charge.
>
>[!DNL Experience Cloud Identity Service] est toujours pris en charge pour le traitement du consentement à Adobe Audience Manager, et la conformité à TCF 2.0 nécessite uniquement que la bibliothèque soit mise à jour vers la [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Une fois que vous avez configuré votre CMP pour générer des chaînes de consentement, vous devez intégrer le SDK [!DNL Experience Platform] Web pour collecter ces chaînes et les envoyer à [!DNL Platform]. Le [!DNL Platform] SDK fournit deux commandes qui peuvent être utilisées pour envoyer des données de consentement IAB à la plate-forme (expliquées dans les sous-sections ci-dessous) et qui doivent être utilisées lorsqu’un client fournit des informations de consentement pour la première fois, et chaque fois que ce consentement change par la suite.

**Le SDK n’interface pas avec les CMP prêtes à l’emploi**. Il vous appartient de déterminer comment intégrer le SDK à votre site Web, d’écouter les modifications apportées au consentement dans le CMP et d’appeler la commande appropriée.

### Créer une configuration de bord

Pour que le SDK envoie des données à [!DNL Experience Platform], vous devez d’abord créer une nouvelle configuration de périphérie pour [!DNL Platform] dans [!DNL Adobe Experience Platform Launch]. La documentation [du](../../../edge/fundamentals/edge-configuration.md)SDK décrit les étapes spécifiques à la création d’une nouvelle configuration.

Après avoir fourni un nom unique pour la configuration, sélectionnez le bouton bascule en regard de **[!UICONTROL Adobe Experience Platform]**. Ensuite, utilisez les valeurs suivantes pour compléter le reste du formulaire :

| Champ de configuration Edge | Valeur |
| --- | --- |
| [!UICONTROL Environnement de test] | Nom du [!DNL Platform] sandbox [](../../../sandboxes/home.md) qui contient la connexion de flux continu et les jeux de données requis pour configurer la configuration du bord. |
| [!UICONTROL Entrée de diffusion en continu] | Connexion en flux continu valide pour [!DNL Experience Platform]. Consultez le didacticiel sur la [création d’une connexion](../../../ingestion/tutorials/create-streaming-connection-ui.md) de diffusion en continu si vous n’avez pas d’entrée de diffusion existante. |
| [!UICONTROL Jeu de données événement] | Sélectionnez le [!DNL XDM ExperienceEvent] jeu de données créé à l’étape [](#datasets)précédente. |
| [!UICONTROL Jeu de données profil] | Sélectionnez le [!DNL XDM Individual Profile] jeu de données créé à l’étape [](#datasets)précédente. |

![](../assets/iab/edge-config.png)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]** en bas de l’écran et continuez à suivre les autres invites pour terminer la configuration.

### Commandes de modification du consentement

Une fois que vous avez créé la configuration de bord décrite dans la section précédente, vous pouvez début à l’aide des commandes SDK pour envoyer des données de consentement à [!DNL Platform]. Les sections ci-dessous fournissent des exemples d’utilisation de chaque commande SDK dans différents scénarios.

>[!NOTE]
>
>Pour une présentation de la syntaxe commune à toutes les commandes [!DNL Platform] SDK, voir le document sur l’ [exécution des commandes](../../../edge/fundamentals/executing-commands.md).

#### Utilisation de crochets de modification du consentement CMP

De nombreux CPM fournissent des crochets prêts à l&#39;emploi qui écoutent les événements de changement de consentement. Lorsque ces événements se produisent, vous pouvez utiliser la `setConsent` commande pour mettre à jour les données de consentement de ce client.

La `setConsent` commande attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, &quot;setConsent&quot;), et (2) une charge utile qui contient un `consent` tableau, qui doit contenir au moins un objet qui fournit les champs de consentement requis, comme indiqué ci-dessous :

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
| `standard` | Norme de consentement utilisée. Cette valeur doit être définie sur &quot;IAB&quot; pour le traitement du consentement TCF 2.0. |
| `version` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur &quot;2.0&quot; pour le traitement du consentement TCF 2.0. |
| `value` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué à ce client, la valeur doit être définie sur &quot;true&quot;. |

La `setConsent` commande doit être utilisée dans le cadre d&#39;un hook CMP qui détecte les modifications des paramètres de consentement. Le code JavaScript suivant fournit un exemple d&#39;utilisation de la `setConsent` commande pour le `OnConsentChanged` hook de OneTrust :

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

Vous pouvez également collecter des données de consentement TCF 2.0 sur chaque événement déclenché dans [!DNL Platform] le à l&#39;aide de la `sendEvent` commande.

>[!NOTE]
>
>Pour utiliser cette méthode, vous devez avoir ajouté la variable [!DNL Experience Event Privacy mixin] à votre [!DNL Profile]schéma [!DNL XDM ExperienceEvent] activé. Consultez la section relative à la [mise à jour du schéma](./dataset-preparation.md#event-schema) ExperienceEvent dans le guide de préparation des jeux de données pour connaître les étapes de configuration de ce .

La `sendEvent` commande doit être utilisée comme rappel dans les écouteurs de événement appropriés de votre site Web. La commande attend deux arguments : (1) une chaîne qui indique le type de commande (dans ce cas, &quot;sendEvent&quot;), et (2) une charge utile contenant un `xdm` objet qui fournit les champs de consentement requis en tant que JSON :

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
| `consentStandard` | Norme de consentement utilisée. Cette valeur doit être définie sur &quot;IAB&quot; pour le traitement du consentement TCF 2.0. |
| `consentStandardVersion` | Numéro de version de la norme de consentement indiquée sous `standard`. Cette valeur doit être définie sur &quot;2.0&quot; pour le traitement du consentement TCF 2.0. |
| `consentStringValue` | Chaîne de consentement codée en base 64 générée par le CMP. |
| `gdprApplies` | Valeur booléenne qui indique si le RGD s’applique au client actuellement connecté. Pour que TCF 2.0 soit appliqué à ce client, la valeur doit être définie sur &quot;true&quot;. |

### Gestion des réponses au SDK

Toutes les [!DNL Platform SDK] commandes renvoient des promesses qui indiquent si l&#39;appel a réussi ou échoué. Vous pouvez ensuite utiliser ces réponses pour une logique supplémentaire, telle que l’affichage de messages de confirmation à l’intention du client. Pour obtenir des exemples spécifiques, reportez-vous à la section relative à la [gestion des réussites ou des échecs](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) dans le guide relatif à l’exécution des commandes du SDK.

## Exportation de segments {#export}

>[!NOTE]
>
>Avant d’exporter des segments, vous devez vous assurer que vos segments incluent tous les champs de consentement obligatoires. Pour plus d’informations, voir la section relative à la [configuration des stratégies](#merge-policies) de fusion.

Une fois que vous avez collecté les données de consentement des clients et créé des segments d’audience contenant les attributs de consentement requis, vous pouvez ensuite appliquer la conformité TCF 2.0 lors de l’exportation de ces segments vers des destinations en aval.

Pour autant que le paramètre de consentement `gdprApplies` soit défini `true` pour un ensemble de profils client, les données provenant de ces profils qui sont exportés vers les destinations en aval sont filtrées en fonction des préférences de consentement pour chaque profil. Tout profil qui ne respecte pas les préférences de consentement requises est ignoré pendant le processus d’exportation.

Les clients doivent consentir aux objectifs suivants (décrits dans les stratégies [](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)TCF 2.0) pour que leurs profils soient inclus dans les segments exportés vers les destinations :

* **Objectif 1**: Stocker et/ou accéder aux informations sur un périphérique
* **But 10**: Développer et améliorer les produits

TCF 2.0 exige également que la source de données vérifie l&#39;autorisation du fournisseur de la destination avant d&#39;envoyer les données vers cette destination. Ainsi, [!DNL Real-time CDP] vérifie si l’autorisation du fournisseur de la destination est activée pour tous les ID de la grappe avant d’inclure les données liées à cette destination.

>[!NOTE]
>
>Tous les segments partagés avec Adobe Audience Manager contiendront les mêmes valeurs de consentement TCF 2.0 que leurs [!DNL Platform] homologues. Puisque [!DNL Audience Manager] partage le même ID de fournisseur que [!DNL Real-time CDP] (565), les mêmes fins et les mêmes autorisations de fournisseur sont requises. Pour plus d’informations, voir le document du module externe [Adobe Audience Manager pour IAB TCF](https://docs.adobe.com/help/fr-FR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) .

## Test your implementation {#test-implementation}

Une fois que vous avez configuré votre implémentation TCF 2.0 et que vous avez exporté des segments vers des destinations, les données qui ne respectent pas les conditions de consentement ne seront pas exportées. Toutefois, pour déterminer si les profils clients appropriés ont été filtrés lors de l’exportation, vous devez vérifier manuellement les entrepôts de données sur vos destinations afin de vérifier si le consentement a été correctement appliqué.

Il est important de noter que si plusieurs identifiants composent un cluster et que TCF 2.0 s’applique, l’ensemble du cluster sera exclu si même un seul identifiant ne contient pas les fins appropriées et les autorisations du fournisseur.

## Étapes suivantes

Ce document portait sur le processus de configuration de vos opérations de données [!DNL Real-time CDP] pour être conforme à TCF 2.0. Pour plus d&#39;informations sur les autres fonctionnalités de confidentialité fournies par [!DNL Real-time CDP], consultez la documentation suivante :

* [Confidentialité dans la plateforme de données client en temps réel](../privacy-overview.md)
* [Gouvernance des données sur la plateforme des données clients en temps réel](../data-governance-overview.md)