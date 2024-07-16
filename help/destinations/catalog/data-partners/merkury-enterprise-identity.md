---
title: Destination Merkury Enterprise Identity
description: Découvrez comment créer une connexion de destination d’identité d’entreprise Merkury à l’aide de l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 17%

---


# Destination Merkury Enterprise Identity

>[!NOTE]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Merkury]. Pour toute question ou demande de mise à jour, contactez votre gestionnaire de compte [!DNL Merkury].

## Vue d’ensemble

Utilisez la destination [!DNL Merkury Enterprise Identity] pour créer des profils consommateurs plus précis, complets et pertinents. Grâce à l’amélioration des données de profil, les marketeurs peuvent optimiser les informations, les segments et les modèles, ce qui se traduit par un ciblage et une modélisation prédictive plus précis.

![ Diagramme montrant l&#39;interconnexion entre Merkury et Experience Platform, y compris l&#39;ingestion et l&#39;activation](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Suivez les étapes de cette page de documentation pour créer une connexion de destination [!DNL Merkury Identity] et activer les audiences pour identification et enrichissement à l’aide de l’interface utilisateur de Adobe Experience Platform.

>[!NOTE]
>
>Si vous souhaitez activer des audiences vers des destinations de média avec votre compte [!DNL Merkury Connect], utilisez plutôt la destination [!DNL Merkury Connections] .

![La carte de destination d’identité d’entreprise Merkury mise en surbrillance dans le catalogue des destinations Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Cas d’utilisation

La destination [!DNL Merkury Enterprise Identity] permet de transférer en toute sécurité les informations d’identification personnelles des consommateurs pour les fonctionnalités [!DNL Merkury] suivantes :

* **Qualité des données** : améliorez la qualité des données du profil client grâce à l’hygiène et à la normalisation des données. [!DNL Merkury] comprend l’hygiène postale aux États-Unis et l’identification des déplacements pour prendre en charge les cas d’utilisation de marketing par courrier les plus avancés.
* **Résolution d’identité** : créez une vue unique exacte et complète du client, en fonction des [!DNL Merkury] identifiants individuels et de foyer. Les Merkury ID offrent un niveau profond de liaison de profils grâce au graphique complet d&#39;identités de consommateurs américains adultes de plus de 268 millions d&#39;utilisateurs de [!DNL Merkury].
* **Enrichissement** : permet d’obtenir de meilleures informations et une meilleure personnalisation avec [!DNL Merkury Data]. [!DNL Merkury Data] comprend plus de 10 000 attributs de données disponibles, allant de la démographie, du style de vie, des événements financiers, de la vie et des données d’achat de [!DNL Merkury Data Suite].

>[!NOTE]
>
>Ces cas d’utilisation sont exécutés par le biais d’une combinaison de connecteurs source et de destination. Le client commencerait par exporter ses dossiers client existants pour enrichissement à l’aide de ce connecteur de destination. Le service de [!DNL Merkury] recherche le fichier, le récupère, l’enrichit avec les données de [!DNL Merkury] et génère un fichier. Le client utilisera alors la carte source du connecteur Source correspondante [!DNL Merkury] pour ingérer à nouveau les profils client hydratés dans Adobe Real-Time CDP.

## Conditions préalables

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **vues des destinations** et **Gérer les destinations**, **activer les destinations**, **afficher les profils** et **** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lisez la [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin du **graphique d’identités** [[autorisation de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identités prises en charge {#supported-identities}

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) pour plus d’informations. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| **Audience** | **Pris en charge** | **Description** | **origin** |
|---|---|---|---|
| Segmentation Service | ✓ | Audiences générées par l’Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Chargements personnalisés | x | Audiences [[importées]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.
|**Audience**|**Pris en charge**|**Description origin**|\
|—|—|—|\
|Segmentation Service|✓|Audiences générées par l’Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).|
Téléchargements personnalisés|X|Audiences [[importé]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV.

{style="table-layout:auto"}

## Se connecter à la destination

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **** et **** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions)   . Lisez la [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, suivez les étapes décrites dans le [[tutoriel de configuration de destination]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination

Pour vous authentifier à la destination, remplissez les champs requis et sélectionnez **Se connecter à la destination**.

Pour accéder à votre compartiment sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

| **Credential** | **Description** |
|---|---|
| Clé d’accès | Identifiant de la clé d’accès pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |
| Clé secrète | Identifiant de clé secrète pour votre compartiment. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |
| Nom du compartiment | Il s’agit de votre compartiment où les fichiers seront partagés. Vous pouvez récupérer cette valeur auprès de l’équipe Merkury. |

{style="table-layout:auto"}

![nouvel écran de création de destination](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Renseigner les détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Capture d’écran des détails de destination](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nom (obligatoire)** - Nom sous lequel la destination sera enregistrée.
* **Description** - brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (requis)** - Si des sous-répertoires d’un compartiment sont utilisés, un chemin d’accès doit être défini ou &quot;/&quot; pour référencer le chemin d’accès racine.
* **Type de fichier** - Sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Contactez votre équipe Merkury pour connaître le type de fichier attendu pour votre compte.

>[!NOTE]
>
>Lorsque vous sélectionnez l’option CSV, les options Délimiteur, Caractère de citation, Caractère d’échappement, Valeur vide, Valeur nulle, Format de compression et Inclure le fichier manifeste s’affichent, consultez votre équipe Merkury pour connaître les paramètres appropriés à votre compte.

![image de l’option csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination Merkury Enterprise Identity apparaissent dans une liste contextuelle. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple dans l’interface utilisateur lorsque vous accédez à **Destinations** > **Comptes** ;

![Copie d’écran du compte de destination sur la page des comptes de destination](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’ [ abonnement aux alertes de destinations à l’aide de l’interface utilisateur ](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **Suivant**.

## Activer des audiences vers cette destination

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **Afficher les destinations**, **Activer les destinations**, **Afficher les profils** et **Afficher les segments**. Lisez la présentation du contrôle d’accès ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous avez besoin de l’autorisation de contrôle d’accès **Afficher le graphique d’identités**.

Lisez [Activer les données d’audience vers les destinations d’exportation de profil de lot](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Suggestions de mappage

Le traitement correct des fichiers du côté [!DNL Merkury] nécessite des éléments de nom et d’adresse. Bien que tous les éléments ne soient pas nécessaires, fournir autant que possible contribue à une correspondance réussie.

Les suggestions de mappage sont fournies dans le tableau ci-dessous, qui répertorie les attributs de votre côté destination utilisés par le traitement [!DNL Merkury] vers lesquels les clients peuvent mapper des attributs de profil. Traitez ces éléments comme des suggestions, car tous les éléments ne sont pas requis et les valeurs source dépendront des besoins du compte.

| Champ cible | Description Source |
|---|---|
| identifiant | Champ d’identité à utiliser pour mapper les données [!DNL Merkury] à l’Experience Platform via le connecteur Source [!DNL Merkury Enterprise Identity] |
| Input_First_Name | La valeur `person.name.firstName` en Experience Platform. |
| Input_Last_Name | La valeur `person.name.lastName` en Experience Platform. |
| Input_Address_Line_1 | La valeur `mailingAddress.street` en Experience Platform. |
| Input_City | La valeur `mailingAddress.city` en Experience Platform. |
| Input_State_Province_Code | La valeur `mailingAddress.state` en Experience Platform. Utilisez cette option si l’état se trouve dans le formulaire de code à deux caractères. |
| Input_State_Province_Name | La valeur `mailingAddress.state` en Experience Platform. Utilisation si l’état est le nom complet de l’état |
| Input_Postal_Code | La valeur `mailingAddress.postalCode` en Experience Platform. |
| Input_Email_Address | La valeur que vous souhaitez mapper comme adresse email des profils. |
| Input_Phone | La valeur que vous souhaitez mapper comme numéro de téléphone des profils. |

{style="table-layout:auto"}

## Valider l’exportation des données

Pour vérifier si les données ont bien été exportées, vérifiez votre compartiment de stockage Amazon S3 et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Utilisation et gouvernance des données

Toutes les destinations Adobe Experience Platform sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la manière dont Adobe Experience Platform applique la gouvernance des données, consultez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour exporter les données de profil de l’Experience Platform vers votre emplacement S3 géré [!DNL Merkury]. Ensuite, vous devez contacter votre représentant [!DNL Merkury] avec le nom du compte, les noms de fichier et le chemin du compartiment pour que le traitement puisse être configuré.