---
title: Connexion via l’API HTTP
keywords: diffusion en continu;
description: Utilisez la destination d’API HTTP dans Adobe Experience Platform pour envoyer des données de profil à un point de terminaison HTTP tiers afin d’exécuter vos propres analyses ou d’effectuer toute autre opération nécessaire sur les données de profil exportées hors d’Experience Platform.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 30549f31e7ba7f9cfafd2e71fb3ccfb701b9883f
workflow-type: tm+mt
source-wordcount: '2296'
ht-degree: 3%

---

# Connexion via l’API HTTP

## Présentation {#overview}

>[!IMPORTANT]
>
> Cette destination n’est disponible que pour [Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) clients.

La destination de l’API HTTP est une [!DNL Adobe Experience Platform] destination de diffusion en continu qui vous aide à envoyer des données de profil à des points de terminaison HTTP tiers.

Pour envoyer des données de profil aux points de terminaison HTTP, vous devez d’abord [se connecter à la destination](#connect-destination) in [!DNL Adobe Experience Platform].

## Cas dʼutilisation {#use-cases}

La destination de l’API HTTP vous permet d’exporter les données de profil XDM et les segments d’audience vers des points de terminaison HTTP génériques. Vous pouvez y exécuter vos propres analyses ou effectuer toute autre opération dont vous aurez besoin sur les données de profil exportées hors d’Experience Platform.

Les points de terminaison HTTP peuvent être les systèmes des clients ou des solutions tierces.

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : l’adresse email, le numéro de téléphone, le nom), tel que sélectionné dans l’écran de mappage de la variable [workflow d’activation de destination](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

Pour utiliser la destination d’API HTTP afin d’exporter des données en dehors d’Experience Platform, vous devez respecter les conditions préalables suivantes :

* Vous devez disposer d’un point de terminaison HTTP qui prend en charge l’API REST.
* Votre point de terminaison HTTP doit prendre en charge le schéma de profil Experience Platform. Aucune transformation en schéma de charge utile tiers n’est prise en charge dans la destination de l’API HTTP. Reportez-vous à la section [données exportées](#exported-data) pour un exemple du schéma de sortie Experience Platform.
* Votre point de terminaison HTTP doit prendre en charge les en-têtes.

>[!TIP]
>
> Vous pouvez également utiliser [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) pour configurer une intégration et envoyer des données de profil Experience Platform à un point de terminaison HTTP.

## LISTE AUTORISÉE d’adresses IP {#ip-address-allowlist}

Pour répondre aux exigences de sécurité et de conformité des clients, Experience Platform fournit une liste d’adresses IP statiques que vous pouvez placer sur la liste autorisée pour la destination de l’API HTTP. Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de diffusion en continu](/help/destinations/catalog/streaming/ip-address-allow-list.md) pour obtenir la liste complète des adresses IP à placer sur la liste autorisée.

## Types d’authentification pris en charge {#supported-authentication-types}

La destination de l’API HTTP prend en charge plusieurs types d’authentification pour votre point de terminaison HTTP :

* point de terminaison HTTP sans authentification ;
* Authentification par jeton porteur ;
* [Informations d’identification du client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) authentification avec le formulaire de corps, avec [!DNL client ID], [!DNL client secret] et [!DNL grant type] dans le corps de la requête HTTP, comme illustré dans l’exemple ci-dessous.

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

* [Subvention du mot de passe OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Se connecter à la destination {#connect-destination}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Lors de la connexion à cette destination, vous devez fournir les informations suivantes :

### Informations d’authentification {#authentication-information}

#### Authentification du jeton porteur {#bearer-token-authentication}

Si vous sélectionnez la variable **[!UICONTROL Jeton de porteur]** type d’authentification pour se connecter à votre point de terminaison HTTP, renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**:

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination de l’API HTTP, à l’aide de l’authentification par jeton porteur](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Jeton de porteur]**: insérez le jeton porteur pour l’authentification à votre emplacement HTTP.

#### Aucune authentification {#no-authentication}

Si vous sélectionnez la variable **[!UICONTROL Aucun]** type d’authentification pour se connecter à votre point d’entrée HTTP :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination de l’API HTTP, sans authentification](../../assets/catalog/http/http-api-authentication-none.png)

Lorsque vous sélectionnez cette authentification ouverte, il vous suffit de sélectionner **[!UICONTROL Se connecter à la destination]** et la connexion à votre point de terminaison est établie.

#### Authentification par mot de passe OAuth 2 {#oauth-2-password-authentication}

Si vous sélectionnez la variable **[!UICONTROL Mot de passe OAuth 2]** type d’authentification pour se connecter à votre point de terminaison HTTP, renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**:

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination de l’API HTTP, à l’aide d’OAuth 2 avec authentification par mot de passe.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL du jeton d’accès]**: URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons.
* **[!UICONTROL ID client]**: Le [!DNL client ID] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Secret du client]**: Le [!DNL client secret] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Nom d’utilisateur]**: Nom d’utilisateur pour accéder à votre point de terminaison HTTP.
* **[!UICONTROL Mot de passe]**: Mot de passe pour accéder à votre point de terminaison HTTP.

