---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de la bibliothèque JavaScript d’Adobe Privacy
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 73%

---


# Présentation de la bibliothèque JavaScript d’Adobe Privacy

En tant que responsable du traitement des données, Adobe traite les données personnelles conformément aux autorisations et aux instructions de votre entreprise. En tant que contrôleur des données, vous déterminez les données personnelles qu’Adobe traite et stocke pour vous. Depending on the information you choose to send through Adobe Experience Cloud solutions, Adobe can store private information applicable to privacy regulations such as the [!DNL General Data Protection Regulation] (GDPR) and [!DNL California Consumer Privacy Act] (CCPA). Pour plus d’informations sur la manière dont les solutions Experience Cloud collectent les données privées, consultez le document sur la [confidentialité dans Adobe Experience Cloud](https://www.adobe.com/fr/privacy/experience-cloud.html).

La **bibliothèque JavaScript d’Adobe Privacy** permet aux contrôleurs de données d’automatiser la récupération de toutes les identités des titulaires de données générées par les solutions solutions pour un domaine spécifique. [!DNL Experience Cloud] Grâce à l’API fournie par [Adobe Experience Platform Privacy Service](home.md), ces identités peuvent ensuite être utilisées pour créer des demandes d’accès et de suppression de données privées appartenant à ces titulaires de données.

>[!NOTE]
>
>The [!DNL Privacy JS Library] typically only needs to be installed on privacy-related pages, and is not required to be installed on all pages of a website or domain.

## Fonctions

Le [!DNL Privacy JS Library] fournit plusieurs fonctions pour gérer les identités dans [!DNL Privacy Service]. Ces fonctions ne peuvent être utilisées que pour gérer les identités stockées dans le navigateur pour un visiteur spécifique. Ils ne peuvent pas être utilisés pour envoyer des informations directement à la [!DNL Experience Cloud Central Service] société.

Le tableau suivant décrit les différentes fonctions proposées par la bibliothèque :

| Fonction | Description |
| --- | --- |
| `retrieveIdentities` | Returns an array of matching identities (`validIds`) that were retrieved from [!DNL Privacy Service], as well as an array of identities that were not found (`failedIds`). |
| `removeIdentities` | Supprime chaque identité correspondante (valide) du navigateur. Renvoie un tableau d’identités correspondantes (`validIds`), chaque identité contenant une valeur booléenne `isDeleteClientSide` qui indique si cet identifiant a été supprimé. |
| `retrieveThenRemoveIdentities` | Récupère un tableau d’identités correspondantes (`validIds`), puis supprime ces identités du navigateur. Bien que cette fonction soit similaire à `removeIdentities`, il est préférable de l’utiliser lorsque la solution Adobe que vous utilisez nécessite une demande d’accès avant qu’une suppression soit possible (par exemple, lorsqu’un identifiant unique doit être récupéré avant de le fournir dans une demande de suppression). |

>[!NOTE]
>
>`removeIdentities` et `retrieveThenRemoveIdentities` ne suppriment les identités du navigateur que pour les solutions Adobe spécifiques qui les prennent en charge. Par exemple, Adobe Audience Manager ne supprime pas les identifiants demdex stockés dans des cookies tiers, alors qu’Adobe Target supprime tous les cookies qui stockent leurs identifiants.

Puisque les trois fonctions représentent des processus asynchrones, toutes les identités récupérées doivent être gérées à l’aide de rappels ou de promesses.


## Installation

To start using the [!DNL Privacy JS Library], you must install it onto your machine using one of the following methods:

* Installez-la à l’aide de npm en exécutant la commande suivante : `npm install @adobe/adobe-privacy`
* Utilisez l’extension Adobe Launch sous le nom d’`AdobePrivacy`
* Téléchargez-la depuis [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instanciez la variable [!DNL Privacy JS Library]

All apps that utilize the [!DNL Privacy JS Library] must instantiate a new `AdobePrivacy` object, which must be configured to a specific Adobe solution. Par exemple, une instanciation pour Adobe Analytics pourrait se présenter comme suit :

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Pour obtenir une liste complète des paramètres pris en charge pour les différentes solutions Adobe, reportez-vous à la section de l’annexe sur les [paramètres de configuration des solutions Adobe](#adobe-solution-configuration-parameters) pris en charge.

## Exemples de code

The following code samples demonstrate how to use the [!DNL Privacy JS Library] for several common scenarios, provided that you are not using [!DNL Launch] or DTM.

### Récupération d’identités

This example demonstrates how to retrieve a list of identities from [!DNL Experience Cloud].

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
| `failedIDs` | A JSON object containing all the IDs that were not retrieved from [!DNL Privacy Service], or otherwise could not be found. |

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
| `failedIDs` | A JSON object containing all the IDs that were not retrieved from [!DNL Privacy Service], or otherwise could not be found. |

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

By reading this document, you have been introduced to the core functionalities of the [!DNL Privacy JS Library]. After using the library to retrieve a list of identities, you can use those identities to create data access and delete requests to the [!DNL Privacy Service] API. Pour plus d’informations, consultez le [guide de développement de Privacy Service](api/getting-started.md).

## Annexe

This section contains supplemental information for using the [!DNL Privacy JS Library].

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
| `aamUUIDCookieName` | Nom du cookie propriétaire contenant l’identifiant unique de l’utilisateur renvoyé par Adobe Audience Manager. |

**Adobe ID Service (ECID)**

| Paramètre | Description |
| --- | --- |
| `imsOrgID` | Votre identifiant d’organisation IMS. |