---
keywords: diffusion en continu;
title: Connexion via l’API HTTP
description: La destination d’API HTTP dans Adobe Experience Platform vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: f098df9df2baa971db44a6746949f021e212ae3e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 4%

---

# (Version bêta) Connexion à l’API HTTP

>[!IMPORTANT]
>
>La destination de l’API HTTP dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

La destination de l’API HTTP est une [!DNL Adobe Experience Platform] destination de diffusion en continu qui vous aide à envoyer des données de profil à des points de terminaison HTTP tiers.

Pour envoyer des données de profil aux points de terminaison HTTP, vous devez d’abord [se connecter à la destination](#connect-destination) in [!DNL Adobe Experience Platform].

## Cas dʼutilisation {#use-cases}

La destination HTTP est destinée aux clients qui doivent exporter les données de profil XDM et les segments d’audience vers des points de terminaison HTTP génériques.

Les points de terminaison HTTP peuvent être les systèmes des clients ou des solutions tierces.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Contactez les représentants de votre Adobe ou l’assistance clientèle Adobe si vous souhaitez activer la fonctionnalité bêta de destination de l’API HTTP pour votre entreprise.

Pour utiliser la destination d’API HTTP afin d’exporter des données en dehors d’Experience Platform, vous devez respecter les conditions préalables suivantes :

* Vous devez disposer d’un point de terminaison HTTP qui prend en charge l’API REST.
* Votre point de terminaison HTTP doit prendre en charge le schéma de profil Experience Platform. Aucune transformation en schéma de charge utile tiers n’est prise en charge dans la destination de l’API HTTP. Reportez-vous à la section [données exportées](#exported-data) pour un exemple du schéma de sortie Experience Platform.
* Votre point de terminaison HTTP doit prendre en charge les en-têtes.
* Votre point de terminaison HTTP doit prendre en charge [Informations d’identification du client OAuth 2.0](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) authentification. Cette exigence est valide lorsque la destination de l’API HTTP est en phase bêta.
* Les informations d’identification du client doivent être incluses dans le corps des requêtes du POST vers votre point de terminaison, comme illustré dans l’exemple ci-dessous.

```shell
curl --location --request POST '<YOUR_API_ENDPOINT>' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```


Vous pouvez également utiliser [Adobe Experience Platform Destination SDK](/help/destinations/destination-sdk/overview.md) pour configurer une intégration et envoyer des données de profil Experience Platform à un point de terminaison HTTP.

## Connexion à la destination {#connect-destination}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL httpEndpoint]**: la valeur [!DNL URL] du point de terminaison HTTP auquel vous souhaitez envoyer les données de profil.
   * Vous pouvez éventuellement ajouter des paramètres de requête au [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: la valeur [!DNL URL] du point de terminaison HTTP utilisé pour [!DNL OAuth2] authentification.
* **[!UICONTROL ID client]**: la valeur [!DNL clientID] du paramètre utilisé dans la variable [!DNL OAuth2] informations d’identification du client.
* **[!UICONTROL Secret du client]**: la valeur [!DNL clientSecret] du paramètre utilisé dans la variable [!DNL OAuth2] informations d’identification du client.

   >[!NOTE]
   >
   >Uniquement [!DNL OAuth2] les informations d’identification du client sont actuellement prises en charge.

* **[!UICONTROL Nom]**: saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL En-têtes personnalisés]**: saisissez les en-têtes personnalisés que vous souhaitez inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >L’implémentation actuelle nécessite au moins un en-tête personnalisé. Cette limitation sera résolue dans une prochaine mise à jour.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Attributs de destination {#attributes}

Dans le [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination d’API HTTP, afin de n’exporter les données vers votre point de terminaison d’API que lorsque des mises à jour appropriées d’un profil se sont produites à la suite de la qualification de segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déclenchée par un changement de l’adhésion au segment pour au moins un des segments mappés à la destination. Par exemple, le profil s’est qualifié pour l’un des segments mappés à la destination ou a quitté l’un des segments mappés à la destination.
* La mise à jour du profil a été déclenchée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’un des segments mappés à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déclenchée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils où des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes n’ont pas changé.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre [!DNL HTTP] destination au format JSON. Par exemple, l’export ci-dessous contient un profil qui s’est qualifié pour un certain segment et qui a quitté un autre segment. Il comprend le prénom, le nom, la date de naissance et l’adresse email personnelle de l’attribut de profil. Les identités de ce profil sont ECID et email.

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
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
