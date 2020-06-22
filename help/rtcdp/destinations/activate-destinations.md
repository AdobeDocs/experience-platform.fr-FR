---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: b1f8cbe245f73e31a8941fc45cefcee595968a70
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 46%

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](/help/rtcdp/destinations/connect-destination.md). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activation des données {#activate-data}

1. Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)
Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.
3. Sélectionnez **[!UICONTROL Activer]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to the destination.
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

   Pour les destinations ** sociales, à l’étape de mappage **** d’identité, vous pouvez sélectionner les attributs source à mapper en tant qu’identités de cible dans la destination. Cette étape est facultative ou obligatoire, selon l&#39;identité principale que vous utilisez dans le schéma. <br> 

   *Adresse électronique en tant qu&#39;identité* principale : Si vous utilisez une adresse électronique comme identité principale dans votre schéma, vous pouvez ignorer l’étape de mappage d’identité, comme indiqué ci-dessous :

   ![Adresse électronique en tant qu&#39;identité](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Autre ID en tant qu&#39;identité* principale : Si vous utilisez un autre identifiant, tel que l’identifiant *de* récompense ou l’identifiant *de* fidélité, en tant qu’identité principale dans votre schéma, vous devez mapper manuellement l’adresse électronique de votre schéma d’identité en tant qu’identité de cible dans la destination sociale, comme indiqué ci-dessous :

   ![Identifiant de fidélité en tant qu&#39;identité](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Sélectionnez `Email_LC_SHA256` comme identité de cible si vous avez haché les adresses électroniques des clients lors de l’assimilation de données dans l’Adobe Experience Platform, conformément aux exigences [de hachage des](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)courriers électroniques de Facebook. <br> Sélectionnez `Email` comme identité de cible si les adresses électroniques que vous utilisez ne sont pas hachées. Adobe Real-time CDP hachera les adresses électroniques pour se conformer aux exigences de Facebook.

   ![mappage d’identité après le remplissage de champs](/help/rtcdp/destinations/assets/identity-mapping.png)

6. On the **[!UICONTROL Segment schedule]** page, you can see the start date for sending data to the destination, as well as the frequency of sending data to the destination.

   >[!IMPORTANT]
   >
   >Pour les destinations sociales, vous devez sélectionner l’origine de votre audience dans cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

   ![choisir l&#39;origine de données](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

   >[!IMPORTANT]
   >
   >Au cours de cette étape, le CDP en temps réel recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](/help/rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![confirm-selection](/help/rtcdp/destinations/assets/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![confirm-selection](/help/rtcdp/destinations/assets/confirm-selection.png)



## Modification de l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans la plateforme des données clients en temps réel :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite pour modifier les segments à envoyer à la destination.

## Vérification de la réussite de l’activation du segment {#verify-activation}

### Destinations de marketing par e-mail et destinations de stockage dans le cloud

Pour les destinations de marketing par e-mail et celles de stockage dans le cloud, la plateforme des données clients en temps réel d’Adobe crée un fichier `.txt` ou `.csv`séparé par des tabulations dans l’emplacement de stockage indiqué. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. Le format du fichier est :
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Les fichiers que vous pouvez recevoir pendant trois jours consécutifs peuvent ressembler à ceux-ci :

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation de la réussite de l’activation.

### Destinations publicitaires

Vérifiez la destination publicitaire vers laquelle vous activez vos données. Si l’activation a réussi, les audiences sont renseignées dans votre plateforme publicitaire.

### Destinations des réseaux sociaux

Pour Facebook, une activation réussie signifie qu’une audience personnalisée Facebook serait créée par programmation dans le Gestionnaire [d’annonces](https://www.facebook.com/adsmanager/manage/)Facebook. L’appartenance à un segment dans l’audience serait ajoutée et supprimée car les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L&#39;intégration entre le CDP en temps réel d&#39;Adobe et Facebook prend en charge les renvois d&#39;audiences historiques. Toutes les qualifications des segments historiques sont envoyées à Facebook lorsque vous activez les segments vers la destination.

## Désactivation de l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.
