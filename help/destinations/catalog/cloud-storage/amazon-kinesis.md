---
keywords: Amazon Kinesis;destination Genesis;Genesis
title: Connexion Amazon Kinesis (version Beta)
description: Créez une connexion sortante en temps réel à votre stockage Amazon Kinesis pour diffuser des données depuis Adobe Experience Platform.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c62117de27b150f072731c910bb0593ce1fca082
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 4%

---

# (Version bêta) [!DNL Amazon Kinesis] connection

## Présentation {#overview}

>[!IMPORTANT]
>
>Le [!DNL Amazon Kinesis] destination dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Le [!DNL Kinesis Data Streams] service by [!DNL Amazon Web Services] vous permet de collecter et de traiter de grands flux d’enregistrements de données en temps réel.

Vous pouvez créer une connexion sortante en temps réel vers votre [!DNL Amazon Kinesis] stockage pour diffuser des données à partir de Adobe Experience Platform.

* Pour plus d’informations sur [!DNL Amazon Kinesis], reportez-vous à la section [Documentation Amazon](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Pour vous connecter à [!DNL Amazon Kinesis] par programmation, reportez-vous à la section [Tutoriel sur l’API des destinations de diffusion en continu](../../api/streaming-destinations.md).
* Pour vous connecter à [!DNL Amazon Kinesis] à l’aide de l’interface utilisateur de Platform, consultez les sections ci-dessous.

![Amazon Kinesis dans l’interface utilisateur](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Cas dʼutilisation {#use-cases}

En utilisant des destinations de diffusion en continu, telles que [!DNL Amazon Kinesis], vous pouvez facilement alimenter les événements de segmentation à valeur élevée et les attributs de profil associés dans vos systèmes de choix.

Par exemple, un prospect a téléchargé un livre blanc qui les qualifie en segment &quot;forte propension à convertir&quot;. En mappant le segment auquel le prospect appartient à la variable [!DNL Amazon Kinesis] destination, vous recevriez cet événement dans [!DNL Amazon Kinesis]. Vous pouvez y utiliser une approche par vous-même et décrire la logique commerciale en plus de l’événement, comme vous le pensez, qui fonctionne le mieux avec vos systèmes informatiques d’entreprise.

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## LISTE AUTORISÉE d’adresses IP {#ip-address-allowlist}

Pour répondre aux exigences de sécurité et de conformité des clients, Experience Platform fournit une liste d’adresses IP statiques que vous pouvez placer sur la liste autorisée pour la variable [!DNL Amazon Kinesis] destination. Voir [LISTE AUTORISÉE d’adresses IP pour les destinations de diffusion en continu](/help/destinations/catalog/streaming/ip-address-allow-list.md) pour obtenir la liste complète des adresses IP à placer sur la liste autorisée.

## Obligatoire [!DNL Amazon Kinesis] permissions {#required-kinesis-permission}

Pour établir une connexion et exporter des données vers votre [!DNL Amazon Kinesis] flux, l’Experience Platform a besoin d’autorisations pour les actions suivantes :

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Ces autorisations sont organisées à l’aide de la fonction [!DNL Kinesis] et sont vérifiées par Platform une fois que vous avez configuré votre destination Kinesis dans l’interface utilisateur de Platform.

L’exemple ci-dessous présente les droits d’accès minimaux requis pour exporter les données vers un [!DNL Kinesis] destination.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `kinesis:ListStreams` | Action qui répertorie vos flux de données Kinesis Amazon. |
| `kinesis:PutRecord` | Action qui écrit un enregistrement de données unique dans un flux de données Kinesis. |
| `kinesis:PutRecords` | Action qui écrit plusieurs enregistrements de données dans un flux de données Kinesis au cours d’un seul appel. |

Pour plus d’informations sur le contrôle de l’accès à [!DNL Kinesis] flux de données, lisez ce qui suit : [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Inclure les noms de segment"
>abstract="Basculez si vous souhaitez que l’exportation des données contienne les noms des segments que vous exportez. Affichez la documentation d’un exemple d’exportation de données avec cette option sélectionnée."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Inclure les horodatages de segment"
>abstract="Basculez si vous souhaitez que l’exportation des données inclue l’horodatage UNIX lors de la création et de la mise à jour des segments, ainsi que l’horodatage UNIX lorsque les segments ont été mappés à la destination pour activation. Affichez la documentation d’un exemple d’exportation de données avec cette option sélectionnée."

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!DNL Amazon Web Services]clé d&#39;accès et clé secrète**: Dans [!DNL Amazon Web Services], générez une `access key - secret access key` pour accorder l’accès à Platform à votre [!DNL Amazon Kinesis] compte . En savoir plus dans la section [Documentation Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Permet d’indiquer [!DNL Amazon Web Services] région vers laquelle diffuser des données.
* **Nom**: Attribuez un nom à votre connexion pour [!DNL Amazon Kinesis]
* **Description**: Fournissez une description de votre connexion à [!DNL Amazon Kinesis].
* **stream**: Indiquez le nom d’un flux de données existant dans votre [!DNL Amazon Kinesis] compte . Platform exportera les données vers ce flux.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activer des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Comportement d’exportation de profils {#profile-export-behavior}

Experience Platform optimise le comportement d’exportation de profils dans votre [!DNL Amazon Kinesis] destination : pour exporter uniquement les données vers votre destination lorsque des mises à jour pertinentes ont eu lieu suite à la qualification du segment ou à d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par un changement de l’adhésion au segment pour au moins un des segments mappés à la destination. Par exemple, le profil s’est qualifié pour l’un des segments mappés à la destination ou a quitté l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md). Par exemple, un profil qui s’était déjà qualifié pour l’un des segments mappés à la destination a été ajouté une nouvelle identité dans l’attribut identity map .
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils où des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour le segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes n’ont pas changé.

### Ce qui détermine un export de données et ce qui est inclus dans l’export {#what-determines-export-what-is-included}

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents de *ce qui détermine l’exportation des données vers votre [!DNL Amazon Kinesis] destination* et *les données incluses dans l’exportation ;*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si un segment mappé change d’état (de null à Reçue ou de get/existing à Extioning) ou que tout attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Puisque les identités ne peuvent actuellement pas être mappées à [!DNL Amazon Kinesis] les destinations, les modifications de toute identité sur un profil donné déterminent également les exportations de destination.</li><li>Une modification pour un attribut est définie comme toute mise à jour de l’attribut, qu’il s’agisse ou non de la même valeur. Cela signifie qu’un remplacement sur un attribut est considéré comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>Tous les segments (avec le dernier état d’adhésion), qu’ils soient mappés ou non dans le flux de données, sont inclus dans la variable `segmentMembership` .</li><li>Toutes les identités dans la variable `identityMap` sont également inclus (l’Experience Platform ne prend actuellement pas en charge le mappage d’identité dans la variable [!DNL Amazon Kinesis] destination).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Par exemple, considérez ce flux de données comme un [!DNL Amazon Kinesis] destination où trois segments sont sélectionnés dans le flux de données et quatre attributs sont mappés à la destination.

![Flux de données de destination Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Un export de profil vers la destination peut être déterminé par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, dans l’exportation des données, dans la variable `segmentMembership` (voir [Données exportées](#exported-data) ci-dessous), d’autres segments non mappés peuvent apparaître si ce profil particulier en fait partie. Si un profil est admissible pour le segment Client avec des voitures de Lorée, mais qu’il est également membre des segments de fans de films et de science-fiction &quot;Retour vers le futur&quot; de la visionneuse, ces deux autres segments seront également présents dans la variable `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et l’un des quatre attributs mappés présents sur le profil sera présent dans l’exportation des données.

## Données exportées {#exported-data}

Votre exportation [!DNL Experience Platform] Les données arrivent dans votre [!DNL Amazon Kinesis] destination au format JSON. Par exemple, l’exportation ci-dessous contient un profil qui s’est qualifié pour un certain segment, qui est membre de deux autres segments et qui a quitté un autre segment. L’exportation inclut également le prénom, le nom, la date de naissance et l’adresse email personnelle de l’attribut de profil. Les identités de ce profil sont ECID et email.

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
>* [Connexion à Amazon Kinesis et activation des données à l’aide de l’API Flow Service](../../api/streaming-destinations.md)
>* [Destination des centres d’événements Azure](./azure-event-hubs.md)
>* [Types et catégories de destination](../../destination-types.md)

