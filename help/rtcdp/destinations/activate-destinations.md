---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: 7dafdf0dd1ad3af2defab3bf6b784fd37e777062
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 77%

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à vous [connecter à une destination](/help/rtcdp/destinations/assets/connect-destination.png). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activation des données {#activate-data}

1. Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)
Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.
3. Sélectionnez **[!UICONTROL Activer]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to the destination.
   ![segments-to-destination](/help/rtcdp/destinations/assets/select-segments.png)
5. *Conditionnel*. Cette étape s’applique uniquement aux segments mappés aux destinations d’enregistrement cloud et aux destinations de marketing par courrier électronique. <br> Sur la page **[!UICONTROL Attributs de destination]**, sélectionnez **[!UICONTROL Ajouter un nouveau champ]** et sélectionnez les attributs à envoyer à la destination.
Nous recommandons que l’un des attributs soit un [identifiant unique](/help/rtcdp/destinations/email-marketing-destinations.md#identity) issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![Attributs des destinations](/help/rtcdp/destinations/assets/destination-attributes.png)
6. On the **[!UICONTROL Segment schedule]** page, you can see the start date for sending data to the destination, as well as the frequency of sending data to the destination.

   >[!IMPORTANT]
   >
   >Pour les destinations sociales, vous devez sélectionner l’origine de votre audience dans cette étape. Vous ne pouvez passer à l’étape suivante qu’après avoir sélectionné l’une des options de l’image ci-dessous.

   ![choisir l&#39;origine de données](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

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

## Désactivation de l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.

