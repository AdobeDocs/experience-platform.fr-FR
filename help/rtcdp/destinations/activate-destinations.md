---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données clientes en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
seo-description: Activez les données de la plateforme de données clientes en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données clientes en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.

## Conditions préalables  {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir [connecté une destination](/help/rtcdp/destinations/assets/connect-destination.png)avec succès. Si vous ne l’avez pas déjà fait, accédez au catalogue [des](/help/rtcdp/destinations/destinations-catalog.md)destinations, parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activer les données {#activate-data}

1. Dans **Destinations > Parcourir**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux Activer.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Notez que si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **Modifier l’activation** dans le rail de droite et suivez les étapes ci-dessous pour modifier les détails de l’activation.
3. Sélectionnez **Activer**;
4. Dans l’assistant **Activer la destination** , sur la page **Sélectionner des segments** , sélectionnez les segments à envoyer à la destination.
   ![segments vers destination](/help/rtcdp/destinations/assets/select-segments.png)
5. *Conditionnel*. Cette étape s’applique uniquement aux segments mappés aux destinations marketing par courrier électronique. <br> Dans la page Attributs **de** destination, sélectionnez **Ajouter un nouveau champ** et sélectionnez les attributs à envoyer à la destination.
Nous recommandons que l’un des attributs soit un identifiant [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) unique issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, voir Identité dans l’article Destinations [marketing par](/help/rtcdp/destinations/email-marketing-destinations.md#identity) courrier électronique.
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Sur la page **Planifier** , vous pouvez voir la date de début de l’envoi des données vers la destination, ainsi que la fréquence d’envoi des données vers la destination.
7. Sur la page **Révision** , vous pouvez voir un résumé de votre sélection. Sélectionnez **Annuler** pour séparer le flux, **Précédent** pour modifier vos paramètres ou **Terminer** pour confirmer votre sélection et commencer à envoyer les données à la destination.

![confirmation-sélection](/help/rtcdp/destinations/assets/confirm-selection.png)

## Modifier l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans le CDP en temps réel :

1. Sélectionnez **Destinations** dans la barre de navigation de gauche, puis cliquez sur l’onglet **Parcourir** , puis sur le nom de destination.
2. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite pour modifier les segments à envoyer à la destination.

## Vérifier que l’activation du segment a réussi {#verify-activation}

### Destinations marketing par courrier électronique

Pour les destinations de marketing par courrier électronique, le CDP en temps réel d’Adobe crée un fichier délimité par des tabulations `.txt` ou `.csv` dans l’emplacement de stockage que vous avez fourni. Attendez-vous à ce qu’un nouveau fichier soit créé chaque jour à votre emplacement de stockage. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Les fichiers que vous recevriez pendant trois jours consécutifs pourraient ressembler à ceci :

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La présence de ces fichiers dans votre emplacement de stockage confirme l’activation réussie.

### Destinations publicitaires

Vérifiez la destination publicitaire vers laquelle vous activez vos données. Si l’activation a réussi, les audiences sont renseignées dans votre plateforme publicitaire.

## Désactiver l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **Destinations** dans la barre de navigation de gauche, puis cliquez sur l’onglet **Parcourir** , puis sur le nom de destination.
2. Cliquez sur le contrôle **[!UICONTROL Activé]** dans le rail droit pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état** du flux de données, sélectionnez **Confirmer** pour désactiver le flux d’activation.

