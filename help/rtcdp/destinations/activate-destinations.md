---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
seo-description: Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à [connecter une destination](/help/rtcdp/destinations/assets/connect-destination.png). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activer les données {#activate-data}

1. In **[!UICONTROL Destinations > Browse]**, select the destination where you want to activate your segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)
Notez que si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Sélectionner **[!UICONTROL Activate]**;
4. Dans le **[!UICONTROL Activate destination]** flux de travaux, sur la **[!UICONTROL Select Segments]** page, sélectionnez les segments à envoyer à la destination.
   ![segments-to-destination](/help/rtcdp/destinations/assets/select-segments.png)
5. *Conditionnel*. Cette étape s’applique uniquement aux segments mappés aux destinations de marketing par e-mail. <br> Sur la **[!UICONTROL Destination Attributes]** page, sélectionnez **[!UICONTROL Add new field]** et sélectionnez les attributs à envoyer à la destination.
Nous recommandons que l’un des attributs soit un [identifiant unique](/help/rtcdp/destinations/email-marketing-destinations.md#identity) issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. On the **[!UICONTROL Segment schedule]** page, you can see the start date for sending data to the destination, as well as the frequency of sending data to the destination.

   >[!IMPORTANT]
   >
   >Pour les destinations sociales, vous devez sélectionner le    de votre  dans cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

   ![choisir les données](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](/help/rtcdp/destinations/assets/confirm-selection.png)

## Modifier l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans la plateforme CDP en temps réel :

1. Select **[!UICONTROL Destinations]** in the left navigation bar, then click the **[!UICONTROL Browse]** tab, and click the destination name.
2. Select **[!UICONTROL Edit activation]** in the right rail to change which segments to send to the destination.

## Vérifier que l’activation du segment a réussi {#verify-activation}

### Destinations de marketing par e-mail et cloud  destinations 

For email marketing destinations and cloud storage destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. Le format du fichier est :
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Les fichiers que vous recevriez pendant trois jours consécutifs pourraient ressembler à ceci :

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La présence de ces fichiers dans votre emplacement de stockage est la confirmation d’une activation réussie.

### Destinations publicitaires

Vérifiez la destination publicitaire vers laquelle vous activez vos données. Si l’activation a réussi, les audiences sont renseignées dans votre plateforme publicitaire.

### Destinations des réseaux sociaux

Pour Facebook, un   réussi signifie qu’un de  personnalisé Facebook serait créé par programmation dans le Gestionnaire [d’annonces](https://www.facebook.com/adsmanager/manage/)Facebook. L’appartenance au segment dans le   serait ajoutée et supprimée, car les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

## Désactiver l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Select **[!UICONTROL Destinations]** in the left navigation bar, then click the **[!UICONTROL Browse]** tab, and click the destination name.
2. Click the **[!UICONTROL Enabled]** control in the right rail to change the activation flow state.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.