#### Authentification des informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Type d’informations d’identification client"
>abstract="Sélectionner **Body Form Encoded** pour inclure l’ID client et le secret client dans le corps de la requête ou **Autorisation de base** pour inclure l’ID client et le secret client dans un en-tête d’autorisation. Consultez des exemples dans la documentation."

Si vous sélectionnez la variable **[!UICONTROL Informations d’identification du client OAuth 2]** type d’authentification pour se connecter à votre point de terminaison HTTP, renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**:

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination de l’API HTTP, à l’aide d’OAuth 2 avec authentification des informations d’identification du client.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

* **[!UICONTROL URL du jeton d’accès]**: URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons.
* **[!UICONTROL ID client]**: Le [!DNL client ID] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Secret du client]**: Le [!DNL client secret] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Type d’informations d’identification du client]**: Sélectionnez le type d’octroi des informations d’identification du client OAuth2 pris en charge par votre point de terminaison :
   * **[!UICONTROL Body Form Encoded]**: Dans ce cas, la variable [!DNL client ID] et [!DNL client secret] sont inclus *dans le corps de la requête* envoyé à votre destination. Pour consulter un exemple, reportez-vous à la section [Types d’authentification pris en charge](#supported-authentication-types) .
   * **[!UICONTROL Autorisation de base]**: Dans ce cas, la variable [!DNL client ID] et [!DNL client secret] sont inclus *dans un `Authorization` header* après avoir été codé en base64 et envoyé à votre destination. Pour consulter un exemple, reportez-vous à la section [Types d’authentification pris en charge](#supported-authentication-types) .

### Détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_headers"
>title="En-têtes"
>abstract="Saisissez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_endpoint"
>title="Point de terminaison HTTP"
>abstract="URL du point de terminaison HTTP vers lequel vous souhaitez envoyer les données de profil."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmentnames"
>title="Inclure les noms de segment"
>abstract="Basculez si vous souhaitez que l’exportation des données contienne les noms des segments que vous exportez. Affichez la documentation d’un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_includesegmenttimestamps"
>title="Inclure les horodatages de segment"
>abstract="Basculez si vous souhaitez que l’exportation des données inclue l’horodatage UNIX lors de la création et de la mise à jour des segments, ainsi que l’horodatage UNIX lorsque les segments ont été mappés à la destination pour activation. Affichez la documentation d’un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_queryparameters"
>title="Paramètres de requête"
>abstract="Vous pouvez éventuellement ajouter des paramètres de requête à l’URL du point de terminaison HTTP. Mettez en forme les paramètres de requête que vous utilisez comme suit : `parameter1=value&parameter2=value`."

Après avoir établi la connexion d’authentification au point de terminaison HTTP, fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination HTTP](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nom]**: Saisissez un nom qui vous permettra de reconnaître cette destination à l’avenir.
* **[!UICONTROL Description]**: Saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL En-têtes]**: Saisissez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Point de terminaison HTTP]**: URL du point de terminaison HTTP vers lequel vous souhaitez envoyer les données de profil.
* **[!UICONTROL Paramètres de requête]**: Vous pouvez éventuellement ajouter des paramètres de requête à l’URL du point de terminaison HTTP. Mettez en forme les paramètres de requête que vous utilisez comme suit : `parameter1=value&parameter2=value`.
* **[!UICONTROL Inclure les noms de segment]**: Basculez si vous souhaitez que l’exportation des données contienne les noms des segments que vous exportez. Pour un exemple d&#39;export de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) voir la section ci-dessous.
* **[!UICONTROL Inclure les horodatages de segment]**: Basculez si vous souhaitez que l’exportation des données inclue l’horodatage UNIX lors de la création et de la mise à jour des segments, ainsi que l’horodatage UNIX lorsque les segments ont été mappés à la destination pour activation. Pour un exemple d&#39;export de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) voir la section ci-dessous.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#attributes}

