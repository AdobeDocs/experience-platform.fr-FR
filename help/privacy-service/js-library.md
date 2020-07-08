---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de la bibliothèque JavaScript de confidentialité Adobe
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 5%

---


# Présentation de la bibliothèque JavaScript de confidentialité Adobe

En tant que traitement de données, Adobe traite les données personnelles conformément aux instructions et autorisations de votre société. En tant que contrôleur des données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. En fonction des informations que vous choisissez d’envoyer par le biais des solutions Adobe Experience Cloud, Adobe peut stocker des informations privées applicables aux règles de confidentialité, telles que le Règlement général sur la protection des données (RGPD) et la Loi sur la protection des renseignements personnels des consommateurs de Californie (CCPA). Pour plus d’informations sur la manière dont les solutions Experience Cloud collectent des données privées, consultez le document sur la [confidentialité dans Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) .

La bibliothèque **JavaScript de confidentialité** Adobe permet aux contrôleurs de données d’automatiser la récupération de toutes les identités de sujet de données générées par des solutions Experience Cloud pour un domaine spécifique. A l&#39;aide de l&#39;API fournie par [Adobe Experience Platform Privacy Service](home.md), ces identités peuvent ensuite être utilisées pour créer des requêtes d&#39;accès et de suppression de données privées appartenant à ces personnes.

>[!NOTE]
>
>En règle générale, la bibliothèque Privacy JS n&#39;a besoin d&#39;être installée que sur les pages liées à la confidentialité et n&#39;est pas requise pour être installée sur toutes les pages d&#39;un site Web ou d&#39;un domaine.

## Fonctions

La bibliothèque Privacy JS fournit plusieurs fonctions pour gérer les identités en Privacy Service. Ces fonctions ne peuvent être utilisées que pour gérer les identités stockées dans le navigateur pour un visiteur spécifique. Ils ne peuvent pas être utilisés pour envoyer directement des informations au Service Central Experience Cloud.

Le tableau suivant décrit les différentes fonctions fournies par la bibliothèque :

| Fonction | Description |
| --- | --- |
| `retrieveIdentities` | Renvoie un tableau d’identités (`validIds`) correspondantes qui ont été récupérées du Privacy Service, ainsi qu’un tableau d’identités qui n’ont pas été trouvées (`failedIds`). |
| `removeIdentities` | Supprime chaque identité correspondante (valide) du navigateur. Renvoie un tableau d’identités correspondantes (`validIds`), chaque identité contenant une `isDeleteClientSide` valeur booléenne indiquant si cet identifiant a été supprimé. |
| `retrieveThenRemoveIdentities` | Récupère un tableau d’identités correspondantes (`validIds`), puis supprime ces identités du navigateur. Bien que cette fonction soit similaire à `removeIdentities`la fonction, elle est mieux utilisée lorsque la solution Adobe que vous utilisez nécessite une demande d’accès avant la suppression (par exemple, lorsqu’un identifiant unique doit être récupéré avant de le fournir dans une demande de suppression). |

>[!NOTE]
>
>`removeIdentities` et `retrieveThenRemoveIdentities` uniquement supprimer des identités du navigateur pour des solutions Adobe spécifiques qui les prennent en charge. Par exemple, l’Adobe Audience Manager ne supprime pas les identifiants demdex stockés dans des cookies tiers, tandis que l’Adobe Target supprime tous les cookies qui stockent leurs identifiants.

Puisque les trois fonctions représentent des processus asynchrones, toute identité récupérée doit être gérée à l’aide de rappels ou de promesses.


## Installation

Pour début à l’aide de la bibliothèque Privacy JS, vous devez l’installer sur votre ordinateur à l’aide de l’une des méthodes suivantes :

