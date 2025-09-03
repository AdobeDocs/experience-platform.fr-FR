---
title: Connexion à l’audience Acxiom
description: Utilisez la destination  [!DNL Acxiom Audience Connection]  pour améliorer les audiences avec la technologie  [!DNL Acxiom's Real ID]  et activer les audiences sur plusieurs plateformes, telles que  [!DNL Altice],  [!DNL Ampersand],  [!DNL Comcast], etc.
badge: label="Beta" type="Informative"
exl-id: bac0f337-bfab-4779-acc8-f70239552666
source-git-commit: 70a1cdcfd99ae006f02289ab5a20ced624b51ccc
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 14%

---

# Destination [!DNL Acxiom Audience Connection]

>[!NOTE]
>
>La destination [!DNL Acxiom Audience Connection] est en version bêta. Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Acxiom]. Pour toute demande ou information, contactez Acxiom directement [ici](mailto:acxiom-adobe-help@acxiom.com).

Utilisez la destination [!DNL Acxiom Audience Connection] pour améliorer les audiences avec [!DNL Acxiom's] technologie [Real ID™](https://www.acxiom.com/real-id/real-id/) et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

Ce tutoriel fournit des instructions pour créer un connecteur de destination [!DNL Acxiom Audience Connection] à l’aide de l’interface utilisateur [!DNL Adobe Experience Platform]. Ce connecteur est utilisé pour créer et distribuer des audiences vers des destinations sélectionnées.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Acxiom Audience Connection], consultez l’exemple de cas d’utilisation ci-dessous que [!DNL Adobe Experience Platform] clients peuvent résoudre à l’aide de ce connecteur.

### Envoi d’audiences d’Experience Platform vers votre compte Acxiom {#send-audiences}

Utilisez ce connecteur de destination si vous êtes un professionnel du marketing qui souhaite envoyer des audiences de [!DNL Experience Platform] vers votre compte [!DNL Acxiom], pour une acquisition cross-canal.

