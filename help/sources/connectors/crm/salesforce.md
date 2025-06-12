---
title: Présentation du connecteur Source de Salesforce
description: Découvrez comment connecter Salesforce à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 4%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>Vous pouvez désormais utiliser la source [!DNL Salesforce] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

>[!WARNING]
>
>L’authentification de base de la source [!DNL Salesforce] sera abandonnée en janvier 2026. Vous devez passer à l’authentification des informations d’identification du client OAuth 2 pour continuer à utiliser la source et à ingérer des données à partir de votre compte [!DNL Salesforce] vers Experience Platform.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers de gestion de la relation client (CRM). La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Salesforce].

## Configurer votre source de [!DNL Salesforce] pour Experience Platform sur Azure {#azure}

Suivez les étapes ci-dessous pour savoir comment configurer votre compte [!DNL Salesforce] pour Experience Platform sur Azure.

### PLACER SUR LA LISTE AUTORISÉE Adresse IP associée pour la connexion à Azure

Vous devez ajouter des adresses IP spécifiques à une région à votre place sur la liste autorisée de données avant de connecter vos sources à Experience Platform sur Azure. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre place sur la liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [place sur la liste autorisée d’adresse IP](../../ip-address-allow-list.md) .

>[!BEGINTABS]

>[!TAB VA7]

- `40.70.226.96/28`
- `40.70.226.32/28`
- `52.232.229.255`
- `52.232.229.253`
- `40.70.226.144/28`
- `40.70.226.64/28`
- `40.70.225.240/28`
- `40.70.225.224/28`
- `40.70.224.64/29`
- `40.70.226.80/28`
- `40.70.226.176/28`
- `52.232.229.230`
- `40.70.226.128/28`
- `40.70.226.0/28`
- `40.70.226.16/28`
- `52.138.119.167`
- `40.70.226.160/28`
- `40.70.226.192/28`
- `40.70.226.48/28`
- `20.96.243.176`
- `40.70.226.112/28`
- `40.70.226.208/28`

>[!TAB NLD2]

- `40.74.4.144/28`
- `40.74.3.176/28`
- `40.74.5.128/28`
- `40.74.4.176/28`
- `40.74.6.112/28`
- `40.74.7.128/28`
- `40.74.6.144/28`
- `51.105.144.81`
- `52.142.236.87`
- `40.74.6.80/28`
- `20.101.246.9`
- `40.74.7.208/28`
- `40.74.6.128/28`
- `40.74.7.176/28`
- `51.124.70.4`
- `40.74.7.144/28`
- `108.141.12.47`
- `20.50.23.153`
- `51.144.184.248/29`
- `40.74.7.160/28`
- `40.74.7.192/28`
- `51.105.144.1`
- `40.74.4.160/28`
- `40.74.6.96/28`

>[!TAB AUS5]

- `20.43.111.32/28`
- `20.43.110.144/28`
- `20.53.111.113`
- `20.227.32.175`
- `20.43.110.96/28`
- `20.43.110.64/28`
- `20.193.56.144/28`
- `20.43.110.192/28`
- `20.43.97.95`
- `20.43.111.16/28`
- `20.43.110.128/28`
- `20.40.185.111`
- `20.193.56.160/28`
- `20.43.110.112/28`
- `40.82.220.111`
- `20.43.111.0/28`
- `20.193.38.208/28`
- `20.43.110.80/28`
- `20.43.110.176/28`
- `20.43.110.48/28`
- `20.193.36.37`
- `20.43.110.208/28`
- `20.43.110.224/28`
- `20.43.110.160/28`
- `20.40.185.225`
- `20.43.110.240/28`
- `20.193.56.128/28`
- `20.40.185.185`

>[!TAB CAN2]

- `20.116.159.48/28`
- `20.116.159.144/28`
- `20.116.159.96/28`
- `20.220.243.238`
- `20.116.159.80/28`
- `20.116.159.32/28`
- `20.151.241.138`
- `4.172.28.20`
- `20.151.241.124`
- `20.116.248.0/28`
- `20.116.155.128/28`
- `20.116.159.64/28`
- `20.116.159.192/28`
- `20.116.159.176/28`
- `20.116.175.240/28`
- `20.116.248.16/28`
- `20.116.158.240/28`
- `20.116.159.112/28`
- `20.151.240.247`
- `20.151.241.173`
- `20.116.159.128/28`
- `20.116.159.160/28`
- `20.116.159.0/28`
- `20.104.5.248`
- `20.116.175.224/28`
- `20.116.159.208/28`
- `20.116.159.224/28`

>[!TAB GBR9]

