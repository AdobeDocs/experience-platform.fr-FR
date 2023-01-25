---
description: Découvrez comment configurer les options de formatage des fichiers lors de l’activation des données vers des destinations basées sur des fichiers.
title: (Beta) Configurer des options de formatage de fichier pour les destinations basées sur des fichiers
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 14ce4a11f53ef24b3008b3f775cc926d05ea8f8e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 88%

---

# (Beta) Configurer des options de formatage de fichier pour les destinations basées sur des fichiers

>[!IMPORTANT]
>
>La fonctionnalité **[!UICONTROL Options de formatage des fichiers]** d’Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.
>Contactez votre représentant Adobe pour accéder à cette fonctionnalité.
> 
>Les options de formatage des fichiers décrites dans ce document ne sont actuellement disponibles que pour les fichiers CSV.

La possibilité de configurer diverses options de formatage des fichiers exportés vous est offerte lorsque vous vous [connectez](/help/destinations/ui/connect-destination.md) à une destination basée sur des fichiers, telle que [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) ou [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Vous pouvez configurer diverses options de formatage des fichiers exportés à l’aide de l’interface utilisateur d’Experience Platform. Vous pouvez modifier plusieurs propriétés des fichiers exportés pour répondre aux exigences du système de réception de fichiers de votre côté, afin de lire et d’interpréter de manière optimale les fichiers provenant d’Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuration du formatage des fichiers {#file-configuration}

Pour afficher les options de formatage de fichier, lancez le [se connecter à la destination](/help/destinations/ui/connect-destination.md) workflow. Sélectionner **Type de données : Segments** et **Type de fichier : CSV** pour afficher les paramètres de formatage de fichier disponibles pour l’exportation `CSV` fichiers .

>[!IMPORTANT]
>
>Toutes ces options ne sont peut-être pas disponibles pour la destination à laquelle vous vous connectez. Il appartient au développeur de la destination de déterminer les options de formatage des fichiers qu’il souhaite prendre en charge dans sa destination. Le développeur de la destination peut déterminer quelles options sont disponibles lors de la connexion à la destination. Les options obligatoires sont marquées d’un astérisque dans l’interface utilisateur d’Experience Platform.
> 
>Les nouvelles destinations de stockage dans le cloud - [(Version bêta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Version bêta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Version bêta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Version bêta) Zone d’entrée des données](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Version bêta) Stockage dans le cloud Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Version bêta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - ne prend actuellement en charge que les six options CSV mises en évidence ci-dessous.

![Image montrant certaines des options de formatage de fichier disponibles.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Délimiteur {#delimiter}

Définit un séparateur pour chaque champ et valeur. Les options disponibles sont les suivantes :

* Deux-points `(:)`
* Virgule `(,)`
* Tube `(|)`
* Point-virgule `(;)`
* Tabulation `(\\t)`

### Guillemets

Définit un caractère unique utilisé pour lʼéchappement des valeurs entre guillemets où le séparateur peut faire partie de la valeur.

### Caractère d’échappement

Définit un caractère unique utilisé pour lʼéchappement des guillemets dans une valeur déjà entre guillemets.

### Sortie de valeur vide

Définit la représentation sous forme de chaîne d’une valeur vide.

### Sortie de valeur nulle

Définit la représentation sous forme de chaîne d’une valeur nulle dans les fichiers exportés.

Exemple de sortie avec **[!UICONTROL null]** sélectionné : `male,NULL,TestLastName`
Exemple de sortie avec **&quot;&quot;** sélectionné : `male,"",TestLastName`
Exemple de sortie avec **[!UICONTROL Chaîne vide]** sélectionnée : `male,,TestLastName`

### Format de compression

Définit le codec de compression à utiliser lors de l’enregistrement de données dans un fichier. Les options prises en charge sont GZIP et NONE.

### Encodage

*Non affiché dans la capture d’écran de l’interface utilisateur*. Indique l’encodage (jeu de caractères) des fichiers CSV enregistrés. Les options sont UTF-8 ou UTF-16.

### Caractère pour échapper les guillemets

*Non affiché dans la capture d’écran de l’interface utilisateur*. Un indicateur précisant si les valeurs contenant des guillemets doivent toujours être placées entre guillemets.

La valeur par défaut est lʼéchappement de toutes les valeurs contenant un guillemet.

### Séparateur de ligne

*Non affiché dans la capture d’écran de l’interface utilisateur*. Définit le séparateur de ligne à utiliser pour l’écriture. Longueur maximale : 1 caractère.

### Ignorer l’espace blanc de début

*Non affiché dans la capture d’écran de l’interface utilisateur*. Indicateur précisant si les espaces de début des valeurs exportées doivent être ignorés.

Exemple de sortie avec **[!UICONTROL Vrai]** sélectionné : `"male","John","TestLastName"`
Exemple de sortie avec **[!UICONTROL Faux]** sélectionné : `" male","John","TestLastName"`

### Ignorer l’espace de fin

Non affiché dans la capture d’écran de l’interface utilisateur. Un indicateur précisant si les espaces blancs de fin de valeurs exportées doivent être ignorés ou non.

Exemple de sortie avec **[!UICONTROL Vrai]** sélectionné : `"male","John","TestLastName"`
Exemple de sortie avec **[!UICONTROL Faux]** sélectionné : `"male ","John","TestLastName"`

### Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment configurer les options d’exportation de vos fichiers de données CSV pour adapter le contenu du fichier aux exigences de votre système de réception de fichiers en aval. Vous pouvez ensuite lire le [tutoriel d’activation des destinations basées sur les fichiers](/help/destinations/ui/activate-batch-profile-destinations.md) pour commencer à exporter des fichiers vers votre emplacement de stockage dans le cloud préféré.
