---
title: (Version bêta) Connexion au stockage dans le cloud Google
description: Découvrez comment vous connecter au stockage dans le cloud Google et activer des segments ou exporter des jeux de données.
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 28%

---

# (Version bêta) [!DNL Google Cloud Storage] connection

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et n’est disponible que pour un nombre limité de clients. Pour demander l’accès à la connexion [!DNL Google Cloud Storage], contactez votre représentant Adobe et fournissez vos [!DNL Organization ID].

## Présentation {#overview}

Créer une connexion sortante active vers [!DNL Google Cloud Storage] pour exporter régulièrement des fichiers de données de Adobe Experience Platform dans vos propres compartiments.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables, tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations de lot exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur [destinations basées sur des fichiers de lots](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Configuration requise pour connecter votre [!DNL Google Cloud Storage] account {#prerequisites}

Pour connecter Platform à [!DNL Google Cloud Storage], vous devez d’abord activer l’interopérabilité pour votre [!DNL Google Cloud Storage] compte . Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** de la **[!UICONTROL Stockage dans le cloud]** dans le panneau de navigation.

![Tableau de bord de la plateforme Google Cloud avec espace de stockage et paramètres en surbrillance.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

Le **[!UICONTROL Paramètres]** s’affiche. À partir de là, vous pouvez voir des informations relatives à votre [!DNL Google] ID de projet et détails sur votre [!DNL Google Cloud Storage] compte . Pour accéder aux paramètres d’interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l’en-tête supérieur.

![Onglet Interopérabilité mis en surbrillance dans le tableau de bord de Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

Le **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte de service. Pour générer un nouvel identifiant de clé d’accès et une clé d’accès secrète pour votre compte de service, sélectionnez **[!UICONTROL Création d’une clé pour un compte de service]**.

![La commande Créer une clé pour un contrôle de compte de service est mise en surbrillance dans le tableau de bord Google Cloud Platform.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secrète pour connecter votre [!DNL Google Cloud Storage] compte à Platform.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](/help/destinations/ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Accès à l’ID de clé]**: Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. Pour plus d’informations sur la manière d’obtenir cette valeur, lisez le [conditions préalables](#prerequisites) ci-dessus.
* **[!UICONTROL Clé d’accès secrète]**: Chaîne codée en base 64 caractères de 40 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. Pour plus d’informations sur la manière d’obtenir cette valeur, lisez le [conditions préalables](#prerequisites) ci-dessus.
* **[!UICONTROL Clé de chiffrement]**: Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que [!DNL Base64-encoded] chaîne. Affichez un exemple d’une clé codée en base64 correctement formatée dans le lien de documentation ci-dessous. La partie centrale est raccourcie par concision.

   ![Image montrant un exemple d’une clé PGP correctement formatée et chiffrée en base64 dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Pour plus d’informations sur ces valeurs, consultez la section [Clés HMAC de stockage dans le cloud Google](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] présentation de la source](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Nom du compartiment]**: Saisissez le nom du [!DNL Google Cloud Storage] compartiment à utiliser par cette destination.
* **[!UICONTROL Chemin du dossier]**: Entrez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification

Dans le **[!UICONTROL Planification]** étape, vous pouvez [configuration du planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre [!DNL Google Cloud Storage] destination et vous pouvez également [configurer le nom des fichiers exportés ;](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mise en correspondance des attributs et des identités {#map}

Dans le **[!UICONTROL Mappage]** vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir la [étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activation de l’interface utilisateur des destinations par lot .

## (Version bêta) Exportation de jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Validation de l’exportation des données réussie {#exported-data}

Pour vérifier si l’exportation des données a réussi, vérifiez votre [!DNL Google Cloud Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
