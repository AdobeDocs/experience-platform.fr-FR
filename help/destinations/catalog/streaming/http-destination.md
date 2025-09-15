---
keywords: flux en continu; destination HTTP
title: Connexion API HTTP
description: Utilisez la destination API HTTP dans Adobe Experience Platform pour envoyer des données de profil vers un point d’entrée HTTP tiers afin d’exécuter vos propres analyses ou toute autre opération dont vous pourriez avoir besoin sur les données de profil exportées hors d’Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 6d8386b4d9ed64128c8d9a9537610f0fd07d74cd
workflow-type: tm+mt
source-wordcount: '2852'
ht-degree: 65%

---

# Connexion API HTTP

## Présentation {#overview}

>[!IMPORTANT]
>
> Cette destination est disponible uniquement pour les clients d’[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

La destination de l’API HTTP est une destination en flux continu [!DNL Adobe Experience Platform] qui vous aide à envoyer des données de profil à des points d’entrée HTTP tiers.

Pour envoyer des données de profil à des points d’entrée HTTP, vous devez d’abord vous [connecter à la destination](#connect-destination) dans [!DNL Adobe Experience Platform].

## Cas d’utilisation {#use-cases}

La destination API HTTP vous permet d’exporter des données de profil XDM et des audiences vers des points d’entrée HTTP génériques. Vous pouvez y lancer vos propres analyses ou effectuer toute autre opération dont vous pourriez avoir besoin sur les données de profil exportées hors d’Experience Platform.

Les points d’entrée HTTP peuvent être les systèmes des client(e)s ou des solutions tierces.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| ---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom), tels qu’ils ont été choisis dans l’écran de mappage du [workflow d’activation de la destination](../../ui/activate-segment-streaming-destinations.md#mapping). |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour utiliser la destination d’API HTTP pour exporter des données en dehors d’Experience Platform, vous devez respecter les conditions préalables suivantes :

* Vous devez disposer d’un point d’entrée HTTP qui prend en charge l’API REST.
* Votre point d’entrée HTTP doit prendre en charge le schéma de profil Experience Platform. Aucune transformation en schéma de payload tiers n’est prise en charge dans la destination de l’API HTTP. Reportez-vous à la section [données exportées](#exported-data) pour un exemple du schéma de sortie Experience Platform.
* Votre point d’entée HTTP doit prendre en charge les en-têtes.
* Votre point d’entrée HTTP doit répondre dans les 2 secondes pour assurer un traitement correct des données et éviter les erreurs de délai d’expiration.

>[!TIP]
>
> Vous pouvez également utiliser [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) pour configurer une intégration et envoyer des données de profil Experience Platform à un point d’entrée HTTP.

## Prise en charge du protocole mTLS et certificat {#mtls-protocol-support}

Vous pouvez utiliser [!DNL Mutual Transport Layer Security] ([!DNL mTLS]) pour garantir une sécurité renforcée dans les connexions sortantes vers vos connexions de destination API HTTP.

[!DNL mTLS] est une méthode de sécurité de bout en bout pour l’authentification mutuelle qui garantit que les deux parties partageant des informations sont bien celles qu’elles prétendent être avant le partage des données. [!DNL mTLS] comprend une étape supplémentaire par rapport à [!DNL TLS], dans laquelle le serveur demande également le certificat du client et le vérifie de son côté.

Si vous souhaitez utiliser [!DNL mTLS] avec des destinations [!DNL HTTP API], l’adresse de serveur que vous placez dans la page [détails de la destination](#destination-details) doit comporter [!DNL TLS] protocoles désactivés et uniquement [!DNL mTLS] activés. Si le protocole [!DNL TLS] 1.2 est toujours activé sur le point d’entrée, aucun certificat n’est envoyé pour l’authentification du client. Cela signifie que pour utiliser [!DNL mTLS] avec votre destination [!DNL HTTP API], le point d’entrée du serveur de « réception » doit être un point d’entrée de connexion activé en [!DNL mTLS] seule.

### Récupération et inspection des détails du certificat {#certificate}

Si vous souhaitez examiner les détails du certificat tels que le [!DNL Common Name] (CN) et le [!DNL Subject Alternative Names] (SAN) pour une validation tierce supplémentaire, utilisez l’API pour récupérer le certificat et extraire ces champs de la réponse.

Pour plus d’informations, consultez la [documentation sur les points d’entrée de certificat public](../../../data-governance/mtls-api/public-certificate-endpoint.md).

## Liste autorisée d’adresses IP {#ip-address-allowlist}

Pour répondre aux exigences de sécurité et de conformité des clients, Experience Platform fournit une liste des adresses IP statiques que vous pouvez inscrire sur la liste autorisée pour la destination de l’API HTTP. Pour obtenir la liste complète des adresses IP à placer sur la liste autorisée placer sur la liste autorisée [ consultez la section ](/help/destinations/catalog/streaming/ip-address-allow-list.md)Adresses IP à configurer pour les destinations de diffusion en continu.

## Types d’authentification pris en charge {#supported-authentication-types}

La destination API HTTP prend en charge plusieurs types d’authentification à votre point d’entrée HTTP :

* Point d’entrée HTTP sans authentification ;
* Authentification par jeton porteur ;
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

* [Octroi du mot de passe OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/password-grant/).

## Se connecter à la destination {#connect-destination}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Lors de la connexion à cette destination, vous devez fournir les informations suivantes :

### Informations d’authentification {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_http_clientcredentialstype"
>title="Type d’informations d’identification client"
>abstract="Sélectionnez **Formulaire de corps encodé** pour inclure l’identifiant client et le secret client dans le corps de la requête ou **Autorisation de base** pour inclure l’identifiant client et le secret client dans un en-tête d’autorisation. Consultez des exemples dans la documentation."

#### Authentification par jeton porteur {#bearer-token-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Jeton porteur]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, à l’aide de l’authentification par jeton porteur.](../../assets/catalog/http/http-api-authentication-bearer.png)

* **[!UICONTROL Jeton porteur]** : insérez le jeton porteur pour l’authentification à votre emplacement HTTP.

#### Aucune authentification {#no-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Aucune]** pour vous connecter à votre point d’entrée HTTP :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, sans utiliser d’authentification.](../../assets/catalog/http/http-api-authentication-none.png)

Lorsque vous sélectionnez cette ouverture d’authentification, il vous suffit de sélectionner **[!UICONTROL Se connecter à la destination]** et la connexion à votre point d’entrée est établie.

#### Authentification par mot de passe OAuth 2 {#oauth-2-password-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Mot de passe OAuth 2]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, à l’aide d’OAuth 2 avec authentification par mot de passe.](../../assets/catalog/http/http-api-authentication-oauth2-password.png)

* **[!UICONTROL URL du jeton d’accès]** : URL de votre côté qui émet des jetons d’accès et, éventuellement, actualise les jetons.
* **[!UICONTROL Identifiant client]** : l’[!DNL client ID] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Secret client]** : le [!DNL client secret] que votre système attribue à Adobe Experience Platform.
* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur pour accéder à votre point d’entrée HTTP.
* **[!UICONTROL Mot de passe]** : mot de passe pour accéder à votre point d’entrée HTTP.

#### Authentification avec informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

Si vous sélectionnez le type d’authentification **[!UICONTROL Informations d’identification du client OAuth 2]** pour vous connecter à votre point d’entrée HTTP, saisissez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination API HTTP, à l’aide d’OAuth 2 avec authentification par informations d’identification du client.](../../assets/catalog/http/http-api-authentication-oauth2-client-credentials.png)

>[!WARNING]
> 
>Lors de l’utilisation de l’authentification [!UICONTROL Informations d’identification du client OAuth 2], l’URL [!UICONTROL URL du jeton d’accès] peut avoir un paramètre de requête au maximum. L’ajout d’une [!UICONTROL URL de jeton d’accès] avec d’autres paramètres de requête peut entraîner des problèmes lors de la connexion à votre point d’entrée.

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

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination HTTP.](../../assets/catalog/http/http-api-destination-details.png)

* **[!UICONTROL Nom]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL En-têtes]** : saisissez tous les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, en suivant ce format : `header1:value1,header2:value2,...headerN:valueN`.
* **[!UICONTROL Point d’entrée HTTP]** : URL du point d’entrée HTTP vers lequel vous souhaitez envoyer les données de profil.
* **[!UICONTROL Paramètres de requête]** : vous pouvez éventuellement ajouter des paramètres de requête à l’URL du point d’entrée HTTP. Mettez en forme les paramètres de requête que vous utilisez comme suit : `parameter1=value&parameter2=value`.
* **[!UICONTROL Inclure les noms de segment]** : activez ce bouton si vous souhaitez que l’exportation des données inclue les noms des audiences que vous exportez. **Remarque** : les noms de segment ne sont inclus que pour les segments mappés à la destination. Les segments non mappés qui apparaissent dans l’exportation n’incluent pas le champ `name` . Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.
* **[!UICONTROL Inclure la date et l’heure de segment]** : activez ce bouton si vous souhaitez que l’exportation de données inclue la date et l’heure UNIX de la création et des mises à jour des audiences, ainsi que la date et l’heure UNIX du mappage des audiences à la destination pour l’activation. Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* L’[évaluation de la politique de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas prise en charge dans les exportations vers la destination API HTTP. [En savoir plus](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Consultez [ Activer les données d’audience vers des destinations d’exportation de profil de diffusion en continu ](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#attributes}

Lors de l’étape [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination d’API HTTP afin d’exporter les données vers votre point d’entrée API uniquement lorsque des mises à jour importantes d’un profil se sont produites à la suite d’une qualification d’audience ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’appartenance à l’audience pour au moins une des audiences mappées à la destination. Par exemple, le profil est éligible à l’une des audiences mappées à la destination ou a quitté l’une de ces audiences.
* La mise à jour du profil a été déterminée par une modification dans le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà éligible à l’une des audiences mappées à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si une audience mappée au flux de destination comporte cent membres et que cinq nouveaux profils sont éligibles à ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation {#what-determines-export-what-is-included}

Concernant les données exportées pour un profil donné, il est important de comprendre les deux concepts différents entre *ce qui détermine l’exportation de données vers votre destination d’API HTTP* et *les données incluses dans l’exportation*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si le statut de `segmentMembership` d’un profil passe à `realized` ou `exiting` ou qu’un attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations d’API HTTP, les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Toute modification pour un attribut est considérée comme une mise à jour, qu’il s’agisse ou non de la même valeur. Cela signifie qu’une réécriture sur un attribut est considérée comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>L’objet `segmentMembership` inclut le segment mappé dans le flux de données d’activation, pour lequel le statut du profil a changé suite à un événement de qualification ou de sortie de segment. Notez que d’autres segments non mappés pour lesquels le profil s’est qualifié peuvent faire partie de l’exportation de destination, si ces segments appartiennent à la même [politique de fusion](/help/profile/merge-policies/overview.md) que le segment mappé dans le flux de données d’activation. <br> **Important** : lorsque l’option **[!UICONTROL Inclure les noms de segment]** est activée, les noms de segment ne sont inclus que pour les segments mappés à la destination. Les segments non mappés qui apparaissent dans l’exportation n’incluent pas le champ `name`, même si l’option est activée. </li><li>Toutes les identités dans l’objet `identityMap` sont également incluses (actuellement Experience Platform ne prend pas en charge le mappage d’identité dans la destination de l’API HTTP).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style="table-layout:fixed"}

Prenons l’exemple d’un flux de données vers une destination HTTP dans lequel trois audiences sont sélectionnées et quatre attributs sont mappés à la destination.

![Exemple de flux de données de destination d’une API HTTP.](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des *trois segments mappés*. Cependant, lors de l’exportation des données, dans l’objet `segmentMembership` (voir la section [Données exportées](#exported-data) ci-dessous), d’autres audiences non mappées peuvent apparaître si ce profil particulier en est membre et s’il partage la même politique de fusion que l’audience qui a déclenché l’exportation. Si un profil est qualifié pour le segment **Client avec des voitures DeLorean**, mais qu’il est également membre des segments **Film « Retour vers le futur »** visionné et **Fans de science-fiction**, alors ces deux autres audiences seront également présentes dans l’objet `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données, si elles partagent la même politique de fusion que le segment **Client avec des voitures DeLorean**.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et chacun de ces quatre attributs mappés et présents sur le profil sera présent dans l’exportation des données.

## Renvoyer des données historiques {#historical-data-backfill}

Lorsque vous ajoutez une nouvelle audience à une destination existante, ou lorsque vous créez une nouvelle destination et que vous y mappez des audiences, Experience Platform exporte les données historiques de qualification d’audience vers la destination. Les profils qualifiés pour l’audience *auparavant* celle-ci a été ajoutée à la destination sont exportés vers la destination sous une heure environ.

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

+++ L’exemple d’exportation de données ci-dessous inclut des noms d’audience dans la section `segmentMembership`

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
          },
          "354e086f-2e11-49a2-9e39-e5d9a76be683": {
            "lastQualificationTime": "2020-04-15T02:41:50+0000",
            "status": "realized"
          }
        }
      }
```

**Remarque** : dans cet exemple, le premier segment (`5b998cb9-9488-4ec3-8d95-fa8338ced490`) est mappé à la destination et inclut le champ `name` . Le deuxième segment (`354e086f-2e11-49a2-9e39-e5d9a76be683`) n’est pas mappé à la destination et n’inclut pas le champ `name`, même si l’option **[!UICONTROL Inclure les noms de segment]** est activée.

+++

+++ L’exemple d’exportation de données ci-dessous inclut les horodatages d’audience dans la section `segmentMembership`

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

## Résolution des problèmes {#troubleshooting}

Pour garantir une diffusion des données fiable et éviter les problèmes de délai d’expiration, assurez-vous que votre point d’entrée HTTP répond dans les 2 secondes aux requêtes Experience Platform, comme spécifié dans la section [conditions préalables](#prerequisites). Les réponses qui prennent plus de temps provoquent des erreurs de temporisation.
