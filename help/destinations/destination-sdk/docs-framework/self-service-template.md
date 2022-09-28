---
title: Modèle de libre-service de documentation // Remplacer par le nom de votre destination
description: Utilisez ce modèle pour créer une documentation publique pour votre destination dans le catalogue Adobe Experience Platform. // Remplacer par le paragraphe dans la section Aperçu
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 46e8f6cf3e135b31dc508274598f9d76df857c8f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 7%

---

# Connexion à YourDestination {#your-destination}

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Veuillez ignorer toutes les instances d&#39;UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

>[!IMPORTANT]
>
>* Renseignez toutes les sections de ce modèle, dans l&#39;ordre dans lequel elles sont décrites dans le modèle.
>* Ce modèle est rarement mis à jour, en fonction des commentaires des partenaires. Avant de commencer à créer de la documentation pour votre destination, assurez-vous d’avoir téléchargé la [dernière version du modèle](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## Présentation {#overview}

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Pour plus d’informations, insérez un lien vers la page d’accueil de la documentation du produit.*

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la fonction *YourDestination* l&#39;équipe. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse *Ajouter un lien ou une adresse électronique où vous pouvez accéder pour obtenir des mises à jour, par exemple `support@YourDestination.com`.*

## Cas d&#39;utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable *YourDestination* destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1 {#use-case-1}

*Pour les plateformes de messagerie mobile :*

*Une plate-forme de location et de vente d’habitations souhaite envoyer des notifications mobiles aux appareils Android et iOS des clients afin de leur faire savoir qu’il y a 100 listes mises à jour dans la zone où ils ont déjà recherché une location.*

### Cas d’utilisation #2 {#use-case-2}

*Pour les plateformes de réseaux sociaux :*

*Une marque de vêtements d’athlétisme veut atteindre ses clients existants par le biais de leurs comptes de médias sociaux. La marque de vêtements peut ingérer des adresses électroniques de son propre service de gestion de la relation client vers Adobe Experience Platform, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à votre destination afin d’afficher des publicités dans les flux de médias sociaux de ses clients.*

## Conditions préalables {#prerequisites}

*Ajoutez des informations dans cette section sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la destination dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir :*

* *à ajouter à une liste autorisée*
* *conditions requises pour le hachage des emails*
* *toute spécification de compte de votre côté ;*
* *Comment obtenir une clé API pour se connecter à votre plateforme*

*Vous pouvez créer un lien vers votre documentation appropriée si cela s’avère utile aux clients.*

## Identités prises en charge {#supported-identities}

*Ajoutez des informations dans cette section sur les identités prises en charge par votre destination. Nous avons prérempli le tableau avec certaines valeurs standard. Supprimez les valeurs qui ne s’appliquent pas à votre destination et celles qui ne sont pas préremplies.*

*YourDestination* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Google Advertising ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lisez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

*Dans le tableau, conservez uniquement les lignes correspondant à votre destination. Vous devez avoir une ligne pour le type Export et une ligne pour la Fréquence d&#39;export. Supprimez les valeurs qui ne s’appliquent pas à votre destination.*

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la variable *YourDestination* destination. |
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |
| Fréquence des exports | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à la destination {#authenticate}

*Ajoutez les champs que les clients doivent renseigner lors de l’authentification à votre destination. Ces champs sont spécifiques à la destination et dépendent de votre configuration dans Destination SDK. Les champs de votre destination peuvent ne pas être identiques à ceux répertoriés ci-dessous. Veuillez également inclure une capture d’écran similaire à l’exemple de capture d’écran ci-dessous.*

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Exemple de capture d’écran montrant comment s’authentifier à la destination](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Jeton de porteur]**: Renseignez le jeton porteur pour vous authentifier à la destination.

### Renseignement des détails de destination {#destination-details}

*Ajoutez les champs que les clients doivent renseigner lors de la configuration d’une nouvelle destination. Ces champs sont spécifiques à la destination et dépendent de votre configuration dans Destination SDK. Les champs de votre destination peuvent ne pas être identiques à ceux répertoriés ci-dessous. Veuillez également inclure une capture d’écran similaire à l’exemple de capture d’écran ci-dessous.*

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Exemple de capture d’écran montrant comment remplir les détails de votre destination](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre *YourDestination* ID de compte.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

*Supprimer le cas échéant : si vous documentez une nouvelle destination de diffusion en continu, conservez le premier paragraphe ci-dessous. Si vous documentez une nouvelle destination basée sur des fichiers, conservez le deuxième paragraphe.*

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mise en correspondance des attributs et des identités {#map}

*Ajoutez des informations sur les mappages pris en charge entre les champs source et cible dans l’étape Mappage du workflow d’activation. Votre destination peut prendre en charge l’exportation d’attributs de profil, d’espaces de noms d’identité ou des deux. Certains champs peuvent être obligatoires. Les attributs Target peuvent être prédéfinis ou personnalisés. Appelez les avertissements importants et utilisez des exemples, de préférence avec des captures d’écran. Voici deux exemples de pages de destination que vous pouvez utiliser comme référence :*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Données exportées / Validation de l’exportation des données {#exported-data}

*Ajoutez un paragraphe sur la manière dont les données sont exportées vers votre destination. Cela permet au client de s’assurer qu’il s’est correctement intégré à votre destination. Par exemple, vous pouvez fournir un exemple JSON comme celui ci-dessous. Vous pouvez également fournir des captures d’écran et des informations provenant de l’interface de votre destination qui indiquent comment les clients doivent s’attendre à ce que les segments soient renseignés dans la plateforme de destination.*

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
        "status": "existing"
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

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

*Vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre ressource que vous considérez importante pour le succès du client.*