Par exemple, le service des opérations marketing d’une marque mondiale de services financiers s’intéresse à l’acquisition de clients cross-canal par le biais de plusieurs plateformes publicitaires. Ils peuvent utiliser le connecteur de destination [!DNL Acxiom Audience Connection] pour envoyer des audiences de [!DNL Experience Platform] à [!DNL Acxiom], améliorer les audiences avec la technologie [!DNL Acxiom's Real ID] et activer les audiences vers plusieurs plateformes, telles que [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], etc.

## Conditions préalables {#prerequisites}

* **Confirmer les conditions d’utilisation :** avant de pouvoir configurer une nouvelle destination [!DNL Acxiom Audience Connection], vous devez lire et signer [!DNL Acxiom's] contrat de conditions d’utilisation. Vous recevrez le lien vers le contrat une fois que votre commande client exécutée sera terminée. Tant que vous n’avez pas signé le contrat, la carte de destination [!DNL Acxiom Audience Connection] ne s’affichera pas dans le catalogue de destinations d’Experience Platform. Une fois que vous avez accepté et signé le contrat, [!DNL Adobe] terminez le processus d’intégration et la carte de destination [!DNL Acxiom Audience Connection] s’affiche.
* **Connaître votre ID d’organisation Adobe :** votre ID d’organisation [!DNL Adobe] est nécessaire pour remplir vos Conditions d’utilisation. Voir [!DNL Adobe's] rubrique *Organisations dans Experience Cloud* pour plus d’informations sur la manière d’[afficher votre ID d’organisation](https://experienceleague.adobe.com/fr/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).

## Destinations prises en charge {#supported-destinations}

La destination [!DNL Acxiom Audience Connection] prend actuellement en charge l’activation des audiences sur les plateformes suivantes <br>

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Se connecter à la destination {#connect}

L’authentification vers [!DNL Acxiom's Audience Connection] destination est automatiquement gérée en arrière-plan pour votre commodité.

## Paramètres spécifiques à la destination {#destination-settings}

Certaines destinations [!DNL Acxiom Audience Connection] nécessitent des informations supplémentaires. Les sections ci-dessous fournissent des instructions détaillées sur la configuration de ces options.

### [!DNL LG Ads] {#lg-ads}

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

* **Catégorie de segments** : la catégorie cible ou la verticale dans laquelle votre segment se trouve. Exemple : services financiers, automobile, santé, etc.

![Détails de la destination LG Ads](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png)

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

>[!NOTE]
>
>La destination [!DNL Acxiom Audience Connection] ne prend en charge que les exportations de fichiers complets.

### Mapper les attributs et les identités {#map}

Pour que la destination [!DNL Acxiom Audience Connection] reçoive correctement les données d’audience, vous devez mapper les champs sources d’Experience Platform aux champs cibles [!DNL Acxiom Audience Connection] corrects.

[!DNL Acxiom Audience Connection] permet uniquement de mapper les champs cibles suivants. Les champs cibles décrits dans le tableau ci-dessous doivent être mappés dans l’ordre indiqué ci-dessous.

| Nom du champ | Description | Obligatoire | Ordre des champs | Longueur max. |
|---|---|---|---|---|          
| Prénom | Prénom de l&#39;individu | Non | 1 | 255 |
| Milieu | Deuxième prénom ou initiale de l’individu | Non | 2 | 50 |
| Nom | Nom de famille de la personne | Oui | 3 | 255 |
| Suffixe générationnel | Suffixe de l’individu | Non | 4 | 10 |
| Ligne d&#39;adresse 1 | Champ Adresse 1 de la résidence principale | Oui | 5 | 255 |
| Ligne d&#39;adresse 2 | Champ adresse 2 de la résidence principale | Non | 6 | 255 |
| Ville | Ville de résidence principale | Oui | 7 | 255 |
| État | Abréviation nationale de la résidence principale | Oui | 8 | 2 |
| Code postal | Code postal complet de la résidence principale | Oui | 9 | 10 |
| E-mail | E-mail de Principal Par défaut, ce champ est utilisé comme clé de déduplication pour rendre les enregistrements uniques | Non | 10 | 255 |
| Téléphone | Numéro de téléphone de l’individu (indicatif + numéro)<br> Par défaut, ce champ est utilisé comme clé de déduplication pour rendre les enregistrements uniques. | Non | 11 | 10 |

Dans la colonne **[!UICONTROL Champ Source]**, saisissez le nom de chacun des attributs sources que vous souhaitez mapper au champ cible correspondant, ou sélectionnez l&#39;icône de flèche pour ouvrir l&#39;écran **[!UICONTROL Sélectionner le champ source]**.<br>
![Écran Mappage](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png)

Après avoir mappé tous les champs, sélectionnez **[!UICONTROL Suivant]**.

Si vous n’utilisez pas [!DNL Adobe's] schéma standard, consultez la documentation du [guide de l’interface utilisateur de Query Service](../../../query-service/ui/overview.md) pour plus d’informations sur l’utilisation de Query Service pour renseigner le schéma standard [!DNL Adobe] avec vos noms de champ.

### Réviser {#review}

Une fois toutes les étapes ci-dessus effectuées, vous avez la possibilité de consulter le statut de la connexion de destination et les détails de l’audience avant de l’activer (la distribuer). Les audiences que vous avez sélectionnées s’affichent en bas d’une liste. Chaque audience sera un appel distinct à l’API [!DNL Acxiom Audience Connection].

Si les résultats vous conviennent, sélectionnez **[!UICONTROL Terminer]** pour activer la destination.

![Vérifier votre audience](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png)

## Résolution des problèmes {#troubleshooting}

Si votre représentant de destination ne parvient pas à localiser votre audience, contactez votre représentant de [!DNL Adobe] pour obtenir de l’aide.

Vous devrez fournir les informations suivantes à votre représentant [!DNL Adobe] :

* Nom de l’audience
* Nom de la destination
* Date d’activation de l’audience
* Nom du fichier exporté

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez activé une audience sur la plateforme de destination sélectionnée. Ensuite, contactez le représentant de votre plateforme de destination pour commencer à configurer votre campagne.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).
