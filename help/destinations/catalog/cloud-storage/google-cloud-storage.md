---
title: Connexion à Google Cloud Storage (version Beta)
description: Découvrez comment vous connecter à Google Cloud Storage et activer des segments ou exporter des jeux de données.
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: d30cd0729aa13044d8e7009fde5cae846e7a2864
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 92%

---

# Connexion à [!DNL Google Cloud Storage] (version Beta)

>[!IMPORTANT]
>
>Cette destination est actuellement en version bêta et nʼest disponible que pour un nombre de clients limité. Pour demander l’accès à la connexion [!DNL Google Cloud Storage], contactez votre représentant Adobe et fournissez votre [!DNL Organization ID].

## Présentation {#overview}

Créez une connexion sortante active vers [!DNL Google Cloud Storage] pour exporter régulièrement des fichiers de données depuis Adobe Experience Platform dans vos propres compartiments.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma applicables, tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Configuration requise pour connecter votre compte [!DNL Google Cloud Storage] {#prerequisites}

Pour connecter Platform à [!DNL Google Cloud Storage], vous devez d’abord activer l’interopérabilité pour votre compte [!DNL Google Cloud Storage]. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** depuis les options de l’**[!UICONTROL espace de stockage]** dans le panneau de navigation.

![Tableau de bord de Google Cloud Platform avec l’espace de stockage et les paramètres mis en surbrillance.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

La page des **[!UICONTROL paramètres]** s’affiche. À partir de là, vous pouvez voir des informations relatives à votre ID de projet [!DNL Google] et les détails de votre compte [!DNL Google Cloud Storage]. Pour accéder aux paramètres d’interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l’en-tête supérieur.

![Onglet Interopérabilité mis en surbrillance dans le tableau de bord de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

Le page **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte de service. Pour générer un nouvel identifiant de clé d’accès et une clé d’accès secrète pour votre compte de service, sélectionnez **[!UICONTROL Créer une clé de compte de service]**.

![Commande Créer une clé de compte de service mise en surbrillance dans le tableau de bord de Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secrète pour connecter votre compte [!DNL Google Cloud Storage] à Platform.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](/help/destinations/ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL ID de clé d’accès]** : chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] auprès de Platform. Pour plus d’informations sur la manière d’obtenir cette valeur, lisez la section [Conditions préalables](#prerequisites) ci-dessus.
* **[!UICONTROL Clé d’accès secrète]** : chaîne codée en base64 de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] auprès de Platform. Pour plus d’informations sur la manière d’obtenir cette valeur, lisez la section [Conditions préalables](#prerequisites) ci-dessus.
* **[!UICONTROL Clé de chiffrement]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Pour plus d’informations sur ces valeurs, consultez le guide sur les [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] Présentation de la source](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du compartiment [!DNL Google Cloud Storage] que cette destination doit utiliser.
* **[!UICONTROL Chemin d’accès au dossier]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Type de fichier]**: sélectionnez le format que l’Experience Platform doit utiliser pour les fichiers exportés. Lorsque vous sélectionnez la variable [!UICONTROL CSV] , vous pouvez également [configuration des options de formatage de fichier](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Format de compression]**: sélectionnez le type de compression que l’Experience Platform doit utiliser pour les fichiers exportés.
* **[!UICONTROL Inclure le fichier manifeste]**: activez cette option si vous souhaitez que les exportations incluent un fichier JSON manifeste contenant des informations sur l’emplacement de l’exportation, la taille de l’exportation, etc.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activer des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification

Dans l’étape **[!UICONTROL Planifier]**, vous pouvez [configurer le planning d’exportation](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) pour votre destination [!DNL Google Cloud Storage] et vous pouvez également [configurer le nom de vos fichiers exportés](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mapper les attributs et les identités {#map}

Dans l’étape **[!UICONTROL Mappage]**, vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## (Version bêta) Exporter des jeux de données {#export-datasets}

Cette destination prend en charge les exportations de jeux de données. Pour obtenir des informations complètes sur la configuration des exportations de jeux de données, consultez la section [tutoriel sur l’exportation de jeux de données](/help/destinations/ui/export-datasets.md).

## Valider l’exportation des données avec succès {#exported-data}

Pour contrôler que l’exportation des données a bien réussi, vérifiez votre compartiment [!DNL Google Cloud Storage] et assurez-vous que les fichiers exportés contiennent les populations de profils attendues.
