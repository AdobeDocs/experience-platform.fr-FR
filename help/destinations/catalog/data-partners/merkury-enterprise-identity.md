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
>La page de documentation et le connecteur de destination sont créés et conservés par la fonction [!DNL Merkury] l&#39;équipe. Pour toute question ou demande de mise à jour, veuillez contacter votre [!DNL Merkury] représentant du compte.

## Vue d’ensemble

Utilisez la variable [!DNL Merkury Enterprise Identity] destination pour créer des profils clients plus précis, complets et pertinents. Grâce à l’amélioration des données de profil, les marketeurs peuvent optimiser les informations, les segments et les modèles, ce qui se traduit par un ciblage et une modélisation prédictive plus précis.

![Un diagramme montrant l&#39;interconnexion entre Merkury et Experience Platform, y compris l&#39;ingestion et l&#39;activation](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Suivez les étapes de cette page de documentation pour créer une [!DNL Merkury Identity] connexion de destination et activation des audiences pour identification et enrichissement à l’aide de l’interface utilisateur de Adobe Experience Platform.

>[!NOTE]
>
>Si vous souhaitez activer des audiences vers des destinations de média avec votre [!DNL Merkury Connect] , utilisez la variable [!DNL Merkury Connections] destination .

![La carte de destination Identité d’entreprise Merkury mise en surbrillance dans le catalogue des destinations Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Cas d’utilisation

La variable [!DNL Merkury Enterprise Identity] La destination permet de transférer en toute sécurité les informations d’identification personnelles des consommateurs pour les éléments suivants : [!DNL Merkury] fonctionnalités :

* **Qualité des données**: améliorez la qualité des données du profil du client grâce à l’hygiène et à la normalisation des données. [!DNL Merkury] inclut l’hygiène postale aux États-Unis et l’identification des déménagements afin de prendre en charge les cas d’utilisation les plus avancés du marketing par courrier.
* **Résolution des identités**: créer une vue unique précise et complète du client, informée par [!DNL Merkury] ID individuels et ID de foyer. Les identifiants Merkury offrent un niveau profond de liaison de profils optimisés par [!DNL Merkury]Le graphique complet de l&#39;identité des consommateurs américains adultes de plus de 268 millions de personnes.
* **Enrichissement**: proposez de meilleures informations et personnalisation avec [!DNL Merkury Data]. [!DNL Merkury Data] comprend plus de 10 000 attributs de données disponibles, allant de données démographiques, de style de vie, financières, d’événements de la vie et des données d’achat auprès de la variable [!DNL Merkury Data Suite].

>[!NOTE]
>
>Ces cas d’utilisation sont exécutés par le biais d’une combinaison de connecteurs source et de destination. Le client commencerait par exporter ses dossiers client existants pour enrichissement à l’aide de ce connecteur de destination. [!DNL Merkury]Le service de recherche de rechercherait le fichier, le récupérerait, l’enrichirait de [!DNL Merkury]des données et générez un fichier. Le client utilisera alors la variable [!DNL Merkury] Carte source du connecteur Source pour ingérer à nouveau les profils client hydratés dans Adobe Real-Time CDP.

## Conditions préalables

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin de l’événement **Affichage des destinations** et **Gestion des destinations**, **Activation des destinations**, **Afficher les profils**, et **Affichage de segments** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lisez la section [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **Affichage du graphique des identités** [[autorisation de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

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

| **Audience** | **Pris en charge** | **Description** | **origine** |
|---|---|---|---|
| Segmentation Service | ✓ | Audiences générées par l’Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Chargements personnalisés | x | Audiences [[importé]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.
|**Audience**|**Pris en charge**|**Description de l’origine**|\
|—|—|—|\
|Segmentation Service|✓|Audiences générées par l’Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).| Téléchargements personnalisés|X|Audiences [[importé]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV.

{style="table-layout:auto"}

## Se connecter à la destination

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’événement **Affichage des destinations** et **Gestion et activation des destinations de jeu de données** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lisez la section [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans la section [[tutoriel sur la configuration de destination]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **Se connecter à la destination**.

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


* **Nom (obligatoire)** : nom sous lequel la destination sera enregistrée.
* **Description** - brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin d’accès au dossier (requis)** - Si des sous-répertoires d’un compartiment sont utilisés, un chemin doit être défini ou &quot;/&quot; pour référencer le chemin racine.
* **Type de fichier** - Sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Contactez votre équipe Merkury pour connaître le type de fichier attendu pour votre compte.

>[!NOTE]
>
>Lorsque vous sélectionnez l’option CSV, les options Délimiteur, Caractère de citation, Caractère d’échappement, Valeur vide, Valeur nulle, Format de compression et Inclure le fichier manifeste s’affichent, consultez votre équipe Merkury pour connaître les paramètres appropriés à votre compte.

![image de l’option csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination Merkury Enterprise Identity apparaissent dans une liste contextuelle. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple dans l’interface utilisateur lorsque vous accédez à **Destinations** > **Comptes**;

![Capture d’écran du compte de destination dans la page des comptes de destination](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **Suivant**.

## Activer des audiences vers cette destination

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin de l’événement **Affichage des destinations**, **Activation des destinations**, **Afficher les profils**, et **Affichage de segments** autorisations de contrôle d’accès. Lisez la présentation du contrôle d’accès ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous avez besoin de l’événement **Affichage du graphique des identités** autorisation de contrôle d’accès.

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Suggestions de mappage

Le traitement correct des fichiers sur l’événement [!DNL Merkury] Le côté nécessite des éléments de nom et d’adresse. Bien que tous les éléments ne soient pas nécessaires, fournir autant que possible contribue à une correspondance réussie.

Les suggestions de mappage sont fournies dans le tableau ci-dessous, qui répertorie les attributs du côté destination utilisés par [!DNL Merkury] traitement auquel les clients peuvent mapper des attributs de profil. Traitez ces éléments comme des suggestions, car tous les éléments ne sont pas requis et les valeurs source dépendront des besoins du compte.

| Champ cible | Description Source |
|---|---|
| identifiant | Champ d’identité à utiliser pour le mappage [!DNL Merkury] données à l’Experience Platform via la variable [!DNL Merkury Enterprise Identity] Connecteur Source |
| Input_First_Name | La variable `person.name.firstName` dans Experience Platform. |
| Input_Last_Name | La variable `person.name.lastName` dans Experience Platform. |
| Input_Address_Line_1 | La variable `mailingAddress.street` dans Experience Platform. |
| Input_City | La variable `mailingAddress.city` dans Experience Platform. |
| Input_State_Province_Code | La variable `mailingAddress.state` dans Experience Platform. Utilisez cette option si l’état se trouve dans le formulaire de code à deux caractères. |
| Input_State_Province_Name | La variable `mailingAddress.state` dans Experience Platform. Utilisation si l’état est le nom complet de l’état |
| Input_Postal_Code | La variable `mailingAddress.postalCode` dans Experience Platform. |
| Input_Email_Address | La valeur que vous souhaitez mapper comme adresse email des profils. |
| Input_Phone | La valeur que vous souhaitez mapper comme numéro de téléphone des profils. |

{style="table-layout:auto"}

## Valider l’exportation des données

Pour vérifier si les données ont bien été exportées, vérifiez votre compartiment de stockage Amazon S3 et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.

## Utilisation et gouvernance des données

Toutes les destinations Adobe Experience Platform sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la manière dont Adobe Experience Platform applique la gouvernance des données, consultez la section [Présentation de la gouvernance des données](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour exporter les données de profil de l’Experience Platform vers votre [!DNL Merkury] emplacement S3 géré. Ensuite, vous devez contacter votre [!DNL Merkury] représentant avec le nom du compte, les noms de fichier et le chemin du compartiment afin que le traitement puisse être configuré.