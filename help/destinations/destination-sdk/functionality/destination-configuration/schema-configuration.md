---
description: Découvrez comment configurer le schéma des partenaires pour les destinations créées avec Destination SDK.
title: Configuration des schémas de partenaire
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 10%

---


# Configuration des schémas de partenaire

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. Lorsque des données sont ingérées dans Platform, elles sont structurées selon un schéma XDM. Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](../../../../xdm/schema/composition.md).

Lors de la création d’une destination avec Destination SDK, vous pouvez définir votre propre schéma de partenaire à utiliser par votre plateforme de destination. Cela permet aux utilisateurs de mapper les attributs de profil de Platform à des champs spécifiques reconnus par votre plateforme de destination, le tout dans l’interface utilisateur de Platform.

Lors de la configuration du schéma des partenaires pour votre destination, vous pouvez affiner le mappage des champs pris en charge par votre plateforme de destination, par exemple :

* Autoriser les utilisateurs à mapper une `phoneNumber` Attribut XDM à un `phone` est pris en charge par votre plateforme de destination.
* Créez des schémas de partenaire dynamique que l’Experience Platform peut appeler dynamiquement pour récupérer une liste de tous les attributs pris en charge dans votre destination.
* Définissez les mappages de champs obligatoires requis par votre plateforme de destination.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination basée sur des fichiers ;](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer vos paramètres de schéma via le `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de configuration de schéma prises en charge que vous pouvez utiliser pour votre destination et indique ce que les clients verront dans l’interface utilisateur de Platform.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Configuration de schéma prise en charge {#supported-schema-types}

Destination SDK prend en charge plusieurs configurations de schéma :

* Les schémas statiques sont définis par le biais de la variable `profileFields` du tableau `schemaConfig` . Dans un schéma statique, vous définissez chaque attribut cible qui doit s’afficher dans l’interface utilisateur de l’Experience Platform dans la variable `profileFields` tableau. Si vous devez mettre à jour votre schéma, vous devez [mise à jour de la configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Les schémas dynamiques utilisent un type de serveur de destination supplémentaire, appelé [serveur de schéma dynamique](../../authoring-api/destination-server/create-destination-server.md), afin de générer dynamiquement des schémas sur la base de votre propre API. Les schémas dynamiques n’utilisent pas le `profileFields` tableau. Si vous devez mettre à jour votre schéma, il n’est pas nécessaire de [mise à jour de la configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md). Au lieu de cela, le serveur de schéma dynamique récupère le schéma mis à jour de votre API.
* Dans la configuration du schéma, vous avez la possibilité d’ajouter des mappages obligatoires (ou prédéfinis). Il s’agit de mappages que les utilisateurs peuvent afficher dans l’interface utilisateur de Platform, mais qu’ils ne peuvent pas modifier lors de la configuration d’une connexion à votre destination. Vous pouvez, par exemple, appliquer le champ de l’adresse électronique pour qu’il soit toujours envoyé à la destination.

Le `schemaConfig` utilise plusieurs paramètres de configuration, en fonction du type de schéma dont vous avez besoin, comme indiqué dans les sections ci-dessous.

## Création d’un schéma statique {#attributes-schema}

Pour créer un schéma statique avec des attributs de profil, définissez les attributs de la cible dans le `profileFields` comme illustré ci-dessous.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---------|----------|------|---|
| `profileFields` | Tableau | Facultatif | Définit le tableau des attributs de cible acceptés par votre plateforme de destination vers lequel les clients peuvent mapper leurs attributs de profil. Lors de l’utilisation d’un `profileFields` , vous pouvez omettre la variable `useCustomerSchemaForAttributeMapping` entièrement. |
| `useCustomerSchemaForAttributeMapping` | Booléen | Facultatif | Active ou désactive le mappage des attributs du schéma client aux attributs que vous définissez dans la variable `profileFields` tableau. <ul><li>Si la variable est définie sur `true`, les utilisateurs ne voient que la colonne source dans le champ de mappage. `profileFields` ne sont pas applicables dans ce cas.</li><li>Si la variable est définie sur `false`, les utilisateurs peuvent mapper les attributs sources de leur schéma aux attributs que vous avez définis dans la variable `profileFields` tableau.</li></ul> La valeur par défaut est `false`. |
| `profileRequired` | Booléen | Facultatif | Utilisation `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil de l’Experience Platform aux attributs personnalisés sur votre plateforme de destination. |
| `segmentRequired` | Booléen | Obligatoire | Ce paramètre est requis par Destination SDK et doit toujours être défini sur `true`. |
| `identityRequired` | Booléen | Obligatoire | Définissez sur . `true` si les utilisateurs doivent être en mesure de mapper [types d’identité](identity-namespace-configuration.md) de l’Experience Platform aux attributs que vous avez définis dans la variable `profileFields` tableau . |

{style="table-layout:auto"}

L’expérience de l’interface utilisateur qui en résulte est affichée dans les images ci-dessous.

Lorsque les utilisateurs sélectionnent le mapping de ciblage, ils peuvent voir les champs définis dans la variable `profileFields` tableau.

![Image de l’interface utilisateur affichant l’écran des attributs de la cible.](../../assets/functionality/destination-configuration/select-attributes.png)

Après avoir sélectionné les attributs, ils peuvent les voir dans la colonne du champ cible.

![Image de l’interface utilisateur présentant un schéma cible statique avec des attributs](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Création d’un schéma dynamique {#dynamic-schema-configuration}

Destination SDK prend en charge la création de schémas de partenaires dynamiques. Contrairement à un schéma statique, un schéma dynamique n’utilise pas une `profileFields` tableau. Au lieu de cela, les schémas dynamiques utilisent un serveur de schéma dynamique qui se connecte à votre propre API à partir de laquelle il récupère la configuration du schéma.

>[!IMPORTANT]
>
>Avant de créer un schéma dynamique, vous devez : [création d’un serveur de schéma dynamique](../../authoring-api/destination-server/create-destination-server.md).

Dans une configuration de schéma dynamique, la variable `profileFields` Le tableau est remplacé par `dynamicSchemaConfig` , comme illustré ci-dessous.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Chaîne | Obligatoire | Indique comment les clients [!DNL Platform] se connectent à votre destination. Les valeurs acceptées sont les suivantes : `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Utilisation `CUSTOMER_AUTHENTICATION` si les clients Platform se connectent à votre système via l’une des méthodes d’authentification décrites [here](customer-authentication.md). </li><li> Utilisez `PLATFORM_AUTHENTICATION` s’il existe un système d’authentification global entre Adobe et votre destination et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez [création d’un objet d’identification](../../credentials-api/create-credential-configuration.md) à l’aide de l’API Credentials. </li><li>Utilisez `NONE` si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `dynamicEnum.destinationServerId` | Chaîne | Obligatoire | Le `instanceId` de votre serveur de schéma dynamique. Ce serveur de destination inclut le point de terminaison de l’API que l’Experience Platform appellera pour récupérer le schéma dynamique. |
| `dynamicEnum.value` | Chaîne | Obligatoire | Nom du schéma dynamique, tel que défini dans la configuration du serveur de schéma dynamique. |
| `dynamicEnum.responseFormat` | Chaîne | Requis | Toujours définie sur `SCHEMA` lors de la définition d’un schéma dynamique. |
| `profileRequired` | Booléen | Facultatif | Utilisation `true` si les utilisateurs doivent être en mesure de mapper les attributs de profil de l’Experience Platform aux attributs personnalisés sur votre plateforme de destination. |
| `segmentRequired` | Booléen | Obligatoire | Ce paramètre est requis par Destination SDK et doit toujours être défini sur `true`. |
| `identityRequired` | Booléen | Obligatoire | Définissez sur . `true` si les utilisateurs doivent être en mesure de mapper [types d’identité](identity-namespace-configuration.md) de l’Experience Platform aux attributs que vous avez définis dans la variable `profileFields` tableau . |

{style="table-layout:auto"}

## Mappings requis {#required-mappings}

Dans la configuration du schéma, en plus de votre schéma statique ou dynamique, vous avez la possibilité d’ajouter des mappages obligatoires (ou prédéfinis). Il s’agit de mappages que les utilisateurs peuvent afficher dans l’interface utilisateur de Platform, mais qu’ils ne peuvent pas modifier lors de la configuration d’une connexion à votre destination.

Vous pouvez, par exemple, appliquer le champ de l’adresse électronique pour qu’il soit toujours envoyé à la destination.

>[!NOTE]
>
>Les combinaisons suivantes de mappages requis sont actuellement prises en charge :
>* Vous pouvez configurer un champ source obligatoire et un champ de destination obligatoire. Dans ce cas, les utilisateurs ne peuvent pas modifier ni sélectionner l’un des deux champs et peuvent uniquement afficher la sélection.
>* Vous ne pouvez configurer qu’un champ de destination obligatoire. Dans ce cas, les utilisateurs seront autorisés à sélectionner un champ source à mapper à la destination.
>
> La configuration d’un champ source requis est actuellement la seule *not* pris en charge.

Voir ci-dessous deux exemples de configuration d’un schéma avec les mappages requis et à quoi ils ressemblent à l’étape de mappage de l’ [Activation des données vers le workflow de destinations par lot](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mappages source et de destination requis]

L’exemple ci-dessous montre les mappages source et de destination requis. Lorsque les champs source et de destination sont spécifiés comme des mappages requis, les utilisateurs ne peuvent pas sélectionner ni modifier l’un des deux champs et peuvent uniquement afficher la sélection prédéfinie.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---|---|---|---|
| `requiredMappingsOnly` | Booléen | Facultatif | Lorsque cette valeur est définie sur true , les utilisateurs ne peuvent pas mapper d’autres attributs et identités dans le flux d’activation, à l’exception des mappages requis que vous définissez dans la variable `requiredMappings` tableau. |
| `requiredMappings.sourceType` | Chaîne | Obligatoire | Indique le type de la variable `source` champ . Valeurs prises en charge : <ul><li>`text/x.schema-path`: Utilisez cette valeur lorsque la variable `source` est un attribut de profil d’un schéma XDM.</li><li>`text/x.aep-xl`: Utilisez cette valeur lorsque la variable `source` est défini par une expression régulière. Exemple : `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Utilisez cette valeur lorsque la variable `source` est défini par un modèle de macro. Actuellement, le seul modèle de macro pris en charge est `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Chaîne | Obligatoire | Indique la valeur du champ source. Types de valeurs pris en charge : <ul><li>Attributs de profil XDM. Exemple : `personalEmail.address`. Lorsque votre attribut source est un attribut de profil XDM, définissez la variable `sourceType` du paramètre `text/x.schema-path`.</li><li>Expressions régulières. Exemple : `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Lorsque votre attribut source est une expression régulière, définissez la variable `sourceType` du paramètre `text/x.aep-xl`.</li><li>Modèles de macro. Exemple : `metadata.segment.alias`. Lorsque votre attribut source est un modèle de macro, définissez la variable `sourceType` du paramètre `text/plain`. Actuellement, le seul modèle de macro pris en charge est `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Chaîne | Obligatoire | Indique la valeur du champ cible. Lorsque les champs source et de destination sont spécifiés comme des mappages requis, les utilisateurs ne peuvent pas sélectionner ou modifier l’un des deux champs et peuvent uniquement afficher la sélection. |

{style="table-layout:auto"}

Par conséquent, la variable **[!UICONTROL Champ source]** et **[!UICONTROL Champ cible]** Les sections de l’interface utilisateur de Platform sont grisées.

![Image des mappages requis dans le flux d’activation de l’interface utilisateur.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Mappage de destination requis]

L’exemple ci-dessous illustre un mappage de destination obligatoire. Si seul le champ de destination est spécifié, les utilisateurs peuvent sélectionner le champ source à mapper.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---|---|---|---|
| `requiredMappingsOnly` | Booléen | Facultatif | Lorsque cette valeur est définie sur true , les utilisateurs ne peuvent pas mapper d’autres attributs et identités dans le flux d’activation, à l’exception des mappages requis que vous définissez dans la variable `requiredMappings` tableau. |
| `requiredMappings.destination` | Chaîne | Obligatoire | Indique la valeur du champ cible. Lorsque seul le champ de destination est spécifié, les utilisateurs peuvent sélectionner un champ source à mapper à la destination. |
| `mandatoryRequired` | Booléen | Facultatif | Indique si le mappage doit être marqué comme une [attribut obligatoire](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booléen | Facultatif | Indique si le mappage doit être marqué comme une [clé de déduplication](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Par conséquent, la variable **[!UICONTROL Champ cible]** dans l’interface utilisateur de Platform est grisée, tandis que la fonction **[!UICONTROL Champ source]** est principale et les utilisateurs peuvent interagir avec celle-ci. Le **[!UICONTROL Clé obligatoire]** et **[!UICONTROL Clé de déduplication]** Les options sont principales et les utilisateurs ne peuvent pas les modifier.

![Image des mappages requis dans le flux d’activation de l’interface utilisateur.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre quels types de schémas sont pris en charge par Destination SDK et comment configurer votre schéma.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Champs de données client](customer-data-fields.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)