* Installez à l&#39;aide de npm en exécutant la commande suivante : `npm install @adobe/adobe-privacy`
* Utilisez l’extension de lancement Adobe sous le nom `AdobePrivacy`
* Téléchargement depuis [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instanciation de la bibliothèque Privacy JS

Toutes les applications qui utilisent la bibliothèque JS Privacy doivent instancier un nouvel `AdobePrivacy` objet, qui doit être configuré pour une solution Adobe spécifique. Par exemple, une instanciation pour Adobe Analytics ressemblerait à ce qui suit :

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Pour une liste complète des paramètres pris en charge pour les différentes solutions Adobe, voir la section de l&#39;annexe sur les paramètres [de configuration des solutions](#adobe-solution-configuration-parameters)Adobe prises en charge.

## Exemples de code

Les exemples de code suivants montrent comment utiliser la bibliothèque JS Privacy pour plusieurs scénarios courants, à condition que vous n’utilisiez pas Launch ou DTM.

### Récupération d’identités

Cet exemple montre comment récupérer une liste d&#39;identités auprès d&#39;un Experience Cloud.

#### JavaScript

Le code suivant définit une fonction, `handleRetrievedIDs`à utiliser comme rappel ou promesse de gérer les identités récupérées par `retrieveIdentities`.

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
| `validIds` | Un objet JSON contenant tous les ID qui ont été récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n’ont pas été récupérés du Privacy Service ou qui n’ont pas été trouvés. |

#### Résultats

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

Cet exemple montre comment supprimer une liste d&#39;identités du navigateur.

#### JavaScript

Le code suivant définit une fonction, `handleRemovedIDs`à utiliser comme rappel ou promesse de gérer les identités récupérées `removeIdentities` après leur suppression du navigateur.

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
| `validIds` | Un objet JSON contenant tous les ID qui ont été récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n’ont pas été récupérés du Privacy Service ou qui n’ont pas été trouvés. |

#### Résultats

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

En lisant ce document, vous avez été initié aux fonctionnalités de base de la bibliothèque JS Privacy. Après avoir utilisé la bibliothèque pour récupérer une liste d’identités, vous pouvez utiliser ces identités pour créer un accès aux données et supprimer des requêtes à l’API du Privacy Service. Consultez le guide [du développeur](api/getting-started.md) Privacy Service pour plus d’informations.

## Annexe

Cette section contient des informations supplémentaires sur l’utilisation de la bibliothèque JS Privacy.

### Paramètres de configuration de la solution Adobe

Voici une liste des paramètres de configuration acceptés pour les solutions Adobe prises en charge, utilisés lors de l’ [instanciation d’un objet](#instantiate-the-privacy-js-library)AdobePrivacy.

**Adobe Analytics**

| Paramètre | Description |
| --- | --- |
| `cookieDomainPeriods` | Nombre de points dans un domaine pour le suivi des cookies (la valeur par défaut est 2). |
| `dataCenter` | Centre de données de collecte de données Adobe. Ceci ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. Les valeurs potentielles sont les suivantes : <ul><li>&quot;d1&quot; : Centre de données de San Jose.</li><li>&quot;d2&quot; : Centre de données de Dallas.</li></ul> |
| `reportSuite` | Identifiant de suite de rapports tel que spécifié dans la balise Web JavaScript (par exemple, &quot;s_code.js&quot; ou &quot;dtm&quot;). |
| `trackingServer` | Domaine de collecte de données (non-SSL). Ceci ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |
| `trackingServerSecure` | Domaine de collecte de données (SSL). Ceci ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |
| `visitorNamespace` | Espace de nommage utilisé pour regrouper des visiteurs. Ceci ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |

**Adobe Target**

| Paramètre | Description |
| --- | --- |
| `clientCode` | Code client qui identifie un client dans Adobe Target System. |

**Adobe Audience Manager**

| Paramètre | Description |
| --- | --- |
| `aamUUIDCookieName` | Nom du cookie propriétaire contenant l’identifiant utilisateur unique renvoyé par l’Adobe Audience Manager. |

**Adobe ID Service (ECID)**

| Paramètre | Description |
| --- | --- |
| `imsOrgID` | Votre ID d’organisation IMS. |