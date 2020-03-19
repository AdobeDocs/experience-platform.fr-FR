---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
seo-description: Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# Activation de profils et de segments vers une destination

Activez les données de la plateforme de données client en temps réel Adobe en mappant les segments aux destinations. Pour ce faire, procédez comme suit.

## Conditions préalables {#prerequisites}

Pour activer des données vers des destinations, vous devez avoir réussi à [connecter une destination](/help/rtcdp/destinations/assets/connect-destination.png). Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md), parcourez les destinations prises en charge et configurez une ou plusieurs destinations.

## Activer les données {#activate-data}

1. Dans **Destinations > Parcourir**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)
Notez que si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **Modifier l’activation** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations de l’activation.
3. Sélectionnez **Activer**.
4. Dans l’assistant d’**activation de la destination**, sur la page **Sélection des segments**, sélectionnez les segments à envoyer à la destination.
   ![segments-to-destination](/help/rtcdp/destinations/assets/select-segments.png)
5. *Conditionnel*. Cette étape s’applique uniquement aux segments mappés aux destinations de marketing par e-mail. <br> Sur la page **Attributs de destination**, sélectionnez **Ajouter un nouveau champ** et sélectionnez les attributs à envoyer à la destination.
Nous recommandons que l’un des attributs soit un [identifiant unique](/help/rtcdp/destinations/email-marketing-destinations.md#identity) issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Sur la page **Planning**, vous pouvez voir la date de début de l’envoi des données vers la destination, ainsi que la fréquence d’envoi des données vers la destination.
7. Sur la page **Examen**, vous pouvez voir un résumé de votre sélection. Sélectionnez **Annuler** pour interrompre le flux, **Précédent** pour modifier vos paramètres ou **Terminer** pour confirmer votre sélection et commencer à envoyer les données vers la destination.

![confirm-selection](/help/rtcdp/destinations/assets/confirm-selection.png)

## Modifier l’activation {#edit-activation}

Suivez les étapes ci-dessous pour modifier les flux d’activation existants dans la plateforme CDP en temps réel :

1. Sélectionnez **Destinations** dans la barre de navigation de gauche, ensuite cliquez sur l’onglet **Parcourir**, puis sur le nom de la destination.
2. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite pour modifier les segments à envoyer vers la destination.

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

## Désactiver l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **Destinations** dans la barre de navigation de gauche, ensuite cliquez sur l’onglet **Parcourir**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.

