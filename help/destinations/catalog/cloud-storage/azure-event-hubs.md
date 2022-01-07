---
keywords: Destination du hub d’événements Azure ; hub d’événements Azure ; thub d’événements azure
title: (Version bêta) Connexion à !DNL Azure Event Hubs
description: Créez une connexion sortante en temps réel à votre stockage !DNL Azure Event Hubs] pour diffuser des données depuis l’Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 8d2c5ef477d4707be4c0da43ba1f672fac797604
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 2%

---

# (Version bêta) [!DNL Azure Event Hubs] connection

## Présentation {#overview}

>[!IMPORTANT]
>
>Le [!DNL Azure Event Hubs] destination dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

[!DNL Azure Event Hubs] est une plateforme de diffusion en continu de données volumineuses et un service d’ingestion d’événements. Il peut recevoir et traiter des millions d’événements par seconde. Les données envoyées à un hub d’événements peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’adaptateurs de traitement par lot/stockage.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Azure Event Hubs] stockage pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Azure Event Hubs], reportez-vous à la section [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Pour vous connecter à [!DNL Azure Event Hubs] par programmation, reportez-vous à la section [Tutoriel sur l’API des destinations de diffusion en continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Platform, consultez les sections ci-dessous.

![AWS Kinesis dans l’interface utilisateur](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en continu, telles que [!DNL Azure Event Hubs], vous pouvez facilement alimenter les événements de segmentation à valeur élevée et les attributs de profil associés dans vos systèmes de choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en segment &quot;forte propension à convertir&quot;. En mappant le segment auquel le prospect appartient à la variable [!DNL Azure Event Hubs] destination, vous recevriez cet événement dans [!DNL Azure Event Hubs]. Vous pouvez y utiliser une approche par vous-même et décrire la logique commerciale en plus de l’événement, comme vous le pensez, qui fonctionne le mieux avec vos systèmes informatiques d’entreprise.

## Type d&#39;export {#export-type}

**Basé sur les profils** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), selon le choix effectué dans l’écran de sélection des attributs de la variable [workflow d&#39;activation d&#39;audience](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom de clé SAS]** et **[!UICONTROL Clé SAS]**: Renseignez le nom et la clé de votre clé SAS. En savoir plus sur l’authentification à [!DNL Azure Event Hubs] avec les clés SAS dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]**: Renseignez vos [!DNL Azure Event Hubs] espace de noms. En savoir plus sur [!DNL Azure Event Hubs] espaces de noms dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nom]**: Renseignez un nom pour la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Hommes intéressés par le kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom à la diffusion de [!DNL Azure Event Hubs] destination.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination Azure Event Hubs afin de n’exporter les données vers votre destination que lorsque des mises à jour pertinentes d’un profil se sont produites après la qualification de segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déclenchée par un changement de l’adhésion au segment pour au moins un des segments mappés à la destination. Par exemple, le profil s’est qualifié pour l’un des segments mappés à la destination ou a quitté l’un des segments mappés à la destination.
* La mise à jour du profil a été déclenchée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’un des segments mappés à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déclenchée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils où des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes n’ont pas changé.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans [!DNL Azure Event Hubs] au format JSON. Par exemple, l’événement ci-dessous contient l’attribut de profil d’adresse électronique d’une audience qui s’est qualifiée pour un certain segment et qui a quitté un autre segment. Les identités de ce prospect sont ECID et email.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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


>[!MORELIKETHIS]
>
>* [Connectez-vous à Azure Event Hubs et activez les données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination AWS Kinesis](./amazon-kinesis.md)
>* [Types et catégories de destination](../../destination-types.md)

