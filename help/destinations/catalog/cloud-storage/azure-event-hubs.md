---
keywords: Destination du hub d’événements Azure ; hub d’événements Azure ; thub d’événements azure
title: (Version bêta) [!DNL Azure Event Hubs] connection
description: Créez une connexion sortante en temps réel avec votre [!DNL Azure Event Hubs] stockage pour diffuser des données depuis l’Experience Platform.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: be09d794a4cbc3afc76df70d11f55b0cae6f2009
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

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

* **[!UICONTROL Nom de clé SAS]**: Nom de la règle d’autorisation, également appelé nom de clé SAS.
* **[!UICONTROL Clé SAS]**: Clé Principale de l’espace de noms des centres d’événements. Le `sasPolicy` que la variable `sasKey` correspond à **gérer** droits configurés pour que la liste des centres d’événements soit renseignée. En savoir plus sur l’authentification à [!DNL Azure Event Hubs] avec les clés SAS dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]**: Renseignez vos [!DNL Azure Event Hubs] espace de noms. En savoir plus sur [!DNL Azure Event Hubs] espaces de noms dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nom]**: Renseignez un nom pour la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]**: Fournissez une description de la connexion.  Exemples : &quot;Clients de niveau Premium&quot;, &quot;Clients intéressés par le kitesurfing&quot;.
* **[!UICONTROL eventHubName]**: Attribuez un nom à la diffusion de [!DNL Azure Event Hubs] destination.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils dans votre [!DNL Azure Event Hubs] destination : pour exporter uniquement les données vers votre destination lorsque des mises à jour pertinentes ont eu lieu suite à la qualification du segment ou à d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’adhésion au segment pour au moins un des segments mappés à la destination. Par exemple, le profil s’est qualifié pour l’un des segments mappés à la destination ou a quitté l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’un des segments mappés à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils où des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes n’ont pas changé.

### Ce qui détermine un export de données et ce qui est inclus dans l’export {#what-determines-export-what-is-included}

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents de *ce qui détermine l’exportation des données vers votre [!DNL Azure Event Hubs] destination* et *les données incluses dans l’exportation ;*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si un segment mappé change d’état (de null à Reçue ou de get/existing à Extioning) ou que tout attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Puisque les identités ne peuvent actuellement pas être mappées à [!DNL Azure Event Hubs] les destinations, les modifications de toute identité sur un profil donné déterminent également les exportations de destination.</li><li>Une modification pour un attribut est définie comme toute mise à jour de l’attribut, qu’il s’agisse ou non de la même valeur. Cela signifie qu’un remplacement sur un attribut est considéré comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>Tous les segments (avec le dernier état d’adhésion), qu’ils soient mappés ou non dans le flux de données, sont inclus dans la variable `segmentMembership` .</li><li>Toutes les identités dans la variable `identityMap` sont également inclus (l’Experience Platform ne prend actuellement pas en charge le mappage d’identité dans la variable [!DNL Azure Event Hubs] destination).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Par exemple, considérez ce flux de données comme un [!DNL Azure Event Hubs] destination où trois segments sont sélectionnés dans le flux de données et quatre attributs sont mappés à la destination.

![Flux de données de destination Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un export de profil vers la destination peut être déterminé par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, dans l’exportation des données, dans la variable `segmentMembership` (voir [Données exportées](#exported-data) ci-dessous), d’autres segments non mappés peuvent apparaître si ce profil particulier en fait partie. Si un profil est admissible pour le segment Client avec des voitures de Lorée, mais qu’il est également membre des segments de fans de films et de science-fiction &quot;Retour vers le futur&quot; de la visionneuse, ces deux autres segments seront également présents dans la variable `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et l’un des quatre attributs mappés présents sur le profil sera présent dans l’exportation des données.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre [!DNL Azure Event Hubs] destination au format JSON. Par exemple, l’exportation ci-dessous contient un profil qui s’est qualifié pour un certain segment, qui est membre de deux autres segments et qui a quitté un autre segment. L’exportation inclut également le prénom, le nom, la date de naissance et l’adresse email personnelle de l’attribut de profil. Les identités de ce profil sont ECID et email.

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


>[!MORELIKETHIS]
>
>* [Connectez-vous à Azure Event Hubs et activez les données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination AWS Kinesis](./amazon-kinesis.md)
>* [Types et catégories de destination](../../destination-types.md)

