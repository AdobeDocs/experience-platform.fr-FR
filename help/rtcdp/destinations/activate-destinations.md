---
keywords: activate destination;activate destinations;activate data
title: Activation de profils et de segments vers une destination
type: Tutorial
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données client en temps réel en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme de données client en temps réel en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: 5928242537acdb1f130a0e8ac1bca3f14c184c6a
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 23%

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données client en temps réel en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.

## Conditions préalables  {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](/help/rtcdp/destinations/connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activation des données {#activate-data}

Les étapes du processus d’activation varient légèrement d’un type de destination à l’autre. Le processus complet pour tous les types de destination est décrit ci-dessous.

### Sélectionnez la destination à laquelle activer les données. {#select-destination}

S&#39;applique à : Toutes les destinations

Dans l’interface utilisateur CDP en temps réel, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**, puis sélectionnez la destination à laquelle vous souhaitez activer vos segments.
![naviguer jusqu’à la destination](assets/oracle-eloqua-connect.png)

Sélectionnez le nom de la destination pour accéder au processus d’activation.

![activate-flow](assets/activate-flow.png)

Notez que si un processus d’activation existe déjà pour une destination, vous pouvez voir les segments actuellement activés pour cette destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.

Une fois que vous avez sélectionné une destination, sélectionnez **[!UICONTROL Activer]**.

### [!UICONTROL Etape de sélection de segments] {#select-segments}

S&#39;applique à : Toutes les destinations

![Procédure de sélection des segments](./assets/select-segments-icon.png)

In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select one or more segments to activate to the destination. Sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante.
![segments-to-destination](assets/email-select-segments.png)

### [!UICONTROL Etape de mappage] d’identité {#identity-mapping}

S&#39;applique à : destinations sociales et destination publicitaire Google Customer Match

![Etape de mappage d’identité](./assets/identity-mapping-icon.png)

Pour les destinations sociales, vous pouvez sélectionner des attributs source à mapper en tant qu’identités de cible dans la destination. Cette étape est facultative ou obligatoire, selon l’identité Principale que vous utilisez dans le schéma.

Si vous utilisez une adresse électronique comme identité Principale dans votre schéma, vous pouvez ignorer l’étape de mappage d’identité, comme indiqué ci-dessous :

