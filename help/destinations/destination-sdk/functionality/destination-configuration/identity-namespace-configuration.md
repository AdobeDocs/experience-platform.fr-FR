---
description: Découvrez comment configurer les identités de cible prises en charge pour les destinations créées avec Destination SDK.
title: Configuration de l’espace de noms d’identité
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 14%

---


# Configuration de l’espace de noms d’identité

Experience Platform utilise des espaces de noms d’identité pour décrire le type d’identités spécifiques. Par exemple, un espace de noms d’identité appelé `Email` identifie une valeur comme `name@email.com` comme adresse électronique.

Lors de la création d’une destination par Destination SDK, en plus de [configuration d&#39;un schéma de partenaire](schema-configuration.md) pour que les utilisateurs puissent mapper des attributs de profil et des identités à, vous pouvez également définir des espaces de noms d’identité pris en charge par votre plateforme de destination.

Dans ce cas, les utilisateurs ont le choix ajouté de sélectionner des identités cibles, en plus des attributs de profil cible.

Pour en savoir plus sur les espaces de noms d’identité dans Experience Platform, voir [documentation sur les espaces de noms d’identité](../../../../identity-service/namespaces.md).

Lors de la configuration des espaces de noms d’identité pour votre destination, vous pouvez affiner le mapping d’identité cible pris en charge par votre destination, par exemple :

* Permet aux utilisateurs de mapper des attributs XDM aux espaces de noms d’identité.
* Autoriser les utilisateurs à mapper [espaces de noms d’identité standard](../../../../identity-service/namespaces.md#standard) à vos propres espaces de noms d’identité.
* Autoriser les utilisateurs à mapper [espaces de noms d’identité personnalisés](../../../../identity-service/namespaces.md#manage-namespaces) à vos propres espaces de noms d’identité.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination basée sur des fichiers ;](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer vos espaces de noms d’identité pris en charge via le `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de configuration des espaces de noms d’identité prises en charge que vous pouvez utiliser pour votre destination et indique ce que les clients verront dans l’interface utilisateur de Platform.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

Lors de la définition des identités cibles prises en charge par votre destination, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer leur comportement.

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---------|----------|---|------|
| `acceptsAttributes` | Booléen | Facultatif | Indique si les clients peuvent mapper des attributs de profil standard à l’identité que vous configurez. |
| `acceptsCustomNamespaces` | Booléen | Facultatif | Indique si les clients peuvent mapper des espaces de noms d’identité personnalisés à l’espace de noms d’identité que vous configurez. |
| `acceptedGlobalNamespaces` | - | Facultatif | Indique : [espaces de noms d’identité standard](../../../../identity-service/namespaces.md#standard) (par exemple, [!UICONTROL IDFA]) les clients peuvent mapper à l’identité que vous configurez. |
| `transformation` | Chaîne | Facultatif | Affiche la variable [[!UICONTROL Appliquer la transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) dans l’interface utilisateur de Platform, lorsque le champ source est un attribut XDM ou un espace de noms d’identité personnalisé. Utilisez cette option pour permettre aux utilisateurs de hacher les attributs source lors de l’exportation. Pour activer cette option, définissez la valeur sur `sha256(lower($))`. |
| `requiredTransformation` | Chaîne | Facultatif | Lorsque les clients sélectionnent cet espace de noms d’identité source, la variable [[!UICONTROL Appliquer la transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) est automatiquement appliquée au mappage et les clients ne peuvent pas le désactiver. Pour activer cette option, définissez la valeur sur `sha256(lower($))`. |

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

Vous devez indiquer quelles identités [!DNL Platform] les clients peuvent exporter vers votre destination. Voici quelques exemples : [!DNL Experience Cloud ID], e-mail haché, identifiant de l’appareil ([!DNL IDFA], [!DNL GAID]). Ces valeurs sont les suivantes : espaces de noms d’identité [!DNL Platform] que les clients peuvent mapper aux espaces de noms d’identité de votre destination.

Les espaces de noms d’identité ne nécessitent pas de correspondance 1-1 entre [!DNL Platform] et votre destination.
Par exemple, les clients peuvent mapper un espace de nom [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL IDFA] depuis votre destination ou mapper le même espace de noms [!DNL Platform] [!DNL IDFA] à un espace de noms [!DNL Customer ID] dans votre destination.

En savoir plus sur les identités dans [présentation de l’espace de noms d’identité](../../../../identity-service/namespaces.md).

## Considérations relatives au mappage

Si les clients sélectionnent un espace de noms d’identité source et ne sélectionnent pas de mapping de ciblage, Platform renseigne automatiquement le mapping de ciblage avec un attribut du même nom.

## Configuration du hachage facultatif des champs source

Les clients Experience Platform peuvent choisir d’ingérer des données dans Platform au format haché ou en texte brut. Si votre plateforme de destination accepte les données hachées et non hachées, vous pouvez donner aux clients la possibilité de choisir si Platform doit hacher les valeurs des champs source lorsqu’elles sont exportées vers votre destination.

La configuration ci-dessous active le paramètre facultatif [Appliquer la transformation](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) dans l’interface utilisateur de Platform, à l’étape Mappage .

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

Cochez cette option lorsque vous utilisez des champs sources non hachés afin qu&#39;Adobe Experience Platform les hache automatiquement lors de l&#39;activation.

Lorsque vous mappez des attributs source non hachés avec des attributs cibles que la destination s’attend à être hachée (par exemple : `email_lc_sha256` ou `phone_sha256`), cochez la variable **Appliquer la transformation** pour que Adobe Experience Platform hache automatiquement les attributs source lors de l’activation.

## Configuration du hachage obligatoire des champs source

Si votre destination accepte uniquement les données hachées, vous pouvez configurer les attributs exportés pour qu’ils soient automatiquement hachés par Platform. La configuration ci-dessous vérifie automatiquement la variable **Appliquer la transformation** lorsque la variable `Email` et `Phone` les identités sont mappées.

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

Après avoir lu cet article, vous devriez mieux comprendre comment configurer les espaces de noms d’identité pour les destinations créées avec Destination SDK.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
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
