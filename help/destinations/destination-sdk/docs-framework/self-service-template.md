---
title: Modèle de libre-service de documentation // Remplacer par le nom de votre destination
description: Utilisez ce modèle pour créer une documentation publique pour votre destination dans le catalogue Adobe Experience Platform. // Remplacer par le paragraphe dans la section Aperçu
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 10521602a5871419c0c49d54c8ed250af39a78a4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 33%

---

# Connexion à YourDestination {#your-destination}

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances d’UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

>[!IMPORTANT]
>
>* Renseignez toutes les sections de ce modèle, dans l&#39;ordre dans lequel elles sont décrites dans le modèle.
>* Ce modèle est rarement mis à jour, en fonction des commentaires des partenaires. Avant de commencer à créer de la documentation pour la destination, veillez à avoir téléchargé la [dernière version du modèle](../assets/docs-framework/yourdestination-template.zip).

## Vue d’ensemble {#overview}

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Insérez un lien vers la page d’accueil de la documentation du produit pour une lecture plus approfondie.*

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *YourDestination*. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l&#39;adresse *Insérer un lien ou une adresse électronique où vous pouvez être contacté pour des mises à jour, par exemple `support@YourDestination.com`.*

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination *YourDestination*, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1 {#use-case-1}

*Pour les plateformes de messagerie mobile :*

*Une plateforme de location et de vente d&#39;une maison souhaite envoyer des notifications mobiles aux appareils Android et iOS des clients pour leur faire savoir qu&#39;il y a 100 listes mises à jour dans la zone où ils ont recherché une location auparavant.*

### Cas d’utilisation #2 {#use-case-2}

*Pour les plateformes de réseaux sociaux :*

*Une marque de vêtements de sport souhaite atteindre ses clients existants par le biais de ses comptes de médias sociaux. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers Adobe Experience Platform, créer des audiences à partir de ses propres données hors ligne et envoyer ces audiences à VotreDestination, afin d’afficher des publicités dans les flux de médias sociaux de ses clients.*

## Conditions préalables {#prerequisites}

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la destination dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir de :*

* *à ajouter à une liste autorisée*
* *Conditions requises pour le hachage des emails*
* *toutes les caractéristiques de compte de votre côté*
* *Comment obtenir une clé API pour se connecter à votre plateforme*

*Vous pouvez créer un lien vers votre documentation appropriée si cela peut être utile aux clients.*

## Identités prises en charge {#supported-identities}

*Ajoutez des informations dans cette section sur les identités prises en charge par votre destination. Nous avons prérempli le tableau avec certaines valeurs standard. Supprimez les valeurs qui ne s&#39;appliquent pas à votre destination et/ou ajoutez des valeurs qui ne sont pas préremplies.*

*YourDestination* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Lisez le document suivant sur [ECID](/help/identity-service/features/ecid.md) pour plus d’informations. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

*Ajoutez des informations dans cette section sur les audiences prises en charge par votre destination. Nous avons prérempli le tableau avec certaines valeurs standard. Utilisez les caractères `✓` et `X` pour indiquer si votre type d’audience est pris en charge par cette destination.*

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

*Dans le tableau, conservez uniquement les lignes correspondant à votre destination. Vous devez avoir une ligne pour le type Export et une ligne pour la Fréquence d&#39;export. Supprimez les valeurs qui ne s&#39;appliquent pas à votre destination.*

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *YourDestination*. |
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’une audience, ainsi que les champs de schéma souhaités (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Type d’exportation | **[!UICONTROL Exportation de jeux de données]** | Vous exportez des jeux de données bruts qui ne sont pas groupés ou structurés selon les intérêts ou les qualifications de l’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

*Ajoutez les champs que les clients doivent renseigner lors de l’authentification à votre destination. Ces champs sont spécifiques à la destination et dépendent de votre configuration dans Destination SDK. Les champs de votre destination peuvent ne pas être identiques à ceux répertoriés ci-dessous. Veuillez également inclure une capture d’écran similaire à l’exemple de capture d’écran illustré ci-dessous.*

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Exemple de capture d’écran montrant comment s’authentifier à la destination](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Jeton porteur]** : renseignez le jeton porteur pour vous authentifier sur la destination.

### Renseigner les détails de la destination {#destination-details}

*Ajoutez les champs que les clients doivent renseigner lors de la configuration d’une nouvelle destination. Ces champs sont spécifiques à la destination et dépendent de votre configuration dans Destination SDK. Les champs de votre destination peuvent ne pas être identiques à ceux répertoriés ci-dessous. Veuillez également inclure une capture d’écran similaire à l’exemple de capture d’écran illustré ci-dessous.*

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Exemple de capture d&#39;écran montrant comment remplir les détails pour votre destination](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID de compte]** : votre ID de compte *YourDestination*.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

*Supprimer selon le cas : si vous documentez une nouvelle destination de diffusion en continu, conservez le premier paragraphe ci-dessous. Si vous documentez une nouvelle destination basée sur des fichiers, conservez le deuxième paragraphe. Si vous documentez une destination qui exporte des jeux de données, conservez le troisième paragraphe.*

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

Lisez [(Beta) Export des jeux de données](/help/destinations/ui/export-datasets.md) pour obtenir des instructions détaillées sur l’exportation de jeux de données vers cette destination.

### Mapper les attributs et les identités {#map}

*Ajoutez des informations sur les mappages pris en charge entre les champs source et cible dans l’étape Mapping du workflow d’activation. Votre destination peut prendre en charge l’exportation d’attributs de profil, d’espaces de noms d’identité ou des deux. Certains champs peuvent être obligatoires. Les attributs Target peuvent être prédéfinis ou personnalisés. Appelez les avertissements importants et utilisez des exemples, de préférence avec des captures d’écran. Voici deux exemples de pages de destination que vous pouvez utiliser comme référence :*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Données exportées / Valider l’exportation des données {#exported-data}

*Ajoutez un paragraphe sur la manière dont les données sont exportées vers votre destination. Cela permet au client de s’assurer qu’il s’est correctement intégré à votre destination. Par exemple, vous pouvez fournir un exemple JSON comme celui ci-dessous. Vous pouvez également fournir des captures d’écran et des informations provenant de l’interface de votre destination qui montrent comment les clients doivent s’attendre à ce que les audiences soient renseignées dans la plateforme de destination.*

```
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
        "status": "realized"
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

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre ressource que vous considérez importante pour le succès du client.*
