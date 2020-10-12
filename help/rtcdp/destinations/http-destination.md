---
keywords: streaming;
title: La destination HTTP est une destination de plateforme de données client en temps réel Adobe qui vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
seo-title: La destination HTTP est une destination de plateforme de données client en temps réel Adobe qui vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
description: La destination HTTP est une destination de plateforme de données client en temps réel Adobe qui vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
seo-description: La destination HTTP est une destination de plateforme de données client en temps réel Adobe qui vous permet d’envoyer des données de profil à des points de terminaison HTTP tiers.
translation-type: tm+mt
source-git-commit: cf100e8df225a665eade5ee6ddab071707e93f8b
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 7%

---


# (Alpha) [!DNL HTTP] Destination

>[!IMPORTANT]
>
>La destination [!DNL HTTP] du CDP en temps réel Adobe est actuellement en alpha. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

La [!DNL HTTP] destination est une destination [!DNL Adobe Real-Time Customer Data Platform] de flux continu qui vous permet d’envoyer des données de profil à des [!DNL HTTP] points de terminaison tiers.

Pour envoyer des données de profil aux [!DNL HTTP] points de terminaison, vous devez d’abord vous connecter à la destination dans le [!DNL Adobe Real-Time Customer Data Platform](#connect-destination).

## Cas d’utilisation {#use-cases}

La [!DNL HTTP] [!DNL HTTP] destination est destinée aux clients qui doivent exporter des données de profil XDM et des segments d’audience vers des points de terminaison génériques.

[!DNL HTTP] les points de terminaison peuvent être des systèmes propres aux clients ou des solutions tierces.

## Connect to Destination {#connect-destination}

1. Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL  HTTP API], puis **[!UICONTROL Configurer]**.

   ![Activer la destination HTTP](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.
   ![Activer la destination HTTP](assets/connect-http-destination.png)

2. À l’étape [!UICONTROL Compte] , vous devez définir les détails de la connexion du point de terminaison HTTP. Sélectionnez **[!UICONTROL Nouveau compte]** et saisissez les détails de la connexion pour le point de terminaison HTTP auquel vous souhaitez vous connecter.
   * **[!UICONTROL httpEndpoint]**: l’intégralité [!DNL URL] du point de terminaison HTTP auquel vous souhaitez envoyer les données du profil.
      * Vous pouvez éventuellement ajouter des paramètres de requête au [!UICONTROL httpEndpoint][!DNL URL].
   * **[!UICONTROL authEndpoint]**: la fin complète [!DNL URL] du point de terminaison HTTP utilisé pour [!DNL OAuth2] l’authentification.
   * **[!UICONTROL ID]** client : le [!DNL clientID] paramètre utilisé dans les informations d’identification du [!DNL OAuth2] client.
   * **[!UICONTROL Secret]** client : le [!DNL clientSecret] paramètre utilisé dans les informations d’identification du [!DNL OAuth2] client.

   >[!NOTE]
   >
   >Seules [!DNL OAuth2] les informations d’identification du client sont actuellement prises en charge.

   ![Connexion au point de terminaison HTTP](assets/connect-http-endpoint.png)
3. Click **[!UICONTROL Connect to destination]**.
4. Une fois la connexion établie, cliquez sur **[!UICONTROL Suivant]**.
5. Dans l’étape [!UICONTROL Authentification] , saisissez les informations d’identification d’authentification du compte :
   * **[!UICONTROL Nom]**: entrez un nom qui vous permettra de reconnaître cette destination à l&#39;avenir.
   * **[!UICONTROL Description]**: entrez une description qui vous aidera à identifier cette destination dans le futur.
   * **[!UICONTROL En-têtes]** personnalisés : saisissez les en-têtes personnalisés à inclure dans les appels de destination, selon le format suivant : `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >L’implémentation actuelle requiert au moins un en-tête personnalisé. Cette limitation sera résolue dans une prochaine mise à jour.
   ![Authentification HTTP](assets/authentication-http-connection.png)

6. **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](../privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../data-governance/policies/overview.md#core-actions)données.
7. Cliquez sur **[!UICONTROL Créer une destination]**.

## Activer les segments

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](activate-destinations.md#select-attributes).

## Attributs de destination

Lors de l&#39;étape [[!UICONTROL Sélectionner les attributs]](activate-destinations.md#select-attributes) , lors de l&#39; [activation des segments](activate-destinations.md) vers une [!DNL HTTP] destination, nous vous recommandons de sélectionner un identifiant unique dans votre schéma [](../../profile/home.md#profile-fragments-and-union-schemas)d&#39;union. Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

## Données exportées {#exported-data}

Vos données [!DNL Experience Platform] exportées s’affichent dans votre [!DNL HTTP] destination au format JSON. Par exemple, le événement ci-dessous contient l’attribut profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et a quitté un autre segment. Les identités de cette prospect sont [!DNL ECID] et e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
