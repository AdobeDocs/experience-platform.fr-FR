---
title: (Alpha) Connexion  [!DNL LiveRamp SFTP]
description: Découvrez comment utiliser le connecteur LiveRamp pour intégrer des audiences d’Adobe Real-time Customer Data Platform vers LiveRamp Connect.
hidefromtoc: true
hide: true
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: d7625018b7b36d8e9516f7884fc00b726d391103
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 100%

---

# (Alpha) Connexion [!DNL LiveRamp - SFTP] {#liveramp-destination}

Utilisez la connexion LiveRamp pour intégrer des audiences depuis Adobe Real-time Customer Data Platform vers [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Cette connexion de destination est actuellement en phase Alpha et n’est disponible que pour une sélection limitée de clientes et clients. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.</p>
&gt;<p>La version finale de cette connexion de destination peut nécessiter la migration des clientes et clients.</p>


## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL LiveRamp SFTP], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

En tant que spécialiste marketing, je souhaite envoyer des audiences d’Adobe Experience Platform vers des identités intégrées dans [!DNL LiveRamp Connect] afin que je puisse cibler les utilisateurs et utilisatrices sur les plateformes [!DNL CTV], à l’aide de l’identifiant [!DNL Ramp ID].

## Conditions préalables {#prerequisites}

La connexion [!DNL LiveRamp - SFTP] exporte les fichiers à l’aide du stockage [SFTP de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).

Avant d’envoyer des données d’Experience Platform vers [!DNL LiveRamp SFTP], vous avez besoin de vos informations d’identification [!DNL LiveRamp]. Veuillez contacter votre représentant ou représentante [!DNL LiveRamp] pour obtenir vos informations d’identification, si vous ne les avez pas déjà.

## Identités prises en charge {#supported-identities}

Le SFTP de LiveRamp prend en charge l’activation d’identités telles que les identifiants basés sur des informations d’identification personnelles, les identifiants connus et les identifiants personnalisés, décrits dans la [documentation officielle de LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

À l’[étape de mappage](#map) du workflow d’activation, vous devez définir les mappages cibles en tant qu’attributs personnalisés.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL LiveRamp SFTP]. |
| Fréquence des exportations | **[!UICONTROL Lot quotidien]** | Étant donné que les profils sont mis à jour dans Experience Platform en fonction de l’évaluation des segments, les profils (identités) sont mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

**Authentification SFTP avec mot de passe** {#sftp-password}

![Exemple de capture d’écran montrant comment s’authentifier à la destination à l’aide du SFTP avec un mot de passe](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur de votre emplacement de stockage [!DNL LiveRamp SFTP].
* **[!UICONTROL Mot de passe]** : mot de passe de votre emplacement de stockage [!DNL LiveRamp SFTP].
* **[!UICONTROL Clé de chiffrement PGP/GPG]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous. Si vous fournissez une clé de chiffrement, vous devez également fournir un **[!UICONTROL ID de sous-clé de chiffrement]** dans la section [détails de la destination](#destination-details).

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP avec authentification par clé SSH** {#sftp-ssh}

![Exemple de capture d’écran montrant comment s’authentifier à la destination à l’aide de la clé SSH](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur de votre emplacement de stockage [!DNL LiveRamp SFTP].
* **[!UICONTROL Clé SSH]** : la clé privée [!DNL SSH] utilisée pour se connecter à votre emplacement de stockage [!DNL LiveRamp SFTP]. La clé privée doit être formatée sous la forme d’une chaîne codée en [!DNL Base64] et ne doit pas être protégée par un mot de passe.

   * Pour connecter votre clé [!DNL SSH] au serveur [!DNL LiveRamp SFTP], vous devez soumettre un ticket via le portail d’assistance technique de [!DNL LiveRamp] et fournir votre clé publique. Pour plus d’informations, voir la [documentation LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Clé de chiffrement PGP/GPG]** : vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Si vous fournissez une clé de chiffrement, vous devez également fournir un **[!UICONTROL ID de sous-clé de chiffrement]** dans la section [détails de la destination](#destination-details). Vous pouvez voir un exemple de clé correctement formatée dans l’image ci-dessous.

   ![Image montrant un exemple de clé PGP correctement formatée dans l’interface utilisateur](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID de sous-clé de chiffrement"
>abstract="ID de sous-clé utilisé pour le chiffrement, basé sur la clé de chiffrement publique LiveRamp. Ce champ est obligatoire si vous avez fourni une clé de chiffrement à l’étape d’authentification."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Découvrez comment obtenir l’ID de sous-clé"

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Capture d’écran de l’interface utilisateur de Platform montrant comment remplir les détails pour votre destination](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Chemin du dossier]** : saisissez le sous-dossier `uploads` de [!DNL LiveRamp] qui hébergera les fichiers exportés. Le préfixe `uploads` est automatiquement ajouté au chemin du dossier.
   * Par exemple, si vous souhaitez exporter vos fichiers vers `uploads/my_export_folder`, saisissez `my_export_folder` dans le champ **[!UICONTROL Chemin du dossier]**.
* **[!UICONTROL Format de compression]** : sélectionnez le type de compression qu’Experience Platform doit utiliser pour les fichiers exportés. Les options disponibles sont **[!UICONTROL GZIP]** ou **[!UICONTROL Aucun]**.
* **[!UICONTROL ID de sous-clé de chiffrement]** : sous-clé utilisée pour le chiffrement, en fonction de la clé de chiffrement publique [!DNL LiveRamp]. Ce champ est obligatoire si vous avez fourni une clé de chiffrement à l’étape d’[authentification](#authenticate). Consultez la [documentation sur le chiffrement](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) de [!DNL LiveRamp] pour savoir comment obtenir l’ID de sous-clé.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Planification {#scheduling}

À l’étape [!UICONTROL Planification], créez une planification d’exportation pour chaque segment, avec les paramètres présentés ci-dessous.

>[!IMPORTANT]
>
>Tous les segments activés vers cette destination doivent être configurés avec exactement le même planning, tel qu’illustré ci-dessous.

* **[!UICONTROL Options d’exportation de fichiers]** : [!UICONTROL Exporter des fichiers complets]. Les [exportations de fichiers incrémentiels](../../ui/activate-batch-profile-destinations.md#export-incremental-files) ne sont actuellement pas prises en charge pour la destination [!DNL LiveRamp].
* **[!UICONTROL Fréquence]** : [!UICONTROL quotidiennement]
* Définissez l’heure d’exportation sur **[!UICONTROL Après l’évaluation du segment]**. Les exportations de segments planifiées et les [exportations de fichiers à la demande](../../ui/export-file-now.md) ne sont actuellement pas prises en charge pour la destination [!DNL LiveRamp].
* **[!UICONTROL Date]** : sélectionnez les heures de début et de fin de l’exportation comme vous le souhaitez.

![Capture d’écran de l’interface utilisateur de Platform montrant l’étape de planification des segments.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

Le nom de fichier exporté ne peut actuellement pas être configuré par l’utilisateur ou l’utilisatrice. Tous les fichiers exportés vers la destination [!DNL LiveRamp SFTP] sont automatiquement nommés en fonction du modèle suivant :

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Capture d’écran de l’interface utilisateur de Platform présentant le modèle de nom de fichier exporté.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Par exemple, le nom d’un fichier exporté pour une organisation nommée [!DNL Luma] pourrait ressembler à ceci :

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Mapper les attributs et les identités {#map}

À l’étape du **[!UICONTROL Mappage]**, vous pouvez sélectionner les attributs et les identités que vous souhaitez exporter pour vos profils.

>[!IMPORTANT]
>
>Cette destination prend en charge l’activation d’un espace de noms d’identité source par flux d’activation. Si vous devez exporter plusieurs espaces de noms d’identité, tels que `Email` et `Phone`, vous devez [créer un flux d’activation distinct](../../ui/activate-batch-profile-destinations.md) pour chaque identité.

À l’étape **[!UICONTROL Mappage]**, le mappage **[!UICONTROL Champ cible]** définit le nom de l’en-tête de colonne dans le fichier CSV exporté. Vous pouvez remplacer les en-têtes de colonne CSV du fichier exporté par n’importe quel nom convivial, en fournissant un nom personnalisé pour le **[!UICONTROL champ cible]**.

1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Une nouvelle ligne de mappage s’affichera à l’écran.

   ![Capture d’écran de l’interface utilisateur d’Experience Platform affichant l’écran Mappage.](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]**, choisissez la catégorie **[!UICONTROL Sélectionner des attributs]** et sélectionnez l’attribut XDM à mapper, ou choisissez la catégorie **[!UICONTROL Sélectionner un espace de noms d’identité]** et sélectionnez une identité à mapper à votre destination.

   ![Capture d’écran de l’interface utilisateur d’Experience Platform affichant l’écran de mappage source.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]**, saisissez le nom de l’attribut auquel vous souhaitez mapper le champ source sélectionné. Le nom d’attribut défini ici se reflète dans le fichier CSV exporté sous la forme d’un en-tête de colonne.

   ![Capture d’écran de l’interface utilisateur d’Experience Platform affichant l’écran de mappage cible.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Vous pouvez également saisir le nom de l’attribut en le saisissant directement dans le **[!UICONTROL champ cible]**.

   ![Capture d’écran de l’interface utilisateur d’Experience Platform affichant l’écran de mappage cible.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Une fois que vous avez ajouté tous les mappages souhaités, sélectionnez **[!UICONTROL Suivant]** et terminez le workflow d’activation.

## Données exportées / Valider l’exportation des données {#exported-data}

Vos données sont exportées vers l’emplacement de stockage [!DNL LiveRamp SFTP] que vous avez configuré, sous forme de fichiers CSV.

Lors de l’exportation de fichiers vers la destination [!DNL LiveRamp SFTP], Platform génère un fichier CSV pour chaque [ID de stratégie de fusion](../../../profile/merge-policies/overview.md).

Prenons par exemple les segments suivants :

* Segment A (stratégie de fusion 1)
* Segment B (stratégie de fusion 2)
* Segment C (stratégie de fusion 1)
* Segment D (stratégie de fusion 1)

Platform exportera deux fichiers CSV vers [!DNL LiveRamp SFTP] :

* Un fichier CSV contenant les segments A, C et D ;
* Un fichier CSV contenant le segment B.

Les fichiers CSV exportés contiennent des profils avec les attributs sélectionnés et l’état du segment correspondant, sur des colonnes distinctes, avec le nom d’attribut et les identifiants de segment comme en-têtes de colonne.

Les profils inclus dans les fichiers exportés peuvent correspondre à l’un des statuts de qualification de segment suivants :

* `Active` : le profil est actuellement qualifié pour le segment.
* `Expired` : le profil n’est plus qualifié pour le segment, mais il l’a déjà été.
* `""` (chaîne vide) : le profil n’a jamais été qualifié pour le segment.


Par exemple, un fichier CSV exporté avec un attribut `email` et 3 segments peuvent ressembler à ceci :

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Comme Platform génère un fichier CSV pour chaque [ID de stratégie de fusion](../../../profile/merge-policies/overview.md), il génère également une exécution de flux de données distincte pour chaque ID de stratégie de fusion.

Cela signifie que les mesures **[!UICONTROL Identités activées]** et **[!UICONTROL Profils reçus]** de la page [exécutions de flux de données](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) sont agrégées pour chaque groupe de segments qui utilisent la même stratégie de fusion, au lieu d’être affichées pour chaque segment.

Du fait de la génération d’exécutions de flux de données pour un groupe de segments qui utilisent la même stratégie de fusion, les noms de segment ne s’affichent pas dans le [tableau de bord de surveillance](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Capture d’écran de l’interface utilisateur d’Experience Platform affichant la mesure Identités activées.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Télécharger des données exportées vers LiveRamp {#upload-to-liveramp}

Une fois vos données exportées vers le stockage [!DNL LiveRamp - SFTP], vous devez télécharger les données vers la plateforme [!DNL LiveRamp].

Pour plus d’informations sur la manière de télécharger vos fichiers depuis le stockage [!DNL LiveRamp - SFTP] vers une audience [!DNL LiveRamp], consultez la documentation suivante : [Remarques concernant le téléchargement du premier fichier vers une audience](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur la configuration de votre stockage SFTP LiveRamp, consultez la [documentation officielle](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
