---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 53%

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.

## Conditions préalables  {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](/help/rtcdp/destinations/connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activation des données {#activate-data}

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**, select the destination where you want to activate your segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)
Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.
3. Sélectionnez **[!UICONTROL Activer]**.
4. Dans le workflow d’**[!UICONTROL activation de destination]**, sur la page **[!UICONTROL Sélection de segments]**, sélectionnez les segments à envoyer à la destination.
   ![segments-to-destination](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *Conditionnel*. Cette étape diffère selon le type de destination dans lequel vous activez vos segments. <br> Pour les destinations *de marketing par* courriel et les destinations *d’enregistrement* cloud, sur la page **[!UICONTROL Sélectionner les attributs]** , sélectionnez **[!UICONTROL Ajouter un nouveau champ et sélectionnez les attributs à envoyer à la destination.]**
Nous recommandons que l’un des attributs soit un [identifiant unique](/help/rtcdp/destinations/email-marketing-destinations.md#identity) issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).

   >[!NOTE]
   > 
   >Si des étiquettes d’utilisation de données ont été appliquées à certains champs d’un jeu de données (plutôt qu’à l’ensemble du jeu de données), l’application de ces étiquettes de niveau champ à l’activation se fait dans les conditions suivantes :
   >* Les champs sont utilisés dans la définition de segment.
   >* Les champs sont configurés en tant qu’attributs prévisionnels pour la destination de la cible.

   >
   > Regardez la capture d&#39;écran ci-dessous. Si, par exemple, le champ `person.name.first.Name` comportait certaines étiquettes d’utilisation des données qui entrent en conflit avec le cas d’utilisation marketing de la destination, une violation de la stratégie d’utilisation des données s’afficherait à l’étape de révision (étape 7). Pour plus d’informations, voir Gouvernance des [données dans le CDP en temps réel](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![Attributs des destinations](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Pour les destinations ** sociales, à l’étape de mappage **** d’identité, vous pouvez sélectionner les attributs source à mapper en tant qu’identités de cible dans la destination. Cette étape est facultative ou obligatoire, selon l’identité Principale que vous utilisez dans le schéma. <br> 

   *Adresse électronique en tant qu&#39;identité* Principale : Si vous utilisez une adresse électronique comme identité Principale dans votre schéma, vous pouvez ignorer l’étape de mappage d’identité, comme indiqué ci-dessous :

   ![Adresse électronique en tant qu&#39;identité](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Un autre ID en tant qu&#39;identité* Principale : Si vous utilisez un autre identifiant, tel que l’identifiant *de* récompense ou l’identifiant *de* fidélité, en tant qu’identité Principale dans votre schéma, vous devez mapper manuellement l’adresse électronique de votre schéma d’identité en tant qu’identité de cible dans la destination sociale, comme indiqué ci-dessous :

   ![Identifiant de fidélité en tant qu&#39;identité](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Sélectionnez `Email_LC_SHA256` comme identité de cible si vous avez haché les adresses électroniques des clients lors de l’assimilation de données dans Adobe Experience Platform, conformément aux exigences [!DNL Facebook] de hachage des [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)courriers électroniques. <br> Sélectionnez `Email` comme identité de cible si les adresses électroniques que vous utilisez ne sont pas hachées. Adobe Le CDP en temps réel hachera les adresses électroniques pour se conformer aux [!DNL Facebook] exigences.

   ![mappage d’identité après le remplissage de champs](/help/rtcdp/destinations/assets/identity-mapping.png)

6. Sur la page **[!UICONTROL Planning de segments]**, vous pouvez voir la date de début de l’envoi des données à la destination, ainsi que la fréquence d’envoi.

   >[!IMPORTANT]
   >
   >Pour les destinations sociales, vous devez sélectionner l’origine de votre audience à cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

   ![choix de l’origine des données](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

   >[!IMPORTANT]
   >
   >Au cours de cette étape, le CDP en temps réel recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](/help/rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![confirm-selection](/help/rtcdp/destinations/assets/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![confirm-selection](/help/rtcdp/destinations/assets/confirm-selection.png)



## Modification de l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans la plateforme de données clients en temps réel :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite pour modifier les segments à envoyer à la destination.

## Vérification de la réussite de l’activation du segment {#verify-activation}

### Destinations de marketing par e-mail  et destinations de stockage dans le cloud {#esp-and-cloud-storage}

Pour les destinations de marketing par e-mail et celles de stockage dans le cloud, la plateforme de données clients en temps réel d’Adobe crée un fichier `.csv` ou `.txt` séparé par des tabulations dans l’emplacement de stockage indiqué. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. Le format du fichier est :
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

Les fichiers que vous pouvez recevoir pendant trois jours consécutifs peuvent ressembler à ceux-ci :

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation de la réussite de l’activation. Pour comprendre comment les fichiers exportés sont structurés, vous pouvez [télécharger un exemple de fichier](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv. Cet exemple de fichier inclut les attributs de profil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`et `personalEmail.address`.

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
