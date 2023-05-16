---
description: Découvrez comment configurer votre destination pour les configurations de mappage d’identité et d’attributs prises en charge.
title: Configurations de mappage prises en charge
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 5%

---


# Configurations de mappage prises en charge

Les destinations créées avec Destination SDK prennent en charge les configurations spécifiques d’espace de noms d’identité et de mappage d’attributs, en fonction du type de destination.

Cet article décrit toutes les configurations de mappage prises en charge que vous pouvez utiliser lors de la configuration de votre destination.

>[!WARNING]
>
>Toute configuration de mappage qui n’est pas décrite dans cet article n’est pas prise en charge par Destination SDK.

Lors de la création de votre destination, configurez vos espaces de noms de schéma et d’identité en fonction de l’une des configurations de mappage décrites dans cette page.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Mappages pris en charge pour les destinations de diffusion en continu {#streaming-mappings}

Les destinations en temps réel (diffusion en continu) créées avec Destination SDK prennent en charge les configurations de mappage décrites dans le tableau ci-dessous.

| Champ source | Champ cible |
| --- | --- |
| Attribut XDM | Attribut personnalisé |
| Espace de noms d’identité | Espace de noms d’identité |

L’exemple de configuration ci-dessous permet aux clients d’utiliser les deux mappages dans le tableau ci-dessus.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Mappage des attributs XDM aux attributs personnalisés {#streaming-xdm-to-custom}

Les utilisateurs peuvent mapper des attributs de leur profil XDM source aux attributs personnalisés du côté de votre destination.

Les utilisateurs doivent saisir manuellement le nom de l’attribut personnalisé cible lors de la sélection du mapping de champ cible.

![Capture d’écran de l’interface utilisateur de Platform montrant la sélection d’attributs personnalisés.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur de Platform montrant le mappage des attributs XDM aux attributs personnalisés pour les destinations de diffusion en continu.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Mappage des espaces de noms d’identité aux espaces de noms d’identité des partenaires {#streaming-identity-to-identity}

Les utilisateurs peuvent mapper des espaces de noms d’identité personnalisés ou globaux de Platform aux espaces de noms d’identité que vous avez définis.

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur de Platform montrant le mappage d’identité pour les destinations de diffusion en continu.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Mappages pris en charge pour les destinations basées sur des fichiers {#batch-mappings}

Les destinations basées sur des fichiers créées avec Destination SDK prennent en charge les configurations de mappage décrites dans le tableau ci-dessous. Consultez les sections suivantes pour obtenir des exemples de mappage détaillés.

| Champ source | Champ cible |
| --- | --- |
| Attribut XDM | Attribut/attribut personnalisé |
| Espace de noms d’identité | Attribut/attribut personnalisé |
| Espace de noms d’identité | Espace de noms d’identité |

L’exemple de configuration ci-dessous permet aux clients d’utiliser tous les mappages du tableau ci-dessus.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Mappage des attributs XDM aux attributs personnalisés {#batch-xdm-to-custom}

Les utilisateurs peuvent mapper des attributs de leur profil XDM source aux attributs personnalisés du côté de votre destination.

Pour les destinations basées sur des fichiers, le champ cible est automatiquement renseigné avec un attribut par défaut du même nom que le champ source.

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur de Platform montrant le mappage XDM aux attributs personnalisés pour les destinations basées sur des fichiers.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Les utilisateurs peuvent laisser le nom par défaut en place ou saisir un nom d’attribut personnalisé dans l’écran de sélection des champs cibles.

![Capture d’écran de l’interface utilisateur de Platform montrant la sélection d’attributs cibles personnalisés pour les destinations basées sur des fichiers.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Mappage des espaces de noms d’identité aux attributs personnalisés {#batch-identity-to-custom}

Les utilisateurs peuvent mapper des espaces de noms d’identité personnalisés ou globaux de Platform aux attributs personnalisés du côté de votre destination.

Lors de la sélection d’un espace de noms d’identité comme champ source, le champ cible est automatiquement renseigné avec un espace de noms d’identité équivalent. Pour remplacer le champ cible par un attribut personnalisé, les utilisateurs doivent saisir un nom d’attribut personnalisé dans l’écran de sélection du champ cible.

![Capture d’écran de l’interface utilisateur de Platform montrant la sélection d’attributs cibles personnalisés pour les destinations basées sur des fichiers.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur de Platform montrant le mappage d’identité avec les attributs personnalisés pour les destinations basées sur des fichiers.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Mappage des espaces de noms d’identité aux espaces de noms d’identité des partenaires {#batch-identity-to-identity}

Les utilisateurs peuvent mapper des espaces de noms d’identité personnalisés ou globaux de Platform à des espaces de noms d’identité équivalents.

Lors de la sélection d’un espace de noms d’identité comme champ source, le champ cible est automatiquement renseigné avec un espace de noms d’identité équivalent.

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur de Platform montrant le mappage d’identité pour les destinations basées sur des fichiers.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre les mappages pris en charge par les destinations créées avec Destination SDK.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)