---
keywords: flux en continu; destination HTTP
title: Connexion API HTTP
description: Utilisez la destination API HTTP dans Adobe Experience Platform pour envoyer des données de profil vers un point d’entrée HTTP tiers afin d’exécuter vos propres analyses ou toute autre opération dont vous pourriez avoir besoin sur les données de profil exportées hors d’Experience Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 74%

---

# Connexion API HTTP

## Présentation {#overview}

>[!IMPORTANT]
>
> Cette destination est disponible uniquement pour les clients d’[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

La destination de l’API HTTP est une destination en flux continu [!DNL Adobe Experience Platform] qui vous aide à envoyer des données de profil à des points d’entrée HTTP tiers.

Pour envoyer des données de profil à des points d’entrée HTTP, vous devez d’abord vous [connecter à la destination](#connect-destination) dans [!DNL Adobe Experience Platform].

## Cas d’utilisation {#use-cases}

La destination de l’API HTTP vous permet d’exporter les données de profil XDM et les audiences vers des points de terminaison HTTP génériques. Vous pouvez y lancer vos propres analyses ou effectuer toute autre opération dont vous pourriez avoir besoin sur les données de profil exportées hors d’Experience Platform.

Les points d’entrée HTTP peuvent être les systèmes des client(e)s ou des solutions tierces.

## Audiences prises en charge {#supported-audiences}

Cette section décrit toutes les audiences que vous pouvez exporter vers cette destination.

Cette destination prend en charge l’activation de toutes les audiences générées par l’Experience Platform. [Segmentation Service](../../../segmentation/home.md).

*En outre*, cette destination prend également en charge l’activation des audiences décrites dans le tableau ci-dessous.

| Type d’audience | Description |
---------|----------|
| Chargements personnalisés | Audiences [importé](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom), tels qu’ils ont été choisis dans l’écran de mappage du [workflow d’activation de la destination](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu&#39;un profil est mis à jour en Experience Platform en fonction de l&#39;évaluation de l&#39;audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour utiliser la destination d’API HTTP pour exporter des données en dehors d’Experience Platform, vous devez respecter les conditions préalables suivantes :

* Vous devez disposer d’un point d’entrée HTTP qui prend en charge l’API REST.
* Votre point d’entrée HTTP doit prendre en charge le schéma de profil Experience Platform. Aucune transformation en schéma de payload tiers n’est prise en charge dans la destination de l’API HTTP. Reportez-vous à la section [données exportées](#exported-data) pour un exemple du schéma de sortie Experience Platform.
* Votre point d’entée HTTP doit prendre en charge les en-têtes.

>[!TIP]
>
> Vous pouvez également utiliser [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) pour configurer une intégration et envoyer des données de profil Experience Platform à un point d’entrée HTTP.

## Liste autorisée d’adresses IP {#ip-address-allowlist}

Pour répondre aux exigences de sécurité et de conformité des clients, Experience Platform fournit une liste des adresses IP statiques que vous pouvez inscrire sur la liste autorisée pour la destination de l’API HTTP. Reportez-vous à la [liste autorisée d’adresses IP pour les destinations en flux continu](/help/destinations/catalog/streaming/ip-address-allow-list.md) pour la liste complète des adresses IP à autoriser.

## Types d’authentification pris en charge {#supported-authentication-types}

La destination API HTTP prend en charge plusieurs types d’authentification à votre point d’entrée HTTP :

* Point d’entrée HTTP sans authentification ;
* Authentification par jeton porteur ;
* Authentification à l’aide des [informations d’identification du client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) avec le formulaire de corps, avec [!DNL client ID], [!DNL client secret] et [!DNL grant type] dans le corps de la requête HTTP, comme illustré dans l’exemple ci-dessous.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

* [Informations d’identification du client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) avec une autorisation de base, avec un en-tête d’autorisation contenant un encodage URL [!DNL client ID] et [!DNL client secret].

```shell
curl --location --request POST 'https://some-api.com/token' \
--header 'Authorization: Basic base64(clientId:clientSecret)' \
--header 'Content-type: application/x-www-form-urlencoded; charset=UTF-8' \
--data-urlencode 'grant_type=client_credentials'
```

* [Octroi du mot de passe OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Se connecter à la destination {#connect-destination}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Lors de la connexion à cette destination, vous devez fournir les informations suivantes :

### Informations d’authentification {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Type d’informations d’identification client"
>abstract="Sélectionnez **Formulaire de corps encodé** pour inclure l’identifiant client et le secret client dans le corps de la requête ou **Autorisation de base** pour inclure l’identifiant client et le secret client dans un en-tête d’autorisation. Consultez des exemples dans la documentation."

#### Authentification par jeton porteur {#bearer-token-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Jeton porteur]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, à l’aide de l’authentification par jeton porteur](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Jeton porteur]** : insérez le jeton porteur pour l’authentification à votre emplacement HTTP.

#### Aucune authentification {#no-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Aucune]** pour vous connecter à votre point d’entrée HTTP :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, sans utiliser d’authentification](../../assets/catalog/http/http-api-authentication-none.png)

Lorsque vous sélectionnez cette ouverture d’authentification, il vous suffit de sélectionner **[!UICONTROL Se connecter à la destination]** et la connexion à votre point d’entrée est établie.

#### Authentification par mot de passe OAuth 2 {#oauth-2-password-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Mot de passe OAuth 2]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, en utilisant l’authentification par mot de passe OAuth 2](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL du jeton d’accès]** : URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons.
* **[!UICONTROL Identifiant client]** : l’[!DNL client ID] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Secret client]** : le [!DNL client secret] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour accéder à votre point d’entrée HTTP.
* **[!UICONTROL Mot de passe]** : mot de passe pour accéder à votre point d’entrée HTTP.

#### Authentification avec informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Informations d’identification du client OAuth 2]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, à l’aide de l’authentification OAuth 2 avec des informations d’identification du client](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL du jeton d’accès]** : URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons.
* **[!UICONTROL Identifiant client]** : l’[!DNL client ID] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Secret client]** : le [!DNL client secret] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Type d’informations d’identification du client]** : sélectionnez le type d’octroi des informations d’identification du client OAuth2 pris en charge par votre point d’entrée :
   * **[!UICONTROL Formulaire de corps encodé]** : dans ce cas, l’[!DNL client ID] et le [!DNL client secret] sont inclus *dans le corps de la requête* envoyée à votre destination. Pour un exemple, consultez la section [Types d’authentification pris en charge](#supported-authentication-types).
   * **[!UICONTROL Autorisation de base]** : dans ce cas, l’[!DNL client ID] et le [!DNL client secret] sont inclus *dans un en-tête d’`Authorization`* après avoir été codés en base64 et envoyés à votre destination. Pour un exemple, consultez la section [Types d’authentification pris en charge](#supported-authentication-types).

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="En-têtes"
>abstract="Saisissez tous les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, en suivant ce format : `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Point d’entrée HTTP"
>abstract="L’URL du point d’entrée HTTP vers lequel vous souhaitez envoyer les données de profil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Inclure les noms de segment"
>abstract="Activez ce bouton si vous voulez que l’export de données inclue les noms des audiences que vous exportez. Consultez la documentation pour un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Inclure la date et l’heure de segment"
>abstract="Activez ce bouton si vous souhaitez que l’export de données inclue la date et l’heure UNIX de la création et des mises à jour des audiences, ainsi que la date et l’heure UNIX du mappage des audiences à la destination pour l’activation. Consultez la documentation pour un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Paramètres de requête"
>abstract="Vous pouvez éventuellement ajouter des paramètres de requête à l’URL du point d’entrée HTTP. Mettez en forme les paramètres de requête que vous utilisez comme suit : `parameter1=value&parameter2=value`."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nom]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL En-têtes]** : saisissez tous les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, en suivant ce format : `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Point d’entrée HTTP]** : URL du point d’entrée HTTP vers lequel vous souhaitez envoyer les données de profil.
* **[!UICONTROL Paramètres de requête]** : vous pouvez éventuellement ajouter des paramètres de requête à l’URL du point d’entrée HTTP. Mettez en forme les paramètres de requête que vous utilisez comme suit : `parameter1=value&parameter2=value`.
* **[!UICONTROL Inclure les noms de segment]**: basculez si vous souhaitez que l’exportation des données contienne les noms des audiences que vous exportez. Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.
* **[!UICONTROL Inclure les horodatages de segment]**: basculez si vous souhaitez que l’exportation des données inclue l’horodatage UNIX lors de la création et de la mise à jour des audiences, ainsi que l’horodatage UNIX lorsque les audiences ont été mappées à la destination pour l’activation. Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer les audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#attributes}

Lors de l’étape [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination d’API HTTP, afin de n’exporter les données vers votre point de terminaison d’API que lorsque des mises à jour pertinentes d’un profil se sont produites à la suite de la qualification de l’audience ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’appartenance à l’audience pour au moins une des audiences mappées à la destination. Par exemple, le profil s’est qualifié pour l’une des audiences mappées à la destination ou a quitté l’une des audiences mappées à la destination.
* La mise à jour du profil a été déterminée par une modification dans le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’une des audiences mappées à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si une audience mappée au flux de destination comporte une centaine de membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Remarque : tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation {#what-determines-export-what-is-included}

Concernant les données exportées pour un profil donné, il est important de comprendre les deux concepts différents entre *ce qui détermine l’exportation de données vers votre destination d’API HTTP* et *les données incluses dans l’exportation*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et audiences mappés servent de repère pour un export de destination. Cela signifie que si des audiences mappées changent d’états (à partir de `null` to `realized` ou de `realized` to `exiting`) ou si les attributs mappés sont mis à jour, une exportation de destination est déclenchée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations d’API HTTP, les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Toute modification pour un attribut est considérée comme une mise à jour, qu’il s’agisse ou non de la même valeur. Cela signifie qu’une réécriture sur un attribut est considérée comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>La variable `segmentMembership` inclut l’audience mappée dans le flux de données d’activation, pour laquelle l’état du profil a changé suite à un événement de qualification ou de sortie d’audience. Notez que les autres audiences non mappées pour lesquelles le profil est qualifié peuvent faire partie de l’exportation de destination, si ces audiences appartiennent au même type. [stratégie de fusion](/help/profile/merge-policies/overview.md) comme audience mappée dans le flux de données d’activation. </li><li>Toutes les identités dans l’objet `identityMap` sont également incluses (actuellement Experience Platform ne prend pas en charge le mappage d’identité dans la destination de l’API HTTP).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style="table-layout:fixed"}

Prenons l’exemple de ce flux de données vers une destination HTTP où trois audiences sont sélectionnées dans le flux de données et où quatre attributs sont mappés à la destination.

![Flux de données à destination d’une API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, dans l’exportation des données, dans la variable `segmentMembership` (voir [Données exportées](#exported-data) ci-dessous), d’autres audiences non mappées peuvent apparaître si ce profil particulier en est membre et si elles partagent la même stratégie de fusion que l’audience qui a déclenché l’exportation. Si un profil est admissible pour la variable **Client avec des voitures DeLorean** , mais est également membre de la fonction **&quot;Retour vers l&#39;avenir&quot;** film et **Fans de science-fiction** , ces deux autres audiences seront également présentes dans la variable `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données, si elles partagent la même stratégie de fusion avec l’objet **Client avec des voitures DeLorean** segment.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et chacun de ces quatre attributs mappés et présents sur le profil sera présent dans l’exportation des données.

## Renvoyer des données historiques {#historical-data-backfill}

Lorsque vous ajoutez une nouvelle audience à une destination existante, ou lorsque vous créez une destination et que vous mappez des audiences avec celle-ci, l’Experience Platform exporte les données historiques de qualification des audiences vers la destination. Profils qualifiés pour l&#39;audience *before* l’audience a été ajoutée à la destination et est exportée vers la destination dans un délai d’environ une heure.

## Données exportées {#exported-data}

Les données [!DNL Experience Platform] exportées arrivent dans votre destination [!DNL HTTP] au format JSON. Par exemple, l’exportation ci-dessous contient un profil qualifié pour un certain segment, qui est membre de deux autres segments et qui a quitté un autre segment. L’exportation inclut également le prénom, le nom, la date de naissance et l’adresse e-mail personnelle de l’attribut de profil. Les identités de ce profil sont ECID et e-mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

Vous trouverez ci-dessous d’autres exemples de données exportées, en fonction des paramètres de l’interface utilisateur que vous sélectionnez dans le flux de connexion à la destination pour les options **[!UICONTROL Inclure les noms de segment]** et **[!UICONTROL Inclure la date et l’heure de segment]** :

+++ L’exemple d’exportation de données ci-dessous inclut les noms d’audience dans la variable `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ L’exemple d’exportation de données ci-dessous inclut les horodatages d’audience dans la variable `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Politique de limitation et de reprise {#limits-retry-policy}

Dans 95 % des cas, Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 demandes par seconde pour chaque flux de données vers une destination HTTP.

En cas d’échec des requêtes vers la destination API HTTP, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point d’entrée.