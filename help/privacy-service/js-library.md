---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Présentation de la bibliothèque JavaScript de confidentialité des Adobes
topic-legacy: overview
description: La bibliothèque JavaScript de confidentialité des Adobes vous permet de récupérer les identités des personnes concernées en vue de les utiliser dans le Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
translation-type: tm+mt
source-git-commit: b70e693b4ffeda561de4d4c8dd8fd1adeec489f7
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 68%

---

# Présentation de la bibliothèque JavaScript d’Adobe Privacy

En tant que responsable du traitement des données, Adobe traite les données personnelles conformément aux autorisations et aux instructions de votre entreprise. En tant que contrôleur des données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. En fonction des informations que vous choisissez d&#39;envoyer par l&#39;intermédiaire des solutions Adobe Experience Cloud, l&#39;Adobe peut stocker des informations privées applicables aux règlements sur la protection des renseignements personnels, comme les [!DNL General Data Protection Regulation] (RGPD) et [!DNL California Consumer Privacy Act] (ACCP). Pour plus d’informations sur la manière dont les solutions Experience Cloud collectent les données privées, consultez le document sur la [confidentialité dans Adobe Experience Cloud](https://www.adobe.com/fr/privacy/experience-cloud.html).

La **bibliothèque JavaScript d’Adobe Privacy** permet aux contrôleurs de données d’automatiser la récupération de toutes les identités des titulaires de données générées par les solutions solutions pour un domaine spécifique. [!DNL Experience Cloud] Grâce à l’API fournie par [Adobe Experience Platform Privacy Service](home.md), ces identités peuvent ensuite être utilisées pour créer des demandes d’accès et de suppression de données privées appartenant à ces titulaires de données.

>[!NOTE]
>
>En règle générale, [!DNL Privacy JS Library] ne doit être installé que sur les pages liées à la confidentialité et n&#39;est pas nécessaire pour être installé sur toutes les pages d&#39;un site Web ou d&#39;un domaine.

## Fonctions

Le [!DNL Privacy JS Library] fournit plusieurs fonctions de gestion des identités dans [!DNL Privacy Service]. Ces fonctions ne peuvent être utilisées que pour gérer les identités stockées dans le navigateur pour un visiteur spécifique. Ils ne peuvent pas être utilisés pour envoyer directement des informations à [!DNL Experience Cloud Central Service].

Le tableau suivant décrit les différentes fonctions proposées par la bibliothèque :

| Fonction | Description |
| --- | --- |
| `retrieveIdentities` | Renvoie un tableau d’identités correspondantes (`validIds`) qui ont été récupérées à partir de [!DNL Privacy Service], ainsi qu’un tableau d’identités introuvables (`failedIds`). |
| `removeIdentities` | Supprime chaque identité correspondante (valide) du navigateur. Renvoie un tableau d’identités correspondantes (`validIds`), chaque identité contenant une valeur booléenne `isDeletedClientSide` qui indique si cet identifiant a été supprimé. |
| `retrieveThenRemoveIdentities` | Récupère un tableau d’identités correspondantes (`validIds`), puis supprime ces identités du navigateur. Bien que cette fonction soit similaire à `removeIdentities`, il est préférable de l’utiliser lorsque la solution Adobe que vous utilisez nécessite une demande d’accès avant qu’une suppression soit possible (par exemple, lorsqu’un identifiant unique doit être récupéré avant de le fournir dans une demande de suppression). |

>[!NOTE]
>
>`removeIdentities` et `retrieveThenRemoveIdentities` ne suppriment les identités du navigateur que pour les solutions Adobe spécifiques qui les prennent en charge. Par exemple, Adobe Audience Manager ne supprime pas les identifiants demdex stockés dans des cookies tiers, alors qu’Adobe Target supprime tous les cookies qui stockent leurs identifiants.

Puisque les trois fonctions représentent des processus asynchrones, toutes les identités récupérées doivent être gérées à l’aide de rappels ou de promesses.


## Installation

Pour début à l&#39;aide de [!DNL Privacy JS Library], vous devez l&#39;installer sur votre ordinateur en utilisant l&#39;une des méthodes suivantes :

