---
keywords: activate destination;activate destinations;activate data
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: 22bca041673cec5eee54ed4234aba19eca470441
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 28%

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.

## Conditions préalables  {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](/help/rtcdp/destinations/connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activation des données {#activate-data}

Les étapes du processus d’activation varient légèrement selon les types de destination. Le processus complet pour tous les types de destination est décrit ci-dessous.

### Sélectionnez la destination à laquelle activer les données. {#select-destination}

S&#39;applique à : Toutes les destinations

1. Dans l’interface utilisateur CDP en temps réel de l’Adobe, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**, puis sélectionnez la destination à laquelle vous souhaitez activer vos segments.
   ![naviguer jusqu’à la destination](assets/oracle-eloqua-connect.png)
2. Cliquez sur le nom de la destination. Vous accédez ainsi au processus d’activation.
   ![activate-flow](assets/activate-flow.png)Notez que si un processus d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement activés pour la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.
3. Select **[!UICONTROL Activate]**.

<br> 

### **[!UICONTROL Etape de sélection de segments]** {#select-segments}

S&#39;applique à : Toutes les destinations

![Procédure de sélection des segments](/help/rtcdp/destinations/assets/select-segments-icon.png)


In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select one or more segments to activate to the destination. Appuyez sur **[!UICONTROL Suivant]** pour passer à l’étape suivante.
![segments-to-destination](assets/email-select-segments.png)

<br> 

### **[!UICONTROL Etape de mappage]** d’identité {#identity-mapping}

S&#39;applique à : destinations sociales et destination publicitaire Google Customer Match

![Etape de mappage d’identité](/help/rtcdp/destinations/assets/identity-mapping-icon.png)

Pour les destinations ** sociales, à l’étape de mappage **** d’identité, vous pouvez sélectionner les attributs source à mapper en tant qu’identités de cible dans la destination. Cette étape est facultative ou obligatoire, selon l’identité Principale que vous utilisez dans le schéma. <br> 

*Adresse électronique en tant qu&#39;identité* Principale : Si vous utilisez une adresse électronique comme identité Principale dans votre schéma, vous pouvez ignorer l’étape de mappage d’identité, comme indiqué ci-dessous :

