---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Présentation de la bibliothèque JavaScript Adobe Privacy
description: La bibliothèque JavaScript Adobe Privacy vous permet de récupérer les identités du sujet des données à utiliser dans Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 55%

---

# Présentation de la bibliothèque JavaScript d’Adobe Privacy

En tant que responsable du traitement des données, Adobe traite les données personnelles conformément aux autorisations et aux instructions de votre entreprise. En tant que contrôleuse ou contrôleur de données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. Selon les informations que vous choisissez d’envoyer par le biais des solutions Adobe Experience Cloud, Adobe peut stocker des informations privées applicables aux réglementations de confidentialité telles que [!DNL General Data Protection Regulation] (RGPD) et [!DNL California Consumer Privacy Act] (CCPA). Pour plus d’informations sur la manière dont les solutions Experience Cloud collectent les données privées, consultez le document sur la [confidentialité dans Adobe Experience Cloud](https://www.adobe.com/fr/privacy/experience-cloud.html).

La **bibliothèque JavaScript Adobe Privacy** permet aux contrôleurs de données d’automatiser la récupération de toutes les identités de sujet de données générées par les solutions [!DNL Experience Cloud] pour un domaine spécifique. Grâce à l’API fournie par [Adobe Experience Platform Privacy Service](home.md), ces identités peuvent ensuite être utilisées pour créer des demandes d’accès et de suppression de données privées appartenant à ces titulaires de données.

>[!NOTE]
>
>[!DNL Privacy JS Library] doit généralement être installé uniquement sur les pages liées à la confidentialité et ne doit pas l’être sur toutes les pages d’un site web ou d’un domaine.

## Fonctions

[!DNL Privacy JS Library] fournit plusieurs fonctions pour gérer les identités dans [!DNL Privacy Service]. Ces fonctions ne peuvent être utilisées que pour gérer les identités stockées dans le navigateur pour un visiteur spécifique. Ils ne peuvent pas être utilisés pour envoyer directement des informations à [!DNL Experience Cloud Central Service].

Le tableau suivant décrit les différentes fonctions proposées par la bibliothèque :

| Fonction | Description |
| --- | --- |
| `retrieveIdentities` | Renvoie un tableau d’identités correspondantes (`validIds`) qui ont été récupérées à partir de [!DNL Privacy Service], ainsi qu’un tableau d’identités introuvables (`failedIds`). |
| `removeIdentities` | Supprime chaque identité correspondante (valide) du navigateur. Renvoie un tableau d’identités correspondantes (`validIds`), chaque identité contenant une valeur booléenne `isDeletedClientSide` qui indique si cet identifiant a été supprimé. |
| `retrieveThenRemoveIdentities` | Récupère un tableau d’identités correspondantes (`validIds`), puis supprime ces identités du navigateur. Bien que cette fonction soit similaire à `removeIdentities`, il est préférable de l’utiliser lorsque la solution Adobe que vous utilisez nécessite une demande d’accès avant qu’une suppression soit possible (par exemple, lorsqu’un identifiant unique doit être récupéré avant de le fournir dans une demande de suppression). |

>[!NOTE]
>
>`removeIdentities` et `retrieveThenRemoveIdentities` suppriment uniquement les identités du navigateur pour les solutions d’Adobe spécifiques qui les prennent en charge. Par exemple, Adobe Audience Manager ne supprime pas les identifiants demdex stockés dans des cookies tiers, alors qu’Adobe Target supprime tous les cookies qui stockent leurs identifiants.

Puisque les trois fonctions représentent des processus asynchrones, toutes les identités récupérées doivent être gérées à l’aide de rappels ou de promesses.


## Installation

Pour commencer à utiliser le [!DNL Privacy JS Library], vous devez l’installer sur votre machine à l’aide de l’une des méthodes suivantes :

* Installez-la à l’aide de npm en exécutant la commande suivante : `npm install @adobe/adobe-privacy`
* Téléchargez à partir du [référentiel GitHub Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Vous pouvez également installer la bibliothèque par le biais d’une extension de balise. Pour plus d’informations, consultez la présentation de l’ [extension de la balise de confidentialité d’Adobe](../tags/extensions/client/privacy/overview.md) .

## Instanciez le [!DNL Privacy JS Library]

Toutes les applications qui utilisent [!DNL Privacy JS Library] doivent instancier un nouvel objet `AdobePrivacy`, qui doit être configuré pour une solution d’Adobe spécifique. Par exemple, une instanciation pour Adobe Analytics pourrait se présenter comme suit :

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Pour obtenir une liste complète des paramètres pris en charge pour les différentes solutions Adobe, reportez-vous à la section de l’annexe sur les [paramètres de configuration des solutions Adobe](#adobe-solution-configuration-parameters) pris en charge.

## Exemples de code {#samples}

Les exemples de code suivants montrent comment utiliser [!DNL Privacy JS Library] pour plusieurs scénarios courants, à condition que vous n’utilisiez pas de balises.

### Récupération d’identités

Cet exemple montre comment récupérer une liste d’identités de [!DNL Experience Cloud].

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
| `failedIDs` | Objet JSON contenant tous les identifiants qui n’ont pas été récupérés à partir de [!DNL Privacy Service] ou qui n’ont pas été trouvés. |

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
| `failedIDs` | Objet JSON contenant tous les identifiants qui n’ont pas été récupérés à partir de [!DNL Privacy Service] ou qui n’ont pas été trouvés. |

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

En lisant ce document, vous avez découvert les principales fonctionnalités de [!DNL Privacy JS Library]. Après avoir utilisé la bibliothèque pour récupérer une liste d’identités, vous pouvez utiliser ces identités pour créer des requêtes d’accès aux données et de suppression de données vers l’API [!DNL Privacy Service]. Pour plus d’informations, consultez le [guide de l’API du Privacy Service](api/overview.md) .

## Annexe

Cette section contient des informations supplémentaires sur l’utilisation de [!DNL Privacy JS Library].

### Paramètres de configuration des solutions Adobe {#config-params}

Voici une liste des paramètres de configuration acceptés pour les solutions Adobe prises en charge, utilisés lors de l’[instanciation d’un objet AdobePrivacy](#instantiate-the-privacy-js-library).

**Toutes les solutions**

| Paramètre | Description |
| --- | --- |
| `key` | Identifiant unique qui identifie l’utilisateur ou le sujet de données. Cette propriété est destinée à être utilisée à des fins de suivi interne et n’est pas utilisée par Adobe. |

**Adobe Analytics**

| Paramètre | Description |
| --- | --- |
| `cookieDomainPeriods` | Nombre de points dans un domaine utilisé pour le suivi des cookies (par défaut : `2`, par exemple `.domain.com`). Ne le définissez pas ici, sauf indication contraire dans votre balise Web JavaScript. |
| `dataCenter` | Centre de données de collecte de données d’Adobe. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. Les valeurs potentielles sont les suivantes : <ul><li>`d1` : centre de données de San Jose</li><li>`d2` : centre de données de Dallas</li></ul> |
| `reportSuite` | Identifiant de suite de rapports tel que spécifié dans la balise Web JavaScript (par exemple, `s_code.js` ou `dtm`). |
| `trackingServer` | Domaine de collecte de données non SSL. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |
| `trackingServerSecure` | Un domaine de collecte de données SSL. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |
| `visitorNamespace` | Espace de noms utilisé pour regrouper les visiteurs. Il ne doit être inclus que s’il est spécifié dans votre balise web JavaScript. |

**Adobe Audience Manager**

| Paramètre | Description |
| --- | --- |
| `aamUUIDCookieName` | Nom du cookie propriétaire contenant l’ID d’utilisateur unique renvoyé par Adobe Audience Manager. |

**Service Adobe Experience Cloud Identity (ECID)**

| Paramètre | Description |
| --- | --- |
| `imsOrgID` | Votre identifiant d’organisation. |

**Adobe Target**

| Paramètre | Description |
| --- | --- |
| `clientCode` | Code client qui identifie un client dans le système Adobe Target. |
