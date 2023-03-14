---
title: Connexion à MediaYahoo DataX Verizon
description: DataX, une infrastructure globale appartenant à Verizon Media/Yahoo, permet dʼhéberger différents composants et dʼéchanger des données avec les partenaires externes de Verizon Media/Yahoo, de manière sécurisée, automatisée et évolutive.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 46%

---

# Connexion [!DNL Verizon Media/Yahoo DataX]

## Présentation {#overview}

[!DNL DataX] est un agrégat [!DNL Verizon Media/Yahoo] infrastructure qui héberge divers composants permettant d’activer [!DNL Verizon Media/Yahoo] d’échanger des données avec ses partenaires externes de manière sécurisée, automatisée et évolutive.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par [!DNL Verizon Media/Yahoo]&#39;s [!DNL DataX] l&#39;équipe. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Conditions préalables {#prerequisites}

**ID MDM**

Il s’agit d’un identifiant unique dans [!DNL Yahoo DataX] et il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre [!DNL Yahoo DataX] gestionnaire de compte.

**Métadonnées de taxonomie**

La ressource Taxonomie définit une extension sur la base [!DNL DataX] Structure des métadonnées

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

En savoir plus sur [Métadonnées de taxonomie](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) dans le [!DNL DataX] documentation destinée aux développeurs.

## Limites de taux et barrières de sécurité {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Lors de l’activation de plus de 100 segments vers [!DNL Verizon Media/Yahoo DataX], vous pouvez recevoir des erreurs de limitation de débit de la destination. Lors de l’activation de segments vers cette destination, essayez d’activer moins de 100 segments dans un seul flux de données d’activation. Si vous devez activer davantage de segments, créez une destination sur le même compte.

[!DNL DataX] est limitée au taux selon les limites de quota pour la taxonomie et les publications d’audience décrites dans la section [Documentation DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Code d’erreur | Message d’erreur | Description |
|---------|----------|---------|
| 429 Too many requests | Limite de taux dépassée par heure **(Limite : 100)** | Nombre de demandes autorisées par heure par fournisseur. |

{style="table-layout:auto"}

## Identités prises en charge {#supported-identities}

[!DNL Verizon Media] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| GAID | Google Advertising ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (email, GAID, IDFA) utilisés dans la destination Verizon Media. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

[!DNL DataX] Les API sont disponibles pour les annonceurs qui souhaitent cibler un groupe d’audience spécifique en dehors des adresses électroniques dans [!DNL Verizon Media] (VMG) peut rapidement créer un nouveau segment et pousser le groupe d’audiences souhaité à l’aide de l’API en temps quasi réel de VMG.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

![Carte de destination Yahoo DataX dans l’interface utilisateur de Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID MDM]**: Il s’agit d’un identifiant unique dans [!DNL Yahoo DataX] et il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre [!DNL Yahoo DataX] gestionnaire de compte.  Avec les identifiants MDM, les données ne peuvent être limitées pour une utilisation qu’avec un certain ensemble d’utilisateurs exclusifs (tels que les données propriétaires pour les annonceurs).

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation de profils et de segments vers une destination](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers les destinations.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, reportez-vous à la section [!DNL Yahoo/Verizon Media] [documentation sur [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