![Adresse électronique en tant qu&#39;identité](assets/email-as-identity.gif)

<br> 

*Un autre ID en tant qu&#39;identité* Principale : Si vous utilisez un autre identifiant, tel que l’identifiant *de* récompense ou l’identifiant *de* fidélité, en tant qu’identité Principale dans votre schéma, vous devez mapper manuellement l’adresse électronique de votre schéma d’identité en tant qu’identité de cible dans la destination sociale, comme indiqué ci-dessous :

![Identifiant de fidélité en tant qu&#39;identité](assets/rewardsid-as-identity.gif)


Sélectionnez `Email_LC_SHA256` comme identité de cible si vous avez haché les adresses électroniques des clients lors de l’assimilation de données dans Adobe Experience Platform, conformément aux exigences [!DNL Facebook] de hachage des [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)courriers électroniques. <br> Sélectionnez `Email` comme identité de cible si les adresses électroniques que vous utilisez ne sont pas hachées. adobe Le CDP en temps réel hachera les adresses électroniques pour se conformer aux [!DNL Facebook] exigences.

![mappage d’identité après le remplissage de champs](assets/identity-mapping.png)

<br> 

### **[!UICONTROL Configurer]** l’étape {#configure}

S&#39;applique à : Destinations marketing par courriel et destinations d’enregistrement par cloud

![Configuration de l’étape](/help/rtcdp/destinations/assets/configure-icon.png)

Cette étape est facultative. A l’étape **[!UICONTROL Configurer]** , vous pouvez configurer les noms de fichier pour chaque segment que vous exportez. Les noms de fichier par défaut se composent du nom de destination, de l’ID de segment et d’un indicateur de date et d’heure. Vous pouvez, par exemple, modifier les noms de fichiers exportés pour faire la distinction entre les différentes campagnes ou pour que le temps d’exportation des données soit annexé aux fichiers.

Sélectionnez **[!UICONTROL Suivant]** pour utiliser les noms de fichier par défaut ou cliquez sur l’icône représentant un crayon pour ouvrir une fenêtre modale et modifier les noms de fichier. Notez que les noms de fichier sont limités à 255 caractères.

![configurer le nom de fichier](assets/activation-workflow-configure-step.png)

Dans l’éditeur de noms de fichier, vous pouvez sélectionner différents composants à ajouter au nom de fichier. Le nom de destination et l&#39;ID de segment ne peuvent pas être supprimés des noms de fichier. Outre ces éléments, vous pouvez ajouter les éléments suivants :

* **[!UICONTROL Nom]** du segment : Vous pouvez ajouter le nom du segment au nom du fichier.
* **[!UICONTROL Date et heure]**: Choisissez entre l’ajout d’un `MMDDYYYY_HHMMSS` format ou d’un horodatage Unix de 10 chiffres de l’heure de génération des fichiers. Sélectionnez l’une de ces options si vous souhaitez que vos fichiers aient un nom de fichier dynamique généré avec chaque exportation incrémentielle.
* **[!UICONTROL Texte]** personnalisé : ajoutez du texte personnalisé aux noms de fichier.

Sélectionnez **[!UICONTROL Appliquer les modifications]** pour confirmer votre sélection.

>[!IMPORTANT]
> 
>Si vous ne sélectionnez pas le composant **[!UICONTROL Date et Heure]** , les noms de fichier seront statiques et le nouveau fichier exporté remplacera le fichier précédent dans votre emplacement d’enregistrement par chaque exportation. Lors de l’exécution d’une tâche d’importation périodique depuis un emplacement d’enregistrement vers une plateforme de marketing par courrier électronique, il s’agit de l’option recommandée.

![modifier les options de nom de fichier](assets/activate-workflow-configure-step-2.png)

<br> 

### **[!UICONTROL Etape de planification]** des segments {#segment-schedule}

S&#39;applique à : destinations publicitaires, destinations sociales

![étape de planification du segment](/help/rtcdp/destinations/assets/segment-schedule-icon.png)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination, as well as the frequency of sending data to the destination.

>[!IMPORTANT]
>
>Pour les destinations sociales, vous devez sélectionner l’origine de votre audience à cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

![choix de l’origine des données](assets/choose-data-origin.png)

<br> 

### **[!UICONTROL Etape de planification]** {#scheduling}

S&#39;applique à : destinations de marketing par courrier électronique et destinations d’enregistrement dans le cloud

![étape de planification du segment](assets/scheduling-icon.png)

On the **[!UICONTROL Scheduling]** page, you can see the start date for sending data to the destination as well as the frequency of sending data to the destination. Ces valeurs ne peuvent pas être modifiées.

<br> 

### **[!UICONTROL Étape de sélection des attributs]** {#select-attributes}

S&#39;applique à : destinations de marketing par courrier électronique et destinations d’enregistrement dans le cloud

![étape de sélection des attributs](/help/rtcdp/destinations/assets/select-attributes-icon.png)


On the **[!UICONTROL Select Attributes]** page, select **[!UICONTROL Add new field]** and select the attributes that you want to send to the destination.

>[!NOTE]
>
> adobe Le CDP en temps réel préremplit votre sélection avec quatre attributs recommandés et couramment utilisés de votre schéma : `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Les exportations de fichiers varient comme suit, selon qu’ `segmentMembership.status` il est sélectionné :
* Si le `segmentMembership.status` champ est sélectionné, les fichiers exportés incluent des membres **Principaux** dans l&#39;instantané complet initial et des membres **Principaux** et **expirés** dans les exportations incrémentielles suivantes.
* Si le `segmentMembership.status` champ n’est pas sélectionné, les fichiers exportés incluent uniquement des membres **Principaux** dans l’instantané complet initial et dans les exportations incrémentielles suivantes.

![attributs recommandés](/help/rtcdp/destinations/assets/recommended-attributes.png)


We recommend one of the attributes to be a [unique identifier](/help/rtcdp/destinations/email-marketing-destinations.md#identity) from your schema. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).

>[!NOTE]
> 
>Si des étiquettes d’utilisation de données ont été appliquées à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu de données), l’application de ces étiquettes de niveau champ à l’activation se fait dans les conditions suivantes :
>* Les champs sont utilisés dans la définition de segment.
>* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination de la cible.

>
> 
Regardez la capture d&#39;écran ci-dessous. Si, par exemple, le champ `person.name.firstName` comportait certaines étiquettes d’utilisation des données qui entrent en conflit avec le cas d’utilisation marketing de la destination, une violation de la stratégie d’utilisation des données s’afficherait au cours de l’étape de révision (étape 9). Pour plus d’informations, voir Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations)en temps réel.

![Attributs des destinations](assets/select-attributes-step.png)

<br> 

### **[!UICONTROL Étape de révision]** {#review}

S&#39;applique à : toutes les destinations

![étape de révision](/help/rtcdp/destinations/assets/review-icon.png)

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

Pour les destinations de marketing par e-mail et celles de stockage dans le cloud, la plateforme de données clients en temps réel d’Adobe crée un fichier `.csv` ou `.txt` séparé par des tabulations dans l’emplacement de stockage indiqué. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. The default file format is:
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
>L&#39;intégration entre le CDP en temps réel de l&#39;Adobe et la prise en charge [!DNL Facebook] des renvois d&#39;audiences historiques. Toutes les qualifications des segments historiques sont envoyées [!DNL Facebook] lorsque vous activez les segments vers la destination.

## Désactivation de l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.
