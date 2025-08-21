---
title: Acxiom Real ID&trade; Audience Connection
description: Utilisez la destination  [!DNL Acxiom Real ID&trade; Audience Connection]  pour améliorer les audiences avec la technologie  [!DNL Acxiom's Real ID]  et activer les audiences sur plusieurs plateformes, telles que  [!DNL Altice],  [!DNL Ampersand],  [!DNL Comcast], etc.
badge: label="Beta" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: 1013487e2c38aeb1e2b0388f0c317afdcf02ba62
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 12%

---

# [!DNL Acxiom Real ID™ Audience Connection] destination

>[!NOTE]
>
>La destination [!DNL Acxiom Real ID™ Audience Connection] est en version bêta. Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Acxiom]. Pour toute demande ou information, contactez Acxiom directement [ici](mailto:acxiom-adobe-help@acxiom.com).

Utilisez la destination [!DNL Acxiom Real ID Audience Connection] pour améliorer les audiences avec [!DNL Acxiom's] technologie [Real ID™](https://www.acxiom.com/real-id/real-id/) et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

Ce tutoriel fournit des instructions pour créer un connecteur de destination [!DNL Acxiom Real ID Audience Connection] à l’aide de l’interface utilisateur [!DNL Adobe Experience Platform]. Ce connecteur est utilisé pour créer et distribuer des audiences vers des destinations sélectionnées.

## Cas d’utilisation {#use-cases}

Ce connecteur prend en charge les clients pour lesquels Acxiom Real Identity est chargé dans Real-Time CDP en tant qu’identifiant. Pour mieux comprendre quand et comment utiliser la destination [!DNL Acxiom Real ID Audience Connection], consultez l’exemple de cas d’utilisation ci-dessous que [!DNL Adobe Experience Platform] clients peuvent résoudre à l’aide de ce connecteur.

### Envoi d’audiences d’Experience Platform vers votre compte Acxiom {#send-audiences}

Utilisez ce connecteur de destination si vous êtes un professionnel du marketing qui souhaite envoyer des audiences de [!DNL Experience Platform] vers votre compte [!DNL Acxiom], pour une acquisition cross-canal.

Par exemple, le service des opérations marketing d’une marque mondiale de services financiers s’intéresse à l’acquisition de clients cross-canal par le biais de plusieurs plateformes publicitaires. Ils peuvent utiliser le connecteur de destination [!DNL Acxiom Real ID Audience Connection] pour envoyer des audiences de [!DNL Experience Platform] à [!DNL Acxiom], améliorer les audiences avec la technologie [!DNL Acxiom's Real ID] et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.


## Conditions préalables {#prerequisites}

* **Confirmer les conditions d’utilisation :** avant de pouvoir configurer une nouvelle destination [!DNL Acxiom Real ID Audience Connection], vous devez lire et signer [!DNL Acxiom's] contrat de conditions d’utilisation. Vous recevrez le lien vers le contrat une fois que votre commande client exécutée sera terminée. Tant que vous n’avez pas signé le contrat, la carte de destination [!DNL Acxiom Real ID Audience Connection] ne s’affichera pas dans le catalogue de destinations d’Experience Platform. Une fois que vous avez accepté et signé le contrat, [!DNL Adobe] terminez le processus d’intégration et la carte de destination [!DNL Acxiom Real ID Audience Connection] s’affiche.
* **Connaître votre ID d’organisation Adobe :** votre ID d’organisation [!DNL Adobe] est nécessaire pour remplir vos Conditions d’utilisation. Voir [!DNL Adobe's] rubrique *Organisations dans Experience Cloud* pour plus d’informations sur la manière d’[afficher votre ID d’organisation](https://experienceleague.adobe.com/fr/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Obtention d’une licence pour [!DNL Acxiom's Real ID] produit :** une fois une licence obtenue, rendez l’ID réel d’Acxiom disponible dans Real-Time CDP. Voir [Acxiom Data Enhancement](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement) pour plus d’informations.


## Identités prises en charge {#supported-identities}

[!DNL Acxiom's Real ID Audience Connection] destination prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/features/namespaces).

| Identité cible | Description | Considérations |
|---------------|----------------|----------------|
| ID réel | [!DNL Acxiom Real ID] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms Acxiom Real ID . |
| extern_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------------|----------------|----------------|
| Service de segmentation | ✓ | Audiences générées via Experience Platform [Segmentation Service](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/home). |
| Chargements personnalisés | ✓ | Audiences [importées](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/ui/audience-portal#import-audience) dans Experience Platform à partir de fichiers CSV. |


## Destinations prises en charge {#supported-destinations}

[!DNL Acxiom's Real ID Audience Connection] destination prend actuellement en charge l’activation des audiences sur les plateformes suivantes.

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Se connecter à la destination {#connect}

L’authentification vers [!DNL Acxiom's Real ID Audience Connection] destination est automatiquement gérée en arrière-plan pour votre commodité.

## Paramètres spécifiques à la destination {#destination-settings}

Certaines destinations [!DNL Acxiom Real ID Audience Connection] nécessitent des informations supplémentaires. Les sections ci-dessous fournissent des instructions détaillées sur la configuration de ces options.

### [!DNL LG Ads] {#lg-ads}

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

* **Catégorie de segments** : la catégorie cible ou la verticale dans laquelle votre segment se trouve. Exemple : services financiers, automobile, santé, etc.

![Détails de la destination LG Ads](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}



Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) pour obtenir des instructions sur l’activation des audience vers cette destination.

>[!NOTE]
>
>La destination [!DNL Acxiom Real ID Audience Connection] ne prend en charge que les exportations de fichiers complets.


### Mapper les attributs et les identités {#map}

Pour que la destination [!DNL Acxiom Real ID Audience Connection] reçoive correctement les données d’audience, vous devez mapper le champ source d’Experience Platform au champ cible [!DNL Acxiom Real ID Audience Connection] correct.

[!DNL Acxiom Real ID Audience Connection] autorise uniquement le mappage au champ cible suivant.

| Nom du champ | Description | Obligatoire |
|--------------------|------------|--------| 
| ID réel | Un ID réel est un identifiant alphanumérique (ID) unique de 36 octets provenant du graphique de résolution d’identité propriétaire d’Acxiom, semblable à une clé primaire d’une base de données relationnelle. Il s’agit d’un identifiant qui représente une personne, un foyer ou une adresse. | Oui |



Dans la colonne **[!UICONTROL Champ Source]**, saisissez le nom de l&#39;attribut source que vous souhaitez mapper au champ cible correspondant, ou sélectionnez l&#39;icône de flèche pour ouvrir l&#39;écran **[!UICONTROL Sélectionner le champ source]**. Sélectionnez ensuite **[!UICONTROL Suivant]**.
![Écran Mappage](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


Si vous n’utilisez pas [!DNL Adobe's] schéma standard, consultez la documentation du [guide de l’interface utilisateur de Query Service](../../../query-service/ui/overview.md) pour plus d’informations sur l’utilisation de Query Service pour renseigner le schéma standard [!DNL Adobe] avec vos noms de champ.


### Réviser {#review}

Une fois toutes les étapes ci-dessus effectuées, vous avez la possibilité de consulter le statut de la connexion de destination et les détails de l’audience avant de l’activer (la distribuer). Les audiences que vous avez sélectionnées s’affichent en bas d’une liste. Chaque audience sera un appel distinct à l’API [!DNL Acxiom Real ID Audience Connection].

Si les résultats vous conviennent, sélectionnez **[!UICONTROL Terminer]** pour activer la destination.

![Vérifier votre audience](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Résolution des problèmes {#troubleshooting}

Si votre représentant de destination ne parvient pas à localiser votre audience, contactez votre représentant de [!DNL Adobe] pour obtenir de l’aide.

Vous devrez fournir les informations suivantes à votre représentant [!DNL Adobe] :

* Nom de l’audience
* Nom de la destination
* Date d’activation de l’audience
* Nom du fichier exporté

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez activé une audience sur la plateforme de destination sélectionnée. Ensuite, contactez le représentant de votre plateforme de destination pour commencer à configurer votre campagne.
