---
description: Découvrez comment configurer les options de formatage de fichier lors de l’activation de données vers des destinations basées sur des fichiers
title: (Version bêta) Configuration des options de formatage de fichier pour les destinations basées sur des fichiers
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 20%

---

# (Version bêta) Configuration des options de formatage de fichier pour les destinations basées sur des fichiers

>[!IMPORTANT]
>
>Le **[!UICONTROL Options de formatage de fichier]** La fonctionnalité de Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.
>Contactez votre représentant Adobe pour accéder à cette fonctionnalité.
> 
>Les options de formatage de fichier décrites dans ce document sont actuellement disponibles uniquement pour les fichiers CSV.

Lorsque vous configurez les différentes options de formatage de fichier pour les fichiers exportés, vous avez la possibilité de [connect](/help/destinations/ui/connect-destination.md) vers une destination basée sur des fichiers, telle que [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)ou [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Vous pouvez configurer différentes options de formatage de fichier pour les fichiers exportés à l’aide de l’interface utilisateur de l’Experience Platform. Vous pouvez modifier plusieurs propriétés des fichiers exportés pour répondre aux exigences du système de réception de fichiers de votre côté, afin de lire et interpréter de manière optimale les fichiers reçus d’Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuration du formatage de fichier {#file-configuration}

>[!IMPORTANT]
>
>Toutes ces options peuvent ne pas être disponibles pour la destination à laquelle vous vous connectez. Il appartient au développeur de destination de déterminer les options de formatage de fichier qu’il souhaite prendre en charge dans sa destination. Le développeur de destination peut déterminer les options disponibles lors de la connexion à la destination. Les options requises sont signalées par un astérisque dans l’interface utilisateur de l’Experience Platform.

Pour afficher les options de formatage de fichier, lancez le [se connecter à la destination](/help/destinations/ui/connect-destination.md) workflow et sélectionner les segments comme **Type de fichier**. Cette section décrit les paramètres de formatage de fichier disponibles pour l’exportation `CSV` fichiers .

![Image montrant certaines des options de formatage de fichier disponibles.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Délimiteur

Définit un séparateur pour chaque champ et valeur. Par exemple : `,` pour les valeurs séparées par des virgules ou `/t` pour les valeurs séparées par des tabulations.

### Caractère de citation

Définit un caractère unique utilisé pour lʼéchappement des valeurs entre guillemets où le séparateur peut faire partie de la valeur.

### Caractère d’échappement

Définit un caractère unique utilisé pour lʼéchappement des guillemets dans une valeur déjà entre guillemets.

### Sortie de valeur vide

Définit la représentation sous forme de chaîne d’une valeur vide.

### Sortie de valeur nulle

Définit la représentation sous forme de chaîne d’une valeur null dans les fichiers exportés.

Exemple de sortie avec **[!UICONTROL null]** selected : `male,NULL,TestLastName`
Exemple de sortie avec **&quot;&quot;** selected : `male,"",TestLastName`
Exemple de sortie avec **[!UICONTROL Chaîne vide]** selected : `male,,TestLastName`

### Format de compression

Définit le codec de compression à utiliser lors de l’enregistrement de données dans un fichier. Les options prises en charge sont GZIP et NONE.

### Encodage

*Non affiché dans la capture d’écran de l’interface utilisateur*. Indique le codage (jeu de caractères) des fichiers CSV enregistrés. Les options sont UTF-8 ou UTF-16.

### Caractère pour échapper les guillemets

*Non affiché dans la capture d’écran de l’interface utilisateur*. Indicateur précisant si les valeurs contenant des guillemets doivent toujours être placées entre guillemets.

La valeur par défaut est lʼéchappement de toutes les valeurs contenant un guillemet.

### Séparateur de ligne

*Non affiché dans la capture d’écran de l’interface utilisateur*. Définit le séparateur de ligne à utiliser pour l’écriture. Longueur maximale : 1 caractère.

### Ignorer l’espace blanc de début

*Non affiché dans la capture d’écran de l’interface utilisateur*. Indicateur précisant si les espaces de début des valeurs exportées doivent être ignorés.

Exemple de sortie avec **[!UICONTROL True]** selected : `"male","John","TestLastName"`
Exemple de sortie avec **[!UICONTROL False]** selected : `" male","John","TestLastName"`

### Ignorer l’espace de fin

Non affiché dans la capture d’écran de l’interface utilisateur. Un indicateur indiquant si les espaces de fin des valeurs exportées doivent être ignorés ou non.

Exemple de sortie avec **[!UICONTROL True]** selected : `"male","John","TestLastName"`
Exemple de sortie avec **[!UICONTROL False]** selected : `"male ","John","TestLastName"`

### Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment configurer les options d’exportation de fichiers pour vos fichiers de données CSV afin d’adapter le contenu des fichiers aux exigences de votre système de réception de fichiers en aval. Vous pouvez ensuite lire le [tutoriel sur l’activation des destinations basées sur des fichiers](/help/destinations/ui/activate-batch-profile-destinations.md) pour commencer à exporter des fichiers vers l’emplacement de stockage dans le cloud de votre choix.
