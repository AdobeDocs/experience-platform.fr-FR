---
keywords: Destination du hub d’événements Azure ; hub d’événements Azure ; thub d’événements azure
title: Connexion Azure Event Hubs
description: Créez une connexion sortante en temps réel à votre  [!DNL Azure Event Hubs] stockage pour diffuser des données depuis l’Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 51%

---

# Connexion [!DNL Azure Event Hubs]

## Présentation {#overview}

>[!IMPORTANT]
>
> Cette destination est disponible uniquement pour les clients d’[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

[!DNL Azure Event Hubs] est une plateforme de diffusion en continu de données volumineuses et un service d’ingestion d’événements. Il peut recevoir et traiter des millions d’événements par seconde. Les données envoyées à un hub d’événements peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’adaptateurs de traitement par lot/stockage.

Vous pouvez créer une connexion sortante en temps réel à votre stockage [!DNL Azure Event Hubs] pour diffuser des données depuis Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Azure Event Hubs], consultez la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Pour vous connecter à [!DNL Azure Event Hubs] par programmation, consultez le [tutoriel sur l’API des destinations de diffusion en continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Platform, reportez-vous aux sections ci-dessous.

![Kinesis AWS dans l’interface utilisateur](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Cas d’utilisation {#use-cases}

En utilisant des destinations de diffusion en continu telles que [!DNL Azure Event Hubs], vous pouvez facilement alimenter les événements de segmentation à valeur élevée et les attributs de profil associés dans vos systèmes de votre choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en segment &quot;forte propension à la conversion&quot;. En mappant l’audience que le prospect appartient à la destination [!DNL Azure Event Hubs], vous recevrez cet événement dans [!DNL Azure Event Hubs]. Vous pouvez y utiliser une approche par vous-même et décrire la logique commerciale en plus de l’événement, comme vous le pensez, qui fonctionne le mieux avec vos systèmes informatiques d’entreprise.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Liste autorisée d’adresses IP {#ip-address-allowlist}

Pour répondre aux exigences de sécurité et de conformité des clients, Experience Platform fournit une liste d’adresses IP statiques que vous pouvez placer sur la liste autorisée pour la destination [!DNL Azure Event Hubs]. Reportez-vous à la [liste autorisée d’adresses IP pour les destinations en flux continu](/help/destinations/catalog/streaming/ip-address-allow-list.md) pour la liste complète des adresses IP à autoriser.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Lors de la connexion à cette destination, vous devez fournir les informations suivantes :

### Informations d’authentification {#authentication-information}

#### Authentification standard {#standard-authentication}

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails d’authentification standard Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Si vous sélectionnez le type **[!UICONTROL Authentification standard]** pour vous connecter à votre point d’entrée HTTP, renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

* **[!UICONTROL Nom de clé SAS]** : nom de la règle d’autorisation, également appelé nom de clé SAS.
* **[!UICONTROL Clé SAS]** : clé primaire de l’espace de noms Event Hubs. Les droits `sasPolicy` auxquels correspond `sasKey` doivent être **manage** pour que la liste des centres d’événements soit renseignée. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] avec des clés SAS dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]** : renseignez votre espace de noms [!DNL Azure Event Hubs]. Découvrez les espaces de noms [!DNL Azure Event Hubs] dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### Authentification SAS (Shared Access Signature) {#sas-authentication}

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails d’authentification standard Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Si vous sélectionnez le type **[!UICONTROL Authentification standard]** pour vous connecter à votre point d’entrée HTTP, renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

* **[!UICONTROL Nom de clé SAS]** : nom de la règle d’autorisation, également appelé nom de clé SAS.
* **[!UICONTROL Clé SAS]** : clé primaire de l’espace de noms Event Hubs. Les droits `sasPolicy` auxquels correspond `sasKey` doivent être **manage** pour que la liste des centres d’événements soit renseignée. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] avec des clés SAS dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Espace de noms]** : renseignez votre espace de noms [!DNL Azure Event Hubs]. Découvrez les espaces de noms [!DNL Azure Event Hubs] dans la [documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Nom du hub d’événements]** : renseignez votre nom [!DNL Azure Event Hub] . Découvrez les [!DNL Azure Event Hubs] noms dans la [documentation Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Inclure les noms de segment"
>abstract="Activez ce bouton si vous voulez que l’export de données inclue les noms des audiences que vous exportez. Consultez la documentation pour un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Inclure la date et l’heure de segment"
>abstract="Activez ce bouton si vous souhaitez que l’export de données inclue la date et l’heure UNIX de la création et des mises à jour des audiences, ainsi que la date et l’heure UNIX du mappage des audiences à la destination pour l’activation. Consultez la documentation pour un exemple d’exportation de données avec cette option sélectionnée."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Nom]** : renseignez un nom pour la connexion à [!DNL Azure Event Hubs].
* **[!UICONTROL Description]** : fournissez une description de la connexion.  Exemples : &quot;Clients Premium&quot;, &quot;Clients intéressés par le kitesurfing&quot;.
* **[!UICONTROL eventHubName]** : donnez un nom au flux vers votre destination [!DNL Azure Event Hubs].
* **[!UICONTROL Inclure les noms de segment]** : basculez si vous souhaitez que l’exportation des données inclut les noms des audiences que vous exportez. Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.
* **[!UICONTROL Inclure les horodatages de segment]** : basculez si vous souhaitez que l’exportation des données inclue l’horodatage UNIX lors de la création et de la mise à jour des audiences, ainsi que l’horodatage UNIX lorsque les audiences ont été mappées à la destination pour l’activation. Pour un exemple d’exportation de données avec cette option sélectionnée, reportez-vous à la section [Données exportées](#exported-data) plus bas.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* [L’évaluation de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas prise en charge dans les exportations vers la destination Azure Event Hubs. [En savoir plus](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Pour obtenir des instructions sur l’activation des audiences vers cette destination, reportez-vous à la section [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) .

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils vers votre destination [!DNL Azure Event Hubs] afin de n’exporter les données vers votre destination que lorsque des mises à jour pertinentes apportées à un profil ont eu lieu suite à la qualification de l’audience ou à d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’appartenance à l’audience pour au moins une des audiences mappées à la destination. Par exemple, le profil est éligible à l’une des audiences mappées à la destination ou a quitté l’une de ces audiences.
* La mise à jour du profil a été déterminée par une modification dans le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà éligible à l’une des audiences mappées à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si une audience mappée au flux de destination comporte cent membres et que cinq nouveaux profils sont éligibles à ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Remarque : tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation. {#what-determines-export-what-is-included}

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents de *qui déterminent une exportation de données vers votre [!DNL Azure Event Hubs] destination* et *quelles données sont incluses dans l’exportation*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et audiences mappés servent de repère pour un export de destination. Cela signifie que si une audience mappée change d’état (de `null` à `realized` ou de `realized` à `exiting`) ou qu’un attribut mappé est mis à jour, une destination est exportée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations [!DNL Azure Event Hubs], les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Toute modification pour un attribut est considérée comme une mise à jour, qu’il s’agisse ou non de la même valeur. Cela signifie qu’une réécriture sur un attribut est considérée comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>L’objet `segmentMembership` inclut l’audience mappée dans le flux de données d’activation, pour lequel le statut du profil a changé suite à un événement d’éligibilité ou de sortie d’audience. Notez que d’autres audiences non mappées pour lesquelles le profil est éligible peuvent faire partie de l’export de destination, si ces audiences appartiennent à la même [politique de fusion](/help/profile/merge-policies/overview.md) que l’audience mappée dans le flux de données d’activation. </li><li>Toutes les identités de l’objet `identityMap` sont également incluses (l’Experience Platform ne prend actuellement pas en charge le mappage d’identité dans la destination [!DNL Azure Event Hubs]).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style="table-layout:fixed"}

Prenons l’exemple de ce flux de données vers une destination [!DNL Azure Event Hubs] où trois audiences sont sélectionnées dans le flux de données et où quatre attributs sont mappés à la destination.

![Flux de données de destination Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des *trois segments mappés*. Cependant, dans l’exportation des données, dans l’objet `segmentMembership` (voir la section [Données exportées](#exported-data) ci-dessous), d’autres audiences non mappées peuvent apparaître, si ce profil particulier en est membre et si elles partagent la même stratégie de fusion que l’audience qui a déclenché l’exportation. Si un profil est admissible pour l’audience **Client avec des DeLorean Cars**, mais qu’il est également membre du film **Watched &quot;Back to the Future&quot;** et des segments **fans de science fiction**, ces deux autres audiences seront également présentes dans l’objet `segmentMembership` de l’exportation de données, même si elles ne sont pas mappées dans le flux de données, si elles partagent la même stratégie de fusion avec la même **Client avec des DeLorean Cars**.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et chacun de ces quatre attributs mappés et présents sur le profil sera présent dans l’exportation des données.

## Renvoyer des données historiques {#historical-data-backfill}

Lorsque vous ajoutez une nouvelle audience à une destination existante, ou lorsque vous créez une destination et que vous mappez des audiences avec celle-ci, l’Experience Platform exporte les données historiques de qualification des audiences vers la destination. Les profils qui remplissent les critères de l’audience *avant* l’audience a été ajoutée à la destination sont exportés vers la destination dans un délai d’environ une heure.

## Données exportées {#exported-data}

Les données [!DNL Experience Platform] exportées arrivent dans votre destination [!DNL Azure Event Hubs] au format JSON. Par exemple, l’exportation ci-dessous contient un profil qualifié pour un certain segment, qui est membre de deux autres segments et qui a quitté un autre segment. L’exportation inclut également le prénom, le nom, la date de naissance et l’adresse e-mail personnelle de l’attribut de profil. Les identités de ce profil sont ECID et e-mail.

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

+++ L’exemple d’exportation de données ci-dessous inclut les noms d’audience dans la section `segmentMembership` .

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

+++ L’exemple d’exportation de données ci-dessous inclut les horodatages d’audience dans la section `segmentMembership` .

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

>[!MORELIKETHIS]
>
>* [Connectez-vous aux centres d’événements Azure et activez les données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination AWS Kinesis](./amazon-kinesis.md)
>* [Types et catégories de destination](../../destination-types.md)