- `20.162.155.16/28`
- `20.162.154.96/28`
- `20.26.64.0/28`
- `20.26.64.96/28`
- `20.162.154.64/28`
- `20.108.200.27`
- `20.162.154.80/28`
- `20.162.153.192/28`
- `20.108.200.61`
- `20.162.154.48/28`
- `20.162.154.192/28`
- `20.162.154.0/28`
- `20.26.64.16/28`
- `20.162.154.112/28`
- `20.162.153.32/28`
- `20.254.80.141`
- `20.162.153.208/28`
- `20.108.203.20`
- `20.26.64.48/28`
- `20.162.154.240/28`
- `20.162.154.208/28`
- `20.162.154.160/28`
- `20.108.205.182`
- `20.108.202.198`
- `20.162.154.32/28`
- `20.162.153.16/28`

>[!TAB IND2]

- `4.188.92.84`
- `4.224.5.224/28`
- `4.224.7.32/28`
- `4.188.92.87`
- `4.188.89.92`
- `4.224.5.112/28`
- `4.224.6.80/28`
- `4.224.144.224/28`
- `4.224.144.240/28`
- `4.224.6.96/28`
- `4.188.89.255`
- `4.188.94.32/28`
- `4.224.5.96/28`
- `4.224.6.64/28`
- `4.224.7.48/28`
- `4.224.5.208/28`
- `4.188.90.65`
- `4.224.6.16/28`
- `4.224.6.0/28`
- `4.224.5.192/28`
- `4.224.7.16/28`
- `4.188.90.67`
- `4.188.90.17`
- `4.188.94.48/28`
- `4.224.6.112/28`
- `4.224.5.240/28`
- `4.224.7.0/28`

>[!ENDTABS]

### Mappage des champs de [!DNL Salesforce] à XDM

Pour établir une connexion source entre [!DNL Salesforce] et Experience Platform, les champs de données sources [!DNL Salesforce] doivent être mappés à leurs champs XDM cibles appropriés avant d’être ingérés dans Experience Platform.

Pour plus d’informations sur les règles de mappage des champs entre les jeux de données [!DNL Salesforce] et Experience Platform, consultez les sections suivantes :

