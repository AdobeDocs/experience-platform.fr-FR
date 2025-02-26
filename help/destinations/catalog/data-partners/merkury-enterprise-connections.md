---
title: Destination des connexions d’entreprise Merkury
description: Découvrez comment créer une connexion de destination Connexions d’entreprise Merkury à l’aide de l’interface utilisateur de Adobe Experience Platform.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: dffc6f4d-b756-4c13-96f3-b1cc57caacdb
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 21%

---

# Destination des connexions d’entreprise Merkury

>[!NOTE]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Merkury]. Pour toute question ou demande de mise à jour, contactez votre gestionnaire de compte [!DNL Merkury].

## Vue d’ensemble

Utilisez la destination [!DNL Merkury Enterprise Connections] pour diffuser en toute sécurité des audiences vers [!DNL Merkury]. [!DNL Merkury] permet aux marketeurs de mettre facilement en correspondance et de diffuser des audiences basées sur des personnes vers les connexions haut débit 80+ de [!DNL Merkury] à la télévision adressable/CTV, à l’éditeur et aux technologies publicitaires. [!DNL Merkury] est alimenté par un graphique complet d&#39;identités de consommateurs américains adultes de plus de 268 millions de personnes.

![ Diagramme montrant l&#39;interconnexion entre Merkury et Experience Platform, y compris l&#39;ingestion et l&#39;activation](../../assets/catalog/data-partners/merkury-connections/media/image1.png)

Suivez les étapes de cette page de documentation pour créer une connexion de destination [!DNL Merkury Connections] et activer les audiences à l’aide de l’interface utilisateur de Adobe Experience Platform.

>[!NOTE]
>
>Si vous souhaitez activer des audiences vers des destinations de média avec votre compte [!DNL Merkury Connect], utilisez plutôt la destination [!DNL Merkury Connections] .

![La carte de destination des connexions d’entreprise Merkury mise en surbrillance dans le catalogue des destinations Experience Platform.](../../assets/catalog/data-partners/merkury-connections/media/image2.png)

## Cas d’utilisation

* **Digital Media Activation** : mise en correspondance et diffusion aisées de vos profils d’audience vers les plus de 50 éditeurs adressables haut de gamme et les connexions ad-tech de [!DNL Merkury].
* **Améliorer les efficacité** : améliorez la portée de vos médias adressables et sans cookies, améliorez l’efficacité du ciblage et réduisez le retour sur dépenses Advertising (ROAS).

## Conditions préalables

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des **vues des destinations** et **Gérer les destinations**, **activer les destinations**, **afficher les profils** et **** [[autorisations de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lisez la [[présentation du contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin du **graphique d’identités** [[autorisation de contrôle d’accès]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](../../assets/catalog/data-partners/merkury-connections/media/image3.png)

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

| **Audience** | **Pris en charge** | **Description origin** |
|---|---|---|      
| Segmentation Service | ✓ | Audiences générées par l’Experience Platform [[Segmentation Service]](https://experienceleague.adobe.com/fr/docs/experience-platform/segmentation/home). |
| Chargements personnalisés | X | Audiences [[importées]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| **Item** | **Type** | **Notes** |
|---|---|---|  
| Type d’exportation | **Basé sur les profils** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [[workflow d’activation de destination]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations#select-attributes). |
| Fréquence | **Lot** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [[destinations de fréquence basées sur des fichiers de lots]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-types#file-based). |

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

![nouvel écran de création de destination](../../assets/catalog/data-partners/merkury-connections/media/image4.png)

### Renseigner les détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Capture d’écran des détails de destination](../../assets/catalog/data-partners/merkury-connections/media/image6.png)

* **Nom (obligatoire)** - Nom sous lequel la destination sera enregistrée.
* **Description** - brève explication de l’objectif de la destination
* **Nom du compartiment (obligatoire)** - Nom du compartiment Amazon S3 configuré sur S3
* **Chemin du dossier (requis)** - Si des sous-répertoires d’un compartiment sont utilisés, un chemin d’accès doit être défini ou &quot;/&quot; pour référencer le chemin d’accès racine.
* **Type de fichier** - Sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Contactez votre équipe Merkury pour connaître le type de fichier attendu pour votre compte.

>[!NOTE]
>
>Lorsque vous sélectionnez l’option CSV, les options Délimiteur, Caractère de citation, Caractère d’échappement, Valeur vide, Valeur nulle, Format de compression et Inclure le fichier manifeste s’affichent, consultez votre équipe Merkury pour connaître les paramètres appropriés à votre compte.

![image des options csv](../../assets/catalog/data-partners/merkury-connections/media/image8.png)

### Compte existant

Les comptes déjà définis à l’aide de la destination Connexions de l’entreprise Merkury s’affichent dans une fenêtre contextuelle de liste. Lorsque cette option est sélectionnée, les détails du compte s’affichent dans le rail de droite. Affichez l’exemple dans l’interface utilisateur lorsque vous accédez à **Destinations** > **Comptes** :

![Copie d’écran du compte de destination sur la page des comptes de destination.](../../assets/catalog/data-partners/merkury-connections/media/image5.png)

## Activer les alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’ [ abonnement aux alertes de destinations à l’aide de l’interface utilisateur ](https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/ui/alerts).

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
