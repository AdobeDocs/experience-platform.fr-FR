---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Authentification et accès aux API des plateformes d’expérience
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Authentification et accès aux API de plateforme d’expérience

Ce fournit un didacticiel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels aux API de la plateforme d’expérience.

## Authentifier pour effectuer des appels d’API

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les demandes aux API d’E/S Adobe doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Le JWT est ensuite utilisé avec les informations spécifiques au client pour générer vos  personnelles.

Ce didacticiel décrit les étapes de l’authentification par la création d’un  décrit dans l’organigramme suivant :
![](images/authentication/authentication-flowchart.png)

## Conditions préalables

Pour réussir les appels aux API de plateforme d’expérience, vous devez disposer des éléments suivants :

* Une organisation IMS ayant accès à Adobe Experience Platform
* Un compte Adobe ID enregistré
* Administrateur de la Console d’administration pour vous ajouter en tant que **développeur** et **utilisateur** d’un produit.

Les sections suivantes décrivent les étapes à suivre pour créer un Adobe ID et devenir développeur et utilisateur pour une organisation.

### Création d’un ID Adobe

Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un à l’aide des étapes suivantes :

1. Accéder à [Adobe I/O Console](https://console.adobe.io)
2. Cliquez sur **Créer un compte**
3. Terminer le processus d&#39;inscription


### Devenir développeur et utilisateur de la plateforme d’expérience pour une entreprise

Avant de créer des intégrations sur les E/S Adobe, votre compte doit disposer des autorisations de développeur pour un produit dans une organisation IMS. Vous trouverez des informations détaillées sur les comptes des développeurs dans la Console d&#39;administration dans le [d&#39;assistance](https://helpx.adobe.com/enterprise/using/manage-developers.html) pour la gestion des développeurs.

**Obtenir un accès pour les développeurs**

Contactez un administrateur de la Console d’administration de votre organisation pour vous ajouter en tant que développeur à l’un des produits de votre organisation à l’aide de la Console [d’administration](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L’administrateur doit vous affecter en tant que développeur à au moins un de produits pour continuer.

![](images/authentication/add-developer.png)

Une fois que vous avez été affecté en tant que développeur, vous disposez de droits d’accès pour créer des intégrations sur les E/S [](https://console.adobe.io/)Adobe. Ces intégrations constituent un pipeline allant des applications et services externes à l’API Adobe.

**Obtenir l&#39;accès des utilisateurs**

L’administrateur de la Console d’administration doit également vous ajouter au produit en tant qu’utilisateur.

![](images/authentication/assign-users.png)

Tout comme le processus d’ajout d’un développeur, l’administrateur doit vous affecter à au moins un de produits pour pouvoir continuer.

![](images/authentication/assign-user-details.png)


## Configuration ponctuelle

Les étapes suivantes ne doivent être effectuées qu’une seule fois :

* Connexion à Adobe I/O Console
* Créer une intégration
* Copier les valeurs d’accès vers le bas

Une fois que vous disposez de vos valeurs d’intégration et d’accès, vous pourrez les réutiliser pour authentification à l’avenir. Chaque étape est traitée en détail ci-dessous.

### Connexion à Adobe I/O Console

Accédez à [Adobe I/O Console](https://console.adobe.io/) et connectez-vous avec votre Adobe ID.

Une fois connecté, cliquez sur l’onglet **Intégrations** en haut de l’écran. Une intégration est un compte de service créé pour l’organisation IMS sélectionnée. Vous n&#39;êtes autorisé à lancer des appels que pour l&#39;organisation IMS dans laquelle l&#39;intégration est créée.

>[!NOTE]
>Si votre compte est associé à plusieurs organisations, le menu déroulant en haut à droite de l’écran vous permet de passer facilement d’une organisation à l’autre.

### Créer une intégration

Dans la page **Intégrations** , cliquez sur **Nouvelle intégration** pour le processus. Le processus comprend trois étapes :
* Choisir le type d’intégration
* Choisir le service Adobe à intégrer
* Ajouter les détails de l’intégration, la clé publique et le de produits 

![](images/authentication/integrations.png)

#### Choisir le type d’intégration

L’écran suivant vous demande si vous souhaitez accéder à une API ou recevoir un  proche du. Sélectionnez **Accéder à une API** , puis **Continuer**.

![](images/authentication/create-new-integration.png)

#### Choisir le service Adobe à intégrer

Si votre compte est associé à plusieurs organisations IMS, vous pouvez passer d’une organisation à l’autre à l’aide du menu déroulant en haut à droite. Sélectionnez **Atelier** et API **de plateforme** d’expérience sous **Adobe Experience Platform** pour accéder aux API.

![](images/authentication/integration-select-service.png)

Cliquez sur **Continuer** pour passer à la section suivante.

#### Ajouter les détails de l’intégration, la clé publique et le de produits 

L’écran suivant vous invite à renseigner les détails de votre intégration, à saisir votre certificat de clé publique et à sélectionner un  de produit.

![](images/authentication/integration-details.png)

Tout d’abord, entrez les détails de votre intégration. Sélectionnez ensuite un  de produit. Le de produits  un accès granulaire à un groupe de fonctionnalités appartenant au service que vous avez sélectionné lors des étapes précédentes.

Pour la section du certificat, vous devez générer un certificat :

**Pour les plateformes MacOS et Linux :**

Ouvrez la ligne de commande et exécutez la commande suivante :

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Pour les plateformes Windows :**

1. Téléchargez un client openssl pour générer des certificats publics (par exemple, client [Windows](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip)Openssl).

1. Extrayez le dossier et copiez-le dans l’emplacement C:/libs/.

1. Ouvrez l’invite de ligne de commande et exécutez les commandes suivantes :

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Vous obtiendrez une réponse similaire à celle-ci, qui vous invite à saisir des informations vous concernant :

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Après avoir saisi les informations, deux fichiers sont générés : `certificate_pub.crt` et `private.key`.

>[!NOTE]
>`certificate_pub.crt` expirera dans 365 jours. Vous pouvez allonger la période en modifiant la valeur de `days` dans la `openssl` commande ci-dessus, mais la rotation périodique des informations d’identification est une bonne pratique de sécurité.

Le `private.key` sera utilisé pour générer notre JWT dans la section suivante.

La `certificate_pub.crt` méthode est utilisée pour créer une clé d’API. Revenez à la console d’E/S Adobe et cliquez sur **Sélectionner un fichier** pour télécharger votre `certificate_pub.crt` fichier.

Cliquez sur **Créer une intégration** pour terminer le processus.

### Copier les valeurs d’accès vers le bas

Après avoir créé votre intégration, vous pouvez  ses détails. Cliquez sur **Récupérer la clé secrète** du client et votre écran ressemblera à celui-ci :

![](images/authentication/access-values.png)

Copiez les valeurs pour `{API KEY}`, `{IMS ORG}` qui est l’ID d’organisation, et `{CLIENT SECRET}` telles qu’elles seront utilisées à l’étape suivante.

## Authentification pour chaque session

La dernière étape consiste à générer votre `{ACCESS_TOKEN}` qui sera utilisé pour authentifier vos appels d’API. Le  doit être inclus dans l’en-tête d’autorisation de chaque appel d’API que vous apportez à Adobe Experience Platform. Les  expirent au bout de 24 heures, après quoi de nouveaux jetons doivent être générés pour continuer à utiliser les API.

### Création de JWT

Dans la page des détails de votre intégration dans la console d’E/S Adobe, accédez à l’onglet **JWT** :

![](images/authentication/generate-jwt.png)

La page vous invite à entrer le code `private.key` que vous avez créé dans la section précédente. Ouvrez la ligne de commande pour  le contenu de votre `private.key` fichier :

```shell
cat private.key
```

Votre sortie ressemblera à ceci :

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Copiez l’intégralité de la sortie et collez-la dans le champ de texte, puis cliquez sur **Générer JWT**. Copiez le fichier JWT généré pour l’étape suivante.

![](images/authentication/generated-jwt.png)

### Générer un  de

Vous pouvez générer un  à l’aide d’une commande cURL. Si cURL n’est pas installé, vous pouvez l’installer à l’aide de `npm install curl`. Vous pouvez en savoir plus sur cURL [ici](https://curl.haxx.se/)

Une fois que cURL est installé, vous devez permuter les champs de la commande suivante avec les vôtres `{API_KEY}`, `{CLIENT_SECRET}`et `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

En cas de succès, la sortie se présentera comme suit :

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Votre  est la valeur sous la `access_token` clé. Ce  86399947 millisecondes (24 heures). `expires_in` Ensuite, vous devrez générer un nouveau  de en suivant les mêmes étapes que ci-dessus.

Vous êtes maintenant prêt à effectuer des demandes d’API dans Adobe Experience Platform !

### Test du code d’accès

Pour tester la validité de votre , vous pouvez effectuer l’appel d’API suivant. Cet appel  toutes les classes dans le `global` :

>[!NOTE]
>`{API_KEY}` et `{IMS_ORG}` faites référence aux valeurs que vous avez générées ci-dessus.

**Requête**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Si votre réponse est similaire à celle illustrée ci-dessous, votre réponse `access_token` est valide et fonctionne. (Cette réponse a été tronquée pour l’espace.)

**Réponse**

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Utilisation de Postman pour l’authentification JWT et les appels d’API

[Postman](https://www.getpostman.com/) est un outil populaire pour travailler avec les API RESTful. Cette publication [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) moyenne décrit la configuration de postman pour qu’il effectue automatiquement l’authentification JWT et l’utilise pour consommer les API Adobe Experience Platform.