- [Contacts](../adobe-applications/mapping/salesforce.md#contact)
- [Prospects](../adobe-applications/mapping/salesforce.md#lead)
- [Comptes](../adobe-applications/mapping/salesforce.md#account)
- [Opportunités](../adobe-applications/mapping/salesforce.md#opportunity)
- [Rôles de contact d’opportunité](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Personnes membres de campagne](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Relation de contact de compte](../adobe-applications/mapping/salesforce.md#account-contact-relation)

### Configurer l’utilitaire de génération automatique d’espace de noms et de schéma [!DNL Salesforce]

Pour utiliser la source de [!DNL Salesforce] dans le cadre de [!DNL B2B-CDP], vous devez d’abord configurer un utilitaire de [!DNL Postman] pour générer automatiquement vos espaces de noms et schémas de [!DNL Salesforce]. La documentation suivante fournit des informations supplémentaires sur la configuration de l’utilitaire [!DNL Postman] :

- Vous pouvez télécharger la collection d’utilitaires et l’environnement de génération automatique d’espace de noms et de schéma à partir de ce [référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Pour plus d’informations sur l’utilisation des API Experience Platform, notamment sur la collecte des valeurs des en-têtes requis et la lecture d’exemples d’appels d’API, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).
- Pour plus d’informations sur la génération de vos informations d’identification pour les API Experience Platform, consultez le tutoriel sur l’[authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
- Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Experience Platform, consultez le tutoriel sur [configuration de Developer Console et  [!DNL Postman]](../../../landing/postman.md).

Grâce à la console de développement et à la configuration des [!DNL Postman] d’Experience Platform, vous pouvez maintenant commencer à appliquer les valeurs d’environnement appropriées à votre environnement de [!DNL Postman].

+++Afficher le guide du tableau des variables

Le tableau suivant contient des exemples de valeurs ainsi que des informations supplémentaires sur la population de votre environnement [!DNL Postman] :

| Variable | Description | Exemple |
| --- | --- | --- |
| `CLIENT_SECRET` | Identifiant unique utilisé pour générer votre `{ACCESS_TOKEN}`. Pour plus d’informations sur la récupération de vos `{CLIENT_SECRET}`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | Le jeton Web JSON (JWT) est des informations d’authentification utilisées pour générer votre {ACCESS_TOKEN}. Pour plus d’informations sur la génération de vos `{JWT_TOKEN}`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `{JWT_TOKEN}` |
| `API_KEY` | Identifiant unique utilisé pour authentifier les appels aux API Experience Platform. Pour plus d’informations sur la récupération de vos `{API_KEY}`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Jeton d’autorisation requis pour effectuer des appels vers les API Experience Platform. Pour plus d’informations sur la récupération de vos `{ACCESS_TOKEN}`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Le conteneur `global` contient toutes les classes, groupes de champs de schéma, types de données et schémas fournis par les partenaires standard d’Adobe et d’Experience Platform. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur `global`. | `global` |
| `PRIVATE_KEY` | Informations d’identification utilisées pour authentifier votre instance [!DNL Postman] auprès des API Experience Platform. Voir les tutoriels Configuration de Developer Console et [ Configuration de Developer Console et  [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de votre {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Informations d’identification utilisées pour intégrer à Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Le système Identity Management (IMS) fournit la structure pour l’authentification aux services Adobe. En ce qui concerne [!DNL Marketo], cette valeur est fixe et est toujours définie sur : `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Entité d’entreprise pouvant posséder des produits et services ou en obtenir la licence et permettre l’accès à ses membres. Consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations de `{ORG_ID}`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Nom de la partition de sandbox virtuelle que vous utilisez. | `prod` |
| `TENANT_ID` | Identifiant utilisé pour s’assurer que les ressources que vous créez ont un espace de noms correct et sont contenues dans votre organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Point d’entrée de l’URL vers lequel vous effectuez des appels API. Cette valeur est fixe et est toujours définie sur : `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | ID unique de votre compte [!DNL Marketo]. Pour plus d’informations sur la récupération de votre `munchkinId`, consultez le tutoriel sur [l’authentification de votre instance [!DNL Marketo] ](../adobe-applications/marketo/marketo-auth.md). | `123-ABC-456` |
| `sfdc_org_id` | Identifiant d’organisation de votre compte [!DNL Salesforce]. Pour plus d’informations sur l’acquisition de votre ID d’organisation [!DNL Salesforce], consultez le [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&type=1&mode=1) suivant. | `00D4W000000FgYJUA0` |
| `has_abm` | Valeur booléenne qui indique si vous êtes abonné aux [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Valeur booléenne qui indique si vous êtes abonné aux [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

+++

### Exécution des scripts

Une fois votre collection de [!DNL Postman] et votre environnement configurés, vous pouvez exécuter le script via l’interface [!DNL Postman].

Dans l’interface [!DNL Postman], sélectionnez le dossier racine de l’utilitaire de génération automatique, puis sélectionnez **[!DNL Run]** dans l’en-tête supérieur.

![dossier-racine](../../images/tutorials/create/salesforce/root-folder.png)

L’interface [!DNL Runner] s’affiche. À partir de là, assurez-vous que toutes les cases à cocher sont sélectionnées, puis sélectionnez **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

Une requête réussie crée les espaces de noms et les schémas B2B conformément aux spécifications bêta.

## Configurer votre source de [!DNL Salesforce] pour Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Pour découvrir comment configurer votre compte [!DNL Salesforce] pour Experience Platform sur Amazon Web Services (AWS), procédez comme suit.

### Conditions préalables

Pour connecter votre compte [!DNL Salesforce] à Experience Platform dans une région AWS, vous devez disposer des éléments suivants :

- Un compte [!DNL Salesforce] avec un accès API.
- [!DNL Salesforce Connected App] que vous pouvez ensuite utiliser pour activer le flux OAuth JWT_BEARER.
- Les autorisations nécessaires dans [!DNL Salesforce] d’accéder aux données.

### PLACER SUR LA LISTE AUTORISÉE Adresse IP utilisée pour la connexion à AWS

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur AWS. Pour plus d’informations, consultez le guide sur [la liste autorisée d’adresses IP pour se connecter à Experience Platform sur AWS](../../ip-address-allow-list.md).

### Création d’un [!DNL Salesforce Connected App]

Tout d’abord, utilisez les éléments suivants pour créer un certificat ou une paire de clés de fichiers PEM.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. Dans le tableau de bord [!DNL Salesforce], sélectionnez les paramètres (![Icône des paramètres.](/help/images/icons/settings.png)), puis sélectionnez **[!DNL Setup]**.
2. Accédez à [!DNL App Manager] , puis sélectionnez **[!DNL New Connection App]**.
3. Attribuez un nom à votre application et autorisez le remplissage automatique du reste des champs.
4. Activez la case à [!DNL Enable OAuth Settings].
5. Définissez une URL de rappel. Comme il ne sera pas utilisé pour le jeton JWT, vous pouvez utiliser `https://localhost`.
6. Activez la case à [!DNL Use Digital Signatures].
7. Chargez le fichier cert.pem créé précédemment.

#### Ajout des autorisations requises

Ajoutez les autorisations suivantes :

1. Gestion des données utilisateur via des API (api)
2. Accéder aux autorisations personnalisées (custom_permissions)
3. Accéder au service d’URL d’identité (identifiant, profil, e-mail, adresse, téléphone)
4. Accéder aux identifiants uniques (openid)
5. Exécuter des requêtes à tout moment (refresh_token, offline_access)

Une fois vos autorisations ajoutées, assurez-vous d’activer la case à **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]**.

Sélectionnez ensuite **[!DNL Save]**, **[!DNL Continue]**, puis **[!DNL Manage Customer Details]**. Utilisez le panneau Détails du client pour récupérer les éléments suivants :

- **Clé du client** : vous utiliserez ultérieurement cette clé du client comme identifiant client lors de l’authentification de votre compte [!DNL Salesforce] à Experience Platform.
- **Secret du client** : vous utiliserez plus tard ce secret du client comme ID client lors de l’authentification de votre compte [!DNL Salesforce] à Experience Platform.

### Autoriser l’utilisateur [!DNL Salesforce] à accéder à l’application connectée

Pour obtenir l’autorisation d’utiliser l’application connectée, procédez comme suit :

1. Accédez à **[!DNL Manage Connected Apps]**.
2. Sélectionnez **[!DNL Edit]**.
3. Configurez **[!DNL Permitted Users]** en tant que **[!DNL Admin approved users are pre-authorized]**, puis sélectionnez **[!DNL Save]**.
4. Accédez à **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]**.
5. Modifiez le profil associé à votre utilisateur.
6. Accédez à **[!DNL Connected App Access]** , puis sélectionnez l’application que vous avez créée lors d’une étape précédente.

### Générer un jeton du porteur JWT

Suivez les étapes ci-dessous pour générer votre jeton du porteur JWT.

#### Convertir une paire de clés en pkcs12

Pour générer votre jeton porteur JWT, vous devez d’abord utiliser la commande suivante pour convertir votre certificat/paire de clés au format pkcs12 . Au cours de cette étape, vous devez également **définir un mot de passe d’exportation** lorsque vous y êtes invité.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Créer un fichier de stockage des clés Java basé sur pkcs12

Ensuite, utilisez la commande suivante pour créer un fichier de stockage des clés Java basé sur le fichier pkcs12 que vous venez de générer. Au cours de cette étape, vous devez également définir un **mot de passe du KeyStore de destination** lorsque vous y êtes invité. En outre, vous devez fournir le mot de passe d’exportation précédent comme mot de passe du fichier de stockage des clés source.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Vérifiez que votre fichier keystroke.jks inclut un alias jwtcert.

Ensuite, utilisez la commande suivante pour confirmer que votre `keystroke.jks` comprend un alias `jwtcert`. Au cours de cette étape, vous serez invité à fournir le mot de passe du KeyStore de destination qui a été généré à l’étape précédente.

```shell
keytool -keystore keystore.jks -list
```

#### Générer un jeton signé

Enfin, utilisez la classe Java JWTExample ci-dessous pour générer votre jeton signé.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Propriété | Configurations  |
| --- | --- |
| `claimArray[0]` | Mettez à jour `claimArray[0]` avec votre identifiant client. |
| `claimArray[1]` | Mettez à jour `claimArray[1]` avec le nom d’utilisateur [!DNL Salesforce] autorisé pour l’application. |
| `claimArray[2]` | Mettez à jour `claimArray[2]` avec votre URL de connexion [!DNL Salesforce]. |
| `claimArray[3]` | Mettez à jour les `claimArray[3]` avec une date d’expiration formatée en millisecondes depuis l’heure Unix. Par exemple, `3660624000000` est le 12-31-2085. |
| `/path/to/keystore` | Remplacez `/path/to/keystore` par le chemin d’accès correct à votre fichier keystore.jks. |
| `keystorepassword` | Remplacez `keystorepassword` par votre mot de passe de stockage des clés de destination. |
| `privatekeypassword` | Remplacez `privatekeypassword` par votre mot de passe de stockage des clés source. |

## Étapes suivantes

Une fois la configuration préalable requise pour votre compte [!DNL Salesforce] terminée, vous pouvez connecter votre compte [!DNL Salesforce] à Experience Platform et ingérer vos données CRM. Pour plus d’informations, consultez la documentation ci-dessous :

### Connexion de [!DNL Salesforce] à Experience Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

- [Connecter Salesforce à Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

### Connexion d’[!DNL Salesforce] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Salesforce dans l’interface utilisateur](../../tutorials/ui/create/crm/salesforce.md)
- [Créer un flux de données pour une connexion CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)