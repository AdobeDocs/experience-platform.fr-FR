---
title: Activation de profils et de segments vers une destination
seo-title: Activation de profils et de segments vers une destination
description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
seo-description: Activez les données de la plateforme des données clients en temps réel d’Adobe en mappant les segments aux destinations. Pour ce faire, suivez la procédure décrite ci-après.
translation-type: tm+mt
source-git-commit: faaa4eda5174bb8d27a76d767891df15df69e30a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 61%

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
5. *Conditionnel*. Cette étape diffère selon le type de destination dans lequel vous activez vos segments. <br> Pour les destinations *de marketing par* courriel et les destinations *d’enregistrement* cloud, sur la page **[!UICONTROL Sélectionner les attributs]** , sélectionnez **[!UICONTROL Ajouter nouveau champ et sélectionnez les attributs à envoyer à la destination.]**
Nous recommandons que l’un des attributs soit un [identifiant unique](/help/rtcdp/destinations/email-marketing-destinations.md#identity) issu de votre schéma d’union. Pour plus d’informations sur les attributs obligatoires, consultez Identité dans l’article [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![Attributs des destinations](/help/rtcdp/destinations/assets/select-attributes-step.png)
Pour les destinations *des réseaux* sociaux, à l’étape de mappage **** d’identité, sélectionnez les attributs source à mapper aux identités de cible.
   ![mappage d’identité avant de remplir des champs](/help/rtcdp/destinations/assets/facebook-identity-mapping-1.png)Dans l’exemple ci-dessous, l’adresse électronique personnelle dans le schéma d’identité a été hachée lors de l’assimilation dans la plateforme d’expérience afin de se conformer aux exigences [de hachage de](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)courrier électronique de Facebook. Appuyez sur **[!UICONTROL Suivant]** après avoir sélectionné le mappage.
   ![mappage d’identité après le remplissage de champs](/help/rtcdp/destinations/assets/facebook-identity-mapping-2.png)

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

>[!TIP]
>
>L’intégration entre Adobe Real-time CDP et Facebook prend en charge les remplissages d’audiences historiques. Toutes les qualifications des segments historiques sont envoyées à Facebook lorsque vous activez les segments vers la destination.

## Désactivation de l’activation {#disable-activation}

Pour désactiver un flux d’activation existant, procédez comme suit :

1. Sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche, cliquez sur l’onglet **[!UICONTROL Parcourir]**, puis sur le nom de la destination.
2. Cliquez sur la commande **[!UICONTROL Activé]** dans le rail de droite pour modifier l’état du flux d’activation.
3. Dans la fenêtre **Mettre à jour l’état du flux de données**, sélectionnez **Confirmer** pour désactiver le flux d’activation.

Dans AWS Kinesis, générez une paire de clés d’accès secrètes pour accorder un accès CDP Adobe en temps réel à votre compte AWS Kinesis. Pour en savoir plus, consultez la documentation [](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)AWS Kinesis.