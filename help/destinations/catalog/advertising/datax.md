---
title: Connexion à MediaYahoo DataX Verizon
description: DataX est une infrastructure Verizon Media/Yahoo agrégée qui héberge divers composants qui permettent à Verizon Media/Yahoo d’échanger des données avec ses partenaires externes de manière sécurisée, automatisée et évolutive.
source-git-commit: 09bae0d24eead5f0b6533ba5b89e1fc87c8c71b5
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 6%

---


# Connexion à Verizon Media/Yahoo DataX

## Présentation {#overview}

DataX est une infrastructure Verizon Media/Yahoo agrégée qui héberge divers composants qui permettent à Verizon Media/Yahoo d’échanger des données avec ses partenaires externes de manière sécurisée, automatisée et évolutive.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par l’équipe DataX de Verizon Media/Yahoo. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l’adresse [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Conditions préalables {#prerequisites}

**ID MDM**

Il s’agit d’un identifiant unique dans Yahoo DataX. Il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre gestionnaire de compte Yahoo Data X.

**Limite de taux**

DataX est limité par le taux selon les limites de quota pour la taxonomie et les publications d’audience décrites dans la [documentation DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Code d’erreur | Message d’erreur | Description |
|---------|----------|---------|
| 429 Too many requests | Limite de débit dépassée par heure **(Limite : 100)** | Nombre de demandes autorisées par heure par fournisseur. |

{style=&quot;table-layout:auto&quot;}

**Métadonnées de taxonomie**

La ressource Taxonomie définit une extension sur la structure de métadonnées DataX de base

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Pour en savoir plus sur les [métadonnées de taxonomie](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/), consultez la documentation destinée aux développeurs de DataX.

## Identités prises en charge {#supported-identities}

Verizon Media prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. |
| GAID | Identifiant Google Advertising | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |

{style=&quot;table-layout:auto&quot;}

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants (e-mail) utilisés dans la destination Verizon Media.

## Cas d’utilisation {#use-cases}

Les API DataX sont disponibles pour les annonceurs qui souhaitent cibler un groupe d’audience spécifique en dehors des adresses électroniques dans Verizon Media (VMG). Elles peuvent rapidement créer un nouveau segment et pousser le groupe d’audience souhaité à l’aide de l’API en temps quasi réel de VMG.

## Se connecter à la destination {#connect}

![Carte de destination Yahoo DataX dans l’interface utilisateur de Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** MDM : Il s’agit d’un identifiant unique dans Yahoo DataX. Il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre gestionnaire de compte Yahoo Data X.  Avec les identifiants MDM, les données ne peuvent être limitées pour une utilisation qu’avec un certain ensemble d’utilisateurs exclusifs (tels que les données propriétaires pour les annonceurs).

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers une destination](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers des destinations.

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, consultez la documentation de Yahoo/Verizon Media [sur DataX](https://developer.verizonmedia.com/datax/guide/).