* Installez-la à l’aide de npm en exécutant la commande suivante : `npm install @adobe/adobe-privacy`
* Installez l’extension de confidentialité de l’Adobe à l’aide de [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en) sous le nom `AdobePrivacy`.
* Téléchargement à partir du [référentiel GitHub Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instancier le [!DNL Privacy JS Library]

Toutes les applications qui utilisent [!DNL Privacy JS Library] doivent instancier un nouvel objet `AdobePrivacy`, qui doit être configuré pour une solution d&#39;Adobe spécifique. Par exemple, une instanciation pour Adobe Analytics pourrait se présenter comme suit :

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Pour obtenir une liste complète des paramètres pris en charge pour les différentes solutions Adobe, reportez-vous à la section de l’annexe sur les [paramètres de configuration des solutions Adobe](#adobe-solution-configuration-parameters) pris en charge.

## Exemples de code

Les exemples de code suivants montrent comment utiliser [!DNL Privacy JS Library] pour plusieurs scénarios courants, à condition que vous n&#39;utilisiez pas [!DNL Platform Launch].

### Récupération d’identités

Cet exemple montre comment récupérer une liste d&#39;identités de [!DNL Experience Cloud].

#### JavaScript

Le code suivant définit une fonction, `handleRetrievedIDs`, à utiliser comme rappel ou promesse pour gérer les identités récupérées par `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variable | Description |
| --- | --- |
| `validIds` | Objet JSON contenant tous les identifiants récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n&#39;ont pas été récupérés à partir de [!DNL Privacy Service] ou qui n&#39;ont pas été trouvés. |

#### Résultat

Si le code s’exécute correctement, `validIDs` est renseigné par une liste d’identités récupérées.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Suppression d’identités

Cet exemple montre comment supprimer une liste d’identités du navigateur.

#### JavaScript

Le code suivant définit une fonction, `handleRemovedIDs`, à utiliser comme rappel ou promesse pour gérer les identités récupérées par `removeIdentities` après leur suppression du navigateur.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variable | Description |
| --- | --- |
| `validIds` | Objet JSON contenant tous les identifiants récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n&#39;ont pas été récupérés à partir de [!DNL Privacy Service] ou qui n&#39;ont pas été trouvés. |

#### Résultat

Si le code s’exécute correctement, `validIDs` est renseigné par une liste d’identités récupérées.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Étapes suivantes

En lisant ce document, vous avez été initié aux fonctionnalités de base de [!DNL Privacy JS Library]. Après avoir utilisé la bibliothèque pour récupérer une liste d&#39;identités, vous pouvez utiliser ces identités pour créer un accès aux données et supprimer des requêtes à l&#39;API [!DNL Privacy Service]. Pour plus d’informations, consultez le [guide de développement de Privacy Service](api/getting-started.md).

## Annexe

Cette section contient des informations supplémentaires sur l&#39;utilisation de [!DNL Privacy JS Library].

### Paramètres de configuration des solutions Adobe

Voici une liste des paramètres de configuration acceptés pour les solutions Adobe prises en charge, utilisés lors de l’[instanciation d’un objet AdobePrivacy](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Paramètre | Description |
| --- | --- |
| `cookieDomainPeriods` | Nombre de points dans un domaine pour le suivi des cookies (par défaut, 2). |
| `dataCenter` | Centre de collecte de données Adobe. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. Les valeurs potentielles sont les suivantes : <ul><li>« d1 » : centre de données de San José.</li><li>« d2 » : centre de données de Dallas.</li></ul> |
| `reportSuite` | Identifiant de suite de rapports tel que spécifié dans votre balise web JavaScript (par exemple, « s_code.js » ou « dtm »). |
| `trackingServer` | Domaine de collecte de données (non-SSL). Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |
| `trackingServerSecure` | Domaine de collecte de données (SSL). Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |
| `visitorNamespace` | Espace de noms utilisé pour regrouper les visiteurs. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |

**Adobe Target**

| Paramètre | Description |
| --- | --- |
| `clientCode` | Code client qui identifie un client dans le système Adobe Target. |

**Adobe Audience Manager**

| Paramètre | Description |
| --- | --- |
| `aamUUIDCookieName` | Nom du cookie propriétaire contenant l’ID d’utilisateur unique renvoyé par Adobe Audience Manager. |

**Adobe ID Service (ECID)**

| Paramètre | Description |
| --- | --- |
| `imsOrgID` | Votre identifiant d’organisation IMS. |
