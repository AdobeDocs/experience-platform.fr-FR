---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de la bibliothèque JavaScript Adobe Privacy
topic: overview
translation-type: tm+mt
source-git-commit: 3b916ac5529db6ca383bf8bad56961bb1b8a0b0c

---


# Présentation de la bibliothèque JavaScript Adobe Privacy

En tant que traitement de données, Adobe traite les données personnelles conformément à vos instructions et à vos  d’autorisation. En tant que contrôleur des données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. En fonction des informations que vous choisissez d’envoyer par le biais des solutions Adobe Experience Cloud, Adobe peut stocker des informations privées applicables aux règles de confidentialité, telles que le Règlement général sur la protection des données (GDPR) et la Loi sur la protection des renseignements personnels des consommateurs (CCPA) de Californie. Pour plus d’informations sur la manière dont les solutions Experience Cloud collectent des données privées, reportez-vous au  sur la [confidentialité dans Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) .

La bibliothèque **JavaScript** Adobe Privacy permet aux contrôleurs de données d’automatiser la récupération de toutes les identités de sujet de données générées par les solutions Experience Cloud pour un domaine spécifique. A l’aide de l’API fournie par [Adobe Experience Platform Privacy Service](home.md), ces identités peuvent ensuite être utilisées pour créer des demandes d’accès et de suppression de données privées appartenant à ces personnes.

>[!NOTE] En règle générale, la bibliothèque JS de confidentialité ne doit être installée que sur les pages liées à la confidentialité et n’est pas nécessaire sur toutes les pages d’un site Web ou d’un domaine.

## Fonctions

La bibliothèque Privacy JS fournit plusieurs fonctions pour gérer les identités dans Privacy Service. Ces fonctions ne peuvent être utilisées que pour gérer les identités stockées dans le navigateur pour un spécifique. Elles ne peuvent pas être utilisées pour envoyer directement des informations au service Central Experience Cloud.

Le tableau suivant décrit les différentes fonctions fournies par la bibliothèque :

| Fonction | Description |
| --- | --- |
| `retrieveIdentities` | Renvoie un tableau d’identités (`validIds`) correspondantes qui ont été extraites de Privacy Service, ainsi qu’un tableau d’identités introuvables (`failedIds`). |
| `removeIdentities` | Supprime chaque identité correspondante (valide) du navigateur. Renvoie un tableau d’identités correspondantes (`validIds`), chaque identité contenant une `isDeleteClientSide` valeur booléenne indiquant si cet identifiant a été supprimé. |
| `retrieveThenRemoveIdentities` | Récupère un tableau d’identités correspondantes (`validIds`), puis supprime ces identités du navigateur. Bien que cette fonction soit similaire à `removeIdentities`celle-ci, elle est préférable lorsque la solution Adobe que vous utilisez nécessite une demande d’accès avant la suppression (par exemple, lorsqu’un identifiant unique doit être récupéré avant de le fournir dans une demande de suppression). |

>[!NOTE] `removeIdentities` et `retrieveThenRemoveIdentities` uniquement supprimer des identités du navigateur pour des solutions Adobe spécifiques qui les prennent en charge. Par exemple, Adobe   Manager ne supprime pas les ID demdex stockés dans des cookies tiers, tandis qu’Adobe supprime tous les cookies qui stockent leurs ID.

Puisque les trois fonctions représentent des processus asynchrones, toutes les identités récupérées doivent être gérées à l’aide de rappels ou de promesses.


## Installation

Pour  à l’aide de la bibliothèque JS de confidentialité, vous devez l’installer sur votre ordinateur à l’aide de l’une des méthodes suivantes :