Dans le [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination d’API HTTP, afin de n’exporter les données vers votre point de terminaison d’API que lorsque des mises à jour appropriées d’un profil se sont produites à la suite de la qualification de segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’adhésion au segment pour au moins un des segments mappés à la destination. Par exemple, le profil s’est qualifié pour l’un des segments mappés à la destination ou a quitté l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’un des segments mappés à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils où des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes n’ont pas changé.

### Ce qui détermine un export de données et ce qui est inclus dans l’export {#what-determines-export-what-is-included}

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents de *ce qui détermine l’exportation des données vers votre destination d’API HTTP* et *les données incluses dans l’exportation ;*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si un segment mappé change d’état (de null à Reçue ou de get/existing à Extioning) ou que tout attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations d’API HTTP, les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Une modification pour un attribut est définie comme toute mise à jour de l’attribut, qu’il s’agisse ou non de la même valeur. Cela signifie qu’un remplacement sur un attribut est considéré comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>Tous les segments (avec le dernier état d’adhésion), qu’ils soient mappés ou non dans le flux de données, sont inclus dans la variable `segmentMembership` .</li><li>Toutes les identités dans la variable `identityMap` sont également inclus (Experience Platform ne prend actuellement pas en charge le mappage d’identité dans la destination de l’API HTTP).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Prenons l’exemple de ce flux de données vers une destination HTTP où trois segments sont sélectionnés dans le flux de données et où quatre attributs sont mappés à la destination.

![Flux de données de destination d’API HTTP](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un export de profil vers la destination peut être déterminé par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, dans l’exportation des données, dans la variable `segmentMembership` (voir [Données exportées](#exported-data) ci-dessous), d’autres segments non mappés peuvent apparaître si ce profil particulier en fait partie. Si un profil est admissible pour le segment Client avec des voitures de Lorée, mais qu’il est également membre des segments de fans de films et de science-fiction &quot;Retour vers le futur&quot; de la visionneuse, ces deux autres segments seront également présents dans la variable `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et l’un des quatre attributs mappés présents sur le profil sera présent dans l’exportation des données.

## Renvoi de données historiques {#historical-data-backfill}

Lorsque vous ajoutez un nouveau segment à une destination existante, ou lorsque vous créez une destination et lui mappez des segments, Experience Platform exporte les données historiques de qualification de segment vers la destination. Profils qualifiés pour le segment *before* le segment ajouté à la destination est exporté vers la destination dans environ une heure.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre [!DNL HTTP] destination au format JSON. Par exemple, l’exportation ci-dessous contient un profil qui s’est qualifié pour un certain segment, qui est membre de deux autres segments et qui a quitté un autre segment. L’exportation inclut également le prénom, le nom, la date de naissance et l’adresse email personnelle de l’attribut de profil. Les identités de ce profil sont ECID et email.

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
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
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

Vous trouverez ci-dessous d’autres exemples de données exportées, en fonction des paramètres de l’interface utilisateur que vous sélectionnez dans le flux de connexion à la destination pour le **[!UICONTROL Inclure les noms de segment]** et **[!UICONTROL Inclure les horodatages de segment]** options :

+++ L’exemple d’exportation de données ci-dessous inclut les noms de segment dans la variable `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
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

+++ L’exemple d’exportation de données ci-dessous inclut des horodatages de segment dans la variable `segmentMembership` section

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Limites et stratégie de reprise {#limits-retry-policy}

Dans 95 % des cas, l’Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 requêtes par seconde pour chaque flux de données vers une destination HTTP.

En cas d’échec des requêtes vers votre destination d’API HTTP, Experience Platform stocke les requêtes en échec et tente à deux reprises d’envoyer les requêtes à votre point de terminaison .