---
description: Découvrez comment configurer les identités cibles prises en charge pour les destinations créées avec Destination SDK.
title: Configuration de l’espace de noms d’identité
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 56%

---

# Configuration de l’espace de noms d’identité

Experience Platform utilise des espaces de noms d’identité pour décrire le type d’identités spécifiques. Par exemple, un espace de noms d’identité intitulé `Email` identifie une valeur telle que `name@email.com` en tant qu’adresse électronique.

Selon le type de destination que vous créez (en flux continu ou basé sur des fichiers), gardez à l’esprit les exigences d’espace de noms d’identité suivantes :

* Lors de la création de destinations en temps réel (streaming) via Destination SDK, vous devez non seulement [configurer un schéma de partenaire](schema-configuration.md) auquel les utilisateurs peuvent mapper des attributs de profil et des identités, mais aussi définir *au moins un* espace de noms d’identité pris en charge par votre plateforme de destination. Par exemple, si votre plateforme de destination accepte les e-mails et les [!DNL IDFA] hachés, vous devez définir ces deux identités comme [décrit plus bas dans ce document](#supported-parameters).

  >[!IMPORTANT]
  >
  >Lors de l’activation des audiences vers des destinations de diffusion en continu, les utilisateurs doivent également mapper _au moins une identité cible_, en plus des attributs de profil cible. Sinon, les audiences ne seront pas activées vers la plateforme de destination.

* Lors de la création de destinations basées sur des fichiers via Destination SDK, la configuration des espaces de noms d’identité est _facultative_.

Pour en savoir plus sur les espaces de noms d’identité dans Experience Platform, consultez la [documentation relative aux espaces de noms d’identité](../../../../identity-service/features/namespaces.md).

Pendant la configuration des espaces de noms d’identité pour la destination, vous pouvez affiner le mapping de ciblage d’identité pris en charge par la destination, par exemple :

* Permettre aux utilisateurs de mapper des attributs XDM aux espaces de noms d’identité.
* Autoriser les utilisateurs à mapper les [espaces de noms d’identité standard](../../../../identity-service/features/namespaces.md#standard) à vos propres espaces de noms d’identité.
* Autoriser les utilisateurs à mapper les [espaces de noms d’identité personnalisés](../../../../identity-service/features/namespaces.md#manage-namespaces) à vos propres espaces de noms d’identité.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [options de configuration](../configuration-options.md) ou consultez le guide sur la [utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer vos espaces de noms d’identité pris en charge via le point d’entrée `/authoring/destinations`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de configuration de noms d’identité prises en charge que vous pouvez utiliser pour la destination et montre ce que la clientèle verra dans l’interface utilisateur d’Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui (obligatoire) |
| Intégrations basées sur des fichiers (par lots) | Oui (facultatif) |

## Paramètres pris en charge {#supported-parameters}

Pendant la définition des identités cibles prises en charge par la destination, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer leur comportement.

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---------|----------|---|------|
| `acceptsAttributes` | Booléen | Facultatif | Indique si la clientèle peut mapper des attributs de profil standard à l’identité que vous configurez. |
| `acceptsCustomNamespaces` | Booléen | Facultatif | Indique si la clientèle peut mapper des espaces de noms d’identité personnalisés à l’espace de noms d’identité que vous configurez. |
| `acceptedGlobalNamespaces` | - | Facultatif | Indique quels [espaces de noms d’identité standard](../../../../identity-service/features/namespaces.md#standard) (par exemple, [!UICONTROL IDFA]) la clientèle peut mapper l’identité que vous configurez. |
| `transformation` | Chaîne | Facultatif | Affiche la case à cocher [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) dans l’interface utilisateur d’Experience Platform, lorsque le champ source est un attribut XDM ou un espace de noms d’identité personnalisée. Utilisez cette option pour permettre aux utilisateurs de hacher les attributs sources au moment de l’exportation. Pour activer cette option, définissez la valeur sur `sha256(lower($))`. |
| `requiredTransformation` | Chaîne | Facultatif | Lorsque la clientèle sélectionne cet espace de noms d’identité source, la case à cocher [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) est automatiquement appliquée au mappage et il n’est pas possible de la désactiver. Pour activer cette option, définissez la valeur sur `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Vous devez indiquer quelles identités [!DNL Experience Platform] les clients peuvent exporter vers votre destination. Voici quelques exemples : [!DNL Experience Cloud ID], e-mail haché, identifiant de l’appareil ([!DNL IDFA], [!DNL GAID]). Ces valeurs sont des espaces de noms d’identité [!DNL Experience Platform] que la clientèle peut mapper aux espaces de noms d’identité de la destination.

Une correspondance 1 à 1 entre [!DNL Experience Platform] et votre destination n’est pas obligatoire dans les espaces de noms d’identités. Par exemple, les clients peuvent mapper un espace de noms [!DNL Experience Platform] [!DNL IDFA] à un espace de noms [!DNL IDFA] de votre destination ou mapper le même espace de noms [!DNL Experience Platform] [!DNL IDFA] à un espace de noms [!DNL Customer ID] de votre destination.

Apprenez-en plus sur les identités dans la [présentation des espaces de noms d’identité](../../../../identity-service/features/namespaces.md).

## Considérations relatives au mappage

Si la clientèle sélectionne un espace de noms d’identité source, mais pas de mapping de ciblage, Experience Platform le renseigne automatiquement avec un attribut du même nom.

## Configuration du hachage facultatif des champs sources

Les clients Experience Platform peuvent choisir d’ingérer des données dans Experience Platform au format haché ou en texte brut. Si votre plateforme de destination accepte les données hachées et non hachées, vous pouvez permettre à la clientèle de choisir si Experience Platform doit hacher les valeurs des champs sources au moment de l’exportation vers la destination.

La configuration ci-dessous active l’option facultative [Apply transformation](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) dans l’interface utilisateur d’Experience Platform, à l’étape Mappage.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Cochez cette option lorsque vous utilisez des champs sources non hachés afin qu’Adobe Experience Platform les hache automatiquement au moment de l’activation.

Quand vous mappez des attributs source non hachés avec des attributs cibles qui sont censés être hachés (par exemple, `email_lc_sha256` ou `phone_sha256`), cochez l’option **Apply transformation** (Appliquer la transformation) pour qu’Adobe Experience Platform hache automatiquement les attributs source au moment de l’activation.

## Configuration du hachage obligatoire des champs sources

Si la destination accepte uniquement les données hachées, vous pouvez configurer les attributs exportés pour qu’ils soient automatiquement hachés par Experience Platform. La configuration ci-dessous vérifie automatiquement l’option **Apply transformation** (Appliquer la transformation) quand les identités `Email` et `Phone` sont mappées.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer vos espaces de noms d’identité pour les destinations créées avec Destination SDK.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