* Installez à l’aide de npm en exécutant la commande suivante : `npm install @adobe/adobe-privacy`
* Utilisez Adobe Launch Extension sous le nom `AdobePrivacy`
* Télécharger à partir de [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instanciation de la bibliothèque JS de confidentialité

Toutes les applications qui utilisent la bibliothèque JS de confidentialité doivent instancier un nouvel `AdobePrivacy` objet, qui doit être configuré pour une solution Adobe spécifique. Par exemple, une instanciation pour Adobe Analytics se présente comme suit :

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Pour un complet des paramètres pris en charge pour les différentes solutions Adobe, reportez-vous à la section de l’annexe sur les paramètres [de configuration des solutions](#adobe-solution-configuration-parameters)Adobe pris en charge.

## Exemples de code

Les exemples de code suivants montrent comment utiliser la bibliothèque JS de confidentialité pour plusieurs scénarios courants, à condition que vous n’utilisiez pas Launch ou DTM.

### Récupération d’identités

Cet exemple montre comment récupérer un d’identités à partir d’Experience Cloud.

#### JavaScript

Le code suivant définit une fonction `handleRetrievedIDs`, à utiliser comme rappel ou promesse de gérer les identités récupérées par `retrieveIdentities`.

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
| `validIds` | Objet JSON contenant tous les ID récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n’ont pas été récupérés auprès de Privacy Service ou qui n’ont pas été trouvés. |

#### Résultats

Si le code s’exécute correctement, `validIDs` est renseigné par un d’identités récupérées.

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

Cet exemple montre comment supprimer un d’identités du navigateur.

#### JavaScript

Le code suivant définit une fonction `handleRemovedIDs`, à utiliser comme rappel ou promesse de gérer les identités récupérées `removeIdentities` après leur suppression du navigateur.

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
| `validIds` | Objet JSON contenant tous les ID récupérés avec succès. |
| `failedIDs` | Un objet JSON contenant tous les ID qui n’ont pas été récupérés auprès de Privacy Service ou qui n’ont pas été trouvés. |

#### Résultats

Si le code s’exécute correctement, `validIDs` est renseigné par un d’identités récupérées.

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

En lisant ce , vous avez été initié aux fonctionnalités de base de la bibliothèque JS de confidentialité. Après avoir utilisé la bibliothèque pour récupérer un d’identités, vous pouvez utiliser ces identités pour créer un accès aux données et supprimer des requêtes à l’API de Privacy Service. Pour plus d’informations, consultez le guide [du développeur](api/getting-started.md) Privacy Service.

## Annexe

Cette section contient des informations supplémentaires sur l’utilisation de la bibliothèque JS de confidentialité.

### Paramètres de configuration de la solution Adobe

Voici un  des paramètres de configuration acceptés pour les solutions Adobe prises en charge, utilisés lors de l’ [instanciation d’un objet](#instantiate-the-privacy-js-library)AdobePrivacy.

**Adobe Analytics**

| Paramètre | Description |
| --- | --- |
| `cookieDomainPeriods` | Nombre de points dans un domaine pour le suivi des cookies (la valeur par défaut est 2). |
| `dataCenter` | Centre de données de collecte de données Adobe. Cela ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. Les valeurs potentielles sont les suivantes : <ul><li>&quot;d1&quot; : Centre de données de San Jose.</li><li>&quot;d2&quot; : Centre de données de Dallas.</li></ul> |
| `reportSuite` | Identifiant de suite de rapports tel que spécifié dans la balise Web JavaScript (par exemple, &quot;s_code.js&quot; ou &quot;dtm&quot;). |
| `trackingServer` | Domaine de collecte de données (non-SSL). Cela ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |
| `trackingServerSecure` | Domaine de collecte de données (SSL). Cela ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |
| `visitorNamespace` |   était utilisé pour regrouper les. Cela ne doit être inclus que s’il est spécifié dans la balise Web JavaScript. |

**Adobe Target**

| Paramètre | Description |
| --- | --- |
| `clientCode` | Code client qui identifie un client dans Adobe System. |

**Adobe Audience Manager**

| Paramètre | Description |
| --- | --- |
| `aamUUIDCookieName` | Nom du cookie propriétaire contenant l’ID utilisateur unique renvoyé par Adobe  Gestionnaire de  de. |

**Adobe ID Service (ECID)**

| Paramètre | Description |
| --- | --- |
| `imsOrgID` | Votre ID d’organisation IMS. |