![Adresse électronique en tant qu&#39;identité](assets/email-as-identity.gif)

Si vous utilisez un autre identifiant, tel que &quot;Identifiant de récompense&quot; ou &quot;Identifiant de fidélité&quot;, en tant qu’identité Principale dans votre schéma, vous devez mapper manuellement l’adresse électronique de votre schéma d’identité en tant qu’identité de cible dans la destination sociale, comme indiqué ci-dessous :

![Identifiant de fidélité en tant qu&#39;identité](assets/rewardsid-as-identity.gif)

Sélectionnez `Email_LC_SHA256` comme identité de cible si vous avez haché les adresses électroniques des clients lors de l’assimilation de données dans Adobe Experience Platform, conformément aux exigences [!DNL Facebook] de hachage des [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)courriers électroniques.

Sélectionnez `Email` comme identité de cible si les adresses électroniques que vous utilisez ne sont pas hachées. Le CDP en temps réel hachera les adresses électroniques pour se conformer aux [!DNL Facebook] exigences.

![mappage d’identité après le remplissage de champs](assets/identity-mapping.png)

### **[!UICONTROL Configurer]** l’étape {#configure}

S&#39;applique à : Destinations marketing par courriel et destinations d’enregistrement par cloud

![Configuration de l’étape](./assets/configure-icon.png)

A l’étape **[!UICONTROL Configurer]** , vous pouvez configurer la planification et les noms de fichier pour chaque segment que vous exportez. La configuration de la planification est obligatoire, mais la configuration du nom de fichier est facultative.

Pour ajouter une planification pour le segment, sélectionnez **[!UICONTROL Créer une planification]**.

![](./assets/activate-destinations/configure-destination-schedule.png)

Une fenêtre contextuelle s’affiche, présentant les options de création de la planification des segments.

- **Exportation** de fichier : Vous avez la possibilité d’exporter des fichiers complets ou des fichiers incrémentiels. L’exportation d’un fichier complet publie un instantané complet de tous les profils admissibles pour ce segment. L’exportation d’un fichier incrémentiel publie le delta des profils qui remplissent les critères pour ce segment depuis la dernière exportation.
- **Fréquence**: Si l’option **[!UICONTROL Exporter des fichiers]** complets est sélectionnée, vous avez la possibilité d’exporter **[!UICONTROL une fois]** ou **[!UICONTROL quotidiennement]**. Si l’option **[!UICONTROL Exporter des fichiers]** incrémentiels est sélectionnée, vous avez la possibilité d’exporter **[!UICONTROL quotidiennement]** uniquement. Exportation d’un fichier **[!UICONTROL Une fois]** exporte le fichier une seule fois. L’exportation d’un fichier Quotidien **** exporte le fichier tous les jours de la date du début à la date de fin à 12h00 UTC (19h00 HNE) si des fichiers complets sont sélectionnés et à 12h00 HNE (7h00 HNE) si des fichiers incrémentiels sont sélectionnés.
- **Date**: Si l’option **[!UICONTROL Une fois]** est sélectionnée, vous pouvez sélectionner la date de l’exportation unique. Si l’option **[!UICONTROL Quotidien]** est sélectionnée, vous pouvez sélectionner les dates de début et de fin des exportations.

![](./assets/activate-destinations/export-full-file.png)

Les noms de fichier par défaut se composent du nom de destination, de l’ID de segment et d’un indicateur de date et d’heure. Vous pouvez, par exemple, modifier les noms de fichiers exportés pour faire la distinction entre les différentes campagnes ou pour que le temps d’exportation des données soit annexé aux fichiers.

Sélectionnez l&#39;icône représentant un crayon pour ouvrir une fenêtre modale et modifier les noms de fichier. Notez que les noms de fichier sont limités à 255 caractères.

![configurer le nom de fichier](./assets/activate-destinations/configure-name.png)

Dans l’éditeur de noms de fichier, vous pouvez sélectionner différents composants à ajouter au nom de fichier. Le nom de destination et l&#39;ID de segment ne peuvent pas être supprimés des noms de fichier. Outre ces éléments, vous pouvez ajouter les éléments suivants :

- **[!UICONTROL Nom]** du segment : Vous pouvez ajouter le nom du segment au nom du fichier.
- **[!UICONTROL Date et heure]**: Choisissez entre l’ajout d’un `MMDDYYYY_HHMMSS` format ou d’un horodatage Unix de 10 chiffres de l’heure de génération des fichiers. Choisissez l’une de ces options si vous souhaitez que vos fichiers aient un nom de fichier dynamique généré avec chaque exportation incrémentielle.
- **[!UICONTROL Texte]** personnalisé : Ajoutez du texte personnalisé aux noms de fichier.

Sélectionnez **[!UICONTROL Appliquer les modifications]** pour confirmer votre sélection.

>[!IMPORTANT]
> 
>Si vous ne sélectionnez pas le composant **[!UICONTROL Date et Heure]** , les noms de fichier seront statiques et le nouveau fichier exporté remplacera le fichier précédent dans votre emplacement d’enregistrement par chaque exportation. Lors de l’exécution d’une tâche d’importation périodique depuis un emplacement d’enregistrement vers une plateforme de marketing par courrier électronique, il s’agit de l’option recommandée.

![modifier les options de nom de fichier](./assets/activate-workflow-configure-step-2.png)

Une fois que vous avez terminé de configurer tous vos segments, sélectionnez **[!UICONTROL Suivant]** pour continuer.

### **[!UICONTROL Etape de planification]** du segment {#segment-schedule}

S&#39;applique à : destinations publicitaires, destinations sociales

![étape de planification du segment](./assets/segment-schedule-icon.png)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination, as well as the frequency of sending data to the destination.

>[!IMPORTANT]
>
>Pour les destinations sociales, vous devez sélectionner l’origine de votre audience à cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

![choix de l’origine des données](./assets/choose-data-origin.png)

### **[!UICONTROL Étape de sélection des attributs]** {#select-attributes}

S&#39;applique à : destinations de marketing par courrier électronique et destinations d’enregistrement dans le cloud

![étape de sélection des attributs](./assets/select-attributes-icon.png)

On the **[!UICONTROL Select attributes]** page, select **[!UICONTROL Add new field]** and choose the attributes that you want to send to the destination.

>[!NOTE]
>
> Le CDP en temps réel préremplit votre sélection avec quatre attributs recommandés, couramment utilisés, de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient comme suit, selon qu’ `segmentMembership.status` il est sélectionné ou non :
- Si le `segmentMembership.status` champ est sélectionné, les fichiers exportés incluent des membres **[!UICONTROL Principaux]** dans l&#39;instantané complet initial et des membres **[!UICONTROL Principaux]** et **[!UICONTROL expirés]** dans les exportations incrémentielles suivantes.
- Si le `segmentMembership.status` champ n’est pas sélectionné, les fichiers exportés incluent uniquement des membres **[!UICONTROL Principaux]** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

![attributs recommandés](./assets/activate-destinations/mark-mandatory.png)

De plus, vous pouvez marquer différents attributs comme obligatoires. Le fait de marquer un attribut comme obligatoire le rend de sorte que le segment exporté doit contenir cet attribut. Par conséquent, il peut être utilisé comme une autre forme de filtrage. Le marquage d’un attribut comme obligatoire **n’est pas** obligatoire.

Il est recommandé que l’un des attributs soit un identifiant [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) unique de votre schéma. For more information about mandatory attributes, see the identity section in the [Email marketing destinations](/help/rtcdp/destinations/email-marketing-destinations.md#identity) documentation.

>[!NOTE]
> 
>Si des étiquettes d’utilisation de données ont été appliquées à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu de données), l’application de ces étiquettes de niveau champ à l’activation se fait dans les conditions suivantes :
>- Les champs sont utilisés dans la définition de segment.
>- Les champs sont configurés en tant qu’attributs prévisionnels pour la destination de la cible.

>
> 
Par exemple, si le champ `person.name.firstName` comporte certains libellés d’utilisation des données qui entrent en conflit avec le cas d’utilisation marketing de la destination, une violation de la stratégie d’utilisation des données s’affichera à l’étape de révision. Pour plus d’informations, voir Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations)en temps réel.

### **[!UICONTROL Étape de révision]** {#review}

S&#39;applique à : toutes les destinations

![étape de révision](./assets/review-icon.png)

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, le CDP en temps réel recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](/help/rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![violation de la stratégie de données](assets/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![confirm-selection](assets/confirm-selection.png)

## Modification de l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans la plateforme de données clients en temps réel :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite pour modifier les segments à envoyer à la destination.

## Vérification de la réussite de l’activation du segment {#verify-activation}

### Destinations de marketing par e-mail  et destinations de stockage dans le cloud {#esp-and-cloud-storage}

For email marketing destinations and cloud storage destinations, Real-time CDP creates a tab-delimited `.csv` or `.txt` file in the storage location that you provided. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. The default file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

Notez que vous pouvez modifier le format de fichier. Pour plus d’informations, reportez-vous à l’étape [Configurer](/help/rtcdp/destinations/activate-destinations.md#configure) pour les destinations d’enregistrement cloud et les destinations de marketing par courrier électronique.

Avec le format de fichier par défaut, les fichiers que vous recevriez trois jours consécutifs peuvent ressembler à ceci :

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation de la réussite de l’activation. Pour comprendre comment les fichiers exportés sont structurés, vous pouvez [télécharger un exemple de fichier](assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv. Cet exemple de fichier inclut les attributs de profil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`et `personalEmail.address`.

### Destinations publicitaires

Vérifiez votre compte dans la destination publicitaire vers laquelle vous activez vos données. Si l’activation a réussi, les audiences sont renseignées dans votre plateforme publicitaire.

### Destinations de réseau social

For [!DNL Facebook], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L&#39;intégration entre le CDP en temps réel et la prise en charge [!DNL Facebook] des renvois d&#39;audiences historiques. Toutes les qualifications des segments historiques sont envoyées [!DNL Facebook] lorsque vous activez les segments vers la destination.

## Désactivation